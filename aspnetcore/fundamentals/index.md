---
title: "ASP.NET Core 基础知识"
author: rick-anderson
description: "了解生成 ASP.NET Core 应用程序的基础概念。"
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 09/30/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: fundamentals/index
ms.openlocfilehash: 85d3eaf033eafbd24c71110ccd7f21ffcc8b0c82
ms.sourcegitcommit: 9f758b1550fcae88ab1eb284798a89e6320548a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="fd75f-103">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="fd75f-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="fd75f-104">ASP.NET Core 应用程序是在其 `Main` 方法中创建 Web 服务器的控制台应用：</span><span class="sxs-lookup"><span data-stu-id="fd75f-104">An ASP.NET Core application is a console app that creates a web server in its `Main` method:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fd75f-105">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fd75f-105">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

<span data-ttu-id="fd75f-106">`Main` 方法调用 `WebHost.CreateDefaultBuilder`，后者按照生成器模式来创建 Web 应用程序主机。</span><span class="sxs-lookup"><span data-stu-id="fd75f-106">The `Main` method invokes `WebHost.CreateDefaultBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="fd75f-107">生成器提供定义 Web 服务器（例如，`UseKestrel`）和启动类 (`UseStartup`) 的方法。</span><span class="sxs-lookup"><span data-stu-id="fd75f-107">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="fd75f-108">在前面的例子中，自动分配了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="fd75f-108">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="fd75f-109">ASP.NET Core 的 Web 主机尝试在 IIS 上运行（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="fd75f-109">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="fd75f-110">对于其他 Web 服务器（如 [HTTP.sys](xref:fundamentals/servers/httpsys)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="fd75f-110">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="fd75f-111">在下一节对 `UseStartup` 进行了更深入的介绍。</span><span class="sxs-lookup"><span data-stu-id="fd75f-111">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="fd75f-112">`IWebHostBuilder` 是 `WebHost.CreateDefaultBuilder` 调用的返回类型，它提供了许多可选方法。</span><span class="sxs-lookup"><span data-stu-id="fd75f-112">`IWebHostBuilder`, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="fd75f-113">其中的一些方法包括用于在 HTTP.sys 中托管应用的 `UseHttpSys`，以及用于指定根内容目录的 `UseContentRoot`。</span><span class="sxs-lookup"><span data-stu-id="fd75f-113">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="fd75f-114">`Build` 和 `Run` 方法生成 `IWebHost` 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="fd75f-114">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fd75f-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fd75f-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs)]

<span data-ttu-id="fd75f-116">`Main` 方法使用 `WebHostBuilder`，后者按照生成器模式来创建 Web 应用程序主机。</span><span class="sxs-lookup"><span data-stu-id="fd75f-116">The `Main` method uses `WebHostBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="fd75f-117">生成器提供定义 Web 服务器（例如，`UseKestrel`）和启动类 (`UseStartup`) 的方法。</span><span class="sxs-lookup"><span data-stu-id="fd75f-117">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="fd75f-118">在前面的示例中，使用了 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="fd75f-118">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="fd75f-119">对于其他 Web 服务器（如 [WebListener](xref:fundamentals/servers/weblistener)），可通过调用相应的扩展方法来使用。</span><span class="sxs-lookup"><span data-stu-id="fd75f-119">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="fd75f-120">在下一节对 `UseStartup` 进行了更深入的介绍。</span><span class="sxs-lookup"><span data-stu-id="fd75f-120">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="fd75f-121">`WebHostBuilder` 提供了许多可选方法，其中包括用于在 IIS 和 IIS Express 中进行托管的 `UseIISIntegration`，以及用于指定根内容目录的 `UseContentRoot`。</span><span class="sxs-lookup"><span data-stu-id="fd75f-121">`WebHostBuilder` provides many optional methods, including `UseIISIntegration` for hosting in IIS and IIS Express and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="fd75f-122">`Build` 和 `Run` 方法生成 `IWebHost` 对象，该对象托管应用并开始侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="fd75f-122">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

---

## <a name="startup"></a><span data-ttu-id="fd75f-123">启动</span><span class="sxs-lookup"><span data-stu-id="fd75f-123">Startup</span></span>

<span data-ttu-id="fd75f-124">`WebHostBuilder` 上的 `UseStartup` 方法为你的应用指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="fd75f-124">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fd75f-125">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fd75f-125">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fd75f-126">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fd75f-126">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

---

<span data-ttu-id="fd75f-127">`Startup` 类用于定义请求处理管道和配置应用所需的任何服务。</span><span class="sxs-lookup"><span data-stu-id="fd75f-127">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="fd75f-128">`Startup` 必须是公共类，并包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="fd75f-128">The `Startup` class must be public and contain the following methods:</span></span>

```csharp
public class Startup
{
    // This method gets called by the runtime. Use this method
    // to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // This method gets called by the runtime. Use this method
    // to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

<span data-ttu-id="fd75f-129">`ConfigureServices` 定义应用所使用的[服务](#dependency-injection-services)（如 ASP.NET Core MVC、Entity Framework Core 和标识）。</span><span class="sxs-lookup"><span data-stu-id="fd75f-129">`ConfigureServices` defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="fd75f-130">`Configure` 定义请求管道的[中间件](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-130">`Configure` defines the [middleware](xref:fundamentals/middleware/index) for the request pipeline.</span></span>

<span data-ttu-id="fd75f-131">有关详细信息，请参阅[应用程序启动](xref:fundamentals/startup)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-131">For more information, see [Application startup](xref:fundamentals/startup).</span></span>

## <a name="content-root"></a><span data-ttu-id="fd75f-132">内容根</span><span class="sxs-lookup"><span data-stu-id="fd75f-132">Content root</span></span>

<span data-ttu-id="fd75f-133">内容根是应用所使用的任何内容的基路径，如视图、[Razor 页面](xref:mvc/razor-pages/index) 和静态资产。</span><span class="sxs-lookup"><span data-stu-id="fd75f-133">The content root is the base path to any content used by the app, such as views, [Razor Pages](xref:mvc/razor-pages/index), and static assets.</span></span> <span data-ttu-id="fd75f-134">默认情况下，内容根与用于托管应用的可执行文件的应用程序基路径相同。</span><span class="sxs-lookup"><span data-stu-id="fd75f-134">By default, the content root is the same as application base path for the executable hosting the app.</span></span>

## <a name="web-root"></a><span data-ttu-id="fd75f-135">Web 根</span><span class="sxs-lookup"><span data-stu-id="fd75f-135">Web root</span></span>

<span data-ttu-id="fd75f-136">应用的 Web 根是项目中的目录，其中包含公共资源、CSS 等静态资源、JavaScript 和图形文件。</span><span class="sxs-lookup"><span data-stu-id="fd75f-136">The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="fd75f-137">依赖关系注入（服务）</span><span class="sxs-lookup"><span data-stu-id="fd75f-137">Dependency Injection (Services)</span></span>

<span data-ttu-id="fd75f-138">服务是应用中常用的组件。</span><span class="sxs-lookup"><span data-stu-id="fd75f-138">A service is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="fd75f-139">可以通过[依存关系注入 (DI)](xref:fundamentals/dependency-injection) 来获取服务。</span><span class="sxs-lookup"><span data-stu-id="fd75f-139">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="fd75f-140">ASP.NET Core 包括默认支持[构造函数注入](xref:mvc/controllers/dependency-injection#constructor-injection)的本机控制反转 (IoC) 容器。</span><span class="sxs-lookup"><span data-stu-id="fd75f-140">ASP.NET Core includes a native **I**nversion **o**f **C**ontrol (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="fd75f-141">可根据需要替换默认本机容器。</span><span class="sxs-lookup"><span data-stu-id="fd75f-141">You can replace the default native container if you wish.</span></span> <span data-ttu-id="fd75f-142">DI 除了具备松散耦合优势以外，还可以使服务（例如，[日志记录](xref:fundamentals/logging/index)）在整个应用中可用。</span><span class="sxs-lookup"><span data-stu-id="fd75f-142">In addition to its loose coupling benefit, DI makes services available throughout your app (for example, [logging](xref:fundamentals/logging/index)).</span></span>

<span data-ttu-id="fd75f-143">有关详细信息，请参阅[依存关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-143">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="fd75f-144">中间件</span><span class="sxs-lookup"><span data-stu-id="fd75f-144">Middleware</span></span>

<span data-ttu-id="fd75f-145">在 ASP.NET Core 中，使用[中间件](xref:fundamentals/middleware/index)来撰写请求管道。</span><span class="sxs-lookup"><span data-stu-id="fd75f-145">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware/index).</span></span> <span data-ttu-id="fd75f-146">ASP.NET Core 中间件在 `HttpContext` 上执行异步逻辑，然后调用序列中的下一个中间件或直接终止请求。</span><span class="sxs-lookup"><span data-stu-id="fd75f-146">ASP.NET Core middleware performs asynchronous logic on an `HttpContext` and then either invokes the next middleware in the sequence or terminates the request directly.</span></span> <span data-ttu-id="fd75f-147">通过在 `Configure` 方法中调用 `UseXYZ` 扩展方法来添加名为“XYZ”的中间件组件。</span><span class="sxs-lookup"><span data-stu-id="fd75f-147">A middleware component called "XYZ" is added by invoking an `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="fd75f-148">ASP.NET Core 包含一组丰富的内置中间件：</span><span class="sxs-lookup"><span data-stu-id="fd75f-148">ASP.NET Core includes a rich set of built-in middleware:</span></span>

* [<span data-ttu-id="fd75f-149">静态文件</span><span class="sxs-lookup"><span data-stu-id="fd75f-149">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="fd75f-150">路由</span><span class="sxs-lookup"><span data-stu-id="fd75f-150">Routing</span></span>](xref:fundamentals/routing)
* [<span data-ttu-id="fd75f-151">身份验证</span><span class="sxs-lookup"><span data-stu-id="fd75f-151">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="fd75f-152">响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="fd75f-152">Response Compression Middleware</span></span>](xref:performance/response-compression)
* [<span data-ttu-id="fd75f-153">URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="fd75f-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)

<span data-ttu-id="fd75f-154">可以将任何基于 [OWIN](http://owin.org) 的中间件与 ASP.NET Core 应用结合使用，也可以编写自己的自定义中间件。</span><span class="sxs-lookup"><span data-stu-id="fd75f-154">[OWIN](http://owin.org)-based middleware is available for ASP.NET Core apps, and you can write your own custom middleware.</span></span>

<span data-ttu-id="fd75f-155">有关详细信息，请参阅[中间件](xref:fundamentals/middleware/index)和 [.NET 的开放 Web 接口 (OWIN)](xref:fundamentals/owin)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-155">For more information, see [Middleware](xref:fundamentals/middleware/index) and [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="environments"></a><span data-ttu-id="fd75f-156">环境</span><span class="sxs-lookup"><span data-stu-id="fd75f-156">Environments</span></span>

<span data-ttu-id="fd75f-157">环境（如“开发”环境和“生产”环境）是 ASP.NET Core 的高级概念，可使用环境变量进行设置。</span><span class="sxs-lookup"><span data-stu-id="fd75f-157">Environments, such as "Development" and "Production", are a first-class notion in ASP.NET Core and can be set using environment variables.</span></span>

<span data-ttu-id="fd75f-158">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-158">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="configuration"></a><span data-ttu-id="fd75f-159">配置</span><span class="sxs-lookup"><span data-stu-id="fd75f-159">Configuration</span></span>

<span data-ttu-id="fd75f-160">ASP.NET Core 基于名称/值对使用配置模型。</span><span class="sxs-lookup"><span data-stu-id="fd75f-160">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="fd75f-161">配置模型不基于 `System.Configuration` 或 *web.config*。配置从一组有序的配置提供程序获取设置。</span><span class="sxs-lookup"><span data-stu-id="fd75f-161">The configuration model isn't based on `System.Configuration` or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="fd75f-162">内置配置提供程序支持各种文件格式（XML、 JSON、INI）和环境变量，从而实现基于环境的配置。</span><span class="sxs-lookup"><span data-stu-id="fd75f-162">The built-in configuration providers support a variety of file formats (XML, JSON, INI) and environment variables to enable environment-based configuration.</span></span> <span data-ttu-id="fd75f-163">也可以编写你自己的自定义配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="fd75f-163">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="fd75f-164">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-164">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="logging"></a><span data-ttu-id="fd75f-165">日志记录</span><span class="sxs-lookup"><span data-stu-id="fd75f-165">Logging</span></span>

<span data-ttu-id="fd75f-166">ASP.NET Core 支持适用于各种日志记录提供程序的日志记录 API。</span><span class="sxs-lookup"><span data-stu-id="fd75f-166">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="fd75f-167">内置提供程序支持向一个或多个目标发送日志。</span><span class="sxs-lookup"><span data-stu-id="fd75f-167">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="fd75f-168">可使用第三方记录框架。</span><span class="sxs-lookup"><span data-stu-id="fd75f-168">Third-party logging frameworks can be used.</span></span>

[<span data-ttu-id="fd75f-169">日志记录</span><span class="sxs-lookup"><span data-stu-id="fd75f-169">Logging</span></span>](xref:fundamentals/logging/index)

## <a name="error-handling"></a><span data-ttu-id="fd75f-170">错误处理</span><span class="sxs-lookup"><span data-stu-id="fd75f-170">Error handling</span></span>

<span data-ttu-id="fd75f-171">ASP.NET Core 的内置功能可处理应用中的错误，包括开发人员异常页、自定义错误页、静态状态代码页和启动异常处理。</span><span class="sxs-lookup"><span data-stu-id="fd75f-171">ASP.NET Core has built-in features for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="fd75f-172">有关详细信息，请参阅[错误处理](xref:fundamentals/error-handling)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-172">For more information, see [Error Handling](xref:fundamentals/error-handling).</span></span>

## <a name="routing"></a><span data-ttu-id="fd75f-173">路由</span><span class="sxs-lookup"><span data-stu-id="fd75f-173">Routing</span></span>

<span data-ttu-id="fd75f-174">ASP.NET Core 提供将应用请求路由到路由处理程序的功能。</span><span class="sxs-lookup"><span data-stu-id="fd75f-174">ASP.NET Core offers features for routing of app requests to route handlers.</span></span>

<span data-ttu-id="fd75f-175">有关详细信息，请参阅[路由](xref:fundamentals/routing)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-175">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="file-providers"></a><span data-ttu-id="fd75f-176">文件提供程序</span><span class="sxs-lookup"><span data-stu-id="fd75f-176">File providers</span></span>

<span data-ttu-id="fd75f-177">ASP.NET Core 通过使用文件提供程序抽象化文件系统访问，文件提供程序可提供一个跨平台处理文件的通用界面。</span><span class="sxs-lookup"><span data-stu-id="fd75f-177">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="fd75f-178">有关详细信息，请参阅[文件提供程序](xref:fundamentals/file-providers)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-178">For more information, see [File Providers](xref:fundamentals/file-providers).</span></span>

## <a name="static-files"></a><span data-ttu-id="fd75f-179">静态文件</span><span class="sxs-lookup"><span data-stu-id="fd75f-179">Static files</span></span>

<span data-ttu-id="fd75f-180">静态文件中间件为静态文件（如 HTML、CSS、映像和 JavaScript）提供服务。</span><span class="sxs-lookup"><span data-stu-id="fd75f-180">Static files middleware serves static files, such as HTML, CSS, image, and JavaScript.</span></span>

<span data-ttu-id="fd75f-181">有关详细信息，请参阅[使用静态文件](xref:fundamentals/static-files)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-181">For more information, see [Working with static files](xref:fundamentals/static-files).</span></span>

## <a name="hosting"></a><span data-ttu-id="fd75f-182">宿主</span><span class="sxs-lookup"><span data-stu-id="fd75f-182">Hosting</span></span>

<span data-ttu-id="fd75f-183">ASP.NET Core 应用可配置和启动一个*主机*，负责应用启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="fd75f-183">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="fd75f-184">有关详细信息，请参阅[托管](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-184">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

## <a name="session-and-application-state"></a><span data-ttu-id="fd75f-185">会话和应用程序状态</span><span class="sxs-lookup"><span data-stu-id="fd75f-185">Session and application state</span></span>

<span data-ttu-id="fd75f-186">会话状态是 ASP.NET Core 中的一项功能，可用于在用户浏览 Web 应用时保存和存储用户数据。</span><span class="sxs-lookup"><span data-stu-id="fd75f-186">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span>

<span data-ttu-id="fd75f-187">有关详细信息，请参阅[会话和应用程序状态](xref:fundamentals/app-state)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-187">For more information, see [Session and application state](xref:fundamentals/app-state).</span></span>

## <a name="servers"></a><span data-ttu-id="fd75f-188">服务器</span><span class="sxs-lookup"><span data-stu-id="fd75f-188">Servers</span></span>

<span data-ttu-id="fd75f-189">ASP.NET Core 托管模型不直接侦听请求。</span><span class="sxs-lookup"><span data-stu-id="fd75f-189">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="fd75f-190">托管模型依赖 HTTP 服务器实现将请求转发到应用。</span><span class="sxs-lookup"><span data-stu-id="fd75f-190">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="fd75f-191">转发的请求被打包为一组可通过接口进行访问的功能对象。</span><span class="sxs-lookup"><span data-stu-id="fd75f-191">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="fd75f-192">ASP.NET Core 包含托管的跨平台 Web 服务器，名为 [Kestrel](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-192">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="fd75f-193">Kestrel 通常在生产 Web 服务器（如 [IIS](https://www.iis.net/) 或 [Nginx](http://nginx.org)）后台运行。</span><span class="sxs-lookup"><span data-stu-id="fd75f-193">Kestrel is often run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org).</span></span> <span data-ttu-id="fd75f-194">Kestrel 可作为边缘服务器运行。</span><span class="sxs-lookup"><span data-stu-id="fd75f-194">Kestrel can be run as an edge server.</span></span>

<span data-ttu-id="fd75f-195">有关详细信息，请参阅[服务器](xref:fundamentals/servers/index)和下列主题：</span><span class="sxs-lookup"><span data-stu-id="fd75f-195">For more information, see [Servers](xref:fundamentals/servers/index) and the following topics:</span></span>

* [<span data-ttu-id="fd75f-196">Kestrel</span><span class="sxs-lookup"><span data-stu-id="fd75f-196">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="fd75f-197">ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="fd75f-197">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* <span data-ttu-id="fd75f-198">[HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）</span><span class="sxs-lookup"><span data-stu-id="fd75f-198">[HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="fd75f-199">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="fd75f-199">Globalization and localization</span></span>

<span data-ttu-id="fd75f-200">使用 ASP.NET Core 创建多语言网站，可让网站拥有更多受众。</span><span class="sxs-lookup"><span data-stu-id="fd75f-200">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="fd75f-201">ASP.NET Core 提供的服务和中间件可将网站本地化为不同的语言和文化。</span><span class="sxs-lookup"><span data-stu-id="fd75f-201">ASP.NET Core provides services and middleware for localizing into different languages and cultures.</span></span>

<span data-ttu-id="fd75f-202">有关详细信息，请参阅[全球化和本地化](xref:fundamentals/localization)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-202">For more information, see [Globalization and localization](xref:fundamentals/localization).</span></span>

## <a name="request-features"></a><span data-ttu-id="fd75f-203">请求功能</span><span class="sxs-lookup"><span data-stu-id="fd75f-203">Request features</span></span>

<span data-ttu-id="fd75f-204">与 HTTP 请求和响应相关的 Web 服务器实现详细信息在接口中定义。</span><span class="sxs-lookup"><span data-stu-id="fd75f-204">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="fd75f-205">服务器实现和中间件使用这些接口来创建和修改应用的托管管道。</span><span class="sxs-lookup"><span data-stu-id="fd75f-205">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="fd75f-206">有关详细信息，请参阅[请求功能](xref:fundamentals/request-features)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-206">For more information, see [Request Features](xref:fundamentals/request-features).</span></span>

## <a name="background-tasks"></a><span data-ttu-id="fd75f-207">后台任务</span><span class="sxs-lookup"><span data-stu-id="fd75f-207">Background tasks</span></span>

<span data-ttu-id="fd75f-208">后台任务作为*托管服务*实现。</span><span class="sxs-lookup"><span data-stu-id="fd75f-208">Background tasks are implemented as *hosted services*.</span></span> <span data-ttu-id="fd75f-209">托管服务是一个类，具有实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="fd75f-209">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span>

<span data-ttu-id="fd75f-210">有关详细信息，请参阅[使用托管服务的后台任务](xref:fundamentals/hosted-services)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-210">For more information, see [Background tasks with hosted services](xref:fundamentals/hosted-services).</span></span>

## <a name="open-web-interface-for-net-owin"></a><span data-ttu-id="fd75f-211">.NET 的开放 Web 接口 (OWIN)</span><span class="sxs-lookup"><span data-stu-id="fd75f-211">Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="fd75f-212">ASP.NET Core 支持 .NET 的开放 Web 接口 (OWIN)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-212">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="fd75f-213">OWIN 允许 Web 应用从 Web 服务器分离。</span><span class="sxs-lookup"><span data-stu-id="fd75f-213">OWIN allows web apps to be decoupled from web servers.</span></span>

<span data-ttu-id="fd75f-214">有关详细信息，请参阅 [.NET 的开放 Web 接口 (OWIN)](xref:fundamentals/owin)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-214">For more information, see [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="websockets"></a><span data-ttu-id="fd75f-215">WebSockets</span><span class="sxs-lookup"><span data-stu-id="fd75f-215">WebSockets</span></span>

<span data-ttu-id="fd75f-216">[WebSocket](https://wikipedia.org/wiki/WebSocket) 是一个协议，支持通过 TCP 连接建立持久的双向信道。</span><span class="sxs-lookup"><span data-stu-id="fd75f-216">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="fd75f-217">它可用于聊天、股票报价和游戏等应用，以及 Web 应用中需要实时功能的任何位置。</span><span class="sxs-lookup"><span data-stu-id="fd75f-217">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="fd75f-218">ASP.NET Core 支持 Web 套接字功能。</span><span class="sxs-lookup"><span data-stu-id="fd75f-218">ASP.NET Core supports web socket features.</span></span>

<span data-ttu-id="fd75f-219">有关详细信息，请参阅 [WebSockets](xref:fundamentals/websockets)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-219">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="fd75f-220">Microsoft.AspNetCore.All 元包</span><span class="sxs-lookup"><span data-stu-id="fd75f-220">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="fd75f-221">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="fd75f-221">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="fd75f-222">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="fd75f-222">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="fd75f-223">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="fd75f-223">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="fd75f-224">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="fd75f-224">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="fd75f-225">有关详细信息，请参阅 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-225">For more information, see [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="fd75f-226">.NET Core 与 .NET Framework 运行时</span><span class="sxs-lookup"><span data-stu-id="fd75f-226">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="fd75f-227">ASP.NET Core 应用可以面向 .NET Core 或 .NET Framework 运行时。</span><span class="sxs-lookup"><span data-stu-id="fd75f-227">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="fd75f-228">有关详细信息，请参阅[在 .NET Core 和 .NET Framework 之间进行选择](/dotnet/articles/standard/choosing-core-framework-server)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-228">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="fd75f-229">在 ASP.NET Core 和 ASP.NET 之间进行选择</span><span class="sxs-lookup"><span data-stu-id="fd75f-229">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="fd75f-230">有关在 ASP.NET Core 和 ASP.NET 之间进行选择的详细信息，请参阅 [在 ASP.NET Core 和 ASP.NET 之间进行选择](xref:fundamentals/choose-between-aspnet-and-aspnetcore)。</span><span class="sxs-lookup"><span data-stu-id="fd75f-230">For more information on choosing between ASP.NET Core and ASP.NET, see [Choose between ASP.NET Core and ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span></span>
