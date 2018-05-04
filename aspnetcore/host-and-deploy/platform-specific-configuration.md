---
title: 在带有 IHostingStartup ASP.NET 核心中添加与特定于平台的配置的应用程序功能
author: guardrex
description: 了解如何从使用 IHostingStartup 实现的外部程序集添加到 ASP.NET 核心应用程序的功能。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/platform-specific-configuration
ms.openlocfilehash: 1b899e3d510be83cbd4c03368e5c2d6226706a66
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="add-app-features-with-a-platform-specific-configuration-in-aspnet-core"></a><span data-ttu-id="8185f-103">在 ASP.NET Core 中添加与特定于平台的配置的应用程序功能</span><span class="sxs-lookup"><span data-stu-id="8185f-103">Add app features with a platform-specific configuration in ASP.NET Core</span></span>

<span data-ttu-id="8185f-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8185f-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8185f-105">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)实现允许将从外部应用程序的外部程序集的功能添加到应用程序在启动`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="8185f-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding features to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="8185f-106">例如，可以使用外部工具库`IHostingStartup`实现，用于提供其他配置提供程序或服务添加到应用。</span><span class="sxs-lookup"><span data-stu-id="8185f-106">For example, an external tooling library can use an `IHostingStartup` implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="8185f-107">`IHostingStartup` *是可用在 ASP.NET 核心 2.0 及更高版本。*</span><span class="sxs-lookup"><span data-stu-id="8185f-107">`IHostingStartup` *is available in ASP.NET Core 2.0 and later.*</span></span>

<span data-ttu-id="8185f-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8185f-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="8185f-109">发现加载托管的启动程序集</span><span class="sxs-lookup"><span data-stu-id="8185f-109">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="8185f-110">若要发现由应用程序或库承载启动程序集加载，启用日志记录和检查应用程序日志。</span><span class="sxs-lookup"><span data-stu-id="8185f-110">To discover hosting startup assemblies loaded by the app or by libraries, enable logging and check the application logs.</span></span> <span data-ttu-id="8185f-111">发生所记录的加载程序集时的错误。</span><span class="sxs-lookup"><span data-stu-id="8185f-111">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="8185f-112">加载托管的启动程序集将记录的调试级别，并将记录所有错误。</span><span class="sxs-lookup"><span data-stu-id="8185f-112">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

<span data-ttu-id="8185f-113">示例应用程序读取[HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey)到`string`数组并在应用程序的索引页中显示结果：</span><span class="sxs-lookup"><span data-stu-id="8185f-113">The sample app reads the [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) into a `string` array and displays the result in the app's Index page:</span></span>

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="8185f-114">禁用托管启动程序集的自动的加载</span><span class="sxs-lookup"><span data-stu-id="8185f-114">Disable automatic loading of hosting startup assemblies</span></span>

<span data-ttu-id="8185f-115">有两种方法来禁用自动加载的托管启动程序集：</span><span class="sxs-lookup"><span data-stu-id="8185f-115">There are two ways to disable the automatic loading of hosting startup assemblies:</span></span>

* <span data-ttu-id="8185f-116">设置[防止承载启动](xref:fundamentals/hosting#prevent-hosting-startup)承载配置设置。</span><span class="sxs-lookup"><span data-stu-id="8185f-116">Set the [Prevent Hosting Startup](xref:fundamentals/hosting#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="8185f-117">设置`ASPNETCORE_preventHostingStartup`环境变量。</span><span class="sxs-lookup"><span data-stu-id="8185f-117">Set the `ASPNETCORE_preventHostingStartup` environment variable.</span></span>

<span data-ttu-id="8185f-118">当主机设置或环境变量设置为`true`或`1`、 宿主启动的程序集并不自动加载。</span><span class="sxs-lookup"><span data-stu-id="8185f-118">When either the host setting or the environment variable is set to `true` or `1`, hosting startup assemblies aren't automatically loaded.</span></span> <span data-ttu-id="8185f-119">如果两者都设置，主机设置将控制行为。</span><span class="sxs-lookup"><span data-stu-id="8185f-119">If both are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="8185f-120">禁用托管启动程序集使用的主机设置或环境变量全局禁用它们，并可能会禁用应用程序的多个功能。</span><span class="sxs-lookup"><span data-stu-id="8185f-120">Disabling hosting startup assemblies using the host setting or environment variable disables them globally and may disable several features of an app.</span></span> <span data-ttu-id="8185f-121">它不是当前可以有选择性地禁用添加由库，除非库提供其自己的配置选项的宿主启动程序集。</span><span class="sxs-lookup"><span data-stu-id="8185f-121">It isn't currently possible to selectively disable a hosting startup assembly added by a library unless the library offers its own configuration option.</span></span> <span data-ttu-id="8185f-122">未来版本将提供的功能有选择性地禁用宿主启动程序集 (请参阅[GitHub 发出 aspnet/宿主 # 1243年](https://github.com/aspnet/Hosting/pull/1243))。</span><span class="sxs-lookup"><span data-stu-id="8185f-122">A future release will offer the ability to selectively disable hosting startup assemblies (see [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)).</span></span>

## <a name="implement-ihostingstartup-features"></a><span data-ttu-id="8185f-123">实现 IHostingStartup 功能</span><span class="sxs-lookup"><span data-stu-id="8185f-123">Implement IHostingStartup features</span></span>

### <a name="create-the-assembly"></a><span data-ttu-id="8185f-124">创建程序集</span><span class="sxs-lookup"><span data-stu-id="8185f-124">Create the assembly</span></span>

<span data-ttu-id="8185f-125">`IHostingStartup`功能部署为基于没有入口点的控制台应用程序集。</span><span class="sxs-lookup"><span data-stu-id="8185f-125">An `IHostingStartup` feature is deployed as an assembly based on a console app without an entry point.</span></span> <span data-ttu-id="8185f-126">程序集引用[Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/)包：</span><span class="sxs-lookup"><span data-stu-id="8185f-126">The assembly references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupFeature.csproj)]

<span data-ttu-id="8185f-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute)属性将类标识的实现为`IHostingStartup`加载和执行生成时[IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)。</span><span class="sxs-lookup"><span data-stu-id="8185f-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="8185f-128">在下面的示例中，命名空间是`StartupFeature`，和类是`StartupFeatureHostingStartup`:</span><span class="sxs-lookup"><span data-stu-id="8185f-128">In the following example, the namespace is `StartupFeature`, and the class is `StartupFeatureHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet1)]

<span data-ttu-id="8185f-129">类实现`IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="8185f-129">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="8185f-130">类的[配置](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure)方法使用[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)将功能添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="8185f-130">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add features to an app:</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="8185f-131">生成时`IHostingStartup`项目依赖项文件 (*\*。 deps.json*) 设置`runtime`到程序集的位置*bin*文件夹：</span><span class="sxs-lookup"><span data-stu-id="8185f-131">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupFeature1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="8185f-132">显示仅属于文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-132">Only part of the file is shown.</span></span> <span data-ttu-id="8185f-133">在示例中的程序集名称是`StartupFeature`。</span><span class="sxs-lookup"><span data-stu-id="8185f-133">The assembly name in the example is `StartupFeature`.</span></span>

### <a name="update-the-dependencies-file"></a><span data-ttu-id="8185f-134">更新依赖项文件</span><span class="sxs-lookup"><span data-stu-id="8185f-134">Update the dependencies file</span></span>

<span data-ttu-id="8185f-135">中指定的运行时位置 *\*。 deps.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-135">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="8185f-136">为活动状态的功能，`runtime`元素必须指定该功能的运行时程序集的位置。</span><span class="sxs-lookup"><span data-stu-id="8185f-136">To active the feature, the `runtime` element must specify the location of the feature's runtime assembly.</span></span> <span data-ttu-id="8185f-137">前缀`runtime`位置与`lib/netcoreapp2.0/`:</span><span class="sxs-lookup"><span data-stu-id="8185f-137">Prefix the `runtime` location with `lib/netcoreapp2.0/`:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupFeature2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="8185f-138">在示例应用中，修改 *\*。 deps.json*文件执行的[PowerShell](/powershell/scripting/powershell-scripting)脚本。</span><span class="sxs-lookup"><span data-stu-id="8185f-138">In the sample app, modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="8185f-139">PowerShell 脚本自动触发项目文件中生成目标。</span><span class="sxs-lookup"><span data-stu-id="8185f-139">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

### <a name="feature-activation"></a><span data-ttu-id="8185f-140">功能激活</span><span class="sxs-lookup"><span data-stu-id="8185f-140">Feature activation</span></span>

<span data-ttu-id="8185f-141">**将程序集文件放在**</span><span class="sxs-lookup"><span data-stu-id="8185f-141">**Place the assembly file**</span></span>

<span data-ttu-id="8185f-142">`IHostingStartup`实现的程序集文件必须为*bin*-在应用程序部署或放入[运行时存储](/dotnet/core/deploying/runtime-store):</span><span class="sxs-lookup"><span data-stu-id="8185f-142">The `IHostingStartup` implementation's assembly file must be *bin*-deployed in the app or placed in the [runtime store](/dotnet/core/deploying/runtime-store):</span></span>

<span data-ttu-id="8185f-143">为每个用户使用，将在用户配置文件的运行时存储在该程序集：</span><span class="sxs-lookup"><span data-stu-id="8185f-143">For per-user use, place the assembly in the user profile's runtime store at:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="8185f-144">共用，将程序集放入.NET 核心安装的运行时存储：</span><span class="sxs-lookup"><span data-stu-id="8185f-144">For global use, place the assembly in the .NET Core installation's runtime store:</span></span>

```
<DRIVE>\Program Files\dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="8185f-145">在部署到运行时存储程序集，符号文件可能也部署，但并不是必需的功能正常工作。</span><span class="sxs-lookup"><span data-stu-id="8185f-145">When deploying the assembly to the runtime store, the symbols file may be deployed as well but isn't required for the feature to work.</span></span>

<span data-ttu-id="8185f-146">**将依赖项文件**</span><span class="sxs-lookup"><span data-stu-id="8185f-146">**Place the dependencies file**</span></span>

<span data-ttu-id="8185f-147">实现 *\*。 deps.json*文件必须在可访问的位置。</span><span class="sxs-lookup"><span data-stu-id="8185f-147">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="8185f-148">为每个用户使用，将该文件置于`additonalDeps`的用户配置文件的文件夹`.dotnet`设置：</span><span class="sxs-lookup"><span data-stu-id="8185f-148">For per-user use, place the file in the `additonalDeps` folder of the user profile's `.dotnet` settings:</span></span> 

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="8185f-149">共用，将该文件置于`additonalDeps`.NET 核心安装的文件夹：</span><span class="sxs-lookup"><span data-stu-id="8185f-149">For global use, place the file in the `additonalDeps` folder of the .NET Core installation:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="8185f-150">记下的版本， `2.0.0`，反映的共享的运行时的目标应用程序使用的版本。</span><span class="sxs-lookup"><span data-stu-id="8185f-150">Note the version, `2.0.0`, reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="8185f-151">共享的运行时所示 *\*。 runtimeconfig.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-151">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="8185f-152">在示例应用中，共享的运行时中指定*HostingStartupSample.runtimeconfig.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-152">In the sample app, the shared runtime is specified in the *HostingStartupSample.runtimeconfig.json* file.</span></span>

<span data-ttu-id="8185f-153">**设置环境变量**</span><span class="sxs-lookup"><span data-stu-id="8185f-153">**Set environment variables**</span></span>

<span data-ttu-id="8185f-154">在应用程序使用的功能的上下文中设置以下环境变量。</span><span class="sxs-lookup"><span data-stu-id="8185f-154">Set the following environment variables in the context of the app that uses the feature.</span></span>

<span data-ttu-id="8185f-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span><span class="sxs-lookup"><span data-stu-id="8185f-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span></span>

<span data-ttu-id="8185f-156">只有宿主启动的程序集扫描的`HostingStartupAttribute`。</span><span class="sxs-lookup"><span data-stu-id="8185f-156">Only hosting startup assemblies are scanned for the `HostingStartupAttribute`.</span></span> <span data-ttu-id="8185f-157">此环境变量中提供了实现的程序集名称。</span><span class="sxs-lookup"><span data-stu-id="8185f-157">The assembly name of the implementation is provided in this environment variable.</span></span> <span data-ttu-id="8185f-158">示例应用程序将此值设置为`StartupDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="8185f-158">The sample app sets this value to `StartupDiagnostics`.</span></span>

<span data-ttu-id="8185f-159">此外可以使用设置值[承载启动程序集](xref:fundamentals/hosting#hosting-startup-assemblies)承载配置设置。</span><span class="sxs-lookup"><span data-stu-id="8185f-159">The value can also be set using the [Hosting Startup Assemblies](xref:fundamentals/hosting#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="8185f-160">DOTNET\_其他\_DEPS</span><span class="sxs-lookup"><span data-stu-id="8185f-160">DOTNET\_ADDITIONAL\_DEPS</span></span>

<span data-ttu-id="8185f-161">实现的位置 *\*。 deps.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-161">The location of the implementation's *\*.deps.json* file.</span></span>

<span data-ttu-id="8185f-162">如果将文件放在用户配置文件的 *.dotnet*为每个用户使用的文件夹：</span><span class="sxs-lookup"><span data-stu-id="8185f-162">If the file is placed in the user profile's *.dotnet* folder for per-user use:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

<span data-ttu-id="8185f-163">如果该文件放置在共用的.NET Core 安装中，提供该文件的完整路径：</span><span class="sxs-lookup"><span data-stu-id="8185f-163">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\<FEATURE_ASSEMBLY_NAME>.deps.json
```

<span data-ttu-id="8185f-164">示例应用程序将此值设置为：</span><span class="sxs-lookup"><span data-stu-id="8185f-164">The sample app sets this value to:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

<span data-ttu-id="8185f-165">有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="8185f-165">For examples of how to set environment variables for various operating systems, see [Work with multiple environments](xref:fundamentals/environments).</span></span>

## <a name="sample-app"></a><span data-ttu-id="8185f-166">示例应用程序</span><span class="sxs-lookup"><span data-stu-id="8185f-166">Sample app</span></span>

<span data-ttu-id="8185f-167">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample)) 使用`IHostingStartup`若要创建一个诊断工具。</span><span class="sxs-lookup"><span data-stu-id="8185f-167">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) uses `IHostingStartup` to create a diagnostics tool.</span></span> <span data-ttu-id="8185f-168">该工具将两个中间件添加到提供的诊断信息的启动时的应用：</span><span class="sxs-lookup"><span data-stu-id="8185f-168">The tool adds two middlewares to the app at startup that provide diagnostic information:</span></span>

* <span data-ttu-id="8185f-169">已注册的服务</span><span class="sxs-lookup"><span data-stu-id="8185f-169">Registered services</span></span>
* <span data-ttu-id="8185f-170">地址： 方案、 主机、 基路径、 路径、 查询字符串</span><span class="sxs-lookup"><span data-stu-id="8185f-170">Address: scheme, host, path base, path, query string</span></span>
* <span data-ttu-id="8185f-171">连接： 远程 IP、 远程端口、 本地 IP，本地端口，客户端证书</span><span class="sxs-lookup"><span data-stu-id="8185f-171">Connection: remote IP, remote port, local IP, local port, client certificate</span></span>
* <span data-ttu-id="8185f-172">请求标头</span><span class="sxs-lookup"><span data-stu-id="8185f-172">Request headers</span></span>
* <span data-ttu-id="8185f-173">环境变量</span><span class="sxs-lookup"><span data-stu-id="8185f-173">Environment variables</span></span>

<span data-ttu-id="8185f-174">若要运行示例：</span><span class="sxs-lookup"><span data-stu-id="8185f-174">To run the sample:</span></span>

1. <span data-ttu-id="8185f-175">启动诊断项目使用[PowerShell](/powershell/scripting/powershell-scripting)若要修改其*StartupDiagnostics.deps.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-175">The Startup Diagnostic project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="8185f-176">默认情况下，从 Windows 7 SP1 和 Windows Server 2008 R2 SP1 的 Windows OS 上安装 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8185f-176">PowerShell is installed by default on Windows OS starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="8185f-177">若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell)。</span><span class="sxs-lookup"><span data-stu-id="8185f-177">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell).</span></span>
2. <span data-ttu-id="8185f-178">生成诊断启动项目。</span><span class="sxs-lookup"><span data-stu-id="8185f-178">Build the Startup Diagnostic project.</span></span> <span data-ttu-id="8185f-179">项目文件中的生成目标：</span><span class="sxs-lookup"><span data-stu-id="8185f-179">A build target in the project file:</span></span>
   * <span data-ttu-id="8185f-180">将程序集和符号文件添加到用户配置文件的运行时存储。</span><span class="sxs-lookup"><span data-stu-id="8185f-180">Moves the assembly and symbols files to the user profile's runtime store.</span></span>
   * <span data-ttu-id="8185f-181">触发 PowerShell 脚本来修改*StartupDiagnostics.deps.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8185f-181">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="8185f-182">将移动*StartupDiagnostics.deps.json*用户配置文件的文件`additionalDeps`文件夹。</span><span class="sxs-lookup"><span data-stu-id="8185f-182">Moves the *StartupDiagnostics.deps.json* file to the user profile's `additionalDeps` folder.</span></span>
3. <span data-ttu-id="8185f-183">设置环境变量：</span><span class="sxs-lookup"><span data-stu-id="8185f-183">Set the environment variables:</span></span>
    * <span data-ttu-id="8185f-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span><span class="sxs-lookup"><span data-stu-id="8185f-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span></span>
    * <span data-ttu-id="8185f-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span><span class="sxs-lookup"><span data-stu-id="8185f-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span></span>
4. <span data-ttu-id="8185f-186">运行示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8185f-186">Run the sample app.</span></span>
5. <span data-ttu-id="8185f-187">请求`/services`终结点以查看应用程序的注册服务。</span><span class="sxs-lookup"><span data-stu-id="8185f-187">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="8185f-188">请求`/diag`终结点若要查看诊断信息。</span><span class="sxs-lookup"><span data-stu-id="8185f-188">Request the `/diag` endpoint to see the diagnostic information.</span></span>
