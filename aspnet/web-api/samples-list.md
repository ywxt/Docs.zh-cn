---
uid: web-api/samples-list
title: Web API 示例列表 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 09/18/2012
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: d25e0890a1b8d42cc638117f7bef9cf6457f3d75
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831063"
---
<a name="web-api-samples-list"></a>Web API 示例列表
====================
## <a name="httpclient-samples"></a>HttpClient 示例

**必应翻译示例** | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

演示如何调用[Microsoft Translator 服务](https://msdn.microsoft.com/library/ff512419.aspx)使用**HttpClient**类。 Microsoft Translator 服务 API 需要的 OAuth 令牌，应用程序获取的请求发送到 translator 服务的每个请求令牌的 Azure 服务器。 令牌的服务器的结果填充到发送给翻译服务的请求。 运行此示例之前，必须获取[从 Azure Marketplace 的应用程序密钥](https://msdn.microsoft.com/library/hh454950.aspx)并填写 AccessTokenMessageHandler 示例类中的信息。

**Google 地图示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

使用**HttpClient**若要下载的映射从 Redmond，WA [Google 地图 API](https://developers.google.com/maps/)、 将其保存为本地文件，并打开默认图像查看器。

**Twitter 客户端示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

演示如何编写使用简单的 Twitter 客户端**HttpClient**。 此示例使用**HttpMessageHandler** OAuth 身份验证信息插入传出**HttpRequestMessage**。 使用 JSON.NET 读取 Twitter 的结果。 运行此示例之前，必须获取[Twitter 中的应用程序密钥](https://dev.twitter.com/)，并填写 OAuthMessageHandler 示例类中的信息。

**世界银行示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

演示如何从世界银行数据站点，使用 JSON.NET 分析结果中检索数据。

## <a name="web-api-samples"></a>Web API 示例

**ASP.NET Web API 入门** | [VS 2012 源](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

演示如何创建基本的 web API，支持 HTTP GET 请求。 本教程包含的源代码[你的第一个 ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。

**ASP.NET Web API JavaScript 方案 – 注释** | [VS 2012 源](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

演示如何使用 ASP.NET Web API 构建 web Api 的支持的浏览器客户端和使用 jQuery 来轻松地调用。

**联系人管理器** | [VS 2010 源](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

此示例使用 ASP.NET Web API 构建一个简单的联系人管理器应用程序。 此应用程序包含了联系人管理器 web API，它使用 ASP.NET MVC 应用程序和 Windows Phone 应用程序来显示和管理的联系人列表。

**批处理示例** | [详细的说明](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

演示如何实现 asp.net HTTP 批处理。 批处理包含将放在一个单独的 MIME 多部分实体主体，然后将它发送到服务器以 HTTP POST 的多个 HTTP 请求。 分别处理请求和响应将放入另一个 MIME 多部分实体正文，返回到客户端。

**内容控制器示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

演示如何读取和写入请求和响应实体以异步方式使用流。 示例控制器具有两个操作： 一个 PUT 操作，以异步方式读取请求实体正文，并将其存储在本地文件，并返回本地文件的内容的 GET 操作。

**自定义程序集冲突解决程序示例** | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

演示如何修改 ASP.NET Web API 以支持动态加载的库程序集从控制器的发现。 此示例实现一个自定义**IAssembliesResolver**它调用的默认实现，并将库程序集添加到默认结果。

**自定义媒体类型格式化程序示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

演示如何创建使用自定义媒体类型格式化程序**BufferedMediaTypeFormatter**基类。 此基类用于格式化程序的主要使用同步读取和写入操作。 除了显示的媒体类型格式化程序，该示例演示如何通过注册的一部分进行挂接**HttpConfiguration**为应用程序。 请注意，它也可以使用**MediaTypeFormatter**基类直接的格式化程序的主要使用异步读取和写入操作。

**自定义参数绑定示例** | [详细的说明](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

演示如何自定义参数绑定过程，它是确定如何将来自请求的信息绑定到操作参数的过程。 在此示例中，主控制器具有四个操作：

1. BindPrincipal 演示如何将 IPrincipal 参数绑定中的自定义的泛型主体，不能从 HTTP GET 消息;
2. BindCustomComplexTypeFromUriOrBody 演示如何将绑定一个复杂类型参数，它可能会从消息正文或从请求 URI 的 HTTP POST 消息;
3. BindCustomComplexTypeFromUriWithRenamedProperty 演示如何将绑定来自请求 URI 的 HTTP POST 消息; 已重命名属性的复杂类型参数
4. PostMultipleParametersFromBody 演示如何将多个参数绑定中的正文在 POST 消息;

**文件上传示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

演示如何将文件上载到**ApiController**使用 MIME 多部分文件上传，以及如何设置与进度通知**HttpClient**使用**ProgressNotificationHandler**. 在控制器异步读取 HTML 文件上传的内容，并将一个或多个正文部分写入到本地文件。 响应包含有关已上传文件 （或文件） 的信息。

**文件上的传到 Azure Blob 存储示例** | [详细的说明](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

此示例类似于文件上传示例中，但而不是保存在本地磁盘上已上载的文件，它以异步方式将文件上载到[Azure Blob 存储区](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)使用[Windows Azure SDK for.NET](https://www.windowsazure.com/develop/net/)。 它还提供了一种机制，用于列出在当前存在的 blob [Azure Blob 存储容器](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 你可以尝试对运行该示例**Azure 存储模拟器**都带有 Azure SDK。 如果有[Azure 存储帐户](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)，可以针对实际的存储服务运行。

**Http 消息处理程序管道示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

演示如何以接通**HttpMessageHandler**这两个客户端上的实例 (**HttpClient**) 和服务器 (ASP.NET Web API)。 在示例中，客户端和服务器上使用相同的处理程序。 虽然很少完全相同的处理程序将在这两个位置中运行，对象模型是在客户端和服务器端相同的。

**JSON 上传示例** | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

演示如何上传和下载 JSON 来回**ApiController**。 此示例使用最小**ApiController**并访问其使用**HttpClient**。

**混合应用程序示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

演示如何从以异步方式访问多个远程站点**ApiController**操作。 每次点击操作时，执行请求的异步，以便会阻塞任何线程。

**内存跟踪示例** | [详细的说明](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

此示例项目创建 Nuget 包将安装到 ASP.NET Web API 的应用程序的自定义的内存中跟踪编写器。

**MongoDB 示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

演示如何使用 MongoDB 作为持久性存储**ApiController**，使用存储库模式。

**响应正文处理器示例** | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

演示如何将响应实体 （即，一个 HTTP 响应正文） 复制到本地文件之前将它传送到客户端，并执行其他处理对该文件以异步方式。 此示例实现**HttpMessageHandler**包装响应实体与一个两者本身写入，到正常输出和到本地文件。

**上传 XDocument 示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

演示如何上传到 XDocument **ApiController**使用**PushStreamContent**并**HttpClient**。

**验证示例** | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

演示如何使用验证特性上 ASP.NET WebAPI 中的模型来验证 HTTP 请求的内容。 演示如何将标记属性为必需的如何将两种框架定义和自定义验证特性来批注模型，以及如何返回的无效模型状态错误响应。

**Web 窗体示例** | [详细的说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

显示添加到 Web 窗体项目 ApiController。

**[RestBugs 示例](https://github.com/howarddierking/RestBugs)**

RestBugs 是一个简单的 bug 跟踪应用程序，演示如何使用 ASP.NET Web API 和新的 HTTP 客户端库创建超媒体驱动系统。 该示例包括使用 ASP.NET Web API 的客户端和服务器实现。 服务器使用自定义 Razor 格式化程序来生成资源表示形式。 此示例还提供了 node.js 服务器，为了说明来自使用超媒体设计分离客户端和服务器的优势。
