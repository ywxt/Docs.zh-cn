---
title: 在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用
author: guardrex
description: 了解如何使用 IHostingStartup 从外部程序集增强 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 08/13/2018
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: 2eddfa03b28564fcca7cc098e353b05e23b7c6f6
ms.sourcegitcommit: a669c4e3f42e387e214a354ac4143555602e6f66
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43336270"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a><span data-ttu-id="4e01e-103">在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用</span><span class="sxs-lookup"><span data-stu-id="4e01e-103">Enhance an app from an external assembly in ASP.NET Core with IHostingStartup</span></span>

<span data-ttu-id="4e01e-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="4e01e-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4e01e-105">通过 [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)（承载启动）实现，在启动时从外部程序集向应用添加增强功能。</span><span class="sxs-lookup"><span data-stu-id="4e01e-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) (hosting startup) implementation adds enhancements to an app at startup from an external assembly.</span></span> <span data-ttu-id="4e01e-106">例如，外部库可使用承载启动实现为应用提供其他配置提供程序或服务。</span><span class="sxs-lookup"><span data-stu-id="4e01e-106">For example, an external library can use a hosting startup implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="4e01e-107">ASP.NET Core 2.0 或更高版本中提供了 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-107">`IHostingStartup` *is available in ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="4e01e-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="4e01e-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="hostingstartup-attribute"></a><span data-ttu-id="4e01e-109">HostingStartup 属性</span><span class="sxs-lookup"><span data-stu-id="4e01e-109">HostingStartup attribute</span></span>

<span data-ttu-id="4e01e-110">[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性表示存在要在运行时激活的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="4e01e-110">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute indicates the presence of a hosting startup assembly to activate at runtime.</span></span>

<span data-ttu-id="4e01e-111">将自动扫描输入程序集或包含 `Startup` 类的程序集以查找 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-111">The entry assembly or the assembly containing the `Startup` class is automatically scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="4e01e-112">用于搜索 `HostingStartup` 属性的程序集列表在运行时从 [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 中的配置加载。</span><span class="sxs-lookup"><span data-stu-id="4e01e-112">The list of assemblies to search for `HostingStartup` attributes is loaded at runtime from configuration in the [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey).</span></span> <span data-ttu-id="4e01e-113">要从发现中排除的程序集列表从 [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey) 加载。</span><span class="sxs-lookup"><span data-stu-id="4e01e-113">The list of assemblies to exclude from discovery is loaded from the [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey).</span></span> <span data-ttu-id="4e01e-114">有关详细信息，请参阅 [Web 主机：承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)和 [Web 主机：承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="4e01e-114">For more information, see [Web Host: Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) and [Web Host: Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies).</span></span>

<span data-ttu-id="4e01e-115">在以下示例中，承载启动程序集的命名空间为 `StartupEnhancement`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-115">In the following example, the namespace of the hosting startup assembly is `StartupEnhancement`.</span></span> <span data-ttu-id="4e01e-116">包含承载启动代码的类是 `StartupEnhancementHostingStartup`：</span><span class="sxs-lookup"><span data-stu-id="4e01e-116">The class containing the hosting startup code is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="4e01e-117">`HostingStartup` 属性通常位于承载启动程序集的 `IHostingStartup` 实现类文件中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-117">The `HostingStartup` attribute is typically located in the hosting startup assembly's `IHostingStartup` implementation class file.</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="4e01e-118">发现加载的承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="4e01e-118">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="4e01e-119">要发现加载的承载启动程序集，请启用日志记录并检查应用的日志。</span><span class="sxs-lookup"><span data-stu-id="4e01e-119">To discover loaded hosting startup assemblies, enable logging and check the app's logs.</span></span> <span data-ttu-id="4e01e-120">记录加载程序集时发生的错误。</span><span class="sxs-lookup"><span data-stu-id="4e01e-120">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="4e01e-121">会在调试级别记录加载的承载启动程序集，并记录所有错误。</span><span class="sxs-lookup"><span data-stu-id="4e01e-121">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="4e01e-122">禁用承载启动程序集的自动加载</span><span class="sxs-lookup"><span data-stu-id="4e01e-122">Disable automatic loading of hosting startup assemblies</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4e01e-123">要禁用承载启动程序集的自动加载，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="4e01e-123">To disable automatic loading of hosting startup assemblies, use one of the following approaches:</span></span>

* <span data-ttu-id="4e01e-124">要阻止加载所有承载启动程序集，请将以下内容之一设置为 `true` 或 `1`：</span><span class="sxs-lookup"><span data-stu-id="4e01e-124">To prevent all hosting startup assemblies from loading, set one of the following to `true` or `1`:</span></span>
  * <span data-ttu-id="4e01e-125">[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-125">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
  * <span data-ttu-id="4e01e-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="4e01e-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>
* <span data-ttu-id="4e01e-127">要阻止加载特定的承载启动程序集，请将以下之一设置为以分号分隔的承载启动程序集字符串，以便在启动时排除：</span><span class="sxs-lookup"><span data-stu-id="4e01e-127">To prevent specific hosting startup assemblies from loading, set one of the following to a semicolon-delimited string of hosting startup assemblies to exclude at startup:</span></span>
  * <span data-ttu-id="4e01e-128">[承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)承载配置设置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-128">[Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies) host configuration setting.</span></span>
  * <span data-ttu-id="4e01e-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="4e01e-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` environment variable.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="4e01e-130">要禁用承载启动程序集的自动加载，请将以下之一设置为 `true` 或 `1`：</span><span class="sxs-lookup"><span data-stu-id="4e01e-130">To disable automatic loading of hosting startup assemblies, set one of the following to `true` or `1`:</span></span>

* <span data-ttu-id="4e01e-131">[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-131">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="4e01e-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="4e01e-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>

::: moniker-end

<span data-ttu-id="4e01e-133">如果同时设置了主机配置设置和环境变量，则主机设置将控制行为。</span><span class="sxs-lookup"><span data-stu-id="4e01e-133">If both the host configuration setting and the environment variable are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="4e01e-134">如果使用主机设置或环境变量来禁用承载启动程序集，将全局禁用程序集，并可能会禁用应用的多个特征。</span><span class="sxs-lookup"><span data-stu-id="4e01e-134">Disabling hosting startup assemblies using the host setting or environment variable disables the assembly globally and may disable several characteristics of an app.</span></span>

## <a name="project"></a><span data-ttu-id="4e01e-135">项目</span><span class="sxs-lookup"><span data-stu-id="4e01e-135">Project</span></span>

<span data-ttu-id="4e01e-136">使用以下任一项目类型创建承载启动：</span><span class="sxs-lookup"><span data-stu-id="4e01e-136">Create a hosting startup with either of the following project types:</span></span>

* [<span data-ttu-id="4e01e-137">类库</span><span class="sxs-lookup"><span data-stu-id="4e01e-137">Class library</span></span>](#class-library)
* [<span data-ttu-id="4e01e-138">无入口点的控制台应用</span><span class="sxs-lookup"><span data-stu-id="4e01e-138">Console app without an entry point</span></span>](#console-app-without-an-entry-point)

### <a name="class-library"></a><span data-ttu-id="4e01e-139">类库</span><span class="sxs-lookup"><span data-stu-id="4e01e-139">Class library</span></span>

<span data-ttu-id="4e01e-140">可在类库中提供承载启动增强。</span><span class="sxs-lookup"><span data-stu-id="4e01e-140">A hosting startup enhancement can be provided in a class library.</span></span> <span data-ttu-id="4e01e-141">库包含 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-141">The library contains a `HostingStartup` attribute.</span></span>

<span data-ttu-id="4e01e-142">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)包括 Razor Pages 应用、HostingStartupApp 和类库 HostingStartupLibrary。</span><span class="sxs-lookup"><span data-stu-id="4e01e-142">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) includes a Razor Pages app, *HostingStartupApp*, and a class library, *HostingStartupLibrary*.</span></span> <span data-ttu-id="4e01e-143">类库：</span><span class="sxs-lookup"><span data-stu-id="4e01e-143">The class library:</span></span>

* <span data-ttu-id="4e01e-144">包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-144">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="4e01e-145">`ServiceKeyInjection` 使用内存中配置提供程序 ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)) 将一对服务字符串添加到应用的配置中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-145">`ServiceKeyInjection` adds a pair of service strings to the app's configuration using the in-memory configuration provider ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)).</span></span>
* <span data-ttu-id="4e01e-146">包含 `HostingStartup` 属性，用于标识承载启动的命名空间和类。</span><span class="sxs-lookup"><span data-stu-id="4e01e-146">Includes a `HostingStartup` attribute that identifies the hosting startup's namespace and class.</span></span>

<span data-ttu-id="4e01e-147">`ServiceKeyInjection` 类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-147">The `ServiceKeyInjection` class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="4e01e-148">用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-148">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configuration provided by the hosting startup assembly.</span></span>

<span data-ttu-id="4e01e-149">HostingStartupLibrary/ServiceKeyInjection.cs：</span><span class="sxs-lookup"><span data-stu-id="4e01e-149">*HostingStartupLibrary/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupLibrary/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="4e01e-150">应用的索引页读取并呈现类库承载启动程序集设置的两个键的配置值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-150">The app's Index page reads and renders the configuration values for the two keys set by the class library's hosting startup assembly:</span></span>

<span data-ttu-id="4e01e-151">HostingStartupApp/Pages/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="4e01e-151">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=5-6,11-12)]

<span data-ttu-id="4e01e-152">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)还包括一个 NuGet 包项目，该项目提供单独的承载启动 HostingStartupPackage。</span><span class="sxs-lookup"><span data-stu-id="4e01e-152">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) also includes a NuGet package project that provides a separate hosting startup, *HostingStartupPackage*.</span></span> <span data-ttu-id="4e01e-153">该包具有与前述类库相同的特征。</span><span class="sxs-lookup"><span data-stu-id="4e01e-153">The package has the same characteristics of the class library described earlier.</span></span> <span data-ttu-id="4e01e-154">包：</span><span class="sxs-lookup"><span data-stu-id="4e01e-154">The package:</span></span>

* <span data-ttu-id="4e01e-155">包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-155">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="4e01e-156">`ServiceKeyInjection` 将一对服务字符串添加到应用的配置中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-156">`ServiceKeyInjection` adds a pair of service strings to the app's configuration.</span></span>
* <span data-ttu-id="4e01e-157">包含 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-157">Includes a `HostingStartup` attribute.</span></span>

<span data-ttu-id="4e01e-158">HostingStartupPackage/ServiceKeyInjection.cs：</span><span class="sxs-lookup"><span data-stu-id="4e01e-158">*HostingStartupPackage/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupPackage/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="4e01e-159">应用的索引页读取并呈现包承载启动程序集设置的两个键的配置值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-159">The app's Index page reads and renders the configuration values for the two keys set by the package's hosting startup assembly:</span></span>

<span data-ttu-id="4e01e-160">HostingStartupApp/Pages/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="4e01e-160">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=7-8,13-14)]

### <a name="console-app-without-an-entry-point"></a><span data-ttu-id="4e01e-161">无入口点的控制台应用</span><span class="sxs-lookup"><span data-stu-id="4e01e-161">Console app without an entry point</span></span>

<span data-ttu-id="4e01e-162">此方法仅适用于 .NET Core 应用，不适用于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="4e01e-162">*This approach is only available for .NET Core apps, not .NET Framework.*</span></span>

<span data-ttu-id="4e01e-163">可在无入口点的控制台应用中提供动态承载启动增强功能，该功能无需编译时引用进行激活。</span><span class="sxs-lookup"><span data-stu-id="4e01e-163">A dynamic hosting startup enhancement that doesn't require a compile-time reference for activation can be provided in a console app without an entry point.</span></span> <span data-ttu-id="4e01e-164">应用包含 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-164">The app contains a `HostingStartup` attribute.</span></span> <span data-ttu-id="4e01e-165">创建动态承载启动：</span><span class="sxs-lookup"><span data-stu-id="4e01e-165">To create a dynamic hosting startup:</span></span>

1. <span data-ttu-id="4e01e-166">从包含 `IHostingStartup` 实现的类创建实现库。</span><span class="sxs-lookup"><span data-stu-id="4e01e-166">An implementation library is created from the class that contains the `IHostingStartup` implementation.</span></span> <span data-ttu-id="4e01e-167">实现库被视为常规包。</span><span class="sxs-lookup"><span data-stu-id="4e01e-167">The implementation library is treated as a normal package.</span></span>
1. <span data-ttu-id="4e01e-168">无入口点的控制台应用引用实现库包。</span><span class="sxs-lookup"><span data-stu-id="4e01e-168">A console app without an entry point references the implementation library package.</span></span> <span data-ttu-id="4e01e-169">使用控制台应用，因为：</span><span class="sxs-lookup"><span data-stu-id="4e01e-169">A console app is used because:</span></span>
   * <span data-ttu-id="4e01e-170">依赖项文件是可运行的应用资产，因此库无法提供依赖项文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-170">A dependencies file is a runnable app asset, so a library can't furnish a dependencies file.</span></span>
   * <span data-ttu-id="4e01e-171">无法直接将库添加到[运行时包存储](/dotnet/core/deploying/runtime-store)，该过程需要一个以已共享运行时为目标的可运行项目。</span><span class="sxs-lookup"><span data-stu-id="4e01e-171">A library can't be added directly to the [runtime package store](/dotnet/core/deploying/runtime-store), which requires a runnable project that targets the shared runtime.</span></span>
1. <span data-ttu-id="4e01e-172">发布控制台应用，获取承载启动的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4e01e-172">The console app is published to obtain the hosting startup's dependencies.</span></span> <span data-ttu-id="4e01e-173">发布控制台应用的结果是从依赖项文件中删除了未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4e01e-173">A consequence of publishing the console app is that unused dependencies are trimmed from the dependencies file.</span></span>
1. <span data-ttu-id="4e01e-174">应用及其依赖项文件位于运行时包存储中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-174">The app and its dependencies file is placed into the runtime package store.</span></span> <span data-ttu-id="4e01e-175">要发现承载启动程序集及其依赖项文件，它们将在一对环境变量中引用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-175">To discover the hosting startup assembly and its dependencies file, they're referenced in a pair of environment variables.</span></span>

<span data-ttu-id="4e01e-176">控制台应用引用 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 包：</span><span class="sxs-lookup"><span data-stu-id="4e01e-176">The console app references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.csproj)]

<span data-ttu-id="4e01e-177">生成 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 时，[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性将类标识为 `IHostingStartup` 的实现，用于加载和执行。</span><span class="sxs-lookup"><span data-stu-id="4e01e-177">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="4e01e-178">在下面的示例中，命名空间为 `StartupEnhancement`，类为 `StartupEnhancementHostingStartup`：</span><span class="sxs-lookup"><span data-stu-id="4e01e-178">In the following example, the namespace is `StartupEnhancement`, and the class is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="4e01e-179">类实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-179">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="4e01e-180">类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-180">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="4e01e-181">用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-181">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configuration provided by the hosting startup assembly.</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="4e01e-182">生成 `IHostingStartup` 项目时，依赖项文件 (\*.deps.json) 将程序集的 `runtime` 位置设为 bin 文件夹：</span><span class="sxs-lookup"><span data-stu-id="4e01e-182">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="4e01e-183">仅显示部分文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-183">Only part of the file is shown.</span></span> <span data-ttu-id="4e01e-184">示例中程序集的名称是 `StartupEnhancement`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-184">The assembly name in the example is `StartupEnhancement`.</span></span>

## <a name="specify-the-hosting-startup-assembly"></a><span data-ttu-id="4e01e-185">指定承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="4e01e-185">Specify the hosting startup assembly</span></span>

<span data-ttu-id="4e01e-186">对于类库或控制台应用提供的承载启动，请在 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中指定承载启动程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="4e01e-186">For either a class library- or console app-supplied hosting startup, specify the hosting startup assembly's name in the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span> <span data-ttu-id="4e01e-187">环境变量是以分号分隔的程序集列表。</span><span class="sxs-lookup"><span data-stu-id="4e01e-187">The environment variable is a semicolon-delimited list of assemblies.</span></span>

<span data-ttu-id="4e01e-188">仅扫描承载启动程序集以查找 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-188">Only hosting startup assemblies are scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="4e01e-189">对于示例应用 HostingStartupApp，要发现前述的承载启动，请将环境变量设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-189">For the sample app, *HostingStartupApp*, to discover the hosting startups described earlier, the environment variable is set to the following value:</span></span>

```
HostingStartupLibrary;HostingStartupPackage;StartupDiagnostics
```

<span data-ttu-id="4e01e-190">还可使用[承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)主机配置设置来设置此承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="4e01e-190">A hosting startup assembly can also be set using the [Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="4e01e-191">存在多个托管启动程序集时，将按列出程序集的顺序执行 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法。</span><span class="sxs-lookup"><span data-stu-id="4e01e-191">When multiple hosting startup assembles are present, their [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) methods are executed in the order that the assemblies are listed.</span></span>

## <a name="activation"></a><span data-ttu-id="4e01e-192">激活</span><span class="sxs-lookup"><span data-stu-id="4e01e-192">Activation</span></span>

<span data-ttu-id="4e01e-193">承载启动激活的选项包括：</span><span class="sxs-lookup"><span data-stu-id="4e01e-193">Options for hosting startup activation are:</span></span>

* <span data-ttu-id="4e01e-194">[运行时存储](#runtime-store) &ndash; 激活无需用于激活的编译时引用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-194">[Runtime store](#runtime-store) &ndash; Activation doesn't require a compile-time reference for activation.</span></span> <span data-ttu-id="4e01e-195">示例应用将承载启动程序集和依赖项文件放入文件夹“deployment”，以便在多计算机环境中部署承载启动。</span><span class="sxs-lookup"><span data-stu-id="4e01e-195">The sample app places the hosting startup assembly and dependencies files into a folder, *deployment*, to facilitate deployment of the hosting startup in a multimachine environment.</span></span> <span data-ttu-id="4e01e-196">“deployment”文件夹还包括 PowerShell 脚本，该脚本可在部署系统上创建或修改环境变量以启用承载启动。</span><span class="sxs-lookup"><span data-stu-id="4e01e-196">The *deployment* folder also includes a PowerShell script that creates or modifies environment variables on the deployment system to enable the hosting startup.</span></span>
* <span data-ttu-id="4e01e-197">激活所需的编译时引用</span><span class="sxs-lookup"><span data-stu-id="4e01e-197">Compile-time reference required for activation</span></span>
  * [<span data-ttu-id="4e01e-198">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4e01e-198">NuGet package</span></span>](#nuget-package)
  * [<span data-ttu-id="4e01e-199">项目 bin 文件夹</span><span class="sxs-lookup"><span data-stu-id="4e01e-199">Project bin folder</span></span>](#project-bin-folder)

### <a name="runtime-store"></a><span data-ttu-id="4e01e-200">运行时存储</span><span class="sxs-lookup"><span data-stu-id="4e01e-200">Runtime store</span></span>

<span data-ttu-id="4e01e-201">承载启动实现位于[运行时存储](/dotnet/core/deploying/runtime-store)中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-201">The hosting startup implementation is placed in the [runtime store](/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="4e01e-202">增强型应用无需对程序集进行编译时引用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-202">A compile-time reference to the assembly isn't required by the enhanced app.</span></span>

<span data-ttu-id="4e01e-203">构建承载启动后，承载启动的项目文件可作为 [dotnet store](/dotnet/core/tools/dotnet-store) 命令的清单文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-203">After the hosting startup is built, the hosting startup's project file serves as the manifest file for the [dotnet store](/dotnet/core/tools/dotnet-store) command.</span></span>

```console
dotnet store --manifest <PROJECT_FILE> --runtime <RUNTIME_IDENTIFIER>
```

<span data-ttu-id="4e01e-204">此命令将承载启动程序集和不属于共享框架的其他依赖项置于用户配置文件的运行时存储中：</span><span class="sxs-lookup"><span data-stu-id="4e01e-204">This command places the hosting startup assembly and other dependencies that aren't part of the shared framework in the user profile's runtime store at:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-205">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-205">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-206">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-206">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-207">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-207">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

<span data-ttu-id="4e01e-208">如果希望将程序集和依赖项放在可供全局使用的位置，请使用以下路径将 `-o|--output` 选项添加到 `dotnet store` 命令：</span><span class="sxs-lookup"><span data-stu-id="4e01e-208">If you desire to place the assembly and dependencies for global use, add the `-o|--output` option to the `dotnet store` command with the following path:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-209">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-209">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-210">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-210">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-211">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-211">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

<span data-ttu-id="4e01e-212">**修改并放置承载启动的依赖项文件**</span><span class="sxs-lookup"><span data-stu-id="4e01e-212">**Modify and place the hosting startup's dependencies file**</span></span>

<span data-ttu-id="4e01e-213">运行时位置在 \*.deps.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="4e01e-213">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="4e01e-214">若要激活增强功能，`runtime` 元素必须指定增强功能运行时程序集的位置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-214">To activate the enhancement, the `runtime` element must specify the location of the enhancement's runtime assembly.</span></span> <span data-ttu-id="4e01e-215">将 `runtime` 位置的前缀设为 `lib/<TARGET_FRAMEWORK_MONIKER>/`：</span><span class="sxs-lookup"><span data-stu-id="4e01e-215">Prefix the `runtime` location with `lib/<TARGET_FRAMEWORK_MONIKER>/`:</span></span>

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="4e01e-216">在示例代码（StartupDiagnostics 项目）中，\*.deps.json 文件的修改由 [PowerShell](/powershell/scripting/powershell-scripting) 脚本执行。</span><span class="sxs-lookup"><span data-stu-id="4e01e-216">In the sample code (*StartupDiagnostics* project), modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="4e01e-217">PowerShell 脚本由项目文件中的生成目标自动触发。</span><span class="sxs-lookup"><span data-stu-id="4e01e-217">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

<span data-ttu-id="4e01e-218">该实现的 \*.deps.json 文件必须位于可访问的位置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-218">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="4e01e-219">若要实现按用户使用，将文件置于用户配置文件 `.dotnet` 设置的 additonalDeps 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="4e01e-219">For per-user use, place the file in the *additonalDeps* folder of the user profile's `.dotnet` settings:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-220">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-220">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-221">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-221">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-222">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-222">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

<span data-ttu-id="4e01e-223">若要实现全局使用，将文件置于 .NET Core 安装的 additonalDeps 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="4e01e-223">For global use, place the file in the *additonalDeps* folder of the .NET Core installation:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-224">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-224">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-225">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-225">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-226">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-226">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

<span data-ttu-id="4e01e-227">共享框架版本反映目标应用使用的共享运行时的版本。</span><span class="sxs-lookup"><span data-stu-id="4e01e-227">The shared framework version reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="4e01e-228">共享运行时显示在 \*.runtimeconfig.json 文件中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-228">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="4e01e-229">在示例应用 (HostingStartupApp) 中，共享运行时在 HostingStartupApp.runtimeconfig.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="4e01e-229">In the sample app (*HostingStartupApp*), the shared runtime is specified in the *HostingStartupApp.runtimeconfig.json* file.</span></span>

<span data-ttu-id="4e01e-230">**列出承载启动的依赖项文件**</span><span class="sxs-lookup"><span data-stu-id="4e01e-230">**List the hosting startup's dependencies file**</span></span>

<span data-ttu-id="4e01e-231">`DOTNET_ADDITIONAL_DEPS` 环境变量中列出了实现的 \*.deps.json 文件的位置。</span><span class="sxs-lookup"><span data-stu-id="4e01e-231">The location of the implementation's *\*.deps.json* file is listed in the `DOTNET_ADDITIONAL_DEPS` environment variable.</span></span>

<span data-ttu-id="4e01e-232">如果文件放在用户配置文件的 .dotnet 文件夹中，请将环境变量的值设置为：</span><span class="sxs-lookup"><span data-stu-id="4e01e-232">If the file is placed in the user profile's *.dotnet* folder, set the environment variable's value to:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-233">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-233">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-234">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-234">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-235">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-235">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

---

<span data-ttu-id="4e01e-236">如果将文件放置在 .NET Core 安装中以实现全局使用，则提供该文件的完整路径：</span><span class="sxs-lookup"><span data-stu-id="4e01e-236">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-237">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-237">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-238">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-238">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-239">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-239">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

---

<span data-ttu-id="4e01e-240">对于用于查找依赖项文件 (HostingStartupApp.runtimeconfig.json) 的示例应用 (HostingStartupApp)，依赖项文件位于用户的配置文件中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-240">For the sample app (*HostingStartupApp*) to find the dependencies file (*HostingStartupApp.runtimeconfig.json*), the dependencies file is placed in the user's profile.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="4e01e-241">Windows</span><span class="sxs-lookup"><span data-stu-id="4e01e-241">Windows</span></span>](#tab/windows)

<span data-ttu-id="4e01e-242">将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-242">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="4e01e-243">macOS</span><span class="sxs-lookup"><span data-stu-id="4e01e-243">macOS</span></span>](#tab/macos)

<span data-ttu-id="4e01e-244">将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-244">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="4e01e-245">Linux</span><span class="sxs-lookup"><span data-stu-id="4e01e-245">Linux</span></span>](#tab/linux)

<span data-ttu-id="4e01e-246">将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="4e01e-246">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

---

<span data-ttu-id="4e01e-247">有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="4e01e-247">For examples of how to set environment variables for various operating systems, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="4e01e-248">**部署**</span><span class="sxs-lookup"><span data-stu-id="4e01e-248">**Deployment**</span></span>

<span data-ttu-id="4e01e-249">为了便于在多计算机环境中部署托承载启动，示例应用在已发布的输出中创建一个“deployment”文件夹，其中包含：</span><span class="sxs-lookup"><span data-stu-id="4e01e-249">To facilitate the deployment of a hosting startup in a multimachine environment, the sample app creates a *deployment* folder in published output that contains:</span></span>

* <span data-ttu-id="4e01e-250">承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="4e01e-250">The hosting startup assembly.</span></span>
* <span data-ttu-id="4e01e-251">承载启动依赖项文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-251">The hosting startup dependencies file.</span></span>
* <span data-ttu-id="4e01e-252">PowerShell 脚本，用于创建或修改 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 和 `DOTNET_ADDITIONAL_DEPS` 以支持激活承载启动。</span><span class="sxs-lookup"><span data-stu-id="4e01e-252">A PowerShell script that creates or modifies the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` and `DOTNET_ADDITIONAL_DEPS` to support the activation of the hosting startup.</span></span> <span data-ttu-id="4e01e-253">从部署系统上的管理 PowerShell 命令提示符运行脚本。</span><span class="sxs-lookup"><span data-stu-id="4e01e-253">Run the script from an administrative PowerShell command prompt on the deployment system.</span></span>

### <a name="nuget-package"></a><span data-ttu-id="4e01e-254">NuGet 程序包</span><span class="sxs-lookup"><span data-stu-id="4e01e-254">NuGet package</span></span>

<span data-ttu-id="4e01e-255">可在 NuGet 包中提供承载启动增强。</span><span class="sxs-lookup"><span data-stu-id="4e01e-255">A hosting startup enhancement can be provided in a NuGet package.</span></span> <span data-ttu-id="4e01e-256">该包含有 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e01e-256">The package has a `HostingStartup` attribute.</span></span> <span data-ttu-id="4e01e-257">包提供的承载启动类型使用以下任一方法提供给应用：</span><span class="sxs-lookup"><span data-stu-id="4e01e-257">The hosting startup types provided by the package are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="4e01e-258">增强型应用的项目文件在应用的项目文件（编译时引用）中为承载启动提供了包引用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-258">The enhanced app's project file makes a package reference for the hosting startup in the app's project file (a compile-time reference).</span></span> <span data-ttu-id="4e01e-259">有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-259">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="4e01e-260">此方法适用于已发布到 [nuget.org](https://www.nuget.org/) 的承载启动程序集包。</span><span class="sxs-lookup"><span data-stu-id="4e01e-260">This approach applies to a hosting startup assembly package published to [nuget.org](https://www.nuget.org/).</span></span>
* <span data-ttu-id="4e01e-261">承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="4e01e-261">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

<span data-ttu-id="4e01e-262">有关 NuGet 包和运行时存储的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="4e01e-262">For more information on NuGet packages and the runtime store, see the following topics:</span></span>

* [<span data-ttu-id="4e01e-263">如何使用跨平台工具创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4e01e-263">How to Create a NuGet Package with Cross Platform Tools</span></span>](/dotnet/core/deploying/creating-nuget-packages)
* [<span data-ttu-id="4e01e-264">发布包</span><span class="sxs-lookup"><span data-stu-id="4e01e-264">Publishing packages</span></span>](/nuget/create-packages/publish-a-package)
* [<span data-ttu-id="4e01e-265">运行时包存储</span><span class="sxs-lookup"><span data-stu-id="4e01e-265">Runtime package store</span></span>](/dotnet/core/deploying/runtime-store)

### <a name="project-bin-folder"></a><span data-ttu-id="4e01e-266">项目 bin 文件夹</span><span class="sxs-lookup"><span data-stu-id="4e01e-266">Project bin folder</span></span>

<span data-ttu-id="4e01e-267">承载启动增强功能可通过增强型应用中的 bin -deployed 程序集提供。</span><span class="sxs-lookup"><span data-stu-id="4e01e-267">A hosting startup enhancement can be provided by a *bin*-deployed assembly in the enhanced app.</span></span> <span data-ttu-id="4e01e-268">程序集提供的承载启动类型使用以下任一方法提供给应用：</span><span class="sxs-lookup"><span data-stu-id="4e01e-268">The hosting startup types provided by the assembly are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="4e01e-269">增强型应用的项目文件对承载启动进行了程序集引用（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="4e01e-269">The enhanced app's project file makes an assembly reference to the hosting startup (a compile-time reference).</span></span> <span data-ttu-id="4e01e-270">有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-270">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="4e01e-271">如果部署方案要求将已编译承载启动库的程序集（DLL 文件）移动到使用项目中或使用项目可访问的位置，并且对承载启动程序集进行编译时引用，此方法适用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-271">This approach applies when the deployment scenario calls for moving the compiled hosting startup library's assembly (DLL file) to the consuming project or to a location accessible by the consuming project and a compile-time reference is made to the hosting startup's assembly.</span></span>
* <span data-ttu-id="4e01e-272">承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="4e01e-272">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

## <a name="sample-code"></a><span data-ttu-id="4e01e-273">示例代码</span><span class="sxs-lookup"><span data-stu-id="4e01e-273">Sample code</span></span>

<span data-ttu-id="4e01e-274">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）演示了承载启动实现方案：</span><span class="sxs-lookup"><span data-stu-id="4e01e-274">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates hosting startup implementation scenarios:</span></span>

* <span data-ttu-id="4e01e-275">两个承载启动程序集（类库）分别设置一对内存中配置键值对：</span><span class="sxs-lookup"><span data-stu-id="4e01e-275">Two hosting startup assemblies (class libraries) set a pair of in-memory configuration key-value pairs each:</span></span>
  * <span data-ttu-id="4e01e-276">NuGet 包 (HostingStartupPackage)</span><span class="sxs-lookup"><span data-stu-id="4e01e-276">NuGet package (*HostingStartupPackage*)</span></span>
  * <span data-ttu-id="4e01e-277">类库 (HostingStartupLibrary)</span><span class="sxs-lookup"><span data-stu-id="4e01e-277">Class library (*HostingStartupLibrary*)</span></span>
* <span data-ttu-id="4e01e-278">从运行时存储部署的程序集 (StartupDiagnostics) 激活承载启动。</span><span class="sxs-lookup"><span data-stu-id="4e01e-278">A hosting startup is activated from a runtime store-deployed assembly (*StartupDiagnostics*).</span></span> <span data-ttu-id="4e01e-279">该程序集在启动时将两个中间件添加到应用，用于提供以下内容的诊断信息：</span><span class="sxs-lookup"><span data-stu-id="4e01e-279">The assembly adds two middlewares to the app at startup that provide diagnostic information on:</span></span>
  * <span data-ttu-id="4e01e-280">已注册服务</span><span class="sxs-lookup"><span data-stu-id="4e01e-280">Registered services</span></span>
  * <span data-ttu-id="4e01e-281">地址（方案、主机、基路径、路径、查询字符串）</span><span class="sxs-lookup"><span data-stu-id="4e01e-281">Address (scheme, host, path base, path, query string)</span></span>
  * <span data-ttu-id="4e01e-282">连接（远程 IP、远程端口、本地 IP、本地端口、客户端证书）</span><span class="sxs-lookup"><span data-stu-id="4e01e-282">Connection (remote IP, remote port, local IP, local port, client certificate)</span></span>
  * <span data-ttu-id="4e01e-283">请求标头</span><span class="sxs-lookup"><span data-stu-id="4e01e-283">Request headers</span></span>
  * <span data-ttu-id="4e01e-284">环境变量</span><span class="sxs-lookup"><span data-stu-id="4e01e-284">Environment variables</span></span>

<span data-ttu-id="4e01e-285">运行示例：</span><span class="sxs-lookup"><span data-stu-id="4e01e-285">To run the sample:</span></span>

<span data-ttu-id="4e01e-286">**从 NuGet 包激活**</span><span class="sxs-lookup"><span data-stu-id="4e01e-286">**Activation from a NuGet package**</span></span>

1. <span data-ttu-id="4e01e-287">使用 [dotnet pack](/dotnet/core/tools/dotnet-pack) 命令编译 HostingStartupPackage 包。</span><span class="sxs-lookup"><span data-stu-id="4e01e-287">Compile the *HostingStartupPackage* package with the [dotnet pack](/dotnet/core/tools/dotnet-pack) command.</span></span>
1. <span data-ttu-id="4e01e-288">将包的程序集名称 HostingStartupPackage 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-288">Add the package's assembly name of the *HostingStartupPackage* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="4e01e-289">编译并运行应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-289">Compile and run the app.</span></span> <span data-ttu-id="4e01e-290">增强型应用中存在包引用（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="4e01e-290">A package reference is present in the enhanced app (a compile-time reference).</span></span> <span data-ttu-id="4e01e-291">应用项目文件中的 `<PropertyGroup>` 指定包项目的输出 (../HostingStartupPackage/bin/Debug) 作为包源。</span><span class="sxs-lookup"><span data-stu-id="4e01e-291">A `<PropertyGroup>` in the app's project file specifies the package project's output (*../HostingStartupPackage/bin/Debug*) as a package source.</span></span> <span data-ttu-id="4e01e-292">这允许应用使用该包而无需将包上传到 [nuget.org](https://www.nuget.org/)。有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。</span><span class="sxs-lookup"><span data-stu-id="4e01e-292">This allows the app to use the package without uploading the package to [nuget.org](https://www.nuget.org/). For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <PropertyGroup>
     <RestoreSources>$(RestoreSources);https://api.nuget.org/v3/index.json;../HostingStartupPackage/bin/Debug</RestoreSources>
   </PropertyGroup>
   ```
1. <span data-ttu-id="4e01e-293">观察到索引页呈现的服务配置键值与包的 `ServiceKeyInjection.Configure` 方法设置的值匹配。</span><span class="sxs-lookup"><span data-stu-id="4e01e-293">Observe that the service configuration key values rendered by the Index page match the values set by the package's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="4e01e-294">如果更改并重新编译 HostingStartupPackage 项目，请清除本地 NuGet 包缓存，确保 HostingStartupApp 从本地缓存中收到更新后的包而不是旧包。</span><span class="sxs-lookup"><span data-stu-id="4e01e-294">If you make changes to the *HostingStartupPackage* project and recompile it, clear the local NuGet package caches to ensure that the *HostingStartupApp* receives the updated package and not a stale package from the local cache.</span></span> <span data-ttu-id="4e01e-295">要清除本地 NuGet 缓存，请执行以下 [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) 命令：</span><span class="sxs-lookup"><span data-stu-id="4e01e-295">To clear the local NuGet caches, execute the following [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) command:</span></span>

```console
dotnet nuget locals all --clear
```

<span data-ttu-id="4e01e-296">**从类库激活**</span><span class="sxs-lookup"><span data-stu-id="4e01e-296">**Activation from a class library**</span></span>

1. <span data-ttu-id="4e01e-297">使用 [dotnet build](/dotnet/core/tools/dotnet-build) 命令编译 HostingStartupLibrary 类库。</span><span class="sxs-lookup"><span data-stu-id="4e01e-297">Compile the *HostingStartupLibrary* class library with the [dotnet build](/dotnet/core/tools/dotnet-build) command.</span></span>
1. <span data-ttu-id="4e01e-298">将类库的程序集名称 HostingStartupLibrary 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-298">Add the class library's assembly name of *HostingStartupLibrary* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="4e01e-299">bin - 通过将类库编译输出中的 HostingStartupLibrary.dll 文件复制到应用的 bin/Debug 文件夹，将类库程序集部署到应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-299">*bin*-deploy the class library's assembly to the app by copying the *HostingStartupLibrary.dll* file from the class library's compiled output to the app's *bin/Debug* folder.</span></span>
1. <span data-ttu-id="4e01e-300">编译并运行应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-300">Compile and run the app.</span></span> <span data-ttu-id="4e01e-301">应用项目文件中的 `<ItemGroup>` 引用类库的程序集 (.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll)（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="4e01e-301">An `<ItemGroup>` in the app's project file references the class library's assembly (*.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll*) (a compile-time reference).</span></span> <span data-ttu-id="4e01e-302">有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。</span><span class="sxs-lookup"><span data-stu-id="4e01e-302">For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <ItemGroup>
     <Reference Include=".\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll">
       <HintPath>.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll</HintPath>
       <SpecificVersion>False</SpecificVersion>
     </Reference>
   </ItemGroup>
   ```
1. <span data-ttu-id="4e01e-303">观察到索引页呈现的服务配置键值与类库的 `ServiceKeyInjection.Configure` 方法设置的值匹配。</span><span class="sxs-lookup"><span data-stu-id="4e01e-303">Observe that the service configuration key values rendered by the Index page match the values set by the class library's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="4e01e-304">**从运行时存储部署的程序集激活**</span><span class="sxs-lookup"><span data-stu-id="4e01e-304">**Activation from a runtime store-deployed assembly**</span></span>

1. <span data-ttu-id="4e01e-305">StartupDiagnostics 项目使用 [PowerShell](/powershell/scripting/powershell-scripting) 修改其 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-305">The *StartupDiagnostics* project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="4e01e-306">默认情况下，Windows 7 SP1 和 Windows Server 2008 R2 SP1 及以后版本的 Windows 上安装有 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4e01e-306">PowerShell is installed by default on Windows starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="4e01e-307">若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core)。</span><span class="sxs-lookup"><span data-stu-id="4e01e-307">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core).</span></span>
1. <span data-ttu-id="4e01e-308">构建 StartupDiagnostics 项目。</span><span class="sxs-lookup"><span data-stu-id="4e01e-308">Build the *StartupDiagnostics* project.</span></span> <span data-ttu-id="4e01e-309">构建项目后，会自动生成项目文件中的构建目标：</span><span class="sxs-lookup"><span data-stu-id="4e01e-309">After the project is built, a build target in the project file automatically:</span></span>
   * <span data-ttu-id="4e01e-310">触发 PowerShell 脚本以修改 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-310">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="4e01e-311">将 StartupDiagnostics.deps.json 文件移动到用户配置文件的 additionalDeps 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4e01e-311">Moves the *StartupDiagnostics.deps.json* file to the user profile's *additionalDeps* folder.</span></span>
1. <span data-ttu-id="4e01e-312">在承载启动目录的命令提示符处执行 `dotnet store` 命令，将程序集及其依赖项存储在用户配置文件的运行时存储中：</span><span class="sxs-lookup"><span data-stu-id="4e01e-312">Execute the `dotnet store` command at a command prompt in the hosting startup's directory to store the assembly and its dependencies in the user profile's runtime store:</span></span>

   ```console
   dotnet store --manifest StartupDiagnostics.csproj --runtime <RID>
   ```
   <span data-ttu-id="4e01e-313">对于 Windows，该命令使用 `win7-x64` [运行时标识符 (RID)](/dotnet/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="4e01e-313">For Windows, the command uses the `win7-x64` [runtime identifier (RID)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="4e01e-314">为其他运行时提供承载启动时，请替换为正确的 RID。</span><span class="sxs-lookup"><span data-stu-id="4e01e-314">When providing the hosting startup for a different runtime, substitute the correct RID.</span></span>
1. <span data-ttu-id="4e01e-315">设置环境变量：</span><span class="sxs-lookup"><span data-stu-id="4e01e-315">Set the environment variables:</span></span>
   * <span data-ttu-id="4e01e-316">将程序集名称 StartupDiagnostics 的添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="4e01e-316">Add the assembly name of *StartupDiagnostics* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
   * <span data-ttu-id="4e01e-317">在 Windows 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`。</span><span class="sxs-lookup"><span data-stu-id="4e01e-317">On Windows, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`.</span></span> <span data-ttu-id="4e01e-318">在 macOS/Linux 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`，其中 `<USER>` 是包含承载启动的用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="4e01e-318">On macOS/Linux, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`, where `<USER>` is the user profile that contains the hosting startup.</span></span>
1. <span data-ttu-id="4e01e-319">运行示例应用。</span><span class="sxs-lookup"><span data-stu-id="4e01e-319">Run the sample app.</span></span>
1. <span data-ttu-id="4e01e-320">请求 `/services` 终结点以查看应用的注册服务。</span><span class="sxs-lookup"><span data-stu-id="4e01e-320">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="4e01e-321">请求 `/diag` 终结点以查看诊断信息。</span><span class="sxs-lookup"><span data-stu-id="4e01e-321">Request the `/diag` endpoint to see the diagnostic information.</span></span>
