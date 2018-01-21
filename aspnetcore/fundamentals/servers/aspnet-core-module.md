---
title: "ASP.NET 核心模块"
author: tdykstra
description: "引入了 ASP.NET 核心模块 (ANCM) 使 Kestrel web 服务器可以使用 IIS 或 IIS Express 作为反向代理服务器的 IIS 模块。"
ms.author: tdykstra
manager: wpickett
ms.date: 08/03/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/servers/aspnet-core-module
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 153c40f0e825ff5826e916c7ea877a25d81954f1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-aspnet-core-module"></a><span data-ttu-id="0ac0f-103">ASP.NET 核心模块简介</span><span class="sxs-lookup"><span data-stu-id="0ac0f-103">Introduction to ASP.NET Core Module</span></span>

<span data-ttu-id="0ac0f-104">通过[Tom Dykstra](https://github.com/tdykstra)， [Rick Strahl](https://github.com/RickStrahl)，和[Chris 跨](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="0ac0f-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span> 

<span data-ttu-id="0ac0f-105">ASP.NET 核心模块 (ANCM) 允许您在 IIS 中，后面的应用程序中运行 ASP.NET 核心的很好地 （安全、 可管理性，还有很多） 使用 IIS 和使用[Kestrel](kestrel.md)为很好地 （在非常短），并获取从一次这两种技术的优势。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-105">ASP.NET Core Module (ANCM) lets you run ASP.NET Core applications behind IIS, using IIS for what it's good at (security, manageability, and lots more) and using [Kestrel](kestrel.md) for what it's good at (being really fast), and getting the benefits from both technologies at once.</span></span> <span data-ttu-id="0ac0f-106">**ANCM 仅适用于 Kestrel;它与不兼容 WebListener (在 ASP.NET Core 1.x) 或 HTTP.sys （在 2.x)。**</span><span class="sxs-lookup"><span data-stu-id="0ac0f-106">**ANCM works only with Kestrel; it isn't compatible with WebListener (in ASP.NET Core 1.x) or HTTP.sys (in 2.x).**</span></span> 

<span data-ttu-id="0ac0f-107">支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="0ac0f-107">Supported Windows versions:</span></span>

* <span data-ttu-id="0ac0f-108">Windows 7 和 Windows Server 2008 R2 及更高版本</span><span class="sxs-lookup"><span data-stu-id="0ac0f-108">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="0ac0f-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0ac0f-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-aspnet-core-module-does"></a><span data-ttu-id="0ac0f-110">ASP.NET 核心模块的用途</span><span class="sxs-lookup"><span data-stu-id="0ac0f-110">What ASP.NET Core Module does</span></span>

<span data-ttu-id="0ac0f-111">ANCM 是一个本机的 IIS 模块，挂钩到 IIS 管道和将流量重定向到后端 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-111">ANCM is a native IIS module that hooks into the IIS pipeline and redirects traffic to the backend ASP.NET Core application.</span></span> <span data-ttu-id="0ac0f-112">大多数其他模块，例如 windows 身份验证，仍有机会运行。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-112">Most other modules, such as windows authentication, still get a chance to run.</span></span> <span data-ttu-id="0ac0f-113">ANCM 仅采用控制时为请求中，选择一个处理程序并在应用程序中定义处理程序映射*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-113">ANCM only takes control when a handler is selected for the request, and handler mapping is defined in the application *web.config* file.</span></span>

<span data-ttu-id="0ac0f-114">因为 ASP.NET Core 应用程序在进程中运行的 IIS 工作进程分开，ANCM 还未处理管理。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-114">Because ASP.NET Core applications run in a process separate from the IIS worker process, ANCM also does process management.</span></span> <span data-ttu-id="0ac0f-115">当第一个请求传入并且重新启动该崩溃时，ANCM 启动 ASP.NET Core 应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-115">ANCM starts the process for the ASP.NET Core application when the first request comes in and restarts it when it crashes.</span></span> <span data-ttu-id="0ac0f-116">这是实质上是相同经典 ASP.NET 应用程序的行为运行中进程在 IIS 中，并且由管理 WAS （Windows 激活服务）。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-116">This is essentially the same behavior as classic ASP.NET applications that run in-process in IIS and are managed by WAS (Windows Activation Service).</span></span>

<span data-ttu-id="0ac0f-117">下面是阐释了 IIS、 ANCM 和 ASP.NET Core 应用程序之间的关系的关系图。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-117">Here's a diagram that illustrates the relationship between IIS, ANCM, and ASP.NET Core applications.</span></span>

![ASP.NET 核心模块](aspnet-core-module/_static/ancm.png)

<span data-ttu-id="0ac0f-119">请求来自 Web 和命中的内核模式 Http.Sys 驱动程序，将其路由到主端口 (80) 或 SSL 端口 (443) 上的 IIS。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-119">Requests come in from the Web and hit the kernel mode Http.Sys driver which routes them into IIS on the primary port (80) or SSL port (443).</span></span> <span data-ttu-id="0ac0f-120">ANCM 将请求转发到 ASP.NET 核心应用程序上不是端口 80/443 对应用程序配置的 HTTP 端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-120">ANCM forwards the requests to the ASP.NET Core application on the HTTP port configured for the application, which is not port 80/443.</span></span>

<span data-ttu-id="0ac0f-121">Kestrel 侦听来自 ANCM 的流量。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-121">Kestrel listens for traffic coming from ANCM.</span></span>  <span data-ttu-id="0ac0f-122">ANCM 指定通过在启动时，环境变量的端口和[UseIISIntegration](#call-useiisintegration)方法将服务器配置为侦听`http://localhost:{port}`。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-122">ANCM specifies the port via environment variable at startup, and the [UseIISIntegration](#call-useiisintegration) method configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="0ac0f-123">有一些其他检查，以拒绝不是从 ANCM 的请求。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-123">There are additional checks to reject requests not from ANCM.</span></span> <span data-ttu-id="0ac0f-124">（ANCM 不支持 HTTPS 转发，因此即使 IIS 通过 HTTPS 接收到请求通过 HTTP 转发。）</span><span class="sxs-lookup"><span data-stu-id="0ac0f-124">(ANCM does not support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.)</span></span>

<span data-ttu-id="0ac0f-125">Kestrel ANCM 从那里获取请求，并将它们推送到 ASP.NET 核心中间件管道，其处理它们，然后将它们作为传递`HttpContext`到应用程序逻辑的实例。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-125">Kestrel picks up requests from ANCM and pushes them into the ASP.NET Core middleware pipeline, which then handles them and passes them on as `HttpContext` instances to application logic.</span></span> <span data-ttu-id="0ac0f-126">然后，应用程序的响应会传递回 IIS，它们回退到 HTTP 客户端启动请求的推送。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-126">The application's responses are then passed back to IIS, which pushes them back out to the HTTP client that initiated the requests.</span></span>

<span data-ttu-id="0ac0f-127">ANCM 具有少数几个其他函数：</span><span class="sxs-lookup"><span data-stu-id="0ac0f-127">ANCM has a few other functions as well:</span></span>

* <span data-ttu-id="0ac0f-128">设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-128">Sets environment variables.</span></span>
* <span data-ttu-id="0ac0f-129">日志`stdout`输出到文件存储。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-129">Logs `stdout` output to file storage.</span></span>
* <span data-ttu-id="0ac0f-130">将转发 Windows 身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-130">Forwards Windows authentication tokens.</span></span>

## <a name="how-to-use-ancm-in-aspnet-core-apps"></a><span data-ttu-id="0ac0f-131">如何在 ASP.NET Core 应用中使用 ANCM</span><span class="sxs-lookup"><span data-stu-id="0ac0f-131">How to use ANCM in ASP.NET Core apps</span></span>

<span data-ttu-id="0ac0f-132">本部分概述了设置的 IIS 服务器和 ASP.NET Core 应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-132">This section provides an overview of the process for setting up an IIS server and ASP.NET Core application.</span></span> <span data-ttu-id="0ac0f-133">有关详细说明，请参阅[使用 IIS 的 Windows 上的主机](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-133">For detailed instructions, see [Host on Windows with IIS](xref:host-and-deploy/iis/index).</span></span>

### <a name="install-ancm"></a><span data-ttu-id="0ac0f-134">安装 ANCM</span><span class="sxs-lookup"><span data-stu-id="0ac0f-134">Install ANCM</span></span>


<span data-ttu-id="0ac0f-135">ASP.NET 核心模块必须安装在 IIS 服务器上和在 IIS Express 在开发计算机上。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-135">The ASP.NET Core Module has to be installed in IIS on your servers and in IIS Express on your development machines.</span></span> <span data-ttu-id="0ac0f-136">对于服务器，纳入 ANCM [.NET 核心 Windows 服务器承载捆绑](https://aka.ms/dotnetcore-2-windowshosting)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-136">For servers, ANCM is included in the [.NET Core Windows Server Hosting bundle](https://aka.ms/dotnetcore-2-windowshosting).</span></span> <span data-ttu-id="0ac0f-137">对于开发计算机，Visual Studio 会自动安装 ANCM 在 IIS Express 中，并在 IIS 中如果计算机上已安装。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-137">For development machines, Visual Studio automatically installs ANCM in IIS Express, and in IIS if it is already installed on the machine.</span></span>

### <a name="install-the-iisintegration-nuget-package"></a><span data-ttu-id="0ac0f-138">安装 IISIntegration NuGet 包</span><span class="sxs-lookup"><span data-stu-id="0ac0f-138">Install the IISIntegration NuGet package</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="0ac0f-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="0ac0f-140">[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)包包含在 ASP.NET Core metapackages ([Microsoft.AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore/)和[Microsoft.AspNetCore.All](xref:fundamentals/metapackage)).</span><span class="sxs-lookup"><span data-stu-id="0ac0f-140">The [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package is included in the ASP.NET Core metapackages ([Microsoft.AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore/) and [Microsoft.AspNetCore.All](xref:fundamentals/metapackage)).</span></span> <span data-ttu-id="0ac0f-141">如果不使用 metapackages 之一时，安装`Microsoft.AspNetCore.Server.IISIntegration`单独。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-141">If you don't use one of the metapackages, install `Microsoft.AspNetCore.Server.IISIntegration` separately.</span></span> <span data-ttu-id="0ac0f-142">`IISIntegration`包是读取广播 ANCM 设置你的应用程序通过环境变量的互操作性包。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-142">The `IISIntegration` package is an interoperability pack that reads environment variables broadcast by ANCM to set up your app.</span></span> <span data-ttu-id="0ac0f-143">环境变量提供配置信息，例如要侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-143">The environment variables provide configuration information, such as the port to listen on.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="0ac0f-144">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-144">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="0ac0f-145">在你的应用程序，安装[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-145">In your application, install [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/).</span></span> <span data-ttu-id="0ac0f-146">`IISIntegration`包是读取广播 ANCM 设置你的应用程序通过环境变量的互操作性包。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-146">The `IISIntegration` package  is an interoperability pack that reads environment variables broadcast by ANCM to set up your app.</span></span> <span data-ttu-id="0ac0f-147">环境变量提供配置信息，例如要侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-147">The environment variables provide configuration information, such as the port to listen on.</span></span> 

---

### <a name="call-useiisintegration"></a><span data-ttu-id="0ac0f-148">调用 UseIISIntegration</span><span class="sxs-lookup"><span data-stu-id="0ac0f-148">Call UseIISIntegration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="0ac0f-149">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-149">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="0ac0f-150">`UseIISIntegration`上的扩展方法[ `WebHostBuilder` ](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder)使用 IIS 运行时自动调用。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-150">The `UseIISIntegration` extension method on [`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) is called automatically when you run with IIS.</span></span>

<span data-ttu-id="0ac0f-151">如果你不使用 ASP.NET Core metapackages 之一，但尚未安装`Microsoft.AspNetCore.Server.IISIntegration`包，则会收到运行时错误。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-151">If you aren't using one of the ASP.NET Core metapackages and haven't installed the  `Microsoft.AspNetCore.Server.IISIntegration` package, you get a runtime error.</span></span> <span data-ttu-id="0ac0f-152">如果调用`UseIISIntegration`显式，获取一个编译时错误，如果未安装此包。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-152">If you call `UseIISIntegration` explicitly, you get a compile time error if the package isn't installed.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="0ac0f-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="0ac0f-154">应用程序中`Main`方法中，调用`UseIISIntegration`上的扩展方法[ `WebHostBuilder` ](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-154">In your application's `Main` method, call the `UseIISIntegration` extension method on [`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> 

[!code-csharp[](aspnet-core-module/sample/Program.cs?name=snippet_Main&highlight=12)]

---

<span data-ttu-id="0ac0f-155">`UseIISIntegration`方法会查找环境变量 ANCM 设置，和它否 ops 如果未找到它们。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-155">The `UseIISIntegration` method looks for environment variables that ANCM sets, and it no-ops if they aren't found.</span></span> <span data-ttu-id="0ac0f-156">此行为帮助实现各种方案，例如开发和测试在 macOS 或 Linux 上和部署到运行 IIS 的服务器。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-156">This behavior facilitates scenarios like developing and testing on macOS or Linux and deploying to a server that runs IIS.</span></span> <span data-ttu-id="0ac0f-157">运行时在 macOS 或 Linux 上，Kestrel 充当 web 服务器;但是，当应用程序部署到 IIS 环境中，它会自动使用 ANCM 和 IIS。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-157">While running on macOS or Linux, Kestrel acts as the web server; but when the app is deployed to the IIS environment, it automatically uses ANCM and IIS.</span></span>

### <a name="ancm-port-binding-overrides-other-port-bindings"></a><span data-ttu-id="0ac0f-158">ANCM 端口绑定将替代其他端口绑定</span><span class="sxs-lookup"><span data-stu-id="0ac0f-158">ANCM port binding overrides other port bindings</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="0ac0f-159">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="0ac0f-160">ANCM 生成要分配给后端进程的动态端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-160">ANCM generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="0ac0f-161">`UseIISIntegration`方法拾取此动态端口，并配置要侦听的 Kestrel `http://locahost:{dynamicPort}/`。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-161">The `UseIISIntegration` method picks up this dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="0ac0f-162">此设置将替代其他 URL 配置，如调用到`UseUrls`或[Kestrel 的侦听 API](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-162">This overrides other URL configurations, such as calls to `UseUrls` or [Kestrel's Listen API](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span> <span data-ttu-id="0ac0f-163">因此，你不必调用`UseUrls`或 Kestrel 的`Listen`API 使用 ANCM 时。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-163">Therefore, you don't need to call `UseUrls` or Kestrel's `Listen` API when you use ANCM.</span></span> <span data-ttu-id="0ac0f-164">如果调用`UseUrls`或`Listen`，Kestrel 在运行不含 IIS 应用程序时指定的端口上侦听。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-164">If you do call `UseUrls` or `Listen`, Kestrel listens on the port you specify when you run the app without IIS.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="0ac0f-165">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="0ac0f-165">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="0ac0f-166">ANCM 生成要分配给后端进程的动态端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-166">ANCM generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="0ac0f-167">`UseIISIntegration`方法拾取此动态端口，并配置要侦听的 Kestrel `http://locahost:{dynamicPort}/`。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-167">The `UseIISIntegration` method picks up this dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="0ac0f-168">此设置将替代其他 URL 配置，如调用到`UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-168">This overrides other URL configurations, such as calls to `UseUrls`.</span></span> <span data-ttu-id="0ac0f-169">因此，你不必调用`UseUrls`当你使用 ANCM。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-169">Therefore, you don't need to call `UseUrls` when you use ANCM.</span></span> <span data-ttu-id="0ac0f-170">如果调用`UseUrls`，Kestrel 在运行不含 IIS 应用程序时指定的端口上侦听。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-170">If you do call `UseUrls`, Kestrel listens on the port you specify when you run the app without IIS.</span></span>

<span data-ttu-id="0ac0f-171">在 ASP.NET 核心 1.0 中，如果调用`UseUrls`，称之为**之前**调用`UseIISIntegration`以便不会被覆盖，ANCM 配置端口。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-171">In ASP.NET Core 1.0, if you call `UseUrls`, call it **before** you call `UseIISIntegration` so that the ANCM-configured port doesn't get overwritten.</span></span> <span data-ttu-id="0ac0f-172">此调用顺序不需要 ASP.NET 核心 1.1 中，因为 ANCM 设置将重写`UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-172">This calling order isn't required in ASP.NET Core 1.1, because the ANCM setting overrides `UseUrls`.</span></span>

---

### <a name="configure-ancm-options-in-webconfig"></a><span data-ttu-id="0ac0f-173">在 Web.config 中配置 ANCM 选项</span><span class="sxs-lookup"><span data-stu-id="0ac0f-173">Configure ANCM options in Web.config</span></span>

<span data-ttu-id="0ac0f-174">ASP.NET 核心模块的配置存储在*web.config*位于应用程序的根文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-174">Configuration for the ASP.NET Core Module is stored in the *web.config* file that is located in the application's root folder.</span></span> <span data-ttu-id="0ac0f-175">此文件中的设置指向启动命令并启动 ASP.NET Core 应用的自变量。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-175">Settings in this file point to the startup command and arguments that start your ASP.NET Core app.</span></span> <span data-ttu-id="0ac0f-176">有关示例*web.config*代码和指南的配置选项，请参阅[ASP.NET 核心模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-176">For sample *web.config* code and guidance on configuration options, see [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module).</span></span>

### <a name="run-with-iis-express-in-development"></a><span data-ttu-id="0ac0f-177">在开发过程中使用 IIS Express 运行</span><span class="sxs-lookup"><span data-stu-id="0ac0f-177">Run with IIS Express in development</span></span>

<span data-ttu-id="0ac0f-178">可以通过使用 ASP.NET Core 模板定义的默认配置文件的 Visual Studio 启动 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-178">IIS Express can be launched by Visual Studio using the default profile defined by the ASP.NET Core templates.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="0ac0f-179">代理配置使用 HTTP 协议和配对令牌</span><span class="sxs-lookup"><span data-stu-id="0ac0f-179">Proxy configuration uses HTTP protocol and a pairing token</span></span>

<span data-ttu-id="0ac0f-180">在 ANCM 和 Kestrel 之间创建的代理服务器使用 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-180">The proxy created between the ANCM and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="0ac0f-181">使用 HTTP 是一种性能优化其中 ANCM 和 Kestrel 之间的通信发生在上环回地址从网络接口中移出。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-181">Using HTTP is a performance optimization where the traffic between the ANCM and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="0ac0f-182">没有任何风险的窃听 ANCM 和 Kestrel 从服务器中移出的位置之间的通信。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-182">There's no risk of eavesdropping the traffic between the ANCM and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="0ac0f-183">配对令牌用于保证收到的 Kestrel 请求已通过 IIS 代理和不是来自某些其他源。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-183">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="0ac0f-184">创建并设置环境变量到配对的令牌 (`ASPNETCORE_TOKEN`) 通过 ANCM。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-184">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the ANCM.</span></span> <span data-ttu-id="0ac0f-185">配对的令牌还设置到标头 (`MSAspNetCoreToken`) 对每个代理的请求。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-185">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="0ac0f-186">IIS 中间件检查每个请求它接收以确认配对的令牌的标头值与匹配的环境变量值。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-186">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="0ac0f-187">如果令牌值不匹配，请求是记录，并拒绝。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-187">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="0ac0f-188">配对的令牌的环境变量和 ANCM 和 Kestrel 之间的通信无法访问从服务器中移出的位置。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-188">The pairing token environment variable and the traffic between the ANCM and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="0ac0f-189">无需知道配对的令牌值，攻击者无法提交绕过检查在 IIS 中间件的请求。</span><span class="sxs-lookup"><span data-stu-id="0ac0f-189">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ac0f-190">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0ac0f-190">Next steps</span></span>

<span data-ttu-id="0ac0f-191">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="0ac0f-191">For more information, see the following resources:</span></span>

* [<span data-ttu-id="0ac0f-192">本文的示例应用</span><span class="sxs-lookup"><span data-stu-id="0ac0f-192">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample)
* [<span data-ttu-id="0ac0f-193">ASP.NET 核心模块的源代码</span><span class="sxs-lookup"><span data-stu-id="0ac0f-193">ASP.NET Core Module source code</span></span>](https://github.com/aspnet/AspNetCoreModule)
* [<span data-ttu-id="0ac0f-194">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="0ac0f-194">ASP.NET Core Module Configuration Reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="0ac0f-195">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="0ac0f-195">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
