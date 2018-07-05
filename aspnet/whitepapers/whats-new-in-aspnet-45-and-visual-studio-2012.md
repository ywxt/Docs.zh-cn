---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: 什么是 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能 |Microsoft Docs
author: rick-anderson
description: 本文档介绍新功能和增强功能 ASP.NET 4.5 中引入的。 它还介绍了用于 web 开发正在进行的改进...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/29/2012
ms.topic: article
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
ms.technology: ''
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: e89b8faa7d513209436d40d15821694cf24fa453
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369342"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>什么是 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能
====================
> 本文档介绍新功能和增强功能 ASP.NET 4.5 中引入的。 它还介绍了 Visual Studio 2012 中针对 web 开发正在进行的改进。 本文档最初在 2012 年 2 月 29 日发布。


- [ASP.NET Core 运行时和框架](#_Toc318097372)

    - [以异步方式读取和写入 HTTP 请求和响应](#_Toc318097373)
    - [HttpRequest 处理的改进](#_Toc318097374)
    - [异步刷新响应](#_Toc318097375)
    - [为支持*await*并*任务*-基于异步模块和处理程序](#_Toc318097376)
    - [异步 HTTP 模块](#_Toc318097377)
    - [异步 HTTP 处理程序](#_Toc318097378)
    - [新的 ASP.NET 请求验证功能](#_Toc318097379)
    - [延迟 （"延迟"） 请求验证](#_Toc318097380)
    - [对未经过验证的请求的支持](#_Toc318097381)
    - [AntiXSS 库](#_Toc318097382)
    - [为 WebSockets 协议支持](#_Toc318097383)
    - [捆绑和缩小](#_Toc318097384)
    - [用于 Web 托管的性能改进](#_Toc_perf)

        - [关键性能因素](#_Toc_perf_1)
        - [新性能功能的要求](#_Toc_perf_2)
        - [共享公共程序集](#_Toc_perf_3)
        - [使用多核 JIT 编译的启动速度更快](#_Toc_perf_4)
        - [优化垃圾回收的内存优化](#_Toc_perf_5)
        - [为 web 应用程序的预提取](#_Toc_perf_6)
- [ASP.NET Web 窗体](#_Toc318097385)

    - [强类型化数据控件](#_Toc318097386)
    - [模型绑定](#_Toc318097387)

        - [选择数据](#_Toc318097388)
        - [值提供程序](#_Toc318097389)
        - [来自控件的值筛选](#_Toc318097390)
    - [HTML 编码的数据绑定表达式](#_Toc318097391)
    - [非介入式验证](#_Toc318097392)
    - [HTML5 更新](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 网页 2](#_Toc318097395)
- [Visual Studio 2012 候选发布版本](#_Toc318097396)

    - [Visual Studio 2010 和 Visual Studio 2012 Release Candidate （项目兼容性） 之间共享的项目](#project-compatibility)
    - [ASP.NET 4.5 网站模板中的配置更改](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [在 IIS 7 ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 编辑器](#_Toc318097397)

        - [智能任务](#_Toc318097398)
        - [WAI-ARIA 支持](#_Toc318097399)
        - [新的 HTML5 代码段](#_Toc318097400)
        - [提取到用户控件](#_Toc318097401)
        - [适用于在特性中的代码片段 IntelliSense](#_Toc318097402)
        - [匹配的标记重命名开始或结束标记时自动重命名](#_Toc318097403)
        - [生成事件处理程序](#_Toc318097404)
        - [智能缩进](#_Toc318097405)
        - [自动减少语句完成](#_Toc318097406)
    - [JavaScript 编辑器](#_Toc318097407)

        - [代码大纲显示](#_Toc318097408)
        - [大括号匹配](#_Toc318097409)
        - [转到定义](#_Toc318097410)
        - [ECMAScript5 的支持](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 签名重载](#_Toc318097413)
        - [隐式引用](#_Toc318097414)
    - [CSS 编辑器](#_Toc318097415)

        - [自动减少语句完成](#_Toc318097416)
        - [分层缩进。](#_Toc318097417)
        - [CSS 攻击支持](#_Toc318097418)
        - [供应商特定的架构 (-moz-，-易于使用的功能)](#_Toc318097419)
        - [注释和取消注释支持](#_Toc318097420)
        - [颜色选取器](#_Toc318097421)
        - [片段](#_Toc318097422)
        - [自定义区域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [发布](#_Toc318097425)

        - [发布配置文件](#_Toc318097426)
        - [ASP.NET 预编译和合并](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免责声明](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core 运行时和框架

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>以异步方式读取和写入 HTTP 请求和响应

ASP.NET 4 引入了读取为流使用的 HTTP 请求实体的功能*HttpRequest.GetBufferlessInputStream*方法。 此方法提供流式处理访问请求实体。 但是，它以同步方式执行，其中请求的持续时间内绑定到某个线程。

ASP.NET 4.5 支持读取以异步方式对 HTTP 请求实体，流的功能和能力以异步方式刷新。 ASP.NET 4.5 还提供了双缓冲 HTTP 请求实体，它提供更轻松地集成使用下游 HTTP 处理程序，例如.aspx 页处理程序和 ASP.NET MVC 控制器的功能。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 处理的改进

ASP.NET 4.5，从返回的 Stream 引用*HttpRequest.GetBufferlessInputStream*支持同步和异步读取的方法。 *Stream*从返回的对象*GetBufferlessInputStream*现在实现了 BeginRead 和 EndRead 方法。 异步*Stream*方法让你以异步方式读取请求实体的区块，而 ASP.NET 释放当前线程之间的异步读取循环每次迭代。

ASP.NET 4.5 还添加了用于缓冲的方式读取请求实体的配套方法： *HttpRequest.GetBufferedInputStream*。 此新重载的工作方式类似于*GetBufferlessInputStream*，支持同步和异步读取。 但是，因为它读取*GetBufferedInputStream*还将实体字节复制到 ASP.NET 内部缓冲区，以便下游模块和处理程序仍然可以访问请求实体。 例如，如果某些上游管道中的代码已经读取请求实体使用*GetBufferedInputStream*，仍可以使用*HttpRequest.Form*或*HttpRequest.Files*. 这允许您执行异步处理请求 （例如，流式处理大型文件上的传到数据库），但仍运行的.aspx 页和 ASP.NET MVC 控制器之后。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>异步刷新响应

发送到 HTTP 客户端的响应可能需要相当长的时间时客户端距离遥远，或具有低带宽连接。 通常情况下 ASP.NET 缓冲响应字节数，因为它们创建应用程序。 ASP.NET 然后执行一个发送操作的请求处理的最末尾应计缓冲区。

如果将缓冲的响应较大 （例如，流式传输到客户端的大型文件），则必须定期调用*HttpResponse.Flush*将缓冲的输出发送到客户端并保持受控制的内存使用情况。 但是，由于*刷新*是一个同步调用，以迭代方式调用*刷新*仍可能需要长时间运行请求的持续时间内使用一个线程。

ASP.NET 4.5 添加的使用以异步方式执行刷新的支持*BeginFlush*并*EndFlush*方法*HttpResponse*类。 使用这些方法，可以创建异步模块和异步处理程序以增量方式将数据发送到客户端而不必占用操作系统线程。 在中间*BeginFlush*并*EndFlush*调用，ASP.NET 释放当前线程。 这极大地减少了为了支持长时间运行 HTTP 下载所需要的活动线程的总数。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>为支持*await*并*任务*-基于异步模块和处理程序

.NET Framework 4 引入了异步编程概念，称为*任务*。 任务由*任务*类型和中的相关的类型*System.Threading.Tasks*命名空间。 使用编译器增强功能，请使用此生成.NET Framework 4.5*任务*简单的对象。 在.NET Framework 4.5 中，编译器都支持两个新关键字： *await*并*异步*。 *Await*关键字是速记语法用于指示在某些其他代码段以异步方式等待一段代码。 *异步*关键字都表示一个提示，可用于将方法标记为基于任务的异步方法。

组合*await*，*异步*，并*任务*对象可大大简化了.NET 4.5 中编写异步代码。 ASP.NET 4.5 支持这些简化与新的 Api，允许你编写异步 HTTP 模块和异步 HTTP 处理程序使用新的编译器增强功能。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>异步 HTTP 模块

假设你想要执行异步工作中返回的方法*任务*对象。 下面的代码示例定义进行异步调用，若要下载 Microsoft 主页上的异步方法。 请注意，使用*异步*方法签名中的关键字和*await*调用*DownloadStringTaskAsync*。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

这就是你已将所有 —.NET Framework 将自动处理时等待下载完成，以及自动完成下载后将还原的调用堆栈展开调用堆栈。

现在假设你想要在异步 ASP.NET HTTP 模块中使用此异步方法。 ASP.NET 4.5 包括一个帮助器方法 (*EventHandlerTaskAsyncHelper*) 和新的委托类型 (*TaskEventHandler*) 可用来集成有较旧的基于任务的异步方法公开的 ASP.NET HTTP 管道的异步编程模型。 此示例演示如何：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>异步 HTTP 处理程序

在 ASP.NET 中编写异步处理程序的传统方法是实现*IHttpAsyncHandler*接口。 ASP.NET 4.5 引入了*HttpTaskAsyncHandler*异步的基类型可以派生，这样，就更简单地编写异步处理程序。

*HttpTaskAsyncHandler*类型是抽象的要求你重写*ProcessRequestAsync*方法。 在内部 ASP.NET 负责集成返回签名的 (*任务*对象) 的*ProcessRequestAsync*与由 ASP.NET 管道中使用的较旧异步编程模型。

下面的示例演示如何使用*任务*并*await*作为异步 HTTP 处理程序的实现的一部分：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新的 ASP.NET 请求验证功能

默认情况下，ASP.NET 将执行请求验证，它会检查请求以查找标记或脚本中的字段、 标头、 cookie 和等等。 如果任何检测到，ASP.NET 将引发异常。 这相当于一系列第一个阻止潜在的跨站点脚本攻击的防御措施。

ASP.NET 4.5 轻松有选择地读取未经验证的请求数据。 ASP.NET 4.5 还集成了常用的 AntiXSS 库之前为外部库。

开发人员已经常要求能够有选择性地关闭对其应用程序的请求验证。 例如，如果你的应用程序论坛软件，您可能想要允许用户提交 HTML 格式的论坛帖子和提出的意见，但仍确保请求验证检查其他所有内容。

ASP.NET 4.5 引入了两项功能，可以轻松可以有选择地使用未经验证的输入： 延迟 （"延迟"） 请求验证和未经验证的请求数据访问权限。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>延迟 （"延迟"） 请求验证

在 ASP.NET 4.5 中，默认情况下所有请求数据都都需要进行请求验证。 但是，可以配置应用程序，以便将延迟实际访问请求数据请求验证。 （这有时称为延迟请求验证，基于的术语，例如延迟加载某些数据方案。）可以配置应用程序的 Web.config 文件中使用推迟的验证，通过设置*requestValidationMode*属性中的 4.5 *httpRUntime*元素，如以下示例所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

在请求验证模式设置为 4.5，仅针对特定请求值且仅当你的代码访问该值，会触发请求验证。 例如，如果你的代码获取的值的 Request.Form["forum\_发布"]，仅针对窗体集合中该元素调用请求验证。 无中的其他元素*窗体*集合进行验证。 在以前版本的 ASP.NET 中，请求验证已访问集合中的任何元素时找不到整个请求触发。 新行为轻松查看请求数据的不同部分而不会触发请求验证的其他部分不同的应用程序组件。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>对未经过验证的请求的支持

延迟的请求验证就不能解决有选择地绕过请求验证的问题。 调用 Request.Form["forum\_发布"] 仍触发器的请求验证该特定请求值。 但是，你可能想要访问此字段不触发验证，因为你想要允许该字段中的标记。

若要允许此操作，ASP.NET 4.5 现在支持对请求数据未经过验证的访问。 ASP.NET 4.5 包括一个新*Unvalidated*集合属性中的*HttpRequest*类。 此集合提供对所有请求数据的常见值访问类似*窗体*， *QueryString*， *Cookie*，以及*Url*。

使用论坛的示例中，若要能够读取未经验证的请求数据，首先需要配置应用程序以使用新的请求验证模式：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

然后，可以使用*HttpRequest.Unvalidated*读取未经验证的表单值的属性：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> 安全性-*谨慎使用未经验证的请求数据 ！* 添加 ASP.NET 4.5 中的未经验证的请求属性和集合以使你更轻松地访问非常具体未经验证的请求数据。 但是，仍必须在原始请求数据，以确保不向用户呈现危险的文本上执行自定义验证。


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 库

由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在结合了核心编码例程与库的版本 4.0。

由实现编码例程*AntiXssEncoder*中的新类型*System.Web.Security.AntiXss*命名空间。 可以使用*AntiXssEncoder*直接通过调用的任何静态类型中实现的编码方法的类型。 但是，使用新的防 XSS 例程的最简单方法是配置 ASP.NET 应用程序中使用*AntiXssEncoder*默认情况下的类。 若要执行此操作，请将以下属性添加到 Web.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

当*encoderType*属性设置为使用*AntiXssEncoder*类型，所有输出自动编码在 ASP.NET 中使用新的编码例程。

这些是已合并到 ASP.NET 4.5 中的外部 AntiXSS 库部分：

- *HtmlEncode*， *HtmlFormUrlEncode*，和*HtmlAttributeEncode*
- *XmlAttributeEncode*和*XmlEncode*
- *UrlEncode*并*UrlPathEncode* （新）
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>为 WebSockets 协议支持

Websocket 协议是一种基于标准的网络协议，用于定义如何建立基于 HTTP 的客户端和服务器之间的安全、 实时的双向通信。 Microsoft 已经与 IETF 和 W3C 标准主体，以帮助定义的协议。 Websocket 协议被支持任何客户端 （而不仅仅是浏览器），与 Microsoft 投资 WebSockets 协议支持客户端和移动操作系统上的大量资源。

Websocket 协议进行创建客户端和服务器之间的长时间运行的数据传输容易得多。 例如，编写的聊天应用程序是更容易的因为您可以建立客户端和服务器之间，则返回 true 的长时间运行连接。 不需要求助于如定期轮询或 HTTP 长轮询模拟套接字的行为的解决方法。

ASP.NET 4.5 和 IIS 8 包括低级别的 Websocket 支持，使 ASP.NET 开发人员能够使用托管的 Api，用于以异步方式读取和写入 Websocket 对象上的字符串和二进制数据。 为 ASP.NET 4.5 新增了一个*System.Web.WebSockets*包含用于使用 WebSockets 协议的类型的命名空间。

浏览器客户端会建立 Websocket 连接，通过创建 DOM *WebSocket*中 ASP.NET 应用程序，如以下示例所示的 URL 所指向的对象：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

可以在 ASP.NET 中使用任何类型的模块或处理程序创建 Websocket 终结点。 在上一示例中，使用.ashx 文件，因为.ashx 文件创建一个处理程序的快速方法。

根据 Websocket 协议，ASP.NET 应用程序接受客户端的 Websocket 请求通过指示请求应从 HTTP GET 请求升级到 Websocket 请求。 以下是一个示例：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest*方法接受一个函数委托，因为 ASP.NET 展开当前 HTTP 请求，然后将控制权转交给函数委托。 从概念上讲这种方法是类似于你如何使用*System.Threading.Thread*，其中定义在后台中执行工作的线程启动委托。

ASP.NET 和客户端已成功完成 Websocket 握手后，ASP.NET 将调用您的代理和 Websocket 应用程序开始运行。 下面的代码示例显示了在 ASP.NET 中使用内置的 Websocket 支持的简单的回显应用程序：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

在.NET 4.5 中的支持*await*关键字和基于任务的异步操作是生就很适合编写 Websocket 的应用程序。 代码示例演示在 ASP.NET 内完全以异步方式运行的 Websocket 请求。 应用程序以异步方式等待通过调用从客户端发送一条消息*await 套接字。ReceiveAsync*。 同样，您可以将异步消息给客户端通过调用*await 套接字。SendAsync*。

在浏览器应用程序接收通过 Websocket 消息*onmessage*函数。 若要从浏览器发送一条消息，请调用*发送*方法*WebSocket* DOM 类型，在此示例中所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

将来，我们可能会发布此功能，抽象消失的低级别的编码，它一些需要在此版本中用于 Websocket 的应用程序的更新。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>捆绑和缩小

绑定可以将各个 JavaScript 和 CSS 文件合并到一个包，可以被视为单个文件。 缩小会 JavaScript 和 CSS 文件将通过删除空白并不是必需的其他字符。 这些功能适用于 Web 窗体、 ASP.NET MVC 和 Web Pages。

使用 Bundle 类或其子类别，ScriptBundle 和 StyleBundle 创建捆绑包。 在配置的绑定实例之后, 捆绑包可对传入的请求只需将其添加到全局 BundleCollection 实例。 默认模板中的绑定配置执行 BundleConfig 文件中。 这种默认配置创建的所有核心脚本和模板使用的 css 文件的捆绑包。

捆绑包将引用从在视图内使用几个可能的帮助器方法之一。 为了支持呈现不同的标记，在发布模式下与调试时绑定，ScriptBundle 和 StyleBundle 类必须呈现的帮助器方法。 如果处于调试模式，呈现器将生成捆绑中的每个资源的标记。 在发布模式下，当呈现器将生成整个绑定的单个标记元素。 切换调试和发布之间，可以通过修改 web.config 中的元素的调试属性，如下所示实现模式：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

此外，可以直接通过 BundleTable.EnableOptimizations 属性设置启用或禁用优化。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

绑定文件，则将首先排序按字母顺序 (中所显示的方式**解决方案资源管理器**)。 它们然后的组织方式，以便知道库以及其自定义扩展插件 （如 jQuery、 MooTools 和 Dojo） 首次加载。 例如，将为绑定脚本文件夹中，如上面所示的最终顺序：

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 文件是按字母顺序排序，然后重新组织，以便 reset.css 和要优先于 normalize.css 出现之前的任何其他文件。 绑定 Styles 文件夹如上所示的最终排序将为此：

1. reset.css
2. content.css
3. forms.css
4. globals.css
5. menu.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>用于 Web 托管的性能改进

.NET Framework 4.5 和 Windows 8 引入了功能，可帮助您实现显著的性能提升为 web 服务器工作负荷。 这包括减少 （最多 35%) 在这两个启动时间和中的内存占用量 web 宿主使用 ASP.NET 的网站。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>关键性能因素

理想情况下，所有网站应都处于活动状态，并且在内存中以确保快速响应的下一个请求，只要涉及。 可能会影响网站响应能力的因素包括：

- 为站点的应用池回收后重新启动花费的时间。 这是网站程序集将不再在内存中时启动该站点在 web 服务器进程所需的时间。 （平台程序集是仍在内存中，因为它们由其他站点。）这种情况下被称为"冷站点，热 framework 启动"或只是"冷站点启动。"
- 站点占用的内存量。 此术语是"每个站点的内存使用情况"取消共享工作集。"

新的性能改进重点介绍这两种因素。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>新性能功能的要求

新功能的要求可以分为以下类别：

- 在.NET Framework 4 运行的改进。
- 需要.NET Framework 4.5，但可以在任何版本的 Windows 上运行的改进。
- 可仅与 Windows 8 上运行的.NET Framework 4.5 的改进。

性能会增加与改进，可以启用每个级别。

某些.NET Framework 4.5 改进充分利用更广泛应用于其他方案的性能功能。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共享公共程序集

**要求**:.NET Framework 4 和 Visual Studio 11 开发者预览版 SDK

在服务器上的不同站点通常使用同一个帮助程序程序集 （例如，从初学者工具包或示例应用程序的程序集）。 每个站点及其 Bin 目录中有其自己的这些程序集副本。 即使对象代码的程序集是相同的它们是物理上独立的程序集，以便每个程序集必须在冷站点启动期间单独读取和单独保留在内存中。

新 interning 功能解决了这种低效情况并减少内存需求和负载时间。 暂留可让 Windows 在文件系统中，保留每个程序集的单个副本和站点的 Bin 文件夹中的单个程序集将替换单个副本的符号链接。 如果单个站点需要不同版本的程序集，符号链接替换为新版本的程序集，并仅该站点受到影响。

共享使用符号链接的程序集需要名为 aspnet 的新工具\_intern.exe，可以创建和管理的存储中暂留的程序集。 它作为 Visual Studio 11 开发人员预览版 SDK 的一部分提供。 (但是，它将在仅安装.NET Framework 4，如果你已安装最新的系统上运行[更新](https://support.microsoft.com/kb/2468871)。)

若要确保所有符合条件的程序集具有暂留，请运行 aspnet\_intern.exe 定期 （例如，每周一次作为计划任务）。 一种典型用法如下所示：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

若要查看所有选项，请不带任何参数运行该工具。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>使用多核 JIT 编译的启动速度更快

**要求**:.NET Framework 4.5

对于冷站点启动时，不仅执行程序集必须从磁盘中读取，但站点必须是 JIT 编译。 对于复杂的站点，这可以添加严重的延迟。 .NET Framework 4.5 中新的通用方法通过 JIT 编译分散到可用处理器核数降低这些延迟。 做到这一点的尽可能多，并尽早使用期间收集的信息之前启动的站点。 此功能由实现[System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法。

因此不需要执行任何操作来利用此功能，使用多核 JIT 编译是在 ASP.NET 中，默认情况下启用。 如果你想要禁用此功能，请在 Web.config 文件中进行以下设置：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>优化垃圾回收的内存优化

**要求**:.NET Framework 4.5

站点运行后，其使用的垃圾回收器 (GC) 堆可以导致其内存使用量的重要因素。 任何垃圾回收器，如.NET Framework GC 使 CPU 时间 （频率和重要性的集合） 和内存消耗 （用于新的、 已释放，或可释放的对象的额外空间） 方面做出权衡。 针对早期版本中，我们提供了指导如何配置之间取得最佳平衡，GC (有关示例，请参阅[ASP.NET 2.0/3.5 共享托管配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。

.NET Framework 4.5 中，而不是多个独立设置，工作负荷定义的配置设置是可用的启用的所有以前建议的 GC 设置，以及新的优化，可提供有关每个站点的其他性能工作集。

若要启用优化的 GC 内存，请将以下设置添加到 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(如果您熟悉到 aspnet.config 更改前面的指导，请注意，此设置将替代旧设置 — 例如，没有必要设置 gcServer、 gcConcurrent，等等。您无需删除旧设置。）

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>为 web 应用程序的预提取

**要求**: Windows 8 上运行的.NET Framework 4.5

Windows 具有几个版本包含一种技术称为[取](http://en.wikipedia.org/wiki/Prefetcher)这样做可以减小应用程序启动的磁盘读取成本。 由于冷启动是主要的客户端应用程序问题，这一技术尚未包含在 Windows Server 中，其中包含对 server 至关重要的组件。 预提取现已推出 Windows Server，它可以在其中优化单独的网站的发布的最新版本。

适用于 Windows Server 在默认情况下不启用取。 若要启用和配置用于高密度 web 托管取，请在命令行运行以下命令集：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

然后，与 ASP.NET 应用程序集成取，以下代码添加到 Web.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>强类型化的数据控件

在 ASP.NET 4.5 Web 窗体包含用于处理数据的一些改进。 第一个改进是强类型化的数据控件。 对于在以前版本的 ASP.NET Web 窗体控件，显示数据绑定值使用*Eval*和数据绑定表达式：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

使用双向数据绑定*绑定*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

在运行时，这些调用使用反射来读取指定的成员的值，然后在标记中显示的结果。 这种方法可以轻松将针对任意、 unshaped 数据的数据绑定。

但是，此类数据绑定表达式不为成员名称、 导航 （例如，请转到定义） 或编译时检查这些名称支持 IntelliSense 等功能。

若要解决此问题，ASP.NET 4.5，请添加了声明将控件绑定到的数据的数据类型的功能。 执行此操作使用新*ItemType*属性。 当设置此属性时，两个新的类型化的变量中的数据绑定表达式作用域有：*项*并*BindItem*。 由于强类型化变量，可以获得完整的 Visual Studio 开发体验。


对于双向数据绑定表达式，使用*BindItem*变量：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


支持数据绑定的 ASP.NET Web 窗体框架中的大多数控件已更新，以支持*ItemType*属性。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>模型绑定

模型绑定扩展了 ASP.NET Web 窗体控件中的数据绑定来处理的代码为中心的数据访问。 它包含从概念*ObjectDataSource*控件和从 ASP.NET MVC 中的模型绑定。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>选择数据

若要配置以使用模型绑定选择数据的数据控件，设置控件的*SelectMethod*属性设置为在页面的代码中方法的名称。 数据控件在页生命周期中的适当时间调用的方法，并自动将绑定返回的数据。 无需显式调用*DataBind*方法。

在以下示例中， *GridView*控件配置为使用一个名为方法*GetCategories*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

您创建*GetCategories*页面的代码中的方法。 对于简单的选择操作，该方法不需要参数，且应返回*IEnumerable*或*IQueryable*对象。 如果新*ItemType*属性设置 (它使强类型化数据绑定表达式，如下面所述[强类型数据控件](#_Toc318097386)之前)，这些接口的泛型版本应返回 — *IEnumerable&lt;T&gt;* 或*IQueryable&lt;T&gt;*，与*T*参数类型相匹配*ItemType*属性 (例如， *IQueryable&lt;类别&gt;*)。

下面的示例演示的代码*GetCategories*方法。 此示例使用 Northwind 示例数据库中使用 Entity Framework Code First 模型。 代码可确保查询将返回方式由的每个类别的相关产品的详细信息*Include*方法。 (这可确保*TemplateField*标记中的元素而无需在每个类别中显示的产品计数[n + 1 选择](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)。)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

当该页运行时，则*GridView*控制调用*GetCategories*方法自动呈现返回使用已配置的字段的数据：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

由于选择的方法会返回*IQueryable*对象， *GridView*控件可以进一步执行前操作查询。 例如， *GridView*控件可以添加用于排序和分页到返回的查询表达式*IQueryable*对象之前执行，以便这些操作均由基础LINQ 提供程序。 在这种情况下，实体框架将确保在数据库中执行这些操作。

下面的示例演示*GridView*控件修改，以便允许排序和分页：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

现在页运行时，该控件可确保显示数据的当前页并按所选列进行排序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

若要筛选返回的数据，需要添加到 select 方法参数。 这些参数将包含在运行时，模型绑定和可用于返回数据之前更改查询。

例如，假设你想要让用户筛选器产品，通过在查询字符串中输入一个关键字。 可以将参数添加到方法，并更新代码以使用参数值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

此代码包括*其中*表达式，如果提供的值*关键字*然后返回查询结果。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>值提供程序

前面的示例不是特定的位置的值*关键字*参数来自。 若要指示此信息，可以使用参数属性。 对于此示例中，可以使用*QueryStringAttribute*中的类*System.Web.ModelBinding*命名空间：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

这会指示要尝试将值绑定到查询字符串中的模型绑定*关键字*在运行时参数。 （这可能涉及执行类型转换，尽管它不会在这种情况下。）如果不能提供一个值，并且该类型是不可以为 null，则将引发异常。

指示要使用的值提供程序的参数属性统称为值提供程序属性和作为值提供程序，这些方法的值的源引用的。 Web 窗体将包括在 Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态，会话状态和配置文件属性值提供程序和所有典型的资源，用户输入的相应属性。 此外可以编写自定义值提供程序。

默认情况下，参数名称用于作为键的值提供程序集合中查找一个值。 在示例中，代码将查找名为关键字的查询字符串值 (例如，~ / default.aspx?keyword=chef)。 可以通过将它作为参数传递给参数特性来指定自定义密钥。 例如，若要使用名为 q 的查询字符串变量的值，无法执行此操作：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

如果此方法是在页面的代码中，用户可以通过使用查询字符串的关键字筛选结果：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

模型绑定可实现许多任务，否则必须手动编写的代码： 读取的值、 检查 null 值、 尝试将其转换为适当的类型、 检查转换是否成功，和最后，使用中的值查询。 模型绑定结果，很少的代码在和中能够重复使用在整个应用程序的功能。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>来自控件的值筛选

假设你想要扩展的示例，以便用户可以从下拉列表中选择筛选器值。 向标记添加下面的下拉列表并将其配置为从另一个方法使用获取数据*SelectMethod*属性：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常还会添加*要*元素*GridView*控件，以便控件将显示一条消息，如果找不到任何匹配的产品：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

在页代码中，将添加新的选择下拉列表的方法：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最后，更新*GetProducts*选择要包含下拉列表从所选类别的 ID 的新参数：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

现在页运行时，用户可以从下拉列表中，选择某个类别并*GridView*控件是否自动显示经过筛选的数据重新绑定。 这可能是因为模型绑定跟踪选择方法的参数的值，并检测到在回发后是否已更改的任何参数值。 如果是这样，模型绑定将强制关联的数据控件重新绑定到数据。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 编码的数据绑定表达式

你可以立即进行 HTML 编码数据绑定表达式的结果。 将冒号 （:） 添加到末尾&lt;%# 前缀将标记数据绑定表达式：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>非介入式验证

现在可以配置的内置验证程序控件可以将非介入式 JavaScript 用于客户端验证逻辑。 这大大减少了呈现页面标记中的内联 JavaScript 并减少整体的页面大小。 可以按照以下任意方式来配置非介入式 JavaScript 验证程序控件：

- 添加以下设置，从而全局*&lt;appSettings&gt;* Web.config 文件中的元素： 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 通过设置静态全局*System.Web.UI.ValidationSettings.UnobtrusiveValidationMode*属性设置为*UnobtrusiveValidationMode.WebForms* (通常是在*应用程序\_启动*Global.asax 文件中的方法)。
- 通过设置新页为单独*UnobtrusiveValidationMode*的属性*页面*类来*UnobtrusiveValidationMode.WebForms*。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 更新

某些已得到改进 Web 窗体服务器控件能够充分利用 HTML5 的新功能：

- *TextMode*的属性*文本框*控件已更新以支持新的 HTML5 输入的类型等*电子邮件*， *datetime*，和等等。
- *FileUpload*控件现在支持多个文件上传从支持此 HTML5 功能的浏览器。
- 验证程序控件现在支持验证 HTML5 输入的元素。
- 了现在表示 URL 的属性的新 HTML5 元素支持 runat ="server"。 因此，您可以使用 ASP.NET 约定中 URL 路径，如 ~ 运算符来表示应用程序根目录 (例如，&lt;视频 runat ="server"src="~/myVideo.wmv"/&gt;)。
- *UpdatePanel*控件已修复，以便支持发布 HTML5 输入的字段。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 beta 版现已随附 Visual Studio 11 Beta。 ASP.NET MVC 是一个框架，用于通过利用模型-视图-控制器 (MVC) 模式开发高度可测试性和可维护 Web 应用程序。 ASP.NET MVC 4 轻松地为移动 Web 构建应用程序，并包含 ASP.NET Web API，它可帮助你构建 HTTP 服务可以访问任何设备。 有关详细信息，请参阅[ASP.NET MVC 4 发行说明](mvc4-release-notes.md)。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 网页 2

新功能包括：

- 新的和更新站点模板。
- 添加服务器端和客户端验证使用*验证*帮助器。
- 若要注册脚本使用资产管理器功能。
- 正在启用 Facebook 和其他站点使用 OAuth 和 OpenID 登录名。
- 使用添加图*映射*帮助器。
- 运行网页的应用程序的并排方案。
- 移动设备的呈现页。

有关这些功能和整页的代码示例的详细信息，请参阅[Web Pages 2 Beta 中的常用功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 测试版

本部分提供有关 Visual Web Developer 11 测试版和 Visual Studio 2012 Release Candidate 中的 web 开发的改进的信息。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 和 Visual Studio 2012 Release Candidate （项目兼容性） 之间共享的项目

Visual Studio 2012 候选发布版本，直到在较新版本的 Visual Studio 中打开现有项目启动转换向导。 这强制内容 （资产） 的项目和解决方案升级为新格式的内容不向后兼容。 因此，在转换后您无法打开该项目在 Visual Studio 的较旧版本中。

许多客户告诉我们这不是正确的方法。 在 Visual Studio 11 Beta，我们现在支持共享项目和解决方案的 Visual Studio 2010 SP1。 这意味着，如果您在 Visual Studio 2012 候选发布版本中打开 2010年项目，您将仍将能够在 Visual Studio 2010 SP1 中打开项目。

> [!NOTE]
> 一些类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 候选发布版本之间共享。 其中包括一些较旧的项目 （如 ASP.NET MVC 2 项目） 或项目出于特定目的 （如安装程序项目）。

当在 Visual Studio 11 Beta 中首次打开 Visual Studio 2010 SP1 Web 项目时，以下属性添加到项目文件：

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags、 UpgradeBackupLocation 和 OldToolsVersion 升级项目文件的进程使用。 它们都使用 Visual Studio 2010 中的项目没有影响。

VisualStudioVersion 是由 MSBuild 4.5，该值指示当前项目的版本的 Visual Studio 的新属性。 在 MSBuild 4.0 （Visual Studio 2010 SP1 使用的 MSBuild 版本） 中不存在此属性，因为我们将默认值注入到项目文件。

VSToolsPath 属性用于确定要导入从 MSBuildExtensionsPath32 设置所表示的路径的正确.targets 文件。

此外，还有与导入元素相关的一些更改。 为了支持这两个版本的 Visual Studio 之间的兼容性需要这些更改。

> [!NOTE]
> 如果项目 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之间在两台不同计算机上共享，并且该项目包括在应用中的本地数据库\_Data 文件夹中，您必须确保所使用的数据库的 SQL Server 的版本是在这两台计算机上安装。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 网站模板中的配置更改

为默认值进行了以下更改*Web.config*在 Visual Studio 2012 候选发布版本中使用的网站模板创建的网站文件：

- 在中`<httpRuntime>`元素，`encoderType`属性现在设置默认情况下，若要使用 AntiXSS 类型已添加到 ASP.NET。 有关详细信息，请参阅[AntiXSS 库](#_Toc318097382)。
- 另外，请在`<httpRuntime>`元素，`requestValidationMode`属性设置为"4.5"。 这意味着默认情况下，请求验证配置为使用推迟的 （"延迟"） 验证。 有关详细信息，请参阅[新的 ASP.NET 请求验证功能](#_Toc318097379)。
- `<modules>`的元素`<system.webServer>`部分不包含`runAllManagedModulesForAllRequests`属性。 （其默认值为 false。）这意味着，如果使用尚未更新到 SP1 的 IIS 7 的版本，则可能必须使用新的站点中的路由问题。 有关详细信息，请参阅[在 IIS 7 ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)。

这些更改不会影响现有应用程序。 但是，它们可能表示之间的现有网站和 ASP.NET 4.5 使用新的模板创建的新网站的行为差异。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>在 IIS 7 ASP.NET 路由中的本机支持

这不是这种情况下，更改到 ASP.NET，但如果你正在 IIS 7 未应用 SP1 更新的版本会影响你的新网站项目的模板中的更改。

在 ASP.NET 中，您可以将以下配置设置添加到应用程序以支持路由：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

时**runAllManagedModulesForAllRequests**是 true 时，URL 如所示`http://mysite/myapp/home`进入 ASP.NET 中，即使没有任何 *.aspx*， *.mvc*，或在类似扩展URL。

IIS 7，已更新可**runAllManagedModulesForAllRequests**设置不必要和支持 ASP.NET 路由以本机方式。 (有关更新的信息，请参阅 Microsoft 支持文章[更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾](https://support.microsoft.com/kb/980368)。)

如果你的网站正在 IIS 7 上运行，并且如果 IIS 已更新，不需要设置**runAllManagedModulesForAllRequests**为 true。 实际上，将其设置为 true 不是建议，因为它会添加不必要的处理开销请求。 当此设置为 true 时，所有请求，其中包含用于 *.htm*， *.jpg*，和其他静态文件，也都经过了 ASP.NET 请求管道。

如果创建新的 ASP.NET 4.5 网站使用 Visual Studio 2012 RC 中提供的模板，为网站配置不包括**runAllManagedModulesForAllRequests**设置。 这意味着默认情况下设置为 false。

然后，如果您运行该网站在 Windows 7 上没有安装 SP1 的情况下，IIS 7 将不包括所需的更新。 因此，路由不起作用，将看到错误。 如果您遇到的问题，路由不起作用，可以执行以下任一操作：

- 更新到 SP1，这样会将更新添加到 IIS 7 的 Windows 7。
- 安装在前面列出的 Microsoft 技术支持文章中所述的更新。
- 设置**runAllManagedModulesForAllRequests**为 true，该网站的 Web.config 文件中。 请注意，这将向请求添加一些开销。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 编辑器

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>智能任务

在设计视图中，复杂属性的服务器控件通常具有关联的对话框和向导，可轻松地将其设置。 例如，使用特殊的对话框中，若要添加到的数据源*Repeater*控制或将列添加到*GridView*控件。

但是，这种类型的复杂属性的用户界面帮助尚未在源视图中可用。 因此，Visual Studio 11 引入了源视图的智能任务。 智能任务是在 C# 和 Visual Basic 编辑器中的常用功能的上下文感知快捷方式。

对于 ASP.NET Web 窗体控件，智能任务显示服务器标记为较小的标志符号时插入点放在元素内，则：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

单击字形或按 CTRL + 时，将扩展智能任务。 （圆点），就像在代码编辑器中一样。 然后，它将显示类似于设计视图中的智能任务的快捷方式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

例如，智能任务在上图中显示的 GridView 任务选项。 如果选择编辑列，将显示以下对话框：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

填写对话框设置相同的属性可以设置在设计视图中。 当您单击确定时，是使用新的设置更新控件的标记：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 支持

编写可访问的网站变得越来越重要。 [WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义开发人员应如何编写可访问的网站。 在 Visual Studio 中现在完全支持此标准。

例如，*角色*属性现在具有完整的 IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 标准还引入了带有前缀的特性*aria-* 能够让你将语义添加到 HTML5 文档。 Visual Studio 也完全支持这些*aria-* 属性：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新的 HTML5 代码段

若要使其更快、 更轻松地编写常用的 HTML5 标记，Visual Studio 提供了大量的代码段。 视频的代码段是一个示例：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

调用代码段，按 Tab 键两次时在 IntelliSense 中选择元素：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

这将产生了可以自定义的段。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>提取到用户控件

在大型 web 页中，它可以是一个好办法将各个部分移动到用户控件。 这种形式的重构可帮助提高页面的可读性和可简化对页结构。

若要简化此过程，编辑源视图中的 Web 窗体页时，您可以立即在页面中选择文本，右键单击它，，然后选择中的提取到用户控件：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>适用于在特性中的代码片段 IntelliSense

Visual Studio 一直在为服务器端代码片段中的任何页面或控件提供 IntelliSense。 现在 Visual Studio 包括 IntelliSense 以及 HTML 属性中的代码片段。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

这使得更轻松地创建数据绑定表达式：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>匹配的标记重命名开始或结束标记时自动重命名

如果重命名的 HTML 元素 (例如，更改*div*标记为*标头*标记)，则相应的打开或关闭标记也发生实时更改。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

这有助于避免忘记更改结束标记或更改的错误的一个错误。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>生成事件处理程序

Visual Studio 现在包含在源视图，以帮助您编写事件处理程序并将其手动绑定中的功能。 如果正在编辑源视图中的事件名称，IntelliSense 将显示&lt;创建新事件&gt;，此操作将创建一个事件处理程序中页面的代码，具有正确的签名：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

默认情况下，事件处理程序将使用控件的 ID 的事件处理方法的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

生成事件处理程序将如下所示 （在这种情况下，在 C# 中）：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>智能缩进

当您按 Enter 空 HTML 元素中的时，编辑器将在适当的位置将插入点：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

如果按 Enter 在此位置，结束标记是向下移动和缩进，以匹配的开始标记。 插入点还缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

Visual Studio 现在筛选器基于，以便它显示仅与相关的选项键入的内容中的 IntelliSense 列表：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 筛选器也基于智能感知列表中的各单词的词首字母大写。 例如，如果键入"dl"时，会显示 dl 和 asp: DataList:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

此功能，可更快地获取已知元素的语句完成。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 编辑器

Visual Studio 2012 Release Candidate 中的 JavaScript 编辑器是一个全新并极大地提高了使用 Visual Studio 中的 JavaScript 的体验。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>代码大纲显示

大纲区域现在会自动创建的所有函数，允许您折叠不相关的当前焦点的文件部分。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>大括号匹配

将插入点放上一个开始标记或右大括号后，编辑器突出显示匹配的一个。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>转到定义

转到定义命令，可以跳转到函数或变量的源。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 的支持

在编辑器中 ECMAScript5，介绍了 JavaScript 语言的标准的最新版本支持的新语法和 Api。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

IntelliSense for DOM Api 已得到改进，支持许多新 HTML5 Api 包括*querySelector*，DOM 存储，跨文档消息传送，并*画布*。 DOM IntelliSense 现在是驱动通过一个简单的 JavaScript 文件，而不是本机类型库定义。 这样，可以轻松进行扩展或替换。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 签名重载

详细的 IntelliSense 注释现在为单独的 JavaScript 函数的重载使用新的声明*&lt;签名&gt;* 元素，在此示例中所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>隐式引用

现在可以添加 JavaScript 文件，将隐式包含的文件列表中任何给定的 JavaScript 文件或块的引用，这意味着，你将获得用于其内容的 IntelliSense 的集中列表。 例如，可以将 jQuery 文件添加到中央列表的文件，并你将获得 IntelliSense 用于 jQuery 函数在文件中，任何 JavaScript 块中是否已显式引用它 (使用 / /&lt;引用 /&gt;) 或不。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 编辑器

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

CSS 现在筛选器基于的 CSS 属性和值受所选架构的智能感知列表。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense 还支持标题大小写搜索：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>分层缩进

CSS 编辑器使用缩进显示层次结构的规则，这将使您的级联规则的逻辑上组织方式概述。 在以下示例中，#list 选择器列表的级联子项，因此缩进。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

下面的示例显示了更复杂的继承：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

规则的缩进取决于其父规则。 默认情况下，启用分层缩进，但您也可以禁用选项对话框中 （工具，从菜单栏中的选项）：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 攻击支持

数百个实际 CSS 文件的分析显示 CSS 攻击是很常见，并且 Visual Studio 现在支持最广泛使用的。 此支持包括 IntelliSense 和验证在星型 (\*) 和下划线 (\_) 属性技巧：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

典型的选择器技巧也支持，以便即使在将其应用维护分层缩进。 用于映射到目标 Internet Explorer 7 典型选择器技巧，也是与一个选择器前面加上 *\*： 第一个子 + html*。 使用该规则将维护分层缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>供应商特定的架构 (-moz--webkit)

CSS3 引入了在不同的时间由不同的浏览器实现的许多属性。 这以前通过使用特定于供应商的语法的强制开发人员对特定浏览器的代码。 现在在 IntelliSense 中包含这些特定于浏览器的属性。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>注释和取消注释支持

现在可以添加注释和取消注释使用的相同的快捷方式 （Ctrl + K、 注释为 C 和 Ctrl + K，您可以取消注释） 在代码编辑器中使用的 CSS 规则。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>颜色选取器

在以前版本的 Visual Studio 中，IntelliSense 的颜色相关属性包括已命名的颜色值的下拉列表。 该列表已替换为全功能颜色选取器。

当您输入颜色值时，颜色选取器，将自动显示并显示一个列表的以前用过跟默认颜色调色板的颜色。 可以选择使用鼠标或键盘的颜色。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

列表可以扩展到完成颜色选取器。 在选取器可用于通过自动转换为任何颜色 RGBA 不透明度滑块移动时控制 alpha 通道：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>代码段

CSS 编辑器中的代码段可使其更加容易和快速创建跨浏览器样式。 需要特定于浏览器设置的许多 CSS3 属性现在为代码片段已回滚。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 代码段支持高级的方案 （如 CSS3 媒体查询），通过键入 at 符号 (@)，它显示了智能感知列表。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

当选择@media值并按 Tab，CSS 编辑器将插入以下代码片段：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

与代码的代码段，可以创建自己的 CSS 代码段。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>自定义区域

名为代码区域，已在代码编辑器中可用，现可用于编辑 CSS。 这样可以轻松地分组相关的样式块。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

一个区域处于折叠状态时将显示区域的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

Page Inspector 是一款呈现网页 （HTML、 Web 窗体、 ASP.NET MVC 或网页） 在 Visual Studio IDE 中，并允许您检查源代码和生成的输出。 对于 ASP.NET 页面，Page Inspector 允许您确定哪些服务器端代码生成到浏览器呈现的 HTML 标记。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

有关 Page Inspector 的详细信息，请参阅以下教程：

- 使用 Page Inspector 中[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- 使用 Page Inspector 中[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>发布

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>发布配置文件

在 Visual Studio 2010 中，Web 应用程序项目的发布信息不存储在版本控制中并不适合与他人共享。 在 Visual Studio 2012 候选发布版，已更改的发布配置文件的格式。 变得一个团队项目，并且现在可以轻松地从基于 MSBuild 的生成使用。 生成配置的信息是在发布对话框中，以便您可以轻松地切换发布前的生成配置。

发布配置文件存储在 PublishProfiles 文件夹中。 文件夹的位置取决于正在使用哪种编程语言：

- C#: Properties\PublishProfiles
- 我 Project\PublishProfiles Visual Basic:

每个配置文件是一个 MSBuild 文件。 在发布期间，此文件导入项目的 MSBuild 文件。 在 Visual Studio 2010 中，如果你想要更改包或发布过程中，则必须将你的自定义放入名为的文件**ProjectName**。 wpp.targets。 仍受支持，但现在可以将你的自定义放入发布配置文件本身。 这样一来，仅为该配置文件，将使用自定义项。

你可以现在还利用发布配置文件从 MSBuild。 为此，请使用以下命令生成项目时：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Project.csproj 值是项目的路径和 ProfileName 是要发布的配置文件的名称。 或者，而不是传递的配置文件名称*PublishProfile*属性，您可以传入的完整路径的发布配置文件。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 预编译和合并

对于 Web 应用程序项目，Visual Studio 2012 候选发布版本中添加一个选项，可以预编译和合并发布时你的站点内容或包项目的打包/发布 Web 属性页上。 若要查看这些选项，用鼠标右键单击解决方案资源管理器中的项目，选择属性，然后选择打包/发布 Web 属性页。 下图显示预编译此应用程序，然后发布选项。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

选中此选项后，Visual Studio 预编译的应用程序每次您发布或打包 web 应用程序。 如果你想要控制如何预编译站点或如何合并程序集，请单击高级按钮以配置这些选项。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

在 Visual Studio 中测试 web 项目的默认 web 服务器现在是 IIS Express。 Visual Studio 开发服务器仍在开发期间，本地 web 服务器的选项，但 IIS Express 现在是建议的服务器。 在 Visual Studio 11 Beta 中使用 IIS Express 的体验是非常类似于在 Visual Studio 2010 SP1 中使用它。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。

(C) 2012 Microsoft Corporation。 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。
