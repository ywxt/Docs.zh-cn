---
title: 在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用
author: guardrex
description: 了解如何使用 IHostingStartup 从外部程序集增强 ASP.NET Core 应用。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: 47d3a64ce0cc543162a066eeeaa0aaaf7dc96a5f
ms.sourcegitcommit: 0d6f151e69c159d776ed0142773279e645edbc0a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2018
ms.locfileid: "35415003"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a><span data-ttu-id="ead3f-103">在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用</span><span class="sxs-lookup"><span data-stu-id="ead3f-103">Enhance an app from an external assembly in ASP.NET Core with IHostingStartup</span></span>

<span data-ttu-id="ead3f-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ead3f-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ead3f-105">通过 [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 实现，可在启动时从应用 `Startup` 类之外的外部程序集向应用添加增强功能。</span><span class="sxs-lookup"><span data-stu-id="ead3f-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="ead3f-106">例如，外部工具库可以使用 `IHostingStartup` 实现为应用提供其他配置提供程序或服务。</span><span class="sxs-lookup"><span data-stu-id="ead3f-106">For example, an external tooling library can use an `IHostingStartup` implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="ead3f-107">ASP.NET Core 2.0 及更高版本提供 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ead3f-107">`IHostingStartup` *is available in ASP.NET Core 2.0 and later.*</span></span>

<span data-ttu-id="ead3f-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="ead3f-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="ead3f-109">发现加载的承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="ead3f-109">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="ead3f-110">若要发现应用或库加载的承载启动程序集，请启用日志记录并检查应用程序日志。</span><span class="sxs-lookup"><span data-stu-id="ead3f-110">To discover hosting startup assemblies loaded by the app or by libraries, enable logging and check the application logs.</span></span> <span data-ttu-id="ead3f-111">记录加载程序集时发生的错误。</span><span class="sxs-lookup"><span data-stu-id="ead3f-111">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="ead3f-112">会在调试级别记录加载的承载启动程序集，并记录所有错误。</span><span class="sxs-lookup"><span data-stu-id="ead3f-112">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

<span data-ttu-id="ead3f-113">示例应用将 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 读入 `string` 数组并在应用的索引页中显示结果：</span><span class="sxs-lookup"><span data-stu-id="ead3f-113">The sample app reads the [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) into a `string` array and displays the result in the app's Index page:</span></span>

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="ead3f-114">禁用承载启动程序集的自动加载</span><span class="sxs-lookup"><span data-stu-id="ead3f-114">Disable automatic loading of hosting startup assemblies</span></span>

<span data-ttu-id="ead3f-115">有两种方法可用于禁用承载启动程序集的自动加载：</span><span class="sxs-lookup"><span data-stu-id="ead3f-115">There are two ways to disable the automatic loading of hosting startup assemblies:</span></span>

* <span data-ttu-id="ead3f-116">设置[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="ead3f-116">Set the [Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="ead3f-117">设置 `ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="ead3f-117">Set the `ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>

<span data-ttu-id="ead3f-118">当主机设置或环境变量设置为 `true` 或 `1` 时，不会自动加载承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="ead3f-118">When either the host setting or the environment variable is set to `true` or `1`, hosting startup assemblies aren't automatically loaded.</span></span> <span data-ttu-id="ead3f-119">如果同时设置了两者，则行为由主机设置控制。</span><span class="sxs-lookup"><span data-stu-id="ead3f-119">If both are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="ead3f-120">如果使用主机设置或环境变量来禁用承载启动程序集，将实现全局性禁用，并可能会禁用应用的多个特征。</span><span class="sxs-lookup"><span data-stu-id="ead3f-120">Disabling hosting startup assemblies using the host setting or environment variable disables them globally and may disable several characteristics of an app.</span></span> <span data-ttu-id="ead3f-121">当前无法选择性地禁用由库添加的承载启动程序集，除非库提供自己的配置选项。</span><span class="sxs-lookup"><span data-stu-id="ead3f-121">It isn't currently possible to selectively disable a hosting startup assembly added by a library unless the library offers its own configuration option.</span></span> <span data-ttu-id="ead3f-122">未来的一个版本将提供选择性禁用承载启动程序集的功能（请参阅 [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)）。</span><span class="sxs-lookup"><span data-stu-id="ead3f-122">A future release will offer the ability to selectively disable hosting startup assemblies (see [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)).</span></span>

## <a name="implement-ihostingstartup"></a><span data-ttu-id="ead3f-123">实现 IHostingStartup</span><span class="sxs-lookup"><span data-stu-id="ead3f-123">Implement IHostingStartup</span></span>

### <a name="create-the-assembly"></a><span data-ttu-id="ead3f-124">创建程序集</span><span class="sxs-lookup"><span data-stu-id="ead3f-124">Create the assembly</span></span>

<span data-ttu-id="ead3f-125">`IHostingStartup` 增强功能基于没有入口点的控制台应用部署为程序集。</span><span class="sxs-lookup"><span data-stu-id="ead3f-125">An `IHostingStartup` enhancement is deployed as an assembly based on a console app without an entry point.</span></span> <span data-ttu-id="ead3f-126">程序集引用 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 包：</span><span class="sxs-lookup"><span data-stu-id="ead3f-126">The assembly references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupEnhancement.csproj)]

<span data-ttu-id="ead3f-127">生成 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 时，[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性将类标识为 `IHostingStartup` 的实现，用于加载和执行。</span><span class="sxs-lookup"><span data-stu-id="ead3f-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="ead3f-128">在下面的示例中，命名空间为 `StartupEnhancement`，类为 `StartupEnhancementHostingStartup`：</span><span class="sxs-lookup"><span data-stu-id="ead3f-128">In the following example, the namespace is `StartupEnhancement`, and the class is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="ead3f-129">类实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ead3f-129">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="ead3f-130">类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。</span><span class="sxs-lookup"><span data-stu-id="ead3f-130">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="ead3f-131">用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。</span><span class="sxs-lookup"><span data-stu-id="ead3f-131">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configruation provided by the hosting startup assembly.</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="ead3f-132">生成 `IHostingStartup` 项目时，依赖项文件 (\*.deps.json) 将程序集的 `runtime` 位置设为 bin 文件夹：</span><span class="sxs-lookup"><span data-stu-id="ead3f-132">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="ead3f-133">仅显示部分文件。</span><span class="sxs-lookup"><span data-stu-id="ead3f-133">Only part of the file is shown.</span></span> <span data-ttu-id="ead3f-134">示例中程序集的名称是 `StartupEnhancement`。</span><span class="sxs-lookup"><span data-stu-id="ead3f-134">The assembly name in the example is `StartupEnhancement`.</span></span>

### <a name="update-the-dependencies-file"></a><span data-ttu-id="ead3f-135">更新依赖项文件</span><span class="sxs-lookup"><span data-stu-id="ead3f-135">Update the dependencies file</span></span>

<span data-ttu-id="ead3f-136">运行时位置在 \*.deps.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="ead3f-136">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="ead3f-137">若要激活增强功能，`runtime` 元素必须指定增强功能运行时程序集的位置。</span><span class="sxs-lookup"><span data-stu-id="ead3f-137">To active the enhancement, the `runtime` element must specify the location of the enhancement's runtime assembly.</span></span> <span data-ttu-id="ead3f-138">将 `runtime` 位置的前缀设为 `lib/<TARGET_FRAMEWORK_MONIKER>/`：</span><span class="sxs-lookup"><span data-stu-id="ead3f-138">Prefix the `runtime` location with `lib/<TARGET_FRAMEWORK_MONIKER>/`:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="ead3f-139">在示例应用中，\*.deps.json 文件的修改由 [PowerShell](/powershell/scripting/powershell-scripting) 脚本执行。</span><span class="sxs-lookup"><span data-stu-id="ead3f-139">In the sample app, modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="ead3f-140">PowerShell 脚本由项目文件中的生成目标自动触发。</span><span class="sxs-lookup"><span data-stu-id="ead3f-140">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

### <a name="enhancement-activation"></a><span data-ttu-id="ead3f-141">增强功能激活</span><span class="sxs-lookup"><span data-stu-id="ead3f-141">Enhancement activation</span></span>

<span data-ttu-id="ead3f-142">**放置程序集文件**</span><span class="sxs-lookup"><span data-stu-id="ead3f-142">**Place the assembly file**</span></span>

<span data-ttu-id="ead3f-143">`IHostingStartup` 实现的程序集文件必须以 bin 方式部署在应用中或放置在[运行时存储](/dotnet/core/deploying/runtime-store)中：</span><span class="sxs-lookup"><span data-stu-id="ead3f-143">The `IHostingStartup` implementation's assembly file must be *bin*-deployed in the app or placed in the [runtime store](/dotnet/core/deploying/runtime-store):</span></span>

<span data-ttu-id="ead3f-144">若要实现按用户使用，将程序集放入用户配置文件的运行时存储：</span><span class="sxs-lookup"><span data-stu-id="ead3f-144">For per-user use, place the assembly in the user profile's runtime store at:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

<span data-ttu-id="ead3f-145">若要实现全局使用，将程序集放入 .NET Core 安装的运行时存储：</span><span class="sxs-lookup"><span data-stu-id="ead3f-145">For global use, place the assembly in the .NET Core installation's runtime store:</span></span>

```
<DRIVE>\Program Files\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

<span data-ttu-id="ead3f-146">将程序集部署到运行时存储时，可能也会部署符号文件，但增强功能的运行无需此文件。</span><span class="sxs-lookup"><span data-stu-id="ead3f-146">When deploying the assembly to the runtime store, the symbols file may be deployed as well but isn't required for the enhancement to work.</span></span>

<span data-ttu-id="ead3f-147">**放置依赖项文件**</span><span class="sxs-lookup"><span data-stu-id="ead3f-147">**Place the dependencies file**</span></span>

<span data-ttu-id="ead3f-148">该实现的 \*.deps.json 文件必须位于可访问的位置。</span><span class="sxs-lookup"><span data-stu-id="ead3f-148">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="ead3f-149">若要实现按用户使用，将文件置于用户配置文件 `.dotnet` 设置的 `additonalDeps`文件夹中：</span><span class="sxs-lookup"><span data-stu-id="ead3f-149">For per-user use, place the file in the `additonalDeps` folder of the user profile's `.dotnet` settings:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

<span data-ttu-id="ead3f-150">若要实现全局使用，将文件置于 .NET Core 安装的 `additonalDeps` 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="ead3f-150">For global use, place the file in the `additonalDeps` folder of the .NET Core installation:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

<span data-ttu-id="ead3f-151">共享框架版本反映目标应用使用的共享运行时的版本。</span><span class="sxs-lookup"><span data-stu-id="ead3f-151">The shared framework version reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="ead3f-152">共享运行时显示在 \*.runtimeconfig.json 文件中。</span><span class="sxs-lookup"><span data-stu-id="ead3f-152">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="ead3f-153">在示例应用中，共享运行时在 HostingStartupSample.runtimeconfig.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="ead3f-153">In the sample app, the shared runtime is specified in the *HostingStartupSample.runtimeconfig.json* file.</span></span>

<span data-ttu-id="ead3f-154">**设置环境变量**</span><span class="sxs-lookup"><span data-stu-id="ead3f-154">**Set environment variables**</span></span>

<span data-ttu-id="ead3f-155">在使用该增强功能的应用的上下文中设置以下环境变量。</span><span class="sxs-lookup"><span data-stu-id="ead3f-155">Set the following environment variables in the context of the app that uses the enhancement.</span></span>

<span data-ttu-id="ead3f-156">ASPNETCORE_HOSTINGSTARTUPASSEMBLIES</span><span class="sxs-lookup"><span data-stu-id="ead3f-156">ASPNETCORE_HOSTINGSTARTUPASSEMBLIES</span></span>

<span data-ttu-id="ead3f-157">仅扫描承载启动程序集以查找 `HostingStartupAttribute`。</span><span class="sxs-lookup"><span data-stu-id="ead3f-157">Only hosting startup assemblies are scanned for the `HostingStartupAttribute`.</span></span> <span data-ttu-id="ead3f-158">在此环境变量中提供实现的程序集名称。</span><span class="sxs-lookup"><span data-stu-id="ead3f-158">The assembly name of the implementation is provided in this environment variable.</span></span> <span data-ttu-id="ead3f-159">示例应用将此值设置为 `StartupDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="ead3f-159">The sample app sets this value to `StartupDiagnostics`.</span></span>

<span data-ttu-id="ead3f-160">还可使用[承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)主机配置设置来设置此值。</span><span class="sxs-lookup"><span data-stu-id="ead3f-160">The value can also be set using the [Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="ead3f-161">存在多个托管启动程序集时，将按列出程序集的顺序执行 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法。</span><span class="sxs-lookup"><span data-stu-id="ead3f-161">When multiple hosting startup assembles are present, their [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) methods are executed in the order that the assemblies are listed.</span></span>

<span data-ttu-id="ead3f-162">DOTNET_ADDITIONAL_DEPS</span><span class="sxs-lookup"><span data-stu-id="ead3f-162">DOTNET_ADDITIONAL_DEPS</span></span>

<span data-ttu-id="ead3f-163">实现的 \*.deps.json 文件的位置。</span><span class="sxs-lookup"><span data-stu-id="ead3f-163">The location of the implementation's *\*.deps.json* file.</span></span>

<span data-ttu-id="ead3f-164">如果将文件放置在用户配置文件的 .dotnet 文件夹中以实现按用户使用：</span><span class="sxs-lookup"><span data-stu-id="ead3f-164">If the file is placed in the user profile's *.dotnet* folder for per-user use:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

<span data-ttu-id="ead3f-165">如果将文件放置在 .NET Core 安装中以实现全局使用，则提供该文件的完整路径：</span><span class="sxs-lookup"><span data-stu-id="ead3f-165">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

<span data-ttu-id="ead3f-166">示例应用将此值设置为：</span><span class="sxs-lookup"><span data-stu-id="ead3f-166">The sample app sets this value to:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

<span data-ttu-id="ead3f-167">有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="ead3f-167">For examples of how to set environment variables for various operating systems, see [Use multiple environments](xref:fundamentals/environments).</span></span>

## <a name="sample-app"></a><span data-ttu-id="ead3f-168">示例应用</span><span class="sxs-lookup"><span data-stu-id="ead3f-168">Sample app</span></span>

<span data-ttu-id="ead3f-169">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）使用 `IHostingStartup` 创建一个诊断工具。</span><span class="sxs-lookup"><span data-stu-id="ead3f-169">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) uses `IHostingStartup` to create a diagnostics tool.</span></span> <span data-ttu-id="ead3f-170">该工具在启动时将两个中间件添加到应用，用于提供诊断信息：</span><span class="sxs-lookup"><span data-stu-id="ead3f-170">The tool adds two middlewares to the app at startup that provide diagnostic information:</span></span>

* <span data-ttu-id="ead3f-171">已注册服务</span><span class="sxs-lookup"><span data-stu-id="ead3f-171">Registered services</span></span>
* <span data-ttu-id="ead3f-172">地址：方案、主机、基路径、路径、查询字符串</span><span class="sxs-lookup"><span data-stu-id="ead3f-172">Address: scheme, host, path base, path, query string</span></span>
* <span data-ttu-id="ead3f-173">连接：远程 IP、远程端口、本地 IP、本地端口、客户端证书</span><span class="sxs-lookup"><span data-stu-id="ead3f-173">Connection: remote IP, remote port, local IP, local port, client certificate</span></span>
* <span data-ttu-id="ead3f-174">请求标头</span><span class="sxs-lookup"><span data-stu-id="ead3f-174">Request headers</span></span>
* <span data-ttu-id="ead3f-175">环境变量</span><span class="sxs-lookup"><span data-stu-id="ead3f-175">Environment variables</span></span>

<span data-ttu-id="ead3f-176">运行示例：</span><span class="sxs-lookup"><span data-stu-id="ead3f-176">To run the sample:</span></span>

1. <span data-ttu-id="ead3f-177">启动诊断项目使用 [PowerShell](/powershell/scripting/powershell-scripting) 修改其 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="ead3f-177">The Startup Diagnostic project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="ead3f-178">默认情况下，Windows 7 SP1 和 Windows Server 2008 R2 SP1 及以后版本的 Windows OS 上安装有 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ead3f-178">PowerShell is installed by default on Windows OS starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="ead3f-179">若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell)。</span><span class="sxs-lookup"><span data-stu-id="ead3f-179">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell).</span></span>
2. <span data-ttu-id="ead3f-180">生成启动诊断项目。</span><span class="sxs-lookup"><span data-stu-id="ead3f-180">Build the Startup Diagnostic project.</span></span> <span data-ttu-id="ead3f-181">项目文件中的生成目标：</span><span class="sxs-lookup"><span data-stu-id="ead3f-181">A build target in the project file:</span></span>
   * <span data-ttu-id="ead3f-182">将程序集和符号文件移动到用户配置文件的运行时存储。</span><span class="sxs-lookup"><span data-stu-id="ead3f-182">Moves the assembly and symbols files to the user profile's runtime store.</span></span>
   * <span data-ttu-id="ead3f-183">触发 PowerShell 脚本以修改 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="ead3f-183">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="ead3f-184">将 StartupDiagnostics.deps.json 文件移动到用户配置文件的 `additionalDeps` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ead3f-184">Moves the *StartupDiagnostics.deps.json* file to the user profile's `additionalDeps` folder.</span></span>
3. <span data-ttu-id="ead3f-185">设置环境变量：</span><span class="sxs-lookup"><span data-stu-id="ead3f-185">Set the environment variables:</span></span>
    * <span data-ttu-id="ead3f-186">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span><span class="sxs-lookup"><span data-stu-id="ead3f-186">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span></span>
    * <span data-ttu-id="ead3f-187">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span><span class="sxs-lookup"><span data-stu-id="ead3f-187">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span></span>
4. <span data-ttu-id="ead3f-188">运行示例应用。</span><span class="sxs-lookup"><span data-stu-id="ead3f-188">Run the sample app.</span></span>
5. <span data-ttu-id="ead3f-189">请求 `/services` 终结点以查看应用的注册服务。</span><span class="sxs-lookup"><span data-stu-id="ead3f-189">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="ead3f-190">请求 `/diag` 终结点以查看诊断信息。</span><span class="sxs-lookup"><span data-stu-id="ead3f-190">Request the `/diag` endpoint to see the diagnostic information.</span></span>
