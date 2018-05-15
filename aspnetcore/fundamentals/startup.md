---
title: ASP.NET Core 中的应用程序启动
author: ardalis
description: 了解 ASP.NET Core 中的 Startup 类如何配置服务和应用的请求管道。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 4/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/startup
ms.openlocfilehash: 8dd632a2c888e65c6420e0fed7acf6fa15173b3d
ms.sourcegitcommit: c4a31aaf902f2e84aaf4a9d882ca980fdf6488c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2018
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="d1adb-103">ASP.NET Core 中的应用程序启动</span><span class="sxs-lookup"><span data-stu-id="d1adb-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="d1adb-104">作者：[Steve Smith](https://ardalis.com)、[Tom Dykstra](https://github.com/tdykstra) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="d1adb-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d1adb-105">`Startup` 类配置服务和应用的请求管道。</span><span class="sxs-lookup"><span data-stu-id="d1adb-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="d1adb-106">Startup 类</span><span class="sxs-lookup"><span data-stu-id="d1adb-106">The Startup class</span></span>

<span data-ttu-id="d1adb-107">ASP.NET Core 应用使用 `Startup` 类，按照约定命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="d1adb-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="d1adb-108">`Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="d1adb-108">The `Startup` class:</span></span>

* <span data-ttu-id="d1adb-109">可选择性地包括 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 方法以配置应用的服务。</span><span class="sxs-lookup"><span data-stu-id="d1adb-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="d1adb-110">必须包括 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 方法以创建应用的请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="d1adb-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="d1adb-111">当应用启动时，运行时调用 `ConfigureServices` 和 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="d1adb-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="d1adb-112">通过 [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions)、[UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 方法指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="d1adb-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="d1adb-113">`Startup` 类构造函数接受由主机定义的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="d1adb-113">The `Startup` class constructor accepts dependencies defined by the host.</span></span> <span data-ttu-id="d1adb-114">在 `Startup` 类中[注入依赖关系](xref:fundamentals/dependency-injection)的常见用途为注入：</span><span class="sxs-lookup"><span data-stu-id="d1adb-114">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject:</span></span>

* <span data-ttu-id="d1adb-115">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) 以按环境配置服务。</span><span class="sxs-lookup"><span data-stu-id="d1adb-115">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment.</span></span>
* <span data-ttu-id="d1adb-116">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) 以在启动过程中配置应用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-116">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) to configure the app during startup.</span></span>

[!code-csharp[](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="d1adb-117">注入 `IHostingEnvironment` 的替代方法是使用基于约定的方法。</span><span class="sxs-lookup"><span data-stu-id="d1adb-117">An alternative to injecting `IHostingEnvironment` is to use a conventions-based approach.</span></span> <span data-ttu-id="d1adb-118">该应用可以为不同的环境（例如 `StartupDevelopment`）定义单独的 `Startup` 类，并在运行时选择适当的 startup 类。</span><span class="sxs-lookup"><span data-stu-id="d1adb-118">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate startup class is selected at runtime.</span></span> <span data-ttu-id="d1adb-119">优先考虑名称后缀与当前环境相匹配的类。</span><span class="sxs-lookup"><span data-stu-id="d1adb-119">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="d1adb-120">如果应用在开发环境中运行并包含 `Startup` 类和 `StartupDevelopment` 类，则使用 `StartupDevelopment` 类。</span><span class="sxs-lookup"><span data-stu-id="d1adb-120">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="d1adb-121">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments#startup-conventions)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-121">For more information, see [Work with multiple environments](xref:fundamentals/environments#startup-conventions).</span></span>

<span data-ttu-id="d1adb-122">若要详细了解 `WebHostBuilder`，请参阅[承载](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="d1adb-122">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/hosting) topic.</span></span> <span data-ttu-id="d1adb-123">有关在启动过程中处理错误的信息，请参阅[启动异常处理](xref:fundamentals/error-handling#startup-exception-handling)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-123">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="d1adb-124">ConfigureServices 方法</span><span class="sxs-lookup"><span data-stu-id="d1adb-124">The ConfigureServices method</span></span>

<span data-ttu-id="d1adb-125">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 方法是：</span><span class="sxs-lookup"><span data-stu-id="d1adb-125">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="d1adb-126">Optional</span><span class="sxs-lookup"><span data-stu-id="d1adb-126">Optional</span></span>
* <span data-ttu-id="d1adb-127">在 `Configure` 方法配置应用服务之前，由 Web 主机调用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-127">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="d1adb-128">其中按常规设置[配置选项](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-128">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="d1adb-129">将服务添加到服务容器，使其在应用和 `Configure` 方法中可用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-129">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="d1adb-130">这些服务通过[依赖关系注入](xref:fundamentals/dependency-injection)或 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices) 解析。</span><span class="sxs-lookup"><span data-stu-id="d1adb-130">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="d1adb-131">Web 主机可能会在调用 `Startup` 方法之前配置某些服务。</span><span class="sxs-lookup"><span data-stu-id="d1adb-131">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="d1adb-132">有关详细信息，请参阅[承载](xref:fundamentals/hosting)主题。</span><span class="sxs-lookup"><span data-stu-id="d1adb-132">Details are available in the [Hosting](xref:fundamentals/hosting) topic.</span></span>

<span data-ttu-id="d1adb-133">对于需要大量设置的功能，[IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection) 上有 `Add[Service]` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="d1adb-133">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="d1adb-134">典型 Web 应用将为实体框架、标识和 MVC 注册服务：</span><span class="sxs-lookup"><span data-stu-id="d1adb-134">A typical web app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

::: moniker range=">= aspnetcore-2.1" 

<a name="setcompatibilityversion"></a>
### <a name="setcompatibilityversion-for-aspnet-core-mvc"></a><span data-ttu-id="d1adb-135">ASP.NET Core MVC 的 SetCompatibilityVersion</span><span class="sxs-lookup"><span data-stu-id="d1adb-135">SetCompatibilityVersion for ASP.NET Core MVC</span></span> 

<span data-ttu-id="d1adb-136">`SetCompatibilityVersion` 方法允许应用选择加入或退出 ASP.NET MVC Core 2.1+ 中引入的潜在中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="d1adb-136">The `SetCompatibilityVersion` method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET MVC Core 2.1+.</span></span> <span data-ttu-id="d1adb-137">这些潜在的中断行为变更通常取决于 MVC 子系统的行为方式以及运行时调用“代码”的方式。</span><span class="sxs-lookup"><span data-stu-id="d1adb-137">These potentially breaking behavior changes are generally in how the MVC subsystem behaves and how **your code** is called by the runtime.</span></span> <span data-ttu-id="d1adb-138">通过选择加入，你将获取最新的行为以及 ASP.NET Core 的长期行为。</span><span class="sxs-lookup"><span data-stu-id="d1adb-138">By opting in, you get the latest behavior, and the long-term behavior of ASP.NET Core.</span></span>

<span data-ttu-id="d1adb-139">以下代码将兼容模式设置为 ASP.NET Core 2.1：</span><span class="sxs-lookup"><span data-stu-id="d1adb-139">The following code sets the compatibility mode to ASP.NET Core 2.1:</span></span>

<span data-ttu-id="d1adb-140">[!code-csharp[Main](startup/sampleCompatibility/Startup.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="d1adb-140">[!code-csharp[Main](startup/sampleCompatibility/Startup.cs?name=snippet1)]</span></span>

<span data-ttu-id="d1adb-141">建议使用最新版本 (`CompatibilityVersion.Version_2_1`) 来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="d1adb-141">We recommend you test your application using the latest version (`CompatibilityVersion.Version_2_1`).</span></span> <span data-ttu-id="d1adb-142">我们预计大多数应用程序不会使用最新版本进行中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="d1adb-142">We anticipate that most applications will not have breaking behavior changes using the latest version.</span></span> 

<span data-ttu-id="d1adb-143">调用 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` 的应用程序会被阻止进行 ASP.NET Core 2.1 MVC 和更高的 2.x 版本中引入的潜在中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="d1adb-143">Applications that call `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` are protected from potentially breaking behavior changes introduced in the ASP.NET Core 2.1 MVC and later 2.x versions.</span></span> <span data-ttu-id="d1adb-144">该阻止操作：</span><span class="sxs-lookup"><span data-stu-id="d1adb-144">This protection:</span></span>

* <span data-ttu-id="d1adb-145">不适用于所有 2.1 和更高版本的更改，它的目标是潜在地中断 MVC 子系统中的 ASP.NET Core 运行时行为变更。</span><span class="sxs-lookup"><span data-stu-id="d1adb-145">Does not apply to all 2.1 and later changes, it's targeted to potentially breaking ASP.NET Core runtime behavior changes in the MVC subsystem.</span></span>
* <span data-ttu-id="d1adb-146">不会扩展到下一个主要版本。</span><span class="sxs-lookup"><span data-stu-id="d1adb-146">Does not extend to the next major version.</span></span>

<span data-ttu-id="d1adb-147">不调用 `SetCompatibilityVersion` 的 ASP.NET Core 2.1 和更高 2.x 版本的应用程序的默认兼容性是 2.0 兼容性。</span><span class="sxs-lookup"><span data-stu-id="d1adb-147">The default compatibility for ASP.NET Core 2.1 and later 2.x applications that do **not** call `SetCompatibilityVersion` is 2.0 compatibility.</span></span> <span data-ttu-id="d1adb-148">即，未调用 `SetCompatibilityVersion` 与调用 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` 相同。</span><span class="sxs-lookup"><span data-stu-id="d1adb-148">That is, not calling `SetCompatibilityVersion` is the same as calling `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`.</span></span>

<span data-ttu-id="d1adb-149">以下代码将兼容模式设置为 ASP.NET Core 2.1（以下行为除外）：</span><span class="sxs-lookup"><span data-stu-id="d1adb-149">The following code sets the compatibility mode to ASP.NET Core 2.1, except for the following behaviors:</span></span>

* [<span data-ttu-id="d1adb-150">AllowCombiningAuthorizeFilters</span><span class="sxs-lookup"><span data-stu-id="d1adb-150">AllowCombiningAuthorizeFilters</span></span>](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)
* [<span data-ttu-id="d1adb-151">InputFormatterExceptionPolicy</span><span class="sxs-lookup"><span data-stu-id="d1adb-151">InputFormatterExceptionPolicy</span></span>](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)

<span data-ttu-id="d1adb-152">[!code-csharp[Main](startup/sampleCompatibility/Startup2.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="d1adb-152">[!code-csharp[Main](startup/sampleCompatibility/Startup2.cs?name=snippet1)]</span></span>

<span data-ttu-id="d1adb-153">对于遇到中断行为变更的应用，请使用适当的兼容性开关：</span><span class="sxs-lookup"><span data-stu-id="d1adb-153">For apps that encounter breaking behavior changes, using the appropriate compatibility switches:</span></span>

* <span data-ttu-id="d1adb-154">允许使用最新版本并选择退出特定的中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="d1adb-154">Allows you to use the latest release and opt out of specific breaking behavior changes.</span></span>
* <span data-ttu-id="d1adb-155">请用些时间更新应用，以便其适用于最新更改。</span><span class="sxs-lookup"><span data-stu-id="d1adb-155">Gives you time to update your app so it works with the latest changes.</span></span>

<span data-ttu-id="d1adb-156">[MvcOptions](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) 类源注释充分地阐述了更改的内容以及为什么更改对大多数用户来说是一种改进。</span><span class="sxs-lookup"><span data-stu-id="d1adb-156">The [MvcOptions](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) class source comments have a good explanation of what changed and why the changes are an improvement for most users.</span></span>

<span data-ttu-id="d1adb-157">将来会推出 [ASP.NET Core 3.0 版本](https://github.com/aspnet/Home/wiki/Roadmap)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-157">At some future date, there will be an [ASP.NET Core 3.0 version](https://github.com/aspnet/Home/wiki/Roadmap).</span></span> <span data-ttu-id="d1adb-158">在 3.0 版本中，将删除兼容性开关支持的旧行为。</span><span class="sxs-lookup"><span data-stu-id="d1adb-158">Old behaviors supported by compatibility switches will be removed in the 3.0 version.</span></span> <span data-ttu-id="d1adb-159">我们认为这些积极的变化几乎使所有用户受益。</span><span class="sxs-lookup"><span data-stu-id="d1adb-159">We feel these are positive changes benefitting nearly all users.</span></span> <span data-ttu-id="d1adb-160">现在通过引入这些更改，大多数应用可以立即受益，其他人员将有时间更新其应用程序。</span><span class="sxs-lookup"><span data-stu-id="d1adb-160">By introducing these changes now, most apps can benefit now, and the others will have time to update their applications.</span></span>

::: moniker-end

## <a name="services-available-in-startup"></a><span data-ttu-id="d1adb-161">Startup 中可用的服务</span><span class="sxs-lookup"><span data-stu-id="d1adb-161">Services available in Startup</span></span>

<span data-ttu-id="d1adb-162">Web 主机提供 `Startup` 类构造函数可用的某些服务。</span><span class="sxs-lookup"><span data-stu-id="d1adb-162">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="d1adb-163">应用通过 `ConfigureServices` 添加其他服务。</span><span class="sxs-lookup"><span data-stu-id="d1adb-163">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="d1adb-164">然后，主机和应用服务都可以在 `Configure` 和整个应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-164">Both the host and app services are then available in `Configure` and throughout the application.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="d1adb-165">Configure 方法</span><span class="sxs-lookup"><span data-stu-id="d1adb-165">The Configure method</span></span>

<span data-ttu-id="d1adb-166">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 方法用于指定应用响应 HTTP 请求的方式。</span><span class="sxs-lookup"><span data-stu-id="d1adb-166">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="d1adb-167">可通过将[中间件](xref:fundamentals/middleware/index)组件添加到 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 实例来配置请求管道。</span><span class="sxs-lookup"><span data-stu-id="d1adb-167">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware/index) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="d1adb-168">`Configure` 方法可使用 `IApplicationBuilder`，但未在服务容器中注册。</span><span class="sxs-lookup"><span data-stu-id="d1adb-168">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="d1adb-169">承载创建 `IApplicationBuilder` 并将其直接传递给 `Configure`（[引用源](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)）。</span><span class="sxs-lookup"><span data-stu-id="d1adb-169">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure` ([reference source](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span></span>

<span data-ttu-id="d1adb-170">[ASP.NET Core 模板](/dotnet/core/tools/dotnet-new)配置支持开发人员异常页、[BrowserLink](http://vswebessentials.com/features/browserlink)、错误页、静态文件和 ASP.NET MVC 的管道：</span><span class="sxs-lookup"><span data-stu-id="d1adb-170">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="d1adb-171">每个 `Use` 扩展方法将中间件组件添加到请求管道。</span><span class="sxs-lookup"><span data-stu-id="d1adb-171">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="d1adb-172">例如，`UseMvc` 扩展方法将[路由中间件](xref:fundamentals/routing)添加到请求管道，并将 [MVC](xref:mvc/overview) 配置为默认处理程序。</span><span class="sxs-lookup"><span data-stu-id="d1adb-172">For instance, the `UseMvc` extension method adds the [Routing Middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="d1adb-173">请求管道中的每个中间件组件负责调用管道中的下一个组件，或在适当情况下使链发生短路。</span><span class="sxs-lookup"><span data-stu-id="d1adb-173">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the chain, if appropriate.</span></span> <span data-ttu-id="d1adb-174">如果中间件链中未发生短路，则每个中间件都有第二次机会在将请求发送到客户端前处理该请求。</span><span class="sxs-lookup"><span data-stu-id="d1adb-174">If short-circuiting doesn't occur along the middleware chain, each middleware has a second chance to process the request before it's sent to the client.</span></span>

<span data-ttu-id="d1adb-175">其他服务（如 `IHostingEnvironment` 和 `ILoggerFactory`），也可以在方法签名中指定。</span><span class="sxs-lookup"><span data-stu-id="d1adb-175">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="d1adb-176">如果指定，其他服务如果可用，将被注入。</span><span class="sxs-lookup"><span data-stu-id="d1adb-176">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="d1adb-177">有关如何使用 `IApplicationBuilder` 和中间件处理顺序的详细信息，请参阅[中间件](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-177">For more information on how to use `IApplicationBuilder` and the order of middleware processing, see [Middleware](xref:fundamentals/middleware/index).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="d1adb-178">便利方法</span><span class="sxs-lookup"><span data-stu-id="d1adb-178">Convenience methods</span></span>

<span data-ttu-id="d1adb-179">可使用 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 和 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 便利方法，而不是指定 `Startup` 类。</span><span class="sxs-lookup"><span data-stu-id="d1adb-179">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="d1adb-180">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="d1adb-180">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="d1adb-181">多次调用 `Configure` 将使用上一个方法调用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-181">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[](startup/snapshot_sample/Program.cs?highlight=18,22)]

## <a name="startup-filters"></a><span data-ttu-id="d1adb-182">Startup 筛选器</span><span class="sxs-lookup"><span data-stu-id="d1adb-182">Startup filters</span></span>

<span data-ttu-id="d1adb-183">在应用的 [Configure](#the-configure-method) 中间件管道的开头或末尾使用 [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) 来配置中间件。</span><span class="sxs-lookup"><span data-stu-id="d1adb-183">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="d1adb-184">`IStartupFilter` 有助于确保中间件在应用请求处理管道的开始或结束时由库添加的中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="d1adb-184">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="d1adb-185">`IStartupFilter` 实现单个方法（即 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)），该方法接收并返回 `Action<IApplicationBuilder>`。</span><span class="sxs-lookup"><span data-stu-id="d1adb-185">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="d1adb-186">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 定义用于配置应用请求管道的类。</span><span class="sxs-lookup"><span data-stu-id="d1adb-186">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="d1adb-187">有关详细信息，请参阅[使用 IApplicationBuilder 创建中间件管道](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-187">For more information, see [Create a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="d1adb-188">在请求管道中，每个 `IStartupFilter` 实现一个或多个中间件。</span><span class="sxs-lookup"><span data-stu-id="d1adb-188">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="d1adb-189">筛选器按照添加到服务容器的顺序调用。</span><span class="sxs-lookup"><span data-stu-id="d1adb-189">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="d1adb-190">筛选器可在将控件传递给下一个筛选器之前或之后添加中间件，从而附加到应用管道的开头或末尾。</span><span class="sxs-lookup"><span data-stu-id="d1adb-190">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="d1adb-191">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）演示如何向 `IStartupFilter` 注册中间件。</span><span class="sxs-lookup"><span data-stu-id="d1adb-191">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="d1adb-192">示例应用包含一个中间件，该中间件从查询字符串参数中设置选项值：</span><span class="sxs-lookup"><span data-stu-id="d1adb-192">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="d1adb-193">在 `RequestSetOptionsStartupFilter` 类中配置 `RequestSetOptionsMiddleware`：</span><span class="sxs-lookup"><span data-stu-id="d1adb-193">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="d1adb-194">在 `ConfigureServices` 的服务容器中注册 `IStartupFilter`：</span><span class="sxs-lookup"><span data-stu-id="d1adb-194">The `IStartupFilter` is registered in the service container in `ConfigureServices`:</span></span>

[!code-csharp[](startup/sample/Startup.cs?name=snippet1&highlight=3)]

<span data-ttu-id="d1adb-195">当提供 `option` 的查询字符串参数时，中间件在 MVC 中间件呈现响应之前处理分配值：</span><span class="sxs-lookup"><span data-stu-id="d1adb-195">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![浏览器窗口显示已呈现的索引页。](startup/_static/index.png)

<span data-ttu-id="d1adb-198">中间件执行顺序由 `IStartupFilter` 注册顺序设置：</span><span class="sxs-lookup"><span data-stu-id="d1adb-198">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="d1adb-199">多个 `IStartupFilter` 实现可能与相同的对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="d1adb-199">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="d1adb-200">如果顺序很重要，请将它们的 `IStartupFilter` 服务注册进行排序，以匹配其中间件应有的运行顺序。</span><span class="sxs-lookup"><span data-stu-id="d1adb-200">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="d1adb-201">库可能添加包含一个或多个 `IStartupFilter` 实现的中间件，这些实现在向 `IStartupFilter` 注册的其他应用中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="d1adb-201">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="d1adb-202">若要在库的 `IStartupFilter` 添加中间件之前调用 `IStartupFilter` 中间件，请在将库添加到服务容器之前定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="d1adb-202">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="d1adb-203">若要在此后调用，请在添加库之后定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="d1adb-203">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1adb-204">其他资源</span><span class="sxs-lookup"><span data-stu-id="d1adb-204">Additional resources</span></span>

* [<span data-ttu-id="d1adb-205">承载</span><span class="sxs-lookup"><span data-stu-id="d1adb-205">Hosting</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="d1adb-206">使用多个环境</span><span class="sxs-lookup"><span data-stu-id="d1adb-206">Work with multiple environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="d1adb-207">中间件</span><span class="sxs-lookup"><span data-stu-id="d1adb-207">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="d1adb-208">日志记录</span><span class="sxs-lookup"><span data-stu-id="d1adb-208">Logging</span></span>](xref:fundamentals/logging/index)
* [<span data-ttu-id="d1adb-209">配置</span><span class="sxs-lookup"><span data-stu-id="d1adb-209">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="d1adb-210">StartupLoader 类：FindStartupType 方法（引用源）</span><span class="sxs-lookup"><span data-stu-id="d1adb-210">StartupLoader class: FindStartupType method (reference source)</span></span>](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
