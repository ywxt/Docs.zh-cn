---
title: "在 ASP.NET Core 中的应用程序启动"
author: ardalis
description: "发现服务和应用程序的请求管道 Startup 类在 ASP.NET 核心中的配置的方式。"
ms.author: tdykstra
manager: wpickett
ms.custom: mvc
ms.date: 12/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/startup
ms.openlocfilehash: dd2eb3d3996bc0bf277c8d5e772c8568ef9f147e
ms.sourcegitcommit: f5a7f0198628f0d152257d90dba6c3a0747a355a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2017
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="7d806-103">在 ASP.NET Core 中的应用程序启动</span><span class="sxs-lookup"><span data-stu-id="7d806-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="7d806-104">通过[Steve Smith](https://ardalis.com)， [Tom Dykstra](https://github.com/tdykstra)，和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="7d806-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="7d806-105">`Startup`类配置服务和应用程序的请求管道。</span><span class="sxs-lookup"><span data-stu-id="7d806-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="7d806-106">Startup 类</span><span class="sxs-lookup"><span data-stu-id="7d806-106">The Startup class</span></span>

<span data-ttu-id="7d806-107">ASP.NET Core 应用使用`Startup`类，该类名为`Startup`按照约定。</span><span class="sxs-lookup"><span data-stu-id="7d806-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="7d806-108">`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="7d806-108">The `Startup` class:</span></span>

* <span data-ttu-id="7d806-109">可以选择性地包含[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices)方法来配置应用程序的服务。</span><span class="sxs-lookup"><span data-stu-id="7d806-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="7d806-110">必须包括[配置](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure)方法来创建应用程序的请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="7d806-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="7d806-111">`ConfigureServices`和`Configure`时启动该应用程序运行时调用：</span><span class="sxs-lookup"><span data-stu-id="7d806-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="7d806-112">指定`Startup`类，该类具有[WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt; ](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)方法：</span><span class="sxs-lookup"><span data-stu-id="7d806-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="7d806-113">`Startup`类构造函数接受由主机定义的依赖项。</span><span class="sxs-lookup"><span data-stu-id="7d806-113">The `Startup` class constructor accepts dependencies defined by the host.</span></span> <span data-ttu-id="7d806-114">一个常见用途[依赖关系注入](xref:fundamentals/dependency-injection)到`Startup`类是将注入[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment)由环境中配置服务：</span><span class="sxs-lookup"><span data-stu-id="7d806-114">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment:</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="7d806-115">将注入的替代方法`IHostingStartup`是使用基于约定的方法。</span><span class="sxs-lookup"><span data-stu-id="7d806-115">An alternative to injecting `IHostingStartup` is to use a conventions-based approach.</span></span> <span data-ttu-id="7d806-116">应用程序可以定义单独`Startup`用于不同的环境的类 (例如， `StartupDevelopment`)，并且在运行时选择了适当的 startup 类。</span><span class="sxs-lookup"><span data-stu-id="7d806-116">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate startup class is selected at runtime.</span></span> <span data-ttu-id="7d806-117">其名称后缀与当前的环境匹配的类进行优先级排序。</span><span class="sxs-lookup"><span data-stu-id="7d806-117">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="7d806-118">如果应用程序在开发环境中运行，并且同时包含`Startup`类和一个`StartupDevelopment`类，`StartupDevelopment`使用类。</span><span class="sxs-lookup"><span data-stu-id="7d806-118">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="7d806-119">有关详细信息请参阅[使用多个环境](xref:fundamentals/environments#startup-conventions)。</span><span class="sxs-lookup"><span data-stu-id="7d806-119">For more information see [Working with multiple environments](xref:fundamentals/environments#startup-conventions).</span></span>

<span data-ttu-id="7d806-120">若要详细了解`WebHostBuilder`，请参阅[宿主](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="7d806-120">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/hosting) topic.</span></span> <span data-ttu-id="7d806-121">有关在启动过程中处理错误的信息，请参阅[启动异常处理](xref:fundamentals/error-handling#startup-exception-handling)。</span><span class="sxs-lookup"><span data-stu-id="7d806-121">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="7d806-122">ConfigureServices 方法</span><span class="sxs-lookup"><span data-stu-id="7d806-122">The ConfigureServices method</span></span>

<span data-ttu-id="7d806-123">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices)方法是：</span><span class="sxs-lookup"><span data-stu-id="7d806-123">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="7d806-124">可选。</span><span class="sxs-lookup"><span data-stu-id="7d806-124">Optional.</span></span>
* <span data-ttu-id="7d806-125">Web 宿主之前调用`Configure`方法来配置应用程序的服务。</span><span class="sxs-lookup"><span data-stu-id="7d806-125">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="7d806-126">其中[配置选项](xref:fundamentals/configuration/index)设置的约定。</span><span class="sxs-lookup"><span data-stu-id="7d806-126">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="7d806-127">将服务添加到服务容器使它们可在应用内和在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="7d806-127">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="7d806-128">服务是通过解析[依赖关系注入](xref:fundamentals/dependency-injection)或从[IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)。</span><span class="sxs-lookup"><span data-stu-id="7d806-128">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="7d806-129">Web 主机可以配置某些服务之前`Startup`调用方法。</span><span class="sxs-lookup"><span data-stu-id="7d806-129">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="7d806-130">中提供了详细信息[宿主](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="7d806-130">Details are available in the [Hosting](xref:fundamentals/hosting) topic.</span></span> 

<span data-ttu-id="7d806-131">对于需要大量的安装程序的功能，有`Add[Service]`上的扩展方法[IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)。</span><span class="sxs-lookup"><span data-stu-id="7d806-131">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="7d806-132">典型 web 应用将注册到服务的实体框架、 标识和 MVC:</span><span class="sxs-lookup"><span data-stu-id="7d806-132">A typical web app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="services-available-in-startup"></a><span data-ttu-id="7d806-133">在启动中可用的服务</span><span class="sxs-lookup"><span data-stu-id="7d806-133">Services available in Startup</span></span>

<span data-ttu-id="7d806-134">Web 主机提供某些服务可供`Startup`类构造函数。</span><span class="sxs-lookup"><span data-stu-id="7d806-134">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="7d806-135">应用程序添加其他服务通过`ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="7d806-135">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="7d806-136">在主机和应用程序服务都然后可以在`Configure`和整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="7d806-136">Both the host and app services are then available in `Configure` and throughout the application.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="7d806-137">Configure 方法</span><span class="sxs-lookup"><span data-stu-id="7d806-137">The Configure method</span></span>

<span data-ttu-id="7d806-138">[配置](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure)方法用于指定应用程序如何响应的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="7d806-138">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="7d806-139">通过添加配置请求管道[中间件](xref:fundamentals/middleware)组件[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)实例。</span><span class="sxs-lookup"><span data-stu-id="7d806-139">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="7d806-140">`IApplicationBuilder`可供`Configure`方法，但它未注册到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="7d806-140">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="7d806-141">承载创建`IApplicationBuilder`并直接将其传递`Configure`([引用源](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192))。</span><span class="sxs-lookup"><span data-stu-id="7d806-141">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure` ([reference source](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span></span>

<span data-ttu-id="7d806-142">[ASP.NET Core 模板](/dotnet/core/tools/dotnet-new)支持开发人员异常页上，配置管道[浏览器链接](http://vswebessentials.com/features/browserlink)，错误页、 静态文件和 ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="7d806-142">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="7d806-143">每个`Use`扩展方法将中间件组件添加到请求管道。</span><span class="sxs-lookup"><span data-stu-id="7d806-143">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="7d806-144">例如，`UseMvc`扩展方法将添加[路由的中间件](xref:fundamentals/routing)向请求管道并配置[MVC](xref:mvc/overview)作为默认处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d806-144">For instance, the `UseMvc` extension method adds the [routing middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="7d806-145">其他服务，如`IHostingEnvironment`和`ILoggerFactory`，还可以将方法签名中指定。</span><span class="sxs-lookup"><span data-stu-id="7d806-145">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="7d806-146">如果指定，如果它们被注入其他服务。</span><span class="sxs-lookup"><span data-stu-id="7d806-146">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="7d806-147">有关详细信息如何使用`IApplicationBuilder`，请参阅[中间件](xref:fundamentals/middleware)。</span><span class="sxs-lookup"><span data-stu-id="7d806-147">For more information on how to use `IApplicationBuilder`, see [Middleware](xref:fundamentals/middleware).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="7d806-148">便利方法</span><span class="sxs-lookup"><span data-stu-id="7d806-148">Convenience methods</span></span>

<span data-ttu-id="7d806-149">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices)和[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure)便捷的方法，可以使用而不是指定`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="7d806-149">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="7d806-150">多次调用`ConfigureServices`将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="7d806-150">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="7d806-151">多次调用`Configure`使用最后一次的方法调用。</span><span class="sxs-lookup"><span data-stu-id="7d806-151">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[Main](startup/snapshot_sample/Program.cs?highlight=16,20)]

## <a name="startup-filters"></a><span data-ttu-id="7d806-152">启动筛选器</span><span class="sxs-lookup"><span data-stu-id="7d806-152">Startup filters</span></span>

<span data-ttu-id="7d806-153">使用[IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter)的开头或末尾应用的配置中间件[配置](#the-configure-method)中间件管道。</span><span class="sxs-lookup"><span data-stu-id="7d806-153">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="7d806-154">`IStartupFilter`可用于确保中间件运行之前或之后添加通过库进行的开头或末尾应用程序的请求处理管道的中间件。</span><span class="sxs-lookup"><span data-stu-id="7d806-154">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="7d806-155">`IStartupFilter`实现单个方法[配置](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)，其接收并返回`Action<IApplicationBuilder>`。</span><span class="sxs-lookup"><span data-stu-id="7d806-155">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="7d806-156">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)定义用于配置应用的请求管道的类。</span><span class="sxs-lookup"><span data-stu-id="7d806-156">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="7d806-157">有关详细信息，请参阅[使用 IApplicationBuilder 创建中间件管道](xref:fundamentals/middleware#creating-a-middleware-pipeline-with-iapplicationbuilder)。</span><span class="sxs-lookup"><span data-stu-id="7d806-157">For more information, see [Creating a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware#creating-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="7d806-158">每个`IStartupFilter`请求管道中实现一个或多个中间件。</span><span class="sxs-lookup"><span data-stu-id="7d806-158">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="7d806-159">筛选器添加到服务容器的顺序调用。</span><span class="sxs-lookup"><span data-stu-id="7d806-159">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="7d806-160">筛选可能会增加中间件之前或之后将控件传递给下一个筛选器，因此它们将追加到的开头或末尾应用管道。</span><span class="sxs-lookup"><span data-stu-id="7d806-160">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="7d806-161">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample)) 演示如何注册与中间件`IStartupFilter`。</span><span class="sxs-lookup"><span data-stu-id="7d806-161">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="7d806-162">示例应用程序包含中间件的查询字符串参数设置选项值：</span><span class="sxs-lookup"><span data-stu-id="7d806-162">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="7d806-163">`RequestSetOptionsMiddleware`中配置`RequestSetOptionsStartupFilter`类：</span><span class="sxs-lookup"><span data-stu-id="7d806-163">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="7d806-164">`IStartupFilter`注册中的服务容器中`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="7d806-164">The `IStartupFilter` is registered in the service container in `ConfigureServices`:</span></span>

[!code-csharp[Main](startup/sample/Startup.cs?name=snippet1&highlight=3)]

<span data-ttu-id="7d806-165">时的查询字符串参数`option`提供该中间件处理的值分配之前 MVC 中间件呈现响应：</span><span class="sxs-lookup"><span data-stu-id="7d806-165">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![显示呈现的索引页的浏览器窗口。](startup/_static/index.png)

<span data-ttu-id="7d806-168">中间件执行顺序设置的顺序由`IStartupFilter`注册：</span><span class="sxs-lookup"><span data-stu-id="7d806-168">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="7d806-169">多个`IStartupFilter`实现可与相同的对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="7d806-169">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="7d806-170">如果排序很重要，排序其`IStartupFilter`服务注册其中间件应运行的顺序相匹配。</span><span class="sxs-lookup"><span data-stu-id="7d806-170">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="7d806-171">库可以添加与一个或多个中间件`IStartupFilter`运行之前或之后向其他应用程序中间件注册的实现`IStartupFilter`。</span><span class="sxs-lookup"><span data-stu-id="7d806-171">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="7d806-172">若要调用`IStartupFilter`之前添加的库的中间件的中间件`IStartupFilter`，库添加到服务容器之前定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="7d806-172">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="7d806-173">若要此后调用它，请添加库后位置服务注册。</span><span class="sxs-lookup"><span data-stu-id="7d806-173">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d806-174">其他资源</span><span class="sxs-lookup"><span data-stu-id="7d806-174">Additional resources</span></span>

* [<span data-ttu-id="7d806-175">承载</span><span class="sxs-lookup"><span data-stu-id="7d806-175">Hosting</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="7d806-176">使用多个环境</span><span class="sxs-lookup"><span data-stu-id="7d806-176">Working with Multiple Environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="7d806-177">中间件</span><span class="sxs-lookup"><span data-stu-id="7d806-177">Middleware</span></span>](xref:fundamentals/middleware)
* [<span data-ttu-id="7d806-178">日志记录</span><span class="sxs-lookup"><span data-stu-id="7d806-178">Logging</span></span>](xref:fundamentals/logging/index)
* [<span data-ttu-id="7d806-179">配置</span><span class="sxs-lookup"><span data-stu-id="7d806-179">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="7d806-180">StartupLoader 类： FindStartupType 方法 （引用源）</span><span class="sxs-lookup"><span data-stu-id="7d806-180">StartupLoader class: FindStartupType method (reference source)</span></span>](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
