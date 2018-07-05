---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: 全局错误处理 ASP.NET Web API 2 中 |Microsoft Docs
author: davidmatson
description: ''
ms.author: aspnetcontent
ms.date: 02/03/2014
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: d1d1a081713da0771981229db8e8bd67a5103bf9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815858"
---
<a name="global-error-handling-in-aspnet-web-api-2"></a>全局错误处理 ASP.NET Web API 2 中
====================
通过[David Matson](https://github.com/davidmatson)， [Rick Anderson](https://github.com/Rick-Anderson)

立即登录，或全局处理错误的 Web API 中是没有简便的方法。 可以通过处理某些未经处理的异常[异常筛选器](exception-handling.md)，但不能处理异常筛选器的事例数。 例如：

1. 从控制器的构造函数引发的异常。
2. 从消息处理程序引发的异常。
3. 在路由期间引发的异常。
4. 响应内容序列化期间引发的异常。

我们想要提供一种简单一致的方式来记录和处理 （如果可能） 这些异常。 

有两种主要情况下，用于处理异常，其中我们将能够发送错误响应，我们可以执行操作的情况是日志异常的情况。 后一种情况的一个示例是当中间流式处理响应的内容; 引发异常在这种情况下它时已晚发送新的响应消息，因为状态代码、 标头和部分内容已通过网络，因此我们只需中止连接。 即使不能处理异常以生成新的响应消息，我们仍支持对异常进行记录。 在我们可以在其中检测到错误的情况下，我们可以返回相应的错误响应，如如下所示：

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>现有的选项

除了[异常筛选器](exception-handling.md)，[消息处理程序](../advanced/http-message-handlers.md)可以立即使用，以观察所有 500 级响应，但对这些响应是很困难，因为它们缺乏有关原始错误的上下文。 消息处理程序还具有一些有关的用例，它们可以处理的异常筛选器与相同的限制。Web API 具有捕获错误条件的跟踪基础结构时跟踪基础结构用于诊断目的和未设计或适合在生产环境中运行。 全局异常处理和日志记录应为服务，可以在生产期间运行，并插入到现有的监视解决方案 (例如， [ELMAH](https://code.google.com/p/elmah/) )。

### <a name="solution-overview"></a>解决方案概述

 我们提供了两个新的用户可替换服务[IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md)和 IExceptionHandler，记录和处理未经处理的异常。 服务是非常相似，两个主要差异：

1. 我们支持注册多个异常记录器，但仅在单个异常处理程序。
2. 异常记录器始终调用，即使我们想要中止此连接。 异常处理程序仅当我们仍能够选择要发送哪个响应消息时调用。

这两个服务提供对异常上下文，其中包含在其中检测到异常时的点中的相关信息的访问特别[HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)，则[HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)，则引发异常和异常源 （下面的详细信息）。

### <a name="design-principles"></a>设计原则

1. **没有重大更改**因为此功能将被添加在次要版本中，一个影响解决方案的重要约束是，有没有重大更改，或者键入协定，或行为。 我们想要根据现有的 catch 块将异常转化为 500 个答复做一些清理排除此约束。 此附加清理是我们可能要考虑的后续的主要版本。 如果这是对重要请对在投票[ASP.NET Web API 用户之声](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)。
2. **维护与 Web API 保持一致构造**Web API 的筛选器管道是使用应用特定于操作的、 特定于控制器或全局范围内的逻辑的灵活性来处理横切关注点的好办法。 筛选器，包括异常筛选器始终具有操作和控制器上下文，即使在全局范围内注册。 协定筛选器，有意义，但这也意味着，异常筛选器，即使全局范围的并不适合某些异常处理的情况，例如消息处理程序中的异常，其中没有操作或控制器上下文的存在。 如果我们想要使用的灵活作用域所提供的异常处理筛选器，我们仍需要异常筛选器。 但如果我们需要处理异常的控制器上下文之外，我们还需要单独构造完整全局错误处理 （内容而无需控制器上下文和操作上下文约束）。

### <a name="when-to-use"></a>何时使用

- 异常记录器是查看所有未处理的异常捕获到由 Web API 的解决方案。
- 异常处理程序是用于自定义所有可能的响应未经处理的异常捕获到由 Web API 的解决方案。
- 异常筛选器是最简单的解决方案用于处理与特定操作或控制器相关的子集未经处理的异常。

### <a name="service-details"></a>服务详细信息

 异常记录器和处理程序服务接口是简单的异步方法执行相应的上下文： 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 我们还为这两个接口提供基类。 重写 core （同步或异步） 方法是只需登录，或在推荐的处理时间。 对于日志记录，`ExceptionLogger`基类将确保 core 日志记录方法仅对于每个异常的一次调用 （即使它更高版本中进行传播进一步调用堆栈并再次捕获）。 `ExceptionHandler`基类将调用仅对在忽略旧版嵌套的调用堆栈顶部的异常 catch 块处理方法的核心。 （这些基类的类的简化的版本是在以下附录中。）这两`IExceptionLogger`并`IExceptionHandler`接收有关的信息通过异常`ExceptionContext`。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

当框架调用异常记录器或异常处理程序时，它将始终提供`Exception`和一个`Request`。 除了单元测试，也始终会提供`RequestContext`。 它很少会提供`ControllerContext`和`ActionContext`（仅当从 catch 块中调用的异常筛选器）。 它很少会提供`Response`（仅在当中间尝试将响应写入某些 IIS 情况下）。 请注意，因为其中的某些属性可能`null`由使用者检查`null`之前访问的异常类的成员。`CatchBlock` 一个字符串，表示的 catch 块看到异常。 Catch 块字符串如下所示：

- HttpServer （SendAsync 方法）
- HttpControllerDispatcher （SendAsync 方法）
- HttpBatchHandler （SendAsync 方法）
- IExceptionFilter （ApiController 的处理的异常筛选器管道中 ExecuteAsync）
- OWIN 主机：

    - HttpMessageHandlerAdapter.BufferResponseContentAsync （适用于缓冲输出）
    - HttpMessageHandlerAdapter.CopyResponseContentAsync （适用于流式处理输出）
- Web 主机：

    - HttpControllerHandler.WriteBufferedResponseContentAsync （适用于缓冲输出）
    - HttpControllerHandler.WriteStreamedResponseContentAsync （适用于流式处理输出）
    - HttpControllerHandler.WriteErrorResponseContentAsync （适用于缓冲的输出模式下的错误恢复中的失败）

Catch 块字符串的列表也是可通过静态只读属性。 （位于静态 ExceptionCatchBlocks 核心 catch 块字符串; 其余部分会显示一个静态类上每个 OWIN 和 web 主机）。`IsTopLevelCatchBlock` 可帮助遵循处理异常仅在调用堆栈顶部的建议的模式。 而不是打开到 500 响应任何位置出现嵌套的 catch 块的异常，异常处理程序可以让异常传播直至他们要看到的主机。

除了`ExceptionContext`，一个记录器获取通过完整的信息的另一段`ExceptionLoggerContext`:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

第二个属性， `CanBeHandled`，使记录器可以通过标识不能处理的异常。 当连接即将中止和可以发送任何新的响应消息，将调用记录器但处理程序将***不***进行调用，以及记录器可以识别此属性从这种情况。

在附加到`ExceptionContext`，一个处理程序获取一个属性可设置完整`ExceptionHandlerContext`处理异常：

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

异常处理程序指示它已通过设置处理异常`Result`属性设置为一个操作结果 (例如， [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)， [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)， [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)，或自定义结果)。 如果`Result`属性为 null、 未经处理的例外情况是，将重新引发原始异常。

有关调用堆栈顶部的例外情况，我们花费了额外的步骤来确保响应适合于 API 的调用方。 如果异常传播由宿主，调用方会死亡的黄色屏幕或某些其他主机提供响应，这通常是 HTML 和通常不适当的 API 错误响应。 在这些情况下，结果一开始不是 null，且仅当自定义异常处理程序显式将其设置回`null`（未经处理的） 将异常传播到主机。 设置`Result`到`null`在这种情况下也可用于两种方案：

1. OWIN 托管自定义异常处理中间件注册前/外部 Web API，Web API。
2. 本地调试通过浏览器，其中死亡的黄色屏幕是实际的有用响应未经处理的异常。

有关的异常记录器和异常处理程序，我们不执行任何操作即可恢复如果记录器或处理程序本身引发异常。 （非让异常传播，将保留在此页底部的反馈，如果有更好的方法。）异常记录器和处理程序的协定是他们不应该允许异常传播到其调用方;否则，该异常将只是传播，通常一直到主机从而导致 HTML 错误 （如 ASP。NET 的黄色屏幕） 发送回客户端 （这通常不是预期 JSON 或 XML 的 API 调用方的首的选项）。

## <a name="examples"></a>示例

### <a name="tracing-exception-logger"></a>跟踪的异常记录器

下面的异常记录器将异常数据发送到已配置的跟踪源 （包括 Visual Studio 中的调试输出窗口）。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>自定义错误消息的异常处理程序

下面的生成自定义错误响应向客户端，包括与支持部门联系的电子邮件地址。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>注册异常筛选器

如果使用"ASP.NET MVC 4 Web 应用程序"项目模板来创建你的项目，将 Web API 配置代码内的放`WebApiConfig`类，在*App/（_s)* 文件夹：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>附录： 基类的详细信息

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
