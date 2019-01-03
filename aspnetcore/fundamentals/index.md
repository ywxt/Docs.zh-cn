---
title: ASP.NET Core 基础知识
author: rick-anderson
description: 了解生成 ASP.NET Core 应用的基础概念。
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: fundamentals/index
ms.openlocfilehash: 11dc6336ae7667038983c967f28232bef325f5bb
ms.sourcegitcommit: 816f39e852a8f453e8682081871a31bc66db153a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53637763"
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="c8c18-103">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="c8c18-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="c8c18-104">ASP.NET Core 应用是一个控制台应用，它在其 `Program.Main` 方法中创建 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-104">An ASP.NET Core app is a console app that creates a web server in its `Program.Main` method.</span></span> <span data-ttu-id="c8c18-105">`Main` 方法是应用的托管入口点：</span><span class="sxs-lookup"><span data-stu-id="c8c18-105">The `Main` method is the app's *managed entry point*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs)]

<span data-ttu-id="c8c18-106">.NET Core 主机：</span><span class="sxs-lookup"><span data-stu-id="c8c18-106">The .NET Core Host:</span></span>

* <span data-ttu-id="c8c18-107">加载 [.NET Core 运行时](https://github.com/dotnet/coreclr)。</span><span class="sxs-lookup"><span data-stu-id="c8c18-107">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="c8c18-108">使用第一个命令行参数作为包含入口点 (`Main`) 的托管二进制文件的路径，并开始执行代码。</span><span class="sxs-lookup"><span data-stu-id="c8c18-108">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="c8c18-109">`Main` 方法调用 [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*)，后者按照[生成器模式](https://wikipedia.org/wiki/Builder_pattern)来创建 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="c8c18-109">The `Main` method invokes [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*), which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web host.</span></span> <span data-ttu-id="c8c18-110">生成器包含定义 Web 服务器（例如，<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>）和启动类 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 的方法。</span><span class="sxs-lookup"><span data-stu-id="c8c18-110">The builder has methods that define a web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="c8c18-111">在前面的例子中，自动分配了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-111">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="c8c18-112">ASP.NET Core 的 Web 主机尝试在 [Internet Information Services (IIS)](https://www.iis.net/)（若有）上运行。</span><span class="sxs-lookup"><span data-stu-id="c8c18-112">ASP.NET Core's web host attempts to run on [Internet Information Services (IIS)](https://www.iis.net/), if available.</span></span> <span data-ttu-id="c8c18-113">对于其他 Web 服务器（如 [HTTP.sys](xref:fundamentals/servers/httpsys)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="c8c18-113">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="c8c18-114">[启动](#startup)部分进一步介绍了 `UseStartup`。</span><span class="sxs-lookup"><span data-stu-id="c8c18-114">`UseStartup` is explained further in the [Startup](#startup) section.</span></span>

<span data-ttu-id="c8c18-115"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder> 是 `WebHost.CreateDefaultBuilder` 调用的返回类型，它提供了许多可选方法。</span><span class="sxs-lookup"><span data-stu-id="c8c18-115"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="c8c18-116">其中的一些方法包括用于在 HTTP.sys 中托管应用的 `UseHttpSys`，以及用于指定根内容目录的 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-116">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="c8c18-117"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 和 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 方法生成 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c8c18-117">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs)]

<span data-ttu-id="c8c18-118">.NET Core 主机：</span><span class="sxs-lookup"><span data-stu-id="c8c18-118">The .NET Core Host:</span></span>

* <span data-ttu-id="c8c18-119">加载 [.NET Core 运行时](https://github.com/dotnet/coreclr)。</span><span class="sxs-lookup"><span data-stu-id="c8c18-119">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="c8c18-120">使用第一个命令行参数作为包含入口点 (`Main`) 的托管二进制文件的路径，并开始执行代码。</span><span class="sxs-lookup"><span data-stu-id="c8c18-120">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="c8c18-121">`Main` 方法使用 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>，后者按照[生成器模式](https://wikipedia.org/wiki/Builder_pattern)来创建 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="c8c18-121">The `Main` method uses <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>, which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web app host.</span></span> <span data-ttu-id="c8c18-122">生成器提供定义 Web 服务器（例如，<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>）和启动类 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 的方法。</span><span class="sxs-lookup"><span data-stu-id="c8c18-122">The builder has methods that define the web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="c8c18-123">在前面的示例中，使用了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-123">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="c8c18-124">对于其他 Web 服务器（如 [HTTP.sys](xref:fundamentals/servers/httpsys)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="c8c18-124">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="c8c18-125">[启动](#startup)部分进一步介绍了 `UseStartup`。</span><span class="sxs-lookup"><span data-stu-id="c8c18-125">`UseStartup` is explained further in the [Startup](#startup) section.</span></span>

<span data-ttu-id="c8c18-126">`WebHostBuilder` 提供了许多可选方法，其中包括用于在 IIS 和 IIS Express 中进行托管的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>，以及用于指定根内容目录的 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-126">`WebHostBuilder` provides many optional methods, including <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> for hosting in IIS and IIS Express and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="c8c18-127"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 和 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 方法生成 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c8c18-127">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

## <a name="startup"></a><span data-ttu-id="c8c18-128">启动</span><span class="sxs-lookup"><span data-stu-id="c8c18-128">Startup</span></span>

<span data-ttu-id="c8c18-129">`WebHostBuilder` 上的 `UseStartup` 方法为你的应用指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="c8c18-129">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs?highlight=10)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs?highlight=7)]

::: moniker-end

<span data-ttu-id="c8c18-130">`Startup` 类用于定义请求处理管道和配置应用所需的任何服务。</span><span class="sxs-lookup"><span data-stu-id="c8c18-130">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="c8c18-131">`Startup` 必须是公共类，并包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="c8c18-131">The `Startup` class must be public and contain the following methods:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Startup.cs)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Startup.cs)]

::: moniker-end

<span data-ttu-id="c8c18-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> 定义应用所使用的[服务](#dependency-injection-services)（如 ASP.NET Core MVC、Entity Framework Core 和标识）。</span><span class="sxs-lookup"><span data-stu-id="c8c18-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="c8c18-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*> 定义在请求管道中调用的[中间件](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="c8c18-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*> defines the [middleware](xref:fundamentals/middleware/index) called in the request pipeline.</span></span>

<span data-ttu-id="c8c18-134">有关更多信息，请参见<xref:fundamentals/startup>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-134">For more information, see <xref:fundamentals/startup>.</span></span>

## <a name="content-root"></a><span data-ttu-id="c8c18-135">内容根</span><span class="sxs-lookup"><span data-stu-id="c8c18-135">Content root</span></span>

<span data-ttu-id="c8c18-136">内容根是应用所使用的任何内容的基路径，如 [Razor Pages](xref:razor-pages/index)、MVC 视图和静态资产。</span><span class="sxs-lookup"><span data-stu-id="c8c18-136">The content root is the base path to any content used by the app, such as [Razor Pages](xref:razor-pages/index), MVC views, and static assets.</span></span> <span data-ttu-id="c8c18-137">默认情况下，内容根位置与用于托管应用的可执行文件的应用基路径相同。</span><span class="sxs-lookup"><span data-stu-id="c8c18-137">By default, the content root is the same location as the app base path for the executable hosting the app.</span></span>

## <a name="web-root-webroot"></a><span data-ttu-id="c8c18-138">Web 根 (webroot)</span><span class="sxs-lookup"><span data-stu-id="c8c18-138">Web root (webroot)</span></span>

<span data-ttu-id="c8c18-139">应用的 webroot 是项目中的目录，其中包含公共资源、CSS 等静态资源、JavaScript 和图形文件。</span><span class="sxs-lookup"><span data-stu-id="c8c18-139">The webroot of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span> <span data-ttu-id="c8c18-140">wwwroot 默认为 webroot。</span><span class="sxs-lookup"><span data-stu-id="c8c18-140">By default, *wwwroot* is the webroot.</span></span>

<span data-ttu-id="c8c18-141">对于 Razor (.cshtml) 文件，波浪号斜杠 `~/` 指向 webroot。</span><span class="sxs-lookup"><span data-stu-id="c8c18-141">For Razor (*.cshtml*) files, the tilde-slash  `~/` points to the webroot.</span></span> <span data-ttu-id="c8c18-142">以 `~/` 开头的路径称为虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="c8c18-142">Paths beginning with `~/` are referred to as virtual paths.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="c8c18-143">依赖关系注入（服务）</span><span class="sxs-lookup"><span data-stu-id="c8c18-143">Dependency injection (services)</span></span>

<span data-ttu-id="c8c18-144">服务是应用中常用的组件。</span><span class="sxs-lookup"><span data-stu-id="c8c18-144">A *service* is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="c8c18-145">可以通过[依存关系注入 (DI)](xref:fundamentals/dependency-injection) 来获取服务。</span><span class="sxs-lookup"><span data-stu-id="c8c18-145">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="c8c18-146">ASP.NET Core 包括默认支持[构造函数注入](xref:mvc/controllers/dependency-injection#constructor-injection)的本机控制反转 (IoC) 容器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-146">ASP.NET Core includes a native Inversion of Control (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="c8c18-147">可根据需要替换默认容器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-147">You can replace the default container if you wish.</span></span> <span data-ttu-id="c8c18-148">DI 除了具备[松散耦合优势](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation)以外，还可以使服务（例如[日志记录](xref:fundamentals/logging/index)）在整个应用中可用。</span><span class="sxs-lookup"><span data-stu-id="c8c18-148">In addition to its [loose coupling benefit](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation), DI makes services, such as [logging](xref:fundamentals/logging/index), available throughout your app.</span></span>

<span data-ttu-id="c8c18-149">有关更多信息，请参见<xref:fundamentals/dependency-injection>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-149">For more information, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="middleware"></a><span data-ttu-id="c8c18-150">中间件</span><span class="sxs-lookup"><span data-stu-id="c8c18-150">Middleware</span></span>

<span data-ttu-id="c8c18-151">在 ASP.NET Core 中，使用[中间件](xref:fundamentals/middleware/index)来撰写请求管道。</span><span class="sxs-lookup"><span data-stu-id="c8c18-151">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware/index).</span></span> <span data-ttu-id="c8c18-152">ASP.NET Core 中间件在 `HttpContext` 上执行异步操作，然后调用管道中的下一个中间件或终止请求。</span><span class="sxs-lookup"><span data-stu-id="c8c18-152">ASP.NET Core middleware performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.</span></span>

<span data-ttu-id="c8c18-153">按照惯例，通过在 `Configure` 方法中调用 `UseXYZ` 扩展方法，向管道添加名为“XYZ”的中间件组件。</span><span class="sxs-lookup"><span data-stu-id="c8c18-153">By convention, a middleware component called "XYZ" is added to the pipeline by invoking a `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="c8c18-154">ASP.NET Core 包含一组丰富的内置中间件，你也可以编写自己的自定义中间件。</span><span class="sxs-lookup"><span data-stu-id="c8c18-154">ASP.NET Core includes a rich set of built-in middleware, and you can write your own custom middleware.</span></span> <span data-ttu-id="c8c18-155">ASP.NET Core 应用中支持 [.NET 的开放 Web 接口 (OWIN)](xref:fundamentals/owin)，它将 Web 应用与 Web 服务器分离。</span><span class="sxs-lookup"><span data-stu-id="c8c18-155">[Open Web Interface for .NET (OWIN)](xref:fundamentals/owin), which allows web apps to be decoupled from web servers, is supported in ASP.NET Core apps.</span></span>

<span data-ttu-id="c8c18-156">有关详细信息，请参阅 <xref:fundamentals/middleware/index> 和 <xref:fundamentals/owin>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-156">For more information, see <xref:fundamentals/middleware/index> and <xref:fundamentals/owin>.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="initiate-http-requests"></a><span data-ttu-id="c8c18-157">启动 HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="c8c18-157">Initiate HTTP requests</span></span>

<span data-ttu-id="c8c18-158"><xref:System.Net.Http.IHttpClientFactory> 可访问 <xref:System.Net.Http.HttpClient> 实例以发出 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c8c18-158"><xref:System.Net.Http.IHttpClientFactory> is available to access <xref:System.Net.Http.HttpClient> instances to make HTTP requests.</span></span>

<span data-ttu-id="c8c18-159">有关更多信息，请参见<xref:fundamentals/http-requests>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-159">For more information, see <xref:fundamentals/http-requests>.</span></span>

::: moniker-end

## <a name="environments"></a><span data-ttu-id="c8c18-160">环境</span><span class="sxs-lookup"><span data-stu-id="c8c18-160">Environments</span></span>

<span data-ttu-id="c8c18-161">环境（如“开发”环境和“生产”环境）是 ASP.NET Core 的高级概念，可使用环境变量、设置文件和命令行参数进行设置。</span><span class="sxs-lookup"><span data-stu-id="c8c18-161">Environments, such as *Development* and *Production*, are a first-class notion in ASP.NET Core and can be set using an environment variable, settings file, and command-line argument.</span></span>

<span data-ttu-id="c8c18-162">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-162">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="hosting"></a><span data-ttu-id="c8c18-163">宿主</span><span class="sxs-lookup"><span data-stu-id="c8c18-163">Hosting</span></span>

<span data-ttu-id="c8c18-164">ASP.NET Core 应用可配置和启动一个*主机*，负责应用启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="c8c18-164">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="c8c18-165">有关更多信息，请参见<xref:fundamentals/host/index>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-165">For more information, see <xref:fundamentals/host/index>.</span></span>

## <a name="servers"></a><span data-ttu-id="c8c18-166">服务器</span><span class="sxs-lookup"><span data-stu-id="c8c18-166">Servers</span></span>

<span data-ttu-id="c8c18-167">ASP.NET Core 托管模型不直接侦听请求。</span><span class="sxs-lookup"><span data-stu-id="c8c18-167">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="c8c18-168">托管模型依赖 HTTP 服务器实现将请求转发到应用。</span><span class="sxs-lookup"><span data-stu-id="c8c18-168">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="c8c18-169">Windows</span><span class="sxs-lookup"><span data-stu-id="c8c18-169">Windows</span></span>](#tab/windows)

<span data-ttu-id="c8c18-170">ASP.NET Core 提供以下服务器实现：</span><span class="sxs-lookup"><span data-stu-id="c8c18-170">ASP.NET Core provides the following server implementations:</span></span>

* <span data-ttu-id="c8c18-171">[Kestrel](xref:fundamentals/servers/kestrel) 服务器是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-171">[Kestrel](xref:fundamentals/servers/kestrel) server is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-172">Kestrel 通常使用 [IIS](https://www.iis.net/) 在反向代理配置中运行。</span><span class="sxs-lookup"><span data-stu-id="c8c18-172">Kestrel is often run in a reverse proxy configuration using [IIS](https://www.iis.net/).</span></span> <span data-ttu-id="c8c18-173">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-173">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>
* <span data-ttu-id="c8c18-174">IIS HTTP 服务器 (`IISHttpServer`) 是 IIS 的[进程内服务器](xref:fundamentals/servers/index#in-process-hosting-model)。</span><span class="sxs-lookup"><span data-stu-id="c8c18-174">IIS HTTP Server (`IISHttpServer`) is an [in-process server](xref:fundamentals/servers/index#in-process-hosting-model) for IIS.</span></span>
* <span data-ttu-id="c8c18-175">[HTTP.sys](xref:fundamentals/servers/httpsys) 服务器是 Windows 上适用于 ASP.NET Core 的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-175">[HTTP.sys](xref:fundamentals/servers/httpsys) server is a web server for ASP.NET Core on Windows.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="c8c18-176">macOS</span><span class="sxs-lookup"><span data-stu-id="c8c18-176">macOS</span></span>](#tab/macos)

<span data-ttu-id="c8c18-177">ASP.NET Core 使用 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器实现。</span><span class="sxs-lookup"><span data-stu-id="c8c18-177">ASP.NET Core uses the [Kestrel](xref:fundamentals/servers/kestrel) server implementation.</span></span> <span data-ttu-id="c8c18-178">Kestrel 是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-178">Kestrel is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-179">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-179">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="c8c18-180">Linux</span><span class="sxs-lookup"><span data-stu-id="c8c18-180">Linux</span></span>](#tab/linux)

<span data-ttu-id="c8c18-181">ASP.NET Core 使用 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器实现。</span><span class="sxs-lookup"><span data-stu-id="c8c18-181">ASP.NET Core uses the [Kestrel](xref:fundamentals/servers/kestrel) server implementation.</span></span> <span data-ttu-id="c8c18-182">Kestrel 是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-182">Kestrel is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-183">Kestrel 通常使用 [Nginx](http://nginx.org) 或 [Apache](https://httpd.apache.org/) 在反向代理配置中运行。</span><span class="sxs-lookup"><span data-stu-id="c8c18-183">Kestrel is often run in a reverse proxy configuration with [Nginx](http://nginx.org) or [Apache](https://httpd.apache.org/).</span></span> <span data-ttu-id="c8c18-184">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-184">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

---

::: moniker-end

::: moniker range="< aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="c8c18-185">Windows</span><span class="sxs-lookup"><span data-stu-id="c8c18-185">Windows</span></span>](#tab/windows)

<span data-ttu-id="c8c18-186">ASP.NET Core 提供以下服务器实现：</span><span class="sxs-lookup"><span data-stu-id="c8c18-186">ASP.NET Core provides the following server implementations:</span></span>

* <span data-ttu-id="c8c18-187">[Kestrel](xref:fundamentals/servers/kestrel) 服务器是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-187">[Kestrel](xref:fundamentals/servers/kestrel) server is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-188">Kestrel 通常使用 [IIS](https://www.iis.net/) 在反向代理配置中运行。</span><span class="sxs-lookup"><span data-stu-id="c8c18-188">Kestrel is often run in a reverse proxy configuration using [IIS](https://www.iis.net/).</span></span> <span data-ttu-id="c8c18-189">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-189">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>
* <span data-ttu-id="c8c18-190">[HTTP.sys](xref:fundamentals/servers/httpsys) 服务器是 Windows 上适用于 ASP.NET Core 的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-190">[HTTP.sys](xref:fundamentals/servers/httpsys) server is a web server for ASP.NET Core on Windows.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="c8c18-191">macOS</span><span class="sxs-lookup"><span data-stu-id="c8c18-191">macOS</span></span>](#tab/macos)

<span data-ttu-id="c8c18-192">ASP.NET Core 使用 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器实现。</span><span class="sxs-lookup"><span data-stu-id="c8c18-192">ASP.NET Core uses the [Kestrel](xref:fundamentals/servers/kestrel) server implementation.</span></span> <span data-ttu-id="c8c18-193">Kestrel 是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-193">Kestrel is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-194">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-194">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="c8c18-195">Linux</span><span class="sxs-lookup"><span data-stu-id="c8c18-195">Linux</span></span>](#tab/linux)

<span data-ttu-id="c8c18-196">ASP.NET Core 使用 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器实现。</span><span class="sxs-lookup"><span data-stu-id="c8c18-196">ASP.NET Core uses the [Kestrel](xref:fundamentals/servers/kestrel) server implementation.</span></span> <span data-ttu-id="c8c18-197">Kestrel 是跨平台托管 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c8c18-197">Kestrel is a managed, cross-platform web server.</span></span> <span data-ttu-id="c8c18-198">Kestrel 通常使用 [Nginx](http://nginx.org) 或 [Apache](https://httpd.apache.org/) 在反向代理配置中运行。</span><span class="sxs-lookup"><span data-stu-id="c8c18-198">Kestrel is often run in a reverse proxy configuration with [Nginx](http://nginx.org) or [Apache](https://httpd.apache.org/).</span></span> <span data-ttu-id="c8c18-199">在 ASP.NET Core 2.0 或更高版本中，Kestrel 也可作为面向公众的边缘服务器运行，直接向 Internet 公开。</span><span class="sxs-lookup"><span data-stu-id="c8c18-199">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

---

::: moniker-end

<span data-ttu-id="c8c18-200">有关更多信息，请参见<xref:fundamentals/servers/index>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-200">For more information, see <xref:fundamentals/servers/index>.</span></span>

## <a name="configuration"></a><span data-ttu-id="c8c18-201">配置</span><span class="sxs-lookup"><span data-stu-id="c8c18-201">Configuration</span></span>

<span data-ttu-id="c8c18-202">ASP.NET Core 基于名称/值对使用配置模型。</span><span class="sxs-lookup"><span data-stu-id="c8c18-202">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="c8c18-203">配置模型不基于 <xref:System.Configuration> 或 *web.config*。配置从一组有序的配置提供程序获取设置。</span><span class="sxs-lookup"><span data-stu-id="c8c18-203">The configuration model isn't based on <xref:System.Configuration> or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="c8c18-204">内置配置提供程序支持各种文件格式（XML、 JSON、INI）、环境变量和命令行参数。</span><span class="sxs-lookup"><span data-stu-id="c8c18-204">The built-in configuration providers support a variety of file formats (XML, JSON, INI), environment variables, and command-line arguments.</span></span> <span data-ttu-id="c8c18-205">也可以编写你自己的自定义配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8c18-205">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="c8c18-206">有关更多信息，请参见<xref:fundamentals/configuration/index>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-206">For more information, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="logging"></a><span data-ttu-id="c8c18-207">日志记录</span><span class="sxs-lookup"><span data-stu-id="c8c18-207">Logging</span></span>

<span data-ttu-id="c8c18-208">ASP.NET Core 支持适用于各种日志记录提供程序的日志记录 API。</span><span class="sxs-lookup"><span data-stu-id="c8c18-208">ASP.NET Core supports a Logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="c8c18-209">内置提供程序支持向一个或多个目标发送日志。</span><span class="sxs-lookup"><span data-stu-id="c8c18-209">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="c8c18-210">可使用第三方记录框架。</span><span class="sxs-lookup"><span data-stu-id="c8c18-210">Third-party logging frameworks can be used.</span></span>

<span data-ttu-id="c8c18-211">有关更多信息，请参见<xref:fundamentals/logging/index>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-211">For more information, see <xref:fundamentals/logging/index>.</span></span>

## <a name="error-handling"></a><span data-ttu-id="c8c18-212">错误处理</span><span class="sxs-lookup"><span data-stu-id="c8c18-212">Error handling</span></span>

<span data-ttu-id="c8c18-213">ASP.NET Core 的内置方案可处理应用中的错误，包括开发人员异常页、自定义错误页、静态状态代码页和启动异常处理。</span><span class="sxs-lookup"><span data-stu-id="c8c18-213">ASP.NET Core has built-in scenarios for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="c8c18-214">有关更多信息，请参见<xref:fundamentals/error-handling>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-214">For more information, see <xref:fundamentals/error-handling>.</span></span>

## <a name="routing"></a><span data-ttu-id="c8c18-215">路由</span><span class="sxs-lookup"><span data-stu-id="c8c18-215">Routing</span></span>

<span data-ttu-id="c8c18-216">ASP.NET Core 提供将应用请求路由到路由处理程序的方案。</span><span class="sxs-lookup"><span data-stu-id="c8c18-216">ASP.NET Core offers scenarios for routing of app requests to route handlers.</span></span>

<span data-ttu-id="c8c18-217">有关更多信息，请参见<xref:fundamentals/routing>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-217">For more information, see <xref:fundamentals/routing>.</span></span>

## <a name="background-tasks"></a><span data-ttu-id="c8c18-218">后台任务</span><span class="sxs-lookup"><span data-stu-id="c8c18-218">Background tasks</span></span>

<span data-ttu-id="c8c18-219">后台任务作为*托管服务*实现。</span><span class="sxs-lookup"><span data-stu-id="c8c18-219">Background tasks are implemented as *hosted services*.</span></span> <span data-ttu-id="c8c18-220">托管服务是一个类，具有实现 <xref:Microsoft.Extensions.Hosting.IHostedService> 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="c8c18-220">A hosted service is a class with background task logic that implements the <xref:Microsoft.Extensions.Hosting.IHostedService> interface.</span></span>

<span data-ttu-id="c8c18-221">有关更多信息，请参见<xref:fundamentals/host/hosted-services>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-221">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

## <a name="access-httpcontext"></a><span data-ttu-id="c8c18-222">访问 HttpContext</span><span class="sxs-lookup"><span data-stu-id="c8c18-222">Access HttpContext</span></span>

<span data-ttu-id="c8c18-223">用 Razor Pages 和 MVC 处理请求时，`HttpContext` 自动可用。</span><span class="sxs-lookup"><span data-stu-id="c8c18-223">`HttpContext` is automatically available when processing requests with Razor Pages and MVC.</span></span> <span data-ttu-id="c8c18-224">当 `HttpContext` 不可立即使用时，可通过 <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> 接口及其默认实现 <xref:Microsoft.AspNetCore.Http.HttpContextAccessor> 访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="c8c18-224">In circumstances where `HttpContext` isn't readily available, you can access the `HttpContext` through the <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> interface and its default implementation, <xref:Microsoft.AspNetCore.Http.HttpContextAccessor>.</span></span>

<span data-ttu-id="c8c18-225">有关更多信息，请参见<xref:fundamentals/httpcontext>。</span><span class="sxs-lookup"><span data-stu-id="c8c18-225">For more information, see <xref:fundamentals/httpcontext>.</span></span>
