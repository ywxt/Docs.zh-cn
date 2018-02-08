---
title: "ASP.NET Core 中的应用程序启动"
author: ardalis
description: "了解 ASP.NET Core 中的 Startup 类如何配置服务和应用的请求管道。"
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/08/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/startup
ms.openlocfilehash: c324918b33af82b619bb2251f32308e4a57c27e5
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="98823-103">ASP.NET Core 中的应用程序启动</span><span class="sxs-lookup"><span data-stu-id="98823-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="98823-104">作者：[Steve Smith](https://ardalis.com)、[Tom Dykstra](https://github.com/tdykstra) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="98823-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="98823-105">`Startup` 类配置服务和应用的请求管道。</span><span class="sxs-lookup"><span data-stu-id="98823-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="98823-106">Startup 类</span><span class="sxs-lookup"><span data-stu-id="98823-106">The Startup class</span></span>

<span data-ttu-id="98823-107">ASP.NET Core 应用使用 `Startup` 类，按照约定命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="98823-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="98823-108">`Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="98823-108">The `Startup` class:</span></span>

* <span data-ttu-id="98823-109">可选择性地包括 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 方法以配置应用的服务。</span><span class="sxs-lookup"><span data-stu-id="98823-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="98823-110">必须包括 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 方法以创建应用的请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="98823-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="98823-111">当应用启动时，运行时调用 `ConfigureServices` 和 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="98823-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="98823-112">通过 [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions)、[UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 方法指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="98823-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="98823-113">`Startup` 类构造函数接受由主机定义的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="98823-113">The `Startup` class constructor accepts dependencies defined by the host.</span></span> <span data-ttu-id="98823-114">在 `Startup` 类中[注入依赖关系](xref:fundamentals/dependency-injection)的常见用途为注入：</span><span class="sxs-lookup"><span data-stu-id="98823-114">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject:</span></span>

* <span data-ttu-id="98823-115">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) 以按环境配置服务。</span><span class="sxs-lookup"><span data-stu-id="98823-115">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment.</span></span>
* <span data-ttu-id="98823-116">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) 以在启动过程中配置应用。</span><span class="sxs-lookup"><span data-stu-id="98823-116">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) to configure the app during startup.</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="98823-117">注入 `IHostingEnvironment` 的替代方法是使用基于约定的方法。</span><span class="sxs-lookup"><span data-stu-id="98823-117">An alternative to injecting `IHostingEnvironment` is to use a conventions-based approach.</span></span> <span data-ttu-id="98823-118">该应用可以为不同的环境（例如 `StartupDevelopment`）定义单独的 `Startup` 类，并在运行时选择适当的 startup 类。</span><span class="sxs-lookup"><span data-stu-id="98823-118">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate startup class is selected at runtime.</span></span> <span data-ttu-id="98823-119">优先考虑名称后缀与当前环境相匹配的类。</span><span class="sxs-lookup"><span data-stu-id="98823-119">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="98823-120">如果应用在开发环境中运行并包含 `Startup` 类和 `StartupDevelopment` 类，则使用 `StartupDevelopment` 类。</span><span class="sxs-lookup"><span data-stu-id="98823-120">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="98823-121">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments#startup-conventions)。</span><span class="sxs-lookup"><span data-stu-id="98823-121">For more information, see [Working with multiple environments](xref:fundamentals/environments#startup-conventions).</span></span>

<span data-ttu-id="98823-122">若要详细了解 `WebHostBuilder`，请参阅[承载](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="98823-122">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/hosting) topic.</span></span> <span data-ttu-id="98823-123">有关在启动过程中处理错误的信息，请参阅[启动异常处理](xref:fundamentals/error-handling#startup-exception-handling)。</span><span class="sxs-lookup"><span data-stu-id="98823-123">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="98823-124">ConfigureServices 方法</span><span class="sxs-lookup"><span data-stu-id="98823-124">The ConfigureServices method</span></span>

<span data-ttu-id="98823-125">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 方法是：</span><span class="sxs-lookup"><span data-stu-id="98823-125">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="98823-126">可选。</span><span class="sxs-lookup"><span data-stu-id="98823-126">Optional.</span></span>
* <span data-ttu-id="98823-127">在 `Configure` 方法配置应用服务之前，由 Web 主机调用。</span><span class="sxs-lookup"><span data-stu-id="98823-127">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="98823-128">其中按常规设置[配置选项](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="98823-128">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="98823-129">将服务添加到服务容器，使其在应用和 `Configure` 方法中可用。</span><span class="sxs-lookup"><span data-stu-id="98823-129">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="98823-130">这些服务通过[依赖关系注入](xref:fundamentals/dependency-injection)或 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices) 解析。</span><span class="sxs-lookup"><span data-stu-id="98823-130">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="98823-131">Web 主机可能会在调用 `Startup` 方法之前配置某些服务。</span><span class="sxs-lookup"><span data-stu-id="98823-131">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="98823-132">有关详细信息，请参阅[承载](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="98823-132">Details are available in the [Hosting](xref:fundamentals/hosting) topic.</span></span> 

<span data-ttu-id="98823-133">对于需要大量设置的功能，[IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection) 上有 `Add[Service]` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="98823-133">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="98823-134">典型 Web 应用将为实体框架、标识和 MVC 注册服务：</span><span class="sxs-lookup"><span data-stu-id="98823-134">A typical web app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="services-available-in-startup"></a><span data-ttu-id="98823-135">Startup 中可用的服务</span><span class="sxs-lookup"><span data-stu-id="98823-135">Services available in Startup</span></span>

<span data-ttu-id="98823-136">Web 主机提供 `Startup` 类构造函数可用的某些服务。</span><span class="sxs-lookup"><span data-stu-id="98823-136">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="98823-137">应用通过 `ConfigureServices` 添加其他服务。</span><span class="sxs-lookup"><span data-stu-id="98823-137">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="98823-138">然后，主机和应用服务都可以在 `Configure` 和整个应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="98823-138">Both the host and app services are then available in `Configure` and throughout the application.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="98823-139">Configure 方法</span><span class="sxs-lookup"><span data-stu-id="98823-139">The Configure method</span></span>

<span data-ttu-id="98823-140">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 方法用于指定应用响应 HTTP 请求的方式。</span><span class="sxs-lookup"><span data-stu-id="98823-140">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="98823-141">可通过将[中间件](xref:fundamentals/middleware/index)组件添加到 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 实例来配置请求管道。</span><span class="sxs-lookup"><span data-stu-id="98823-141">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware/index) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="98823-142">`Configure` 方法可使用 `IApplicationBuilder`，但未在服务容器中注册。</span><span class="sxs-lookup"><span data-stu-id="98823-142">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="98823-143">承载创建 `IApplicationBuilder` 并将其直接传递给 `Configure`（[引用源](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)）。</span><span class="sxs-lookup"><span data-stu-id="98823-143">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure` ([reference source](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span></span>

<span data-ttu-id="98823-144">[ASP.NET Core 模板](/dotnet/core/tools/dotnet-new)配置支持开发人员异常页、[BrowserLink](http://vswebessentials.com/features/browserlink)、错误页、静态文件和 ASP.NET MVC 的管道：</span><span class="sxs-lookup"><span data-stu-id="98823-144">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="98823-145">每个 `Use` 扩展方法将中间件组件添加到请求管道。</span><span class="sxs-lookup"><span data-stu-id="98823-145">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="98823-146">例如，`UseMvc` 扩展方法将[路由中间件](xref:fundamentals/routing)添加到请求管道，并将 [MVC](xref:mvc/overview) 配置为默认设置。</span><span class="sxs-lookup"><span data-stu-id="98823-146">For instance, the `UseMvc` extension method adds the [routing middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="98823-147">其他服务（如 `IHostingEnvironment` 和 `ILoggerFactory`），也可以在方法签名中指定。</span><span class="sxs-lookup"><span data-stu-id="98823-147">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="98823-148">如果指定，其他服务如果可用，将被注入。</span><span class="sxs-lookup"><span data-stu-id="98823-148">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="98823-149">有关如何使用 `IApplicationBuilder` 的详细信息，请参阅[中间件](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="98823-149">For more information on how to use `IApplicationBuilder`, see [Middleware](xref:fundamentals/middleware/index).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="98823-150">便利方法</span><span class="sxs-lookup"><span data-stu-id="98823-150">Convenience methods</span></span>

<span data-ttu-id="98823-151">可使用 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 和 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 便利方法，而不是指定 `Startup` 类。</span><span class="sxs-lookup"><span data-stu-id="98823-151">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="98823-152">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="98823-152">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="98823-153">多次调用 `Configure` 将使用上一个方法调用。</span><span class="sxs-lookup"><span data-stu-id="98823-153">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[Main](startup/snapshot_sample/Program.cs?highlight=18,22)]

## <a name="startup-filters"></a><span data-ttu-id="98823-154">Startup 筛选器</span><span class="sxs-lookup"><span data-stu-id="98823-154">Startup filters</span></span>

<span data-ttu-id="98823-155">在应用的 [Configure](#the-configure-method) 中间件管道的开头或末尾使用 [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) 来配置中间件。</span><span class="sxs-lookup"><span data-stu-id="98823-155">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="98823-156">`IStartupFilter` 有助于确保中间件在应用请求处理管道的开始或结束时由库添加的中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="98823-156">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="98823-157">`IStartupFilter` 实现单个方法（即 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)），该方法接收并返回 `Action<IApplicationBuilder>`。</span><span class="sxs-lookup"><span data-stu-id="98823-157">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="98823-158">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 定义用于配置应用请求管道的类。</span><span class="sxs-lookup"><span data-stu-id="98823-158">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="98823-159">有关详细信息，请参阅[使用 IApplicationBuilder 创建中间件管道](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)。</span><span class="sxs-lookup"><span data-stu-id="98823-159">For more information, see [Creating a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="98823-160">在请求管道中，每个 `IStartupFilter` 实现一个或多个中间件。</span><span class="sxs-lookup"><span data-stu-id="98823-160">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="98823-161">筛选器按照添加到服务容器的顺序调用。</span><span class="sxs-lookup"><span data-stu-id="98823-161">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="98823-162">筛选器可在将控件传递给下一个筛选器之前或之后添加中间件，从而附加到应用管道的开头或末尾。</span><span class="sxs-lookup"><span data-stu-id="98823-162">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="98823-163">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）演示如何向 `IStartupFilter` 注册中间件。</span><span class="sxs-lookup"><span data-stu-id="98823-163">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="98823-164">示例应用包含一个中间件，该中间件从查询字符串参数中设置选项值：</span><span class="sxs-lookup"><span data-stu-id="98823-164">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="98823-165">在 `RequestSetOptionsStartupFilter` 类中配置 `RequestSetOptionsMiddleware`：</span><span class="sxs-lookup"><span data-stu-id="98823-165">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="98823-166">在 `ConfigureServices` 的服务容器中注册 `IStartupFilter`：</span><span class="sxs-lookup"><span data-stu-id="98823-166">The `IStartupFilter` is registered in the service container in `ConfigureServices`:</span></span>

[!code-csharp[Main](startup/sample/Startup.cs?name=snippet1&highlight=3)]

<span data-ttu-id="98823-167">当提供 `option` 的查询字符串参数时，中间件在 MVC 中间件呈现响应之前处理分配值：</span><span class="sxs-lookup"><span data-stu-id="98823-167">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![浏览器窗口显示已呈现的索引页。](startup/_static/index.png)

<span data-ttu-id="98823-170">中间件执行顺序由 `IStartupFilter` 注册顺序设置：</span><span class="sxs-lookup"><span data-stu-id="98823-170">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="98823-171">多个 `IStartupFilter` 实现可能与相同的对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="98823-171">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="98823-172">如果顺序很重要，请将它们的 `IStartupFilter` 服务注册进行排序，以匹配其中间件应有的运行顺序。</span><span class="sxs-lookup"><span data-stu-id="98823-172">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="98823-173">库可能添加包含一个或多个 `IStartupFilter` 实现的中间件，这些实现在向 `IStartupFilter` 注册的其他应用中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="98823-173">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="98823-174">若要在库的 `IStartupFilter` 添加中间件之前调用 `IStartupFilter` 中间件，请在将库添加到服务容器之前定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="98823-174">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="98823-175">若要在此后调用，请在添加库之后定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="98823-175">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98823-176">其他资源</span><span class="sxs-lookup"><span data-stu-id="98823-176">Additional resources</span></span>

* [<span data-ttu-id="98823-177">承载</span><span class="sxs-lookup"><span data-stu-id="98823-177">Hosting</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="98823-178">使用多个环境</span><span class="sxs-lookup"><span data-stu-id="98823-178">Working with Multiple Environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="98823-179">中间件</span><span class="sxs-lookup"><span data-stu-id="98823-179">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="98823-180">日志记录</span><span class="sxs-lookup"><span data-stu-id="98823-180">Logging</span></span>](xref:fundamentals/logging/index)
* [<span data-ttu-id="98823-181">配置</span><span class="sxs-lookup"><span data-stu-id="98823-181">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="98823-182">StartupLoader 类：FindStartupType 方法（引用源）</span><span class="sxs-lookup"><span data-stu-id="98823-182">StartupLoader class: FindStartupType method (reference source)</span></span>](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
