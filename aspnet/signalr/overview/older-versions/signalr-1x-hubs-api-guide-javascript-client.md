---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x 中心 API 指南-JavaScript 客户端 |Microsoft 文档
author: pfletcher
description: 本文档提供使用中心 API 为 SignalR JavaScript 客户端，如浏览器和 Windows 应用商店 (WinJS) applic 中的版本 1.1 的说明...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: f92470b2022f343cfd6d822abb255dc19947b4d1
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28036916"
---
<a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="4e504-103">SignalR 1.x 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="4e504-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>
====================
<span data-ttu-id="4e504-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4e504-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="4e504-105">本文档提供使用 SignalR JavaScript 客户端，如浏览器和 Windows 应用商店 (WinJS) 应用程序中的版本 1.1 的中心 API 的简介。</span><span class="sxs-lookup"><span data-stu-id="4e504-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="4e504-106">SignalR 中心 API 使您能够远程过程调用 (Rpc) 从连接的客户端到服务器和客户端到服务器。</span><span class="sxs-lookup"><span data-stu-id="4e504-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="4e504-107">在服务器代码中，你定义可以由客户端，调用的方法和调用客户端运行的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="4e504-108">在客户端代码中，定义在服务器上，可以调用的方法，并调用在服务器运行的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="4e504-109">SignalR 将负责为你的客户端到服务器管道的所有。</span><span class="sxs-lookup"><span data-stu-id="4e504-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="4e504-110">SignalR 还提供了一个称为永久连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="4e504-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="4e504-111">简介 SignalR、 集线器和永久连接，或者有关演示如何生成完整的 SignalR 应用程序的教程，请参阅[SignalR-入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4e504-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="4e504-112">概述</span><span class="sxs-lookup"><span data-stu-id="4e504-112">Overview</span></span>

<span data-ttu-id="4e504-113">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="4e504-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="4e504-114">生成的代理及它为你的作用</span><span class="sxs-lookup"><span data-stu-id="4e504-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="4e504-115">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="4e504-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="4e504-116">客户端安装程序</span><span class="sxs-lookup"><span data-stu-id="4e504-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="4e504-117">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="4e504-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="4e504-118">如何为 SignalR 创建物理文件生成代理</span><span class="sxs-lookup"><span data-stu-id="4e504-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="4e504-119">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="4e504-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="4e504-120">$。 connection.hub 是相同对象该 $.hubConnection() 创建</span><span class="sxs-lookup"><span data-stu-id="4e504-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="4e504-121">异步执行的 start 方法</span><span class="sxs-lookup"><span data-stu-id="4e504-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="4e504-122">如何建立的跨域连接</span><span class="sxs-lookup"><span data-stu-id="4e504-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="4e504-123">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="4e504-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="4e504-124">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="4e504-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="4e504-125">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="4e504-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="4e504-126">如何获取代理的中心类</span><span class="sxs-lookup"><span data-stu-id="4e504-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="4e504-127">如何在该服务器可以调用的客户端上定义方法</span><span class="sxs-lookup"><span data-stu-id="4e504-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="4e504-128">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="4e504-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="4e504-129">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="4e504-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="4e504-130">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="4e504-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="4e504-131">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="4e504-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="4e504-132">有关如何进行编程的服务器或.NET 客户端的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="4e504-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="4e504-133">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="4e504-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="4e504-134">SignalR 中心 API 指南-.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="4e504-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="4e504-135">API 参考主题的链接将指向 API 的.NET 4.5 版本。</span><span class="sxs-lookup"><span data-stu-id="4e504-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="4e504-136">如果你使用.NET 4，请参阅[API 主题的.NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e504-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="4e504-137">生成的代理及它为你的作用</span><span class="sxs-lookup"><span data-stu-id="4e504-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="4e504-138">你可以编程 JavaScript 客户端与 SignalR 服务使用或不使用 SignalR 将为你生成的代理进行通信。</span><span class="sxs-lookup"><span data-stu-id="4e504-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="4e504-139">代理为你的作用是代码的简化的语法使用连接，服务器调用时，写入方法并在服务器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="4e504-140">当你编写代码，调用服务器方法调用时，生成的代理，您可以使用看起来好像你正在执行本地函数的语法： 可以编写`serverMethod(arg1, arg2)`而不是`invoke('serverMethod', arg1, arg2)`。</span><span class="sxs-lookup"><span data-stu-id="4e504-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="4e504-141">生成的代理语法还允许即时和容易理解客户端错误，如果键入服务器方法名称。</span><span class="sxs-lookup"><span data-stu-id="4e504-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="4e504-142">并且，如果你手动创建定义代理的文件，你还可以编写调用服务器方法的代码来获得 IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="4e504-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="4e504-143">例如，假设在服务器上有下面的中心类：</span><span class="sxs-lookup"><span data-stu-id="4e504-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="4e504-144">下面的代码示例演示 JavaScript 代码看起来像调用`NewContosoChatMessage`上服务器和接收的调用的方法`addContosoChatMessageToPage`从服务器的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="4e504-145">**使用生成代理**</span><span class="sxs-lookup"><span data-stu-id="4e504-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="4e504-146">**不生成代理**</span><span class="sxs-lookup"><span data-stu-id="4e504-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="4e504-147">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="4e504-147">When to use the generated proxy</span></span>

<span data-ttu-id="4e504-148">如果你想要注册的服务器调用的客户端方法的多个事件处理程序，则无法使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="4e504-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="4e504-149">否则为你可以选择使用生成的代理或不基于编码的首选项。</span><span class="sxs-lookup"><span data-stu-id="4e504-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="4e504-150">如果你选择不使用它，无需引用中的"signalr/中心"URL`script`在客户端代码中的元素。</span><span class="sxs-lookup"><span data-stu-id="4e504-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="4e504-151">客户端安装程序</span><span class="sxs-lookup"><span data-stu-id="4e504-151">Client setup</span></span>

<span data-ttu-id="4e504-152">JavaScript 客户端需要对 jQuery 和 SignalR 的核心 JavaScript 文件的引用。</span><span class="sxs-lookup"><span data-stu-id="4e504-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="4e504-153">JQuery 版本必须是 1.6.4 或主要的更高版本，如 1.7.2、 1.8.2 或 1.9.1。</span><span class="sxs-lookup"><span data-stu-id="4e504-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="4e504-154">如果你决定使用生成的代理，你还需要对生成的 SignalR 代理 JavaScript 文件的引用。</span><span class="sxs-lookup"><span data-stu-id="4e504-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="4e504-155">下面的示例演示什么引用可能如下所示使用生成的代理的 HTML 页中。</span><span class="sxs-lookup"><span data-stu-id="4e504-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="4e504-156">必须按此顺序包含这些引用： jQuery 名字，在此之后，SignalR core 和 SignalR 代理姓氏。</span><span class="sxs-lookup"><span data-stu-id="4e504-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="4e504-157">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="4e504-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="4e504-158">在前面的示例中，生成的 SignalR 代理到引用的是动态生成的 JavaScript 代码，不是指向物理文件。</span><span class="sxs-lookup"><span data-stu-id="4e504-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="4e504-159">SignalR 为代理服务器在运行过程中创建的 JavaScript 代码，并提供给客户端以响应"/ signalr/中心"URL。</span><span class="sxs-lookup"><span data-stu-id="4e504-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="4e504-160">如果你指定的不同的基 URL 的 SignalR 连接在服务器上你`MapHubs`方法，动态生成的代理文件的 URL 是你使用的自定义 URL"/ 中心"追加到它。</span><span class="sxs-lookup"><span data-stu-id="4e504-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="4e504-161">对于 Windows 8 （Windows 应用商店） JavaScript 客户端，而不是动态生成一个中使用的物理代理文件。</span><span class="sxs-lookup"><span data-stu-id="4e504-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="4e504-162">有关详细信息，请参阅[How to create for SignalR 的物理文件生成代理](#manualproxy)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="4e504-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>


<span data-ttu-id="4e504-163">在 ASP.NET MVC 4 Razor 视图中，使用波形符来引用在您的代理文件引用中的应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="4e504-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="4e504-164">有关在 MVC 4 中使用 SignalR 的详细信息，请参阅[开始使用 SignalR 和 MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="4e504-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="4e504-165">在 ASP.NET MVC 3 Razor 视图中，使用`Url.Content`为你的代理文件引用：</span><span class="sxs-lookup"><span data-stu-id="4e504-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="4e504-166">在 ASP.NET Web 窗体应用程序，使用`ResolveClientUrl`为你的代理文件引用或通过使用应用程序根相对路径 （开头波形符） ScriptManager 注册，它：</span><span class="sxs-lookup"><span data-stu-id="4e504-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="4e504-167">作为一般规则，用于指定用于 CSS 或 JavaScript 文件"/ signalr/中心"URL 中使用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="4e504-168">如果不使用波形符指定 URL，在某些情况下你的应用程序将正常工作时使用 IIS Express 的 Visual Studio 中的测试，但当你将部署到完整 IIS 时将失败，404 错误。</span><span class="sxs-lookup"><span data-stu-id="4e504-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="4e504-169">有关详细信息，请参阅**解析对资源的引用根级别**中[用于 ASP.NET Web 项目的 Visual Studio 中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)MSDN 网站上的。</span><span class="sxs-lookup"><span data-stu-id="4e504-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="4e504-170">当你在调试模式下，Visual Studio 2012 中运行 web 项目和作为浏览器使用 Internet Explorer，如果你可以看到中的代理文件**解决方案资源管理器**下**脚本文档**中, 所示下图。</span><span class="sxs-lookup"><span data-stu-id="4e504-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![在解决方案资源管理器中的 JavaScript 生成的代理文件](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="4e504-172">若要查看文件的内容，请双击**中心**。</span><span class="sxs-lookup"><span data-stu-id="4e504-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="4e504-173">如果你不使用 Visual Studio 2012 和 Internet Explorer 中，或者如果你不在调试模式下，你还可以通过浏览到"/ signalR/中心"URL 获取文件的内容。</span><span class="sxs-lookup"><span data-stu-id="4e504-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="4e504-174">例如，如果你的站点运行在`http://localhost:56699`，请转到`http://localhost:56699/SignalR/hubs`在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="4e504-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="4e504-175">如何为 SignalR 创建物理文件生成代理</span><span class="sxs-lookup"><span data-stu-id="4e504-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="4e504-176">作为动态生成的代理的替代方法，可以创建具有代理代码的物理文件并引用该文件。</span><span class="sxs-lookup"><span data-stu-id="4e504-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="4e504-177">你可能想要执行该操作控制缓存或绑定行为，或你在编码对服务器方法的调用时，可获取 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="4e504-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="4e504-178">若要创建代理文件，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="4e504-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="4e504-179">安装[Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4e504-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="4e504-180">打开命令提示符，并浏览到*工具*包含 SignalR.exe 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4e504-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="4e504-181">工具文件夹位于以下位置：</span><span class="sxs-lookup"><span data-stu-id="4e504-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="4e504-182">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="4e504-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="4e504-183">路径你 *.dll*通常是*bin*项目文件夹中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4e504-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="4e504-184">此命令创建名为的文件*server.js*在所在的文件夹*signalr.exe*。</span><span class="sxs-lookup"><span data-stu-id="4e504-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="4e504-185">Put *server.js*文件在项目中的相应文件夹中，将其重命名为适合你的应用程序，并添加对它代替"signalr/中心"引用的引用。</span><span class="sxs-lookup"><span data-stu-id="4e504-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="4e504-186">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="4e504-186">How to establish a connection</span></span>

<span data-ttu-id="4e504-187">你可以建立连接之前，必须创建连接对象、 创建代理，并注册事件处理程序可以从服务器调用的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="4e504-188">当设置代理和事件处理程序时，通过调用建立连接`start`方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="4e504-189">如果你使用的生成的代理，你无需在你自己的代码中创建连接对象，因为生成的代理代码执行此操作。</span><span class="sxs-lookup"><span data-stu-id="4e504-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="4e504-190">**（与生成的代理） 建立连接**</span><span class="sxs-lookup"><span data-stu-id="4e504-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="4e504-191">**建立的连接 （而无需生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="4e504-192">示例代码使用默认值"/ signalr"URL 以连接到你 SignalR 的服务。</span><span class="sxs-lookup"><span data-stu-id="4e504-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="4e504-193">有关如何指定不同的基 URL 的信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="4e504-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="4e504-194">通常情况下注册事件处理程序之前调用`start`方法，以建立连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="4e504-195">如果你想要建立连接后注册某些事件处理程序，你可以这样做，但你必须注册你之前调用的事件处理程序中至少一个`start`方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="4e504-196">一个原因是在应用程序，可以有多个中心，但你不想要触发`OnConnected`如果你仅将使用到其中每个中心上的事件。</span><span class="sxs-lookup"><span data-stu-id="4e504-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="4e504-197">在中心的代理服务器上的客户端方法存在建立连接后，将告诉 SignalR 触发`OnConnected`事件。</span><span class="sxs-lookup"><span data-stu-id="4e504-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="4e504-198">如果你未注册任何事件处理程序之前调用`start`方法，你将能够对中心，但中心的调用的方法`OnConnected`不会调用方法并将从服务器调用任何客户端方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>


<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="4e504-199">$。 connection.hub 是相同对象该 $.hubConnection() 创建</span><span class="sxs-lookup"><span data-stu-id="4e504-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="4e504-200">如你所见从示例中，当你使用生成的代理，`$.connection.hub`引用的连接对象。</span><span class="sxs-lookup"><span data-stu-id="4e504-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="4e504-201">这是通过调用获取的相同对象`$.hubConnection()`时未使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="4e504-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="4e504-202">生成的代理代码通过执行下面的语句来创建你的连接：</span><span class="sxs-lookup"><span data-stu-id="4e504-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![在生成的代理文件创建连接](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="4e504-204">当你使用的生成的代理时，您可以执行任何操作与`$.connection.hub`时你不使用生成的代理可以执行与连接对象。</span><span class="sxs-lookup"><span data-stu-id="4e504-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="4e504-205">异步执行的 start 方法</span><span class="sxs-lookup"><span data-stu-id="4e504-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="4e504-206">`start`方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="4e504-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="4e504-207">它将返回[jQuery 延迟对象](http://api.jquery.com/category/deferred-object/)，这意味着，你可以通过调用方法，如添加回调函数`pipe`， `done`，和`fail`。</span><span class="sxs-lookup"><span data-stu-id="4e504-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="4e504-208">如果你有想要在建立连接后，执行的代码，例如，对服务器方法调用，将该代码放在回调函数，或从一个回调函数调用它。</span><span class="sxs-lookup"><span data-stu-id="4e504-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="4e504-209">`.done`后已建立连接，和任何代码，之后必须执行回调方法你`OnConnected`执行完毕后在服务器上的事件处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="4e504-210">如果将"现在已连接"语句从前面的示例作为下一步后的代码行放`start`方法调用 (不在`.done`回调)，则`console.log`行之前将执行建立连接时，在下面的示例所示示例：</span><span class="sxs-lookup"><span data-stu-id="4e504-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![错误的方式编写运行建立连接后的代码](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="4e504-212">如何建立的跨域连接</span><span class="sxs-lookup"><span data-stu-id="4e504-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="4e504-213">通常如果浏览器加载从页`http://contoso.com`，SignalR 连接处于同一域中，在`http://contoso.com/signalr`。</span><span class="sxs-lookup"><span data-stu-id="4e504-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="4e504-214">如果此页`http://contoso.com`建立连接`http://fabrikam.com/signalr`，即跨域连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="4e504-215">出于安全原因，默认情况下禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="4e504-216">若要建立的跨域连接，请确保在服务器上，启用了跨域连接，在创建连接对象时指定该连接 URL。</span><span class="sxs-lookup"><span data-stu-id="4e504-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="4e504-217">SignalR 将使用适当的技术跨域连接，如[JSONP](http://en.wikipedia.org/wiki/JSONP)或[CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)。</span><span class="sxs-lookup"><span data-stu-id="4e504-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="4e504-218">选择该选项，在调用时，在服务器上，启用跨域连接`MapHubs`方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="4e504-219">在客户端上，指定 URL 时创建连接对象 （而不生成的代理） 或之前 （使用生成的代理） 中调用 start 方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="4e504-220">**指定 （与生成的代理） 的跨域连接的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="4e504-221">**指定 （无需生成的代理） 的跨域连接的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="4e504-222">当你使用`$.hubConnection`构造函数，你不需要包括`signalr`在 URL 中因为它将自动添加 (除非你指定`useDefaultUrl`作为`false`)。</span><span class="sxs-lookup"><span data-stu-id="4e504-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="4e504-223">你可以创建多个连接到不同的终结点。</span><span class="sxs-lookup"><span data-stu-id="4e504-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="4e504-224">未设置`jQuery.support.cors`为 true，在代码中。</span><span class="sxs-lookup"><span data-stu-id="4e504-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![未设置为 true 的 jQuery.support.cors](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="4e504-226">SignalR 处理使用 JSONP 还是 CORS。</span><span class="sxs-lookup"><span data-stu-id="4e504-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="4e504-227">设置`jQuery.support.cors`以 true 禁用 JSONP，因为它会导致 SignalR 假定浏览器支持 CORS。</span><span class="sxs-lookup"><span data-stu-id="4e504-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="4e504-228">当您正在连接到本地主机 URL 时，Internet Explorer 10 不会考虑将它的跨域连接，因此应用程序将使用本地 IE 10 即使尚未启用该服务器上的跨域连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="4e504-229">有关使用 Internet Explorer 9 的跨域连接的信息的信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。</span><span class="sxs-lookup"><span data-stu-id="4e504-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="4e504-230">有关使用 Chrome 的跨域连接的信息的信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。</span><span class="sxs-lookup"><span data-stu-id="4e504-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="4e504-231">示例代码使用默认值"/ signalr"URL 以连接到你 SignalR 的服务。</span><span class="sxs-lookup"><span data-stu-id="4e504-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="4e504-232">有关如何指定不同的基 URL 的信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="4e504-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>


<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="4e504-233">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="4e504-233">How to configure the connection</span></span>

<span data-ttu-id="4e504-234">建立连接之前，你可以指定查询字符串参数或指定的传输方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="4e504-235">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="4e504-235">How to specify query string parameters</span></span>

<span data-ttu-id="4e504-236">如果你想要将数据发送到服务器，当客户端连接时，你可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="4e504-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="4e504-237">下面的示例演示如何在客户端代码中设置的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="4e504-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="4e504-238">**（使用生成的代理） 调用 start 方法前设置查询字符串值**</span><span class="sxs-lookup"><span data-stu-id="4e504-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="4e504-239">**在调用 （无需生成的代理） 的启动方法之前设置查询字符串值**</span><span class="sxs-lookup"><span data-stu-id="4e504-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="4e504-240">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="4e504-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="4e504-241">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="4e504-241">How to specify the transport method</span></span>

<span data-ttu-id="4e504-242">作为连接的过程的一部分，SignalR 客户端通常与服务器协商来确定支持的最佳传输由服务器和客户端。</span><span class="sxs-lookup"><span data-stu-id="4e504-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="4e504-243">如果你已经知道你想要使用的传输，你可以通过在调用时指定的传输方法来跳过此协商过程`start`方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="4e504-244">**指定的传输方法 （使用生成的代理） 的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="4e504-245">**指定的传输方法 （而无需生成的代理） 的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="4e504-246">作为替代方法，你可以在其中你希望 SignalR 尝试它们的顺序来指定多个传输方法：</span><span class="sxs-lookup"><span data-stu-id="4e504-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="4e504-247">**指定自定义传输回退方案 （使用生成的代理） 的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="4e504-248">**指定自定义传输回退方案 （无需生成的代理） 的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="4e504-249">用于指定的传输方法，可以使用以下值：</span><span class="sxs-lookup"><span data-stu-id="4e504-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="4e504-250">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="4e504-250">"webSockets"</span></span>
- <span data-ttu-id="4e504-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="4e504-251">"foreverFrame"</span></span>
- <span data-ttu-id="4e504-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="4e504-252">"serverSentEvents"</span></span>
- <span data-ttu-id="4e504-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="4e504-253">"longPolling"</span></span>

<span data-ttu-id="4e504-254">下面的示例演示如何找出连接正在使用哪种传输方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="4e504-255">**显示使用 （与生成的代理） 的连接的传输方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="4e504-256">**显示使用 （无需生成的代理） 的连接的传输方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="4e504-257">有关如何检查在服务器代码中的传输方法的信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-如何从上下文属性中获取有关客户端的信息](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="4e504-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="4e504-258">有关传输和回退机制的详细信息，请参阅[简介 SignalR 的传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="4e504-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="4e504-259">如何获取代理的中心类</span><span class="sxs-lookup"><span data-stu-id="4e504-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="4e504-260">你创建的每个连接对象封装有关连接到包含一个或多个中心类 SignalR 服务的信息。</span><span class="sxs-lookup"><span data-stu-id="4e504-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="4e504-261">若要与中心类通信，你使用代理对象 （如果你不使用生成的代理），会创建您自己或为你生成。</span><span class="sxs-lookup"><span data-stu-id="4e504-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="4e504-262">客户端上的代理名称是中心类名称采用 camel 大小写版本。</span><span class="sxs-lookup"><span data-stu-id="4e504-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="4e504-263">SignalR 自动使此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="4e504-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="4e504-264">**在服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="4e504-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="4e504-265">**获取对生成的客户端代理的引用的中心**</span><span class="sxs-lookup"><span data-stu-id="4e504-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="4e504-266">**创建中心类 （而不生成的代理） 的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="4e504-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="4e504-267">如果修饰你中心类`HubName`特性，请使用的确切名称，而无需更改大小写。</span><span class="sxs-lookup"><span data-stu-id="4e504-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="4e504-268">**具有 HubName 属性的服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="4e504-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="4e504-269">**获取对生成的客户端代理的引用的中心**</span><span class="sxs-lookup"><span data-stu-id="4e504-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="4e504-270">**创建中心类 （而不生成的代理） 的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="4e504-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="4e504-271">如何在该服务器可以调用的客户端上定义方法</span><span class="sxs-lookup"><span data-stu-id="4e504-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="4e504-272">若要定义服务器可从一个中心中调用的方法，通过将添加一个事件处理程序到中心代理`client`属性生成的代理，或调用`on`方法如果你未使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="4e504-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="4e504-273">参数可以是复杂的对象。</span><span class="sxs-lookup"><span data-stu-id="4e504-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="4e504-274">添加事件处理程序，然后才能调用`start`方法，以建立连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="4e504-275">(如果你想要在调用后添加事件处理程序`start`方法，请参阅中的说明[如何建立连接](#establishconnection)前面在此文档，并使用用于定义一种方法，而无需使用生成的代理所示的语法。)</span><span class="sxs-lookup"><span data-stu-id="4e504-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="4e504-276">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="4e504-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="4e504-277">例如，`Clients.All.addContosoChatMessageToPage`在服务器上将执行`AddContosoChatMessageToPage`， `addContosoChatMessageToPage`，或`addcontosochatmessagetopage`客户端上。</span><span class="sxs-lookup"><span data-stu-id="4e504-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="4e504-278">**（使用生成的代理） 的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="4e504-279">**另一种方法 （使用生成的代理） 的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="4e504-280">**客户端 （不生成的代理，或调用 start 方法之后添加时） 上定义方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="4e504-281">**调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="4e504-282">下面的示例包括复杂对象作为方法参数。</span><span class="sxs-lookup"><span data-stu-id="4e504-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="4e504-283">**采用 （具有生成的代理） 的复杂对象的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="4e504-284">**采用复杂对象 （而不生成的代理） 的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="4e504-285">**定义的复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="4e504-286">**服务器代码，调用使用复杂对象的客户端方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="4e504-287">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="4e504-287">How to call server methods from the client</span></span>

<span data-ttu-id="4e504-288">若要从客户端调用服务器方法，使用`server`属性生成的代理或`invoke`中心代理，如果你未使用生成的代理上的方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="4e504-289">返回值或参数可以是复杂的对象。</span><span class="sxs-lookup"><span data-stu-id="4e504-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="4e504-290">在中心传入方法名称的 camel 大小写版本。</span><span class="sxs-lookup"><span data-stu-id="4e504-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="4e504-291">SignalR 自动使此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="4e504-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="4e504-292">下面的示例演示如何调用没有返回值的服务器方法以及如何调用服务器方法没有返回值。</span><span class="sxs-lookup"><span data-stu-id="4e504-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="4e504-293">**没有 HubMethodName 属性与服务器方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="4e504-294">**在参数中传递定义的复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4e504-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="4e504-295">**客户端代码调用 （使用生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="4e504-296">**客户端代码调用 （无需生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="4e504-297">如果修饰具有的中心方法`HubMethodName`特性，请使用该名称，而无需更改大小写。</span><span class="sxs-lookup"><span data-stu-id="4e504-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="4e504-298">**服务器方法**具有 HubMethodName 属性</span><span class="sxs-lookup"><span data-stu-id="4e504-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="4e504-299">**客户端代码调用 （使用生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="4e504-300">**客户端代码调用 （无需生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="4e504-301">前面的示例演示如何调用没有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="4e504-302">下面的示例演示如何调用具有一个返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="4e504-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="4e504-303">**服务器代码具有一个返回值的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="4e504-304">**Stock 类用于**返回值</span><span class="sxs-lookup"><span data-stu-id="4e504-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="4e504-305">**客户端代码调用 （使用生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="4e504-306">**客户端代码调用 （无需生成的代理） 服务器的方法**</span><span class="sxs-lookup"><span data-stu-id="4e504-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="4e504-307">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="4e504-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="4e504-308">SignalR 提供以下连接可以处理的生存期事件：</span><span class="sxs-lookup"><span data-stu-id="4e504-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="4e504-309">`starting`： 通过连接发送任何数据之前引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="4e504-310">`received`： 引发时的连接上收到任何数据。</span><span class="sxs-lookup"><span data-stu-id="4e504-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="4e504-311">提供接收到的数据。</span><span class="sxs-lookup"><span data-stu-id="4e504-311">Provides the received data.</span></span>
- <span data-ttu-id="4e504-312">`connectionSlow`： 当客户端检测到慢速或经常删除连接时引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="4e504-313">`reconnecting`： 基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="4e504-314">`reconnected`： 基础传输已重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="4e504-315">`stateChanged`： 在连接状态更改时引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="4e504-316">提供的旧的状态和新的状态 （连接、 已连接、 Reconnecting，或已断开连接）。</span><span class="sxs-lookup"><span data-stu-id="4e504-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="4e504-317">`disconnected`： 连接已断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="4e504-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="4e504-318">例如，如果你想要有可能会导致明显延迟的连接问题时显示警告消息，处理`connectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="4e504-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="4e504-319">**句柄 connectionSlow 事件 （使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="4e504-320">**句柄 connectionSlow 事件 （而无需生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="4e504-321">有关详细信息，请参阅[了解和处理连接生存期中事件的 SignalR](index.md)。</span><span class="sxs-lookup"><span data-stu-id="4e504-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="4e504-322">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="4e504-322">How to handle errors</span></span>

<span data-ttu-id="4e504-323">SignalR JavaScript 客户端提供`error`可以添加的处理程序的事件。</span><span class="sxs-lookup"><span data-stu-id="4e504-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="4e504-324">失败方法还可用于添加而从服务器方法调用导致的错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="4e504-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="4e504-325">如果未显式启用服务器上的详细的错误消息，在出错后返回 SignalR 的异常对象包含有关错误的极少信息。</span><span class="sxs-lookup"><span data-stu-id="4e504-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="4e504-326">例如，如果调用`newContosoChatMessage`失败，错误对象中的错误消息包含"`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`"发送到在生产环境中的客户端的详细的错误消息不建议出于安全原因，但如果你想要启用详细的错误消息疑难解答的目的，在服务器上使用下面的代码。</span><span class="sxs-lookup"><span data-stu-id="4e504-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="4e504-327">下面的示例演示如何添加错误事件的处理程序。</span><span class="sxs-lookup"><span data-stu-id="4e504-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="4e504-328">**添加一个错误处理程序 （具有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="4e504-329">**添加错误处理程序 （而无需生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="4e504-330">下面的示例演示如何处理的方法调用中出现错误。</span><span class="sxs-lookup"><span data-stu-id="4e504-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="4e504-331">**句柄 （使用生成的代理） 的方法调用中出现错误**</span><span class="sxs-lookup"><span data-stu-id="4e504-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="4e504-332">**句柄 （无需生成的代理） 的方法调用中出现错误**</span><span class="sxs-lookup"><span data-stu-id="4e504-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="4e504-333">如果方法调用失败，`error`也会引发事件，因此你的代码中`error`方法处理程序并在`.fail`方法回调会执行。</span><span class="sxs-lookup"><span data-stu-id="4e504-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="4e504-334">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="4e504-334">How to enable client-side logging</span></span>

<span data-ttu-id="4e504-335">若要启用客户端日志记录在连接上，设置`logging`属性上的连接对象，然后才能调用`start`方法，以建立连接。</span><span class="sxs-lookup"><span data-stu-id="4e504-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="4e504-336">**启用日志记录 （使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="4e504-337">**启用日志记录 （无需生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="4e504-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="4e504-338">若要查看日志，请打开浏览器的开发人员工具，并转到控制台选项卡。本教程演示的分步说明和屏幕截图显示如何执行此操作，请参阅[服务器广播使用 ASP.NET Signalr-启用日志记录](index.md)。</span><span class="sxs-lookup"><span data-stu-id="4e504-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
