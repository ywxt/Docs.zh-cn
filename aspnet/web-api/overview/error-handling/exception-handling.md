---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API 中的异常处理 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2012
ms.topic: article
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: ac01a4f35cde99a1f8ec699e6d31bf597f1d334e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400815"
---
<a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API 中的异常处理
====================
通过[Mike Wasson](https://github.com/MikeWasson)

本指南介绍了错误和异常处理 ASP.NET Web API 中。

- [HttpResponseException](#httpresponserexception)
- [异常筛选器](#exception_filters)
- [注册异常筛选器](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

如果 Web API 控制器引发未捕获的异常，则会发生什么情况？ 默认情况下，大多数异常将转换为状态代码 500 内部服务器错误的 HTTP 响应。

**HttpResponseException**类型是一种特殊情况。 此异常将返回异常构造函数中指定任何 HTTP 状态代码。 例如，以下方法将返回 404，找不到，如果*id*参数无效。

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

更好地响应的控制，还可以构造的整个响应消息，并将其与包含**HttpResponseException:** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>异常筛选器

您可以自定义 Web API 通过编写处理异常的方式*异常筛选器*。 异常筛选器时，控制器方法引发任何未处理的异常时执行*不* **HttpResponseException**异常。 **HttpResponseException**类型是一种特殊情况，因为它专为返回的 HTTP 响应。

异常筛选器实现**System.Web.Http.Filters.IExceptionFilter**接口。 编写异常筛选器的最简单方法是从派生**System.Web.Http.Filters.ExceptionFilterAttribute**类并重写**OnException**方法。

> [!NOTE]
> ASP.NET Web API 中的异常筛选器是 ASP.NET MVC 中类似的。 但是，它们是在一个单独的命名空间和函数中单独声明。 具体而言， **HandleErrorAttribute**在 MVC 中使用的类不处理由 Web API 控制器引发的异常。


下面是将转换的筛选器**NotImplementedException**异常转化为 HTTP 状态代码 501，未实现：

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**响应**的属性**HttpActionExecutedContext**对象包含将发送到客户端的 HTTP 响应消息。

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>注册异常筛选器

有几种方法来注册 Web API 异常筛选器：

- 由操作
- 由控制器
- 全局

筛选器应用到特定的操作，请将作为属性的筛选器添加到操作：

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

筛选器应用到所有控制器上的操作，将筛选器作为属性添加到控制器类：

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

若要对 Web API 的所有控制器全局应用筛选器，将添加到筛选器的实例**GlobalConfiguration.Configuration.Filters**集合。 在此集合中的异常筛选器适用于任何 Web API 控制器操作。

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

如果使用"ASP.NET MVC 4 Web 应用程序"项目模板来创建你的项目，将 Web API 配置代码内的放`WebApiConfig`类，该类在应用程序位于\_开始文件夹：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

**HttpError**对象提供一致的方法来响应正文中返回的错误信息。 下面的示例演示如何返回 HTTP 状态代码 404 （找不到） 与**HttpError**响应正文中。

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**CreateErrorResponse**中定义的扩展方法**System.Net.Http.HttpRequestMessageExtensions**类。 在内部， **CreateErrorResponse**创建**HttpError**实例，然后创建**HttpResponseMessage** ，其中包含**HttpError**.

在此示例中，如果该方法成功，它将返回 HTTP 响应中的产品。 但是，如果找不到请求的产品，包含 HTTP 响应**HttpError**请求正文中。 响应可能如下所示：

[!code-console[Main](exception-handling/samples/sample9.cmd)]

请注意， **HttpError**在此示例中，已将它们序列化为 JSON。 使用的一个优点**HttpError**是转到通过同一[内容协商](../formats-and-model-binding/content-negotiation.md)和序列化处理任何其他强类型化模型。

### <a name="httperror-and-model-validation"></a>HttpError 和模型验证

可以为模型验证，请将传递到模型状态**CreateErrorResponse**，以在响应中包括的验证错误：

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

此示例中可能会返回以下响应：

[!code-console[Main](exception-handling/samples/sample11.cmd)]

有关模型验证的详细信息，请参阅[ASP.NET Web API 中的模型验证](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。

### <a name="using-httperror-with-httpresponseexception"></a>使用 HttpResponseException HttpError

前面的示例返回**HttpResponseMessage**消息从控制器操作，但您还可以使用**HttpResponseException**返回**HttpError**。 这样就可以返回强类型化模型中正常成功的情况下，同时仍返回**HttpError**如果出现错误：

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
