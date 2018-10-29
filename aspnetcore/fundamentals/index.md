---
title: ASP.NET Core 基础知识
author: rick-anderson
description: 了解生成 ASP.NET Core 应用的基础概念。
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/index
ms.openlocfilehash: 56344315acc59003248ffaf1e61455b94a93a545
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090714"
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="adbb3-103">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="adbb3-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="adbb3-104">ASP.NET Core 应用是一个控制台应用，它在其 `Program.Main` 方法中创建 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="adbb3-104">An ASP.NET Core app is a console app that creates a web server in its `Program.Main` method.</span></span> <span data-ttu-id="adbb3-105">`Main` 方法是应用的托管入口点：</span><span class="sxs-lookup"><span data-stu-id="adbb3-105">The `Main` method is the app's *managed entry point*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs)]

<span data-ttu-id="adbb3-106">.NET Core 主机：</span><span class="sxs-lookup"><span data-stu-id="adbb3-106">The .NET Core Host:</span></span>

* <span data-ttu-id="adbb3-107">加载 [.NET Core 运行时](https://github.com/dotnet/coreclr)。</span><span class="sxs-lookup"><span data-stu-id="adbb3-107">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="adbb3-108">使用第一个命令行参数作为包含入口点 (`Main`) 的托管二进制文件的路径，并开始执行代码。</span><span class="sxs-lookup"><span data-stu-id="adbb3-108">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="adbb3-109">`Main` 方法调用 [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*)，后者按照[生成器模式](https://wikipedia.org/wiki/Builder_pattern)来创建 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="adbb3-109">The `Main` method invokes [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*), which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web host.</span></span> <span data-ttu-id="adbb3-110">生成器提供定义 Web 服务器（例如，<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>）和启动类 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 的方法。</span><span class="sxs-lookup"><span data-stu-id="adbb3-110">The builder has methods that define the web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="adbb3-111">在前面的例子中，自动分配了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="adbb3-111">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="adbb3-112">ASP.NET Core 的 Web 主机尝试在 IIS 上运行（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="adbb3-112">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="adbb3-113">对于其他 Web 服务器（如 [HTTP.sys](xref:fundamentals/servers/httpsys)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="adbb3-113">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="adbb3-114">在下一节对 `UseStartup` 进行了更深入的介绍。</span><span class="sxs-lookup"><span data-stu-id="adbb3-114">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="adbb3-115"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder> 是 `WebHost.CreateDefaultBuilder` 调用的返回类型，它提供了许多可选方法。</span><span class="sxs-lookup"><span data-stu-id="adbb3-115"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="adbb3-116">其中的一些方法包括用于在 HTTP.sys 中托管应用的 `UseHttpSys`，以及用于指定根内容目录的 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-116">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="adbb3-117"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 和 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 方法生成 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="adbb3-117">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs)]

<span data-ttu-id="adbb3-118">.NET Core 主机：</span><span class="sxs-lookup"><span data-stu-id="adbb3-118">The .NET Core Host:</span></span>

* <span data-ttu-id="adbb3-119">加载 [.NET Core 运行时](https://github.com/dotnet/coreclr)。</span><span class="sxs-lookup"><span data-stu-id="adbb3-119">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="adbb3-120">使用第一个命令行参数作为包含入口点 (`Main`) 的托管二进制文件的路径，并开始执行代码。</span><span class="sxs-lookup"><span data-stu-id="adbb3-120">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="adbb3-121">`Main` 方法使用 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>，后者按照[生成器模式](https://wikipedia.org/wiki/Builder_pattern)来创建 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="adbb3-121">The `Main` method uses <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>, which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web app host.</span></span> <span data-ttu-id="adbb3-122">生成器提供定义 Web 服务器（例如，<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>）和启动类 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 的方法。</span><span class="sxs-lookup"><span data-stu-id="adbb3-122">The builder has methods that define the web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="adbb3-123">在前面的示例中，使用了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="adbb3-123">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="adbb3-124">对于其他 Web 服务器（如 [WebListener](xref:fundamentals/servers/weblistener)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="adbb3-124">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="adbb3-125">在下一节对 `UseStartup` 进行了更深入的介绍。</span><span class="sxs-lookup"><span data-stu-id="adbb3-125">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="adbb3-126">`WebHostBuilder` 提供了许多可选方法，其中包括用于在 IIS 和 IIS Express 中进行托管的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>，以及用于指定根内容目录的 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-126">`WebHostBuilder` provides many optional methods, including <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> for hosting in IIS and IIS Express and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="adbb3-127"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 和 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 方法生成 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="adbb3-127">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

## <a name="startup"></a><span data-ttu-id="adbb3-128">启动</span><span class="sxs-lookup"><span data-stu-id="adbb3-128">Startup</span></span>

<span data-ttu-id="adbb3-129">`WebHostBuilder` 上的 `UseStartup` 方法为你的应用指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="adbb3-129">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs?highlight=10)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs?highlight=7)]

::: moniker-end

<span data-ttu-id="adbb3-130">`Startup` 类用于定义请求处理管道和配置应用所需的任何服务。</span><span class="sxs-lookup"><span data-stu-id="adbb3-130">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="adbb3-131">`Startup` 必须是公共类，并包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="adbb3-131">The `Startup` class must be public and contain the following methods:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Startup.cs)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Startup.cs)]

::: moniker-end

<span data-ttu-id="adbb3-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> 定义应用所使用的[服务](#dependency-injection-services)（如 ASP.NET Core MVC、Entity Framework Core 和标识）。</span><span class="sxs-lookup"><span data-stu-id="adbb3-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="adbb3-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*> 定义在请求管道中调用的[中间件](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="adbb3-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*> defines the [middleware](xref:fundamentals/middleware/index) called in the request pipeline.</span></span>

<span data-ttu-id="adbb3-134">有关更多信息，请参见<xref:fundamentals/startup>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-134">For more information, see <xref:fundamentals/startup>.</span></span>

## <a name="content-root"></a><span data-ttu-id="adbb3-135">内容根</span><span class="sxs-lookup"><span data-stu-id="adbb3-135">Content root</span></span>

<span data-ttu-id="adbb3-136">内容根是应用所使用的任何内容的基路径，如 [Razor Pages](xref:razor-pages/index)、MVC 视图和静态资产。</span><span class="sxs-lookup"><span data-stu-id="adbb3-136">The content root is the base path to any content used by the app, such as [Razor Pages](xref:razor-pages/index), MVC views, and static assets.</span></span> <span data-ttu-id="adbb3-137">默认情况下，内容根位置与用于托管应用的可执行文件的应用基路径相同。</span><span class="sxs-lookup"><span data-stu-id="adbb3-137">By default, the content root is the same location as the app base path for the executable hosting the app.</span></span>

## <a name="web-root-webroot"></a><span data-ttu-id="adbb3-138">Web 根 (webroot)</span><span class="sxs-lookup"><span data-stu-id="adbb3-138">Web root (webroot)</span></span>

<span data-ttu-id="adbb3-139">应用的 webroot 是项目中的目录，其中包含公共资源、CSS 等静态资源、JavaScript 和图形文件。</span><span class="sxs-lookup"><span data-stu-id="adbb3-139">The webroot of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span> <span data-ttu-id="adbb3-140">wwwroot 默认为 webroot。</span><span class="sxs-lookup"><span data-stu-id="adbb3-140">By default, *wwwroot* is the webroot.</span></span>

<span data-ttu-id="adbb3-141">对于 Razor (.cshtml) 文件，波浪号斜杠 `~/` 指向 webroot。</span><span class="sxs-lookup"><span data-stu-id="adbb3-141">For Razor (*.cshtml*) files, the tilde-slash  `~/` points to the webroot.</span></span> <span data-ttu-id="adbb3-142">以 `~/` 开头的路径称为虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="adbb3-142">Paths beginning with `~/` are referred to as virtual paths.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="adbb3-143">依赖关系注入（服务）</span><span class="sxs-lookup"><span data-stu-id="adbb3-143">Dependency injection (services)</span></span>

<span data-ttu-id="adbb3-144">服务是应用中常用的组件。</span><span class="sxs-lookup"><span data-stu-id="adbb3-144">A *service* is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="adbb3-145">可以通过[依存关系注入 (DI)](xref:fundamentals/dependency-injection) 来获取服务。</span><span class="sxs-lookup"><span data-stu-id="adbb3-145">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="adbb3-146">ASP.NET Core 包括默认支持[构造函数注入](xref:mvc/controllers/dependency-injection#constructor-injection)的本机控制反转 (IoC) 容器。</span><span class="sxs-lookup"><span data-stu-id="adbb3-146">ASP.NET Core includes a native Inversion of Control (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="adbb3-147">可根据需要替换默认容器。</span><span class="sxs-lookup"><span data-stu-id="adbb3-147">You can replace the default container if you wish.</span></span> <span data-ttu-id="adbb3-148">DI 除了具备[松散耦合优势](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation)以外，还可以使服务（例如[日志记录](xref:fundamentals/logging/index)）在整个应用中可用。</span><span class="sxs-lookup"><span data-stu-id="adbb3-148">In addition to its [loose coupling benefit](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation), DI makes services, such as [logging](xref:fundamentals/logging/index), available throughout your app.</span></span>

<span data-ttu-id="adbb3-149">有关更多信息，请参见<xref:fundamentals/dependency-injection>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-149">For more information, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="middleware"></a><span data-ttu-id="adbb3-150">中间件</span><span class="sxs-lookup"><span data-stu-id="adbb3-150">Middleware</span></span>

<span data-ttu-id="adbb3-151">在 ASP.NET Core 中，使用[中间件](xref:fundamentals/middleware/index)来撰写请求管道。</span><span class="sxs-lookup"><span data-stu-id="adbb3-151">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware/index).</span></span> <span data-ttu-id="adbb3-152">ASP.NET Core 中间件在 `HttpContext` 上执行异步操作，然后调用管道中的下一个中间件或终止请求。</span><span class="sxs-lookup"><span data-stu-id="adbb3-152">ASP.NET Core middleware performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.</span></span>

<span data-ttu-id="adbb3-153">按照惯例，通过在 `Configure` 方法中调用 `UseXYZ` 扩展方法，向管道添加名为“XYZ”的中间件组件。</span><span class="sxs-lookup"><span data-stu-id="adbb3-153">By convention, a middleware component called "XYZ" is added to the pipeline by invoking a `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="adbb3-154">ASP.NET Core 包含一组丰富的内置中间件，你也可以编写自己的自定义中间件。</span><span class="sxs-lookup"><span data-stu-id="adbb3-154">ASP.NET Core includes a rich set of built-in middleware, and you can write your own custom middleware.</span></span> <span data-ttu-id="adbb3-155">ASP.NET Core 应用中支持 [.NET 的开放 Web 接口 (OWIN)](xref:fundamentals/owin)，它将 Web 应用与 Web 服务器分离。</span><span class="sxs-lookup"><span data-stu-id="adbb3-155">[Open Web Interface for .NET (OWIN)](xref:fundamentals/owin), which allows web apps to be decoupled from web servers, is supported in ASP.NET Core apps.</span></span>

<span data-ttu-id="adbb3-156">有关详细信息，请参阅 <xref:fundamentals/middleware/index> 和 <xref:fundamentals/owin>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-156">For more information, see <xref:fundamentals/middleware/index> and <xref:fundamentals/owin>.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="initiate-http-requests"></a><span data-ttu-id="adbb3-157">启动 HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="adbb3-157">Initiate HTTP requests</span></span>

<span data-ttu-id="adbb3-158"><xref:System.Net.Http.IHttpClientFactory> 可访问 <xref:System.Net.Http.HttpClient> 实例以发出 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="adbb3-158"><xref:System.Net.Http.IHttpClientFactory> is available to access <xref:System.Net.Http.HttpClient> instances to make HTTP requests.</span></span>

<span data-ttu-id="adbb3-159">有关更多信息，请参见<xref:fundamentals/http-requests>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-159">For more information, see <xref:fundamentals/http-requests>.</span></span>

::: moniker-end

## <a name="environments"></a><span data-ttu-id="adbb3-160">环境</span><span class="sxs-lookup"><span data-stu-id="adbb3-160">Environments</span></span>

<span data-ttu-id="adbb3-161">环境（如“开发”环境和“生产”环境）是 ASP.NET Core 的高级概念，可使用环境变量、设置文件和命令行参数进行设置。</span><span class="sxs-lookup"><span data-stu-id="adbb3-161">Environments, such as *Development* and *Production*, are a first-class notion in ASP.NET Core and can be set using an environment variable, settings file, and command-line argument.</span></span>

<span data-ttu-id="adbb3-162">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-162">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="hosting"></a><span data-ttu-id="adbb3-163">宿主</span><span class="sxs-lookup"><span data-stu-id="adbb3-163">Hosting</span></span>

<span data-ttu-id="adbb3-164">ASP.NET Core 应用可配置和启动一个*主机*，负责应用启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="adbb3-164">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="adbb3-165">有关更多信息，请参见<xref:fundamentals/host/index>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-165">For more information, see <xref:fundamentals/host/index>.</span></span>

## <a name="servers"></a><span data-ttu-id="adbb3-166">服务器</span><span class="sxs-lookup"><span data-stu-id="adbb3-166">Servers</span></span>

<span data-ttu-id="adbb3-167">ASP.NET Core 托管模型不直接侦听请求。</span><span class="sxs-lookup"><span data-stu-id="adbb3-167">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="adbb3-168">托管模型依赖 HTTP 服务器实现将请求转发到应用。</span><span class="sxs-lookup"><span data-stu-id="adbb3-168">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="adbb3-169">转发的请求被打包为一组可通过接口进行访问的功能对象。</span><span class="sxs-lookup"><span data-stu-id="adbb3-169">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="adbb3-170">ASP.NET Core 包含托管的跨平台 Web 服务器，名为 [Kestrel](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="adbb3-170">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="adbb3-171">Kestrel 通常在生产 Web 服务器（如反向代理配置中的 [IIS](https://www.iis.net/) 或 [Nginx](http://nginx.org)）后台运行。</span><span class="sxs-lookup"><span data-stu-id="adbb3-171">Kestrel is commonly run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org) in a reverse proxy configuration.</span></span> <span data-ttu-id="adbb3-172">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="adbb3-172">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

<span data-ttu-id="adbb3-173">有关更多信息，请参见<xref:fundamentals/servers/index>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-173">For more information, see <xref:fundamentals/servers/index>.</span></span>

## <a name="configuration"></a><span data-ttu-id="adbb3-174">配置</span><span class="sxs-lookup"><span data-stu-id="adbb3-174">Configuration</span></span>

<span data-ttu-id="adbb3-175">ASP.NET Core 基于名称/值对使用配置模型。</span><span class="sxs-lookup"><span data-stu-id="adbb3-175">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="adbb3-176">配置模型不基于 <xref:System.Configuration> 或 *web.config*。配置从一组有序的配置提供程序获取设置。</span><span class="sxs-lookup"><span data-stu-id="adbb3-176">The configuration model isn't based on <xref:System.Configuration> or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="adbb3-177">内置配置提供程序支持各种文件格式（XML、 JSON、INI）、环境变量和命令行参数。</span><span class="sxs-lookup"><span data-stu-id="adbb3-177">The built-in configuration providers support a variety of file formats (XML, JSON, INI), environment variables, and command-line arguments.</span></span> <span data-ttu-id="adbb3-178">也可以编写你自己的自定义配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="adbb3-178">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="adbb3-179">有关更多信息，请参见<xref:fundamentals/configuration/index>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-179">For more information, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="logging"></a><span data-ttu-id="adbb3-180">日志记录</span><span class="sxs-lookup"><span data-stu-id="adbb3-180">Logging</span></span>

<span data-ttu-id="adbb3-181">ASP.NET Core 支持适用于各种日志记录提供程序的日志记录 API。</span><span class="sxs-lookup"><span data-stu-id="adbb3-181">ASP.NET Core supports a Logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="adbb3-182">内置提供程序支持向一个或多个目标发送日志。</span><span class="sxs-lookup"><span data-stu-id="adbb3-182">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="adbb3-183">可使用第三方记录框架。</span><span class="sxs-lookup"><span data-stu-id="adbb3-183">Third-party logging frameworks can be used.</span></span>

<span data-ttu-id="adbb3-184">有关更多信息，请参见<xref:fundamentals/logging/index>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-184">For more information, see <xref:fundamentals/logging/index>.</span></span>

## <a name="error-handling"></a><span data-ttu-id="adbb3-185">错误处理</span><span class="sxs-lookup"><span data-stu-id="adbb3-185">Error handling</span></span>

<span data-ttu-id="adbb3-186">ASP.NET Core 的内置方案可处理应用中的错误，包括开发人员异常页、自定义错误页、静态状态代码页和启动异常处理。</span><span class="sxs-lookup"><span data-stu-id="adbb3-186">ASP.NET Core has built-in scenarios for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="adbb3-187">有关更多信息，请参见<xref:fundamentals/error-handling>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-187">For more information, see <xref:fundamentals/error-handling>.</span></span>

## <a name="routing"></a><span data-ttu-id="adbb3-188">路由</span><span class="sxs-lookup"><span data-stu-id="adbb3-188">Routing</span></span>

<span data-ttu-id="adbb3-189">ASP.NET Core 提供将应用请求路由到路由处理程序的方案。</span><span class="sxs-lookup"><span data-stu-id="adbb3-189">ASP.NET Core offers scenarios for routing of app requests to route handlers.</span></span>

<span data-ttu-id="adbb3-190">有关更多信息，请参见<xref:fundamentals/routing>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-190">For more information, see <xref:fundamentals/routing>.</span></span>

## <a name="file-providers"></a><span data-ttu-id="adbb3-191">文件提供程序</span><span class="sxs-lookup"><span data-stu-id="adbb3-191">File Providers</span></span>

<span data-ttu-id="adbb3-192">ASP.NET Core 通过使用文件提供程序抽象化文件系统访问，文件提供程序可提供一个跨平台处理文件的通用界面。</span><span class="sxs-lookup"><span data-stu-id="adbb3-192">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="adbb3-193">有关更多信息，请参见<xref:fundamentals/file-providers>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-193">For more information, see <xref:fundamentals/file-providers>.</span></span>

## <a name="static-files"></a><span data-ttu-id="adbb3-194">静态文件</span><span class="sxs-lookup"><span data-stu-id="adbb3-194">Static files</span></span>

<span data-ttu-id="adbb3-195">静态文件中间件为静态文件（如 HTML、CSS、映像和 JavaScript 文件）提供服务。</span><span class="sxs-lookup"><span data-stu-id="adbb3-195">Static Files Middleware serves static files, such as HTML, CSS, image, and JavaScript files.</span></span>

<span data-ttu-id="adbb3-196">有关更多信息，请参见<xref:fundamentals/static-files>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-196">For more information, see <xref:fundamentals/static-files>.</span></span>

## <a name="session-and-app-state"></a><span data-ttu-id="adbb3-197">会话和应用状态</span><span class="sxs-lookup"><span data-stu-id="adbb3-197">Session and app state</span></span>

<span data-ttu-id="adbb3-198">ASP.NET Core 提供几种可在用户浏览 web 应用时保留会话和应用状态的方法。</span><span class="sxs-lookup"><span data-stu-id="adbb3-198">ASP.NET Core offers several approaches to preserve session and app state while a user browses a web app.</span></span>

<span data-ttu-id="adbb3-199">有关更多信息，请参见<xref:fundamentals/app-state>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-199">For more information, see <xref:fundamentals/app-state>.</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="adbb3-200">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="adbb3-200">Globalization and localization</span></span>

<span data-ttu-id="adbb3-201">使用 ASP.NET Core 创建多语言网站，可让网站拥有更多受众。</span><span class="sxs-lookup"><span data-stu-id="adbb3-201">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="adbb3-202">ASP.NET Core 可提供服务和中间件，将内容本地化为不同的语言和区域性。</span><span class="sxs-lookup"><span data-stu-id="adbb3-202">ASP.NET Core provides services and middleware for localizing content into different languages and cultures.</span></span>

<span data-ttu-id="adbb3-203">有关更多信息，请参见<xref:fundamentals/localization>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-203">For more information, see <xref:fundamentals/localization>.</span></span>

## <a name="request-features"></a><span data-ttu-id="adbb3-204">请求功能</span><span class="sxs-lookup"><span data-stu-id="adbb3-204">Request features</span></span>

<span data-ttu-id="adbb3-205">与 HTTP 请求和响应相关的 Web 服务器实现详细信息在接口中定义。</span><span class="sxs-lookup"><span data-stu-id="adbb3-205">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="adbb3-206">服务器实现和中间件使用这些接口来创建和修改应用的托管管道。</span><span class="sxs-lookup"><span data-stu-id="adbb3-206">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="adbb3-207">有关更多信息，请参见<xref:fundamentals/request-features>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-207">For more information, see <xref:fundamentals/request-features>.</span></span>

## <a name="background-tasks"></a><span data-ttu-id="adbb3-208">后台任务</span><span class="sxs-lookup"><span data-stu-id="adbb3-208">Background tasks</span></span>

<span data-ttu-id="adbb3-209">后台任务作为*托管服务*实现。</span><span class="sxs-lookup"><span data-stu-id="adbb3-209">Background tasks are implemented as *hosted services*.</span></span> <span data-ttu-id="adbb3-210">托管服务是一个类，具有实现 <xref:Microsoft.Extensions.Hosting.IHostedService> 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="adbb3-210">A hosted service is a class with background task logic that implements the <xref:Microsoft.Extensions.Hosting.IHostedService> interface.</span></span>

<span data-ttu-id="adbb3-211">有关更多信息，请参见<xref:fundamentals/host/hosted-services>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-211">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

## <a name="access-httpcontext"></a><span data-ttu-id="adbb3-212">访问 HttpContext</span><span class="sxs-lookup"><span data-stu-id="adbb3-212">Access HttpContext</span></span>

<span data-ttu-id="adbb3-213">用 Razor Pages 和 MVC 处理请求时，`HttpContext` 自动可用。</span><span class="sxs-lookup"><span data-stu-id="adbb3-213">`HttpContext` is automatically available when processing requests with Razor Pages and MVC.</span></span> <span data-ttu-id="adbb3-214">当 `HttpContext` 不可立即使用时，可通过 <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> 接口及其默认实现 <xref:Microsoft.AspNetCore.Http.HttpContextAccessor> 访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="adbb3-214">In circumstances where `HttpContext` isn't readily available, you can access the `HttpContext` through the <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> interface and its default implementation, <xref:Microsoft.AspNetCore.Http.HttpContextAccessor>.</span></span>

<span data-ttu-id="adbb3-215">有关更多信息，请参见<xref:fundamentals/httpcontext>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-215">For more information, see <xref:fundamentals/httpcontext>.</span></span>

## <a name="websockets"></a><span data-ttu-id="adbb3-216">WebSockets</span><span class="sxs-lookup"><span data-stu-id="adbb3-216">WebSockets</span></span>

<span data-ttu-id="adbb3-217">[WebSocket](https://wikipedia.org/wiki/WebSocket) 是一个协议，支持通过 TCP 连接建立持久的双向信道。</span><span class="sxs-lookup"><span data-stu-id="adbb3-217">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="adbb3-218">它可用于聊天、股票报价和游戏等应用，以及 Web 应用中需要实时功能的任何位置。</span><span class="sxs-lookup"><span data-stu-id="adbb3-218">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="adbb3-219">ASP.NET Core 支持 Web 套接字方案。</span><span class="sxs-lookup"><span data-stu-id="adbb3-219">ASP.NET Core supports web socket scenarios.</span></span>

<span data-ttu-id="adbb3-220">有关更多信息，请参见<xref:fundamentals/websockets>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-220">For more information, see <xref:fundamentals/websockets>.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="microsoftaspnetcoreapp-metapackage"></a><span data-ttu-id="adbb3-221">Microsoft.AspNetCore.App 元包</span><span class="sxs-lookup"><span data-stu-id="adbb3-221">Microsoft.AspNetCore.App metapackage</span></span>

<span data-ttu-id="adbb3-222">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) 元包简化了包管理。</span><span class="sxs-lookup"><span data-stu-id="adbb3-222">The [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) metapackage simplifies package management.</span></span>

<span data-ttu-id="adbb3-223">有关更多信息，请参见<xref:fundamentals/metapackage-app>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-223">For more information, see <xref:fundamentals/metapackage-app>.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="adbb3-224">Microsoft.AspNetCore.All 元包</span><span class="sxs-lookup"><span data-stu-id="adbb3-224">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="adbb3-225">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="adbb3-225">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="adbb3-226">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="adbb3-226">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="adbb3-227">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="adbb3-227">All supported packages by Entity Framework Core.</span></span>
* <span data-ttu-id="adbb3-228">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="adbb3-228">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="adbb3-229">有关更多信息，请参见<xref:fundamentals/metapackage>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-229">For more information, see <xref:fundamentals/metapackage>.</span></span>

::: moniker-end

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="adbb3-230">.NET Core 与 .NET Framework 运行时</span><span class="sxs-lookup"><span data-stu-id="adbb3-230">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="adbb3-231">ASP.NET Core 应用可以面向 .NET Core 或 .NET Framework 运行时。</span><span class="sxs-lookup"><span data-stu-id="adbb3-231">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="adbb3-232">有关详细信息，请参阅[在 .NET Core 和 .NET Framework 之间进行选择](/dotnet/articles/standard/choosing-core-framework-server)。</span><span class="sxs-lookup"><span data-stu-id="adbb3-232">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="adbb3-233">在 ASP.NET Core 和 ASP.NET 之间进行选择</span><span class="sxs-lookup"><span data-stu-id="adbb3-233">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="adbb3-234">有关在 ASP.NET Core 和 ASP.NET 之间进行选择的详细信息，请参阅 <xref:fundamentals/choose-between-aspnet-and-aspnetcore>。</span><span class="sxs-lookup"><span data-stu-id="adbb3-234">For more information on choosing between ASP.NET Core and ASP.NET, see <xref:fundamentals/choose-between-aspnet-and-aspnetcore>.</span></span>
