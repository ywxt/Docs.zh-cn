---
title: 在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用
author: guardrex
description: 了解如何使用 IHostingStartup 从外部程序集增强 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 08/13/2018
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: a06c2da04c1631f5811a535c891ca5190b0d8864
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207532"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a>在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用

作者：[Luke Latham](https://github.com/guardrex)

通过 [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)（承载启动）实现，在启动时从外部程序集向应用添加增强功能。 例如，外部库可使用承载启动实现为应用提供其他配置提供程序或服务。 ASP.NET Core 2.0 或更高版本中提供了 `IHostingStartup`。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="hostingstartup-attribute"></a>HostingStartup 属性

[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性表示存在要在运行时激活的承载启动程序集。

将自动扫描输入程序集或包含 `Startup` 类的程序集以查找 `HostingStartup` 属性。 用于搜索 `HostingStartup` 属性的程序集列表在运行时从 [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 中的配置加载。 要从发现中排除的程序集列表从 [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey) 加载。 有关详细信息，请参阅 [Web 主机：承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)和 [Web 主机：承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)。

在以下示例中，承载启动程序集的命名空间为 `StartupEnhancement`。 包含承载启动代码的类是 `StartupEnhancementHostingStartup`：

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

`HostingStartup` 属性通常位于承载启动程序集的 `IHostingStartup` 实现类文件中。

## <a name="discover-loaded-hosting-startup-assemblies"></a>发现加载的承载启动程序集

要发现加载的承载启动程序集，请启用日志记录并检查应用的日志。 记录加载程序集时发生的错误。 会在调试级别记录加载的承载启动程序集，并记录所有错误。

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a>禁用承载启动程序集的自动加载

::: moniker range=">= aspnetcore-2.1"

要禁用承载启动程序集的自动加载，请使用以下方法之一：

* 要阻止加载所有承载启动程序集，请将以下内容之一设置为 `true` 或 `1`：
  * [阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。
  * `ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。
* 要阻止加载特定的承载启动程序集，请将以下之一设置为以分号分隔的承载启动程序集字符串，以便在启动时排除：
  * [承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)承载配置设置。
  * `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` 环境变量。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

要禁用承载启动程序集的自动加载，请将以下之一设置为 `true` 或 `1`：

* [阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。
* `ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。

::: moniker-end

如果同时设置了主机配置设置和环境变量，则主机设置将控制行为。

如果使用主机设置或环境变量来禁用承载启动程序集，将全局禁用程序集，并可能会禁用应用的多个特征。

## <a name="project"></a>项目

使用以下任一项目类型创建承载启动：

* [类库](#class-library)
* [无入口点的控制台应用](#console-app-without-an-entry-point)

### <a name="class-library"></a>类库

可在类库中提供承载启动增强。 库包含 `HostingStartup` 属性。

[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)包括 Razor Pages 应用、HostingStartupApp 和类库 HostingStartupLibrary。 类库：

* 包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。 `ServiceKeyInjection` 使用内存中配置提供程序 ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)) 将一对服务字符串添加到应用的配置中。
* 包含 `HostingStartup` 属性，用于标识承载启动的命名空间和类。

`ServiceKeyInjection` 类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。 用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。

HostingStartupLibrary/ServiceKeyInjection.cs：

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupLibrary/ServiceKeyInjection.cs?name=snippet1)]

应用的索引页读取并呈现类库承载启动程序集设置的两个键的配置值：

HostingStartupApp/Pages/Index.cshtml.cs：

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=5-6,11-12)]

[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)还包括一个 NuGet 包项目，该项目提供单独的承载启动 HostingStartupPackage。 该包具有与前述类库相同的特征。 包：

* 包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。 `ServiceKeyInjection` 将一对服务字符串添加到应用的配置中。
* 包含 `HostingStartup` 属性。

HostingStartupPackage/ServiceKeyInjection.cs：

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupPackage/ServiceKeyInjection.cs?name=snippet1)]

应用的索引页读取并呈现包承载启动程序集设置的两个键的配置值：

HostingStartupApp/Pages/Index.cshtml.cs：

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=7-8,13-14)]

### <a name="console-app-without-an-entry-point"></a>无入口点的控制台应用

此方法仅适用于 .NET Core 应用，不适用于 .NET Framework。

可在无入口点的控制台应用中提供动态承载启动增强功能，该功能无需编译时引用进行激活。 应用包含 `HostingStartup` 属性。 创建动态承载启动：

1. 从包含 `IHostingStartup` 实现的类创建实现库。 实现库被视为常规包。
1. 无入口点的控制台应用引用实现库包。 使用控制台应用，因为：
   * 依赖项文件是可运行的应用资产，因此库无法提供依赖项文件。
   * 无法直接将库添加到[运行时包存储](/dotnet/core/deploying/runtime-store)，该过程需要一个以已共享运行时为目标的可运行项目。
1. 发布控制台应用，获取承载启动的依赖项。 发布控制台应用的结果是从依赖项文件中删除了未使用的依赖项。
1. 应用及其依赖项文件位于运行时包存储中。 要发现承载启动程序集及其依赖项文件，它们将在一对环境变量中引用。

控制台应用引用 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 包：

[!code-xml[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.csproj)]

生成 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 时，[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性将类标识为 `IHostingStartup` 的实现，用于加载和执行。 在下面的示例中，命名空间为 `StartupEnhancement`，类为 `StartupEnhancementHostingStartup`：

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

类实现 `IHostingStartup`。 类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。 用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

生成 `IHostingStartup` 项目时，依赖项文件 (\*.deps.json) 将程序集的 `runtime` 位置设为 bin 文件夹：

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

仅显示部分文件。 示例中程序集的名称是 `StartupEnhancement`。

## <a name="specify-the-hosting-startup-assembly"></a>指定承载启动程序集

对于类库或控制台应用提供的承载启动，请在 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中指定承载启动程序集的名称。 环境变量是以分号分隔的程序集列表。

仅扫描承载启动程序集以查找 `HostingStartup` 属性。 对于示例应用 HostingStartupApp，要发现前述的承载启动，请将环境变量设置为以下值：

```
HostingStartupLibrary;HostingStartupPackage;StartupDiagnostics
```

还可使用[承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)主机配置设置来设置此承载启动程序集。

存在多个托管启动程序集时，将按列出程序集的顺序执行 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法。

## <a name="activation"></a>激活

承载启动激活的选项包括：

* [运行时存储](#runtime-store) &ndash; 激活无需用于激活的编译时引用。 示例应用将承载启动程序集和依赖项文件放入文件夹“deployment”，以便在多计算机环境中部署承载启动。 “deployment”文件夹还包括 PowerShell 脚本，该脚本可在部署系统上创建或修改环境变量以启用承载启动。
* 激活所需的编译时引用
  * [NuGet 包](#nuget-package)
  * [项目 bin 文件夹](#project-bin-folder)

### <a name="runtime-store"></a>运行时存储

承载启动实现位于[运行时存储](/dotnet/core/deploying/runtime-store)中。 增强型应用无需对程序集进行编译时引用。

构建承载启动后，承载启动的项目文件可作为 [dotnet store](/dotnet/core/tools/dotnet-store) 命令的清单文件。

```console
dotnet store --manifest <PROJECT_FILE> --runtime <RUNTIME_IDENTIFIER>
```

此命令将承载启动程序集和不属于共享框架的其他依赖项置于用户配置文件的运行时存储中：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

如果希望将程序集和依赖项放在可供全局使用的位置，请使用以下路径将 `-o|--output` 选项添加到 `dotnet store` 命令：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

**修改并放置承载启动的依赖项文件**

运行时位置在 \*.deps.json 文件中指定。 若要激活增强功能，`runtime` 元素必须指定增强功能运行时程序集的位置。 将 `runtime` 位置的前缀设为 `lib/<TARGET_FRAMEWORK_MONIKER>/`：

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

在示例代码（StartupDiagnostics 项目）中，\*.deps.json 文件的修改由 [PowerShell](/powershell/scripting/powershell-scripting) 脚本执行。 PowerShell 脚本由项目文件中的生成目标自动触发。

该实现的 \*.deps.json 文件必须位于可访问的位置。

若要实现按用户使用，将文件置于用户配置文件 `.dotnet` 设置的 additonalDeps 文件夹中：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

若要实现全局使用，将文件置于 .NET Core 安装的 additonalDeps 文件夹中：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

共享框架版本反映目标应用使用的共享运行时的版本。 共享运行时显示在 \*.runtimeconfig.json 文件中。 在示例应用 (HostingStartupApp) 中，共享运行时在 HostingStartupApp.runtimeconfig.json 文件中指定。

**列出承载启动的依赖项文件**

`DOTNET_ADDITIONAL_DEPS` 环境变量中列出了实现的 \*.deps.json 文件的位置。

如果文件放在用户配置文件的 .dotnet 文件夹中，请将环境变量的值设置为：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

---

如果将文件放置在 .NET Core 安装中以实现全局使用，则提供该文件的完整路径：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

---

对于用于查找依赖项文件 (HostingStartupApp.runtimeconfig.json) 的示例应用 (HostingStartupApp)，依赖项文件位于用户的配置文件中。

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为以下值：

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

---

有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。

**部署**

为了便于在多计算机环境中部署托承载启动，示例应用在已发布的输出中创建一个“deployment”文件夹，其中包含：

* 承载启动程序集。
* 承载启动依赖项文件。
* PowerShell 脚本，用于创建或修改 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 和 `DOTNET_ADDITIONAL_DEPS` 以支持激活承载启动。 从部署系统上的管理 PowerShell 命令提示符运行脚本。

### <a name="nuget-package"></a>NuGet 程序包

可在 NuGet 包中提供承载启动增强。 该包含有 `HostingStartup` 属性。 包提供的承载启动类型使用以下任一方法提供给应用：

* 增强型应用的项目文件在应用的项目文件（编译时引用）中为承载启动提供了包引用。 有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。 此方法适用于已发布到 [nuget.org](https://www.nuget.org/) 的承载启动程序集包。
* 承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。

有关 NuGet 包和运行时存储的详细信息，请参阅以下主题：

* [如何使用跨平台工具创建 NuGet 包](/dotnet/core/deploying/creating-nuget-packages)
* [发布包](/nuget/create-packages/publish-a-package)
* [运行时包存储](/dotnet/core/deploying/runtime-store)

### <a name="project-bin-folder"></a>项目 bin 文件夹

承载启动增强功能可通过增强型应用中的 bin -deployed 程序集提供。 程序集提供的承载启动类型使用以下任一方法提供给应用：

* 增强型应用的项目文件对承载启动进行了程序集引用（编译时引用）。 有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。 如果部署方案要求将已编译承载启动库的程序集（DLL 文件）移动到使用项目中或使用项目可访问的位置，并且对承载启动程序集进行编译时引用，此方法适用。
* 承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。

## <a name="sample-code"></a>示例代码

[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:index#how-to-download-a-sample)）演示了承载启动实现方案：

* 两个承载启动程序集（类库）分别设置一对内存中配置键值对：
  * NuGet 包 (HostingStartupPackage)
  * 类库 (HostingStartupLibrary)
* 从运行时存储部署的程序集 (StartupDiagnostics) 激活承载启动。 该程序集在启动时将两个中间件添加到应用，用于提供以下内容的诊断信息：
  * 已注册服务
  * 地址（方案、主机、基路径、路径、查询字符串）
  * 连接（远程 IP、远程端口、本地 IP、本地端口、客户端证书）
  * 请求标头
  * 环境变量

运行示例：

**从 NuGet 包激活**

1. 使用 [dotnet pack](/dotnet/core/tools/dotnet-pack) 命令编译 HostingStartupPackage 包。
1. 将包的程序集名称 HostingStartupPackage 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。
1. 编译并运行应用。 增强型应用中存在包引用（编译时引用）。 应用项目文件中的 `<PropertyGroup>` 指定包项目的输出 (../HostingStartupPackage/bin/Debug) 作为包源。 这允许应用使用该包而无需将包上传到 [nuget.org](https://www.nuget.org/)。有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。

   ```xml
   <PropertyGroup>
     <RestoreSources>$(RestoreSources);https://api.nuget.org/v3/index.json;../HostingStartupPackage/bin/Debug</RestoreSources>
   </PropertyGroup>
   ```
1. 观察到索引页呈现的服务配置键值与包的 `ServiceKeyInjection.Configure` 方法设置的值匹配。

如果更改并重新编译 HostingStartupPackage 项目，请清除本地 NuGet 包缓存，确保 HostingStartupApp 从本地缓存中收到更新后的包而不是旧包。 要清除本地 NuGet 缓存，请执行以下 [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) 命令：

```console
dotnet nuget locals all --clear
```

**从类库激活**

1. 使用 [dotnet build](/dotnet/core/tools/dotnet-build) 命令编译 HostingStartupLibrary 类库。
1. 将类库的程序集名称 HostingStartupLibrary 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。
1. bin - 通过将类库编译输出中的 HostingStartupLibrary.dll 文件复制到应用的 bin/Debug 文件夹，将类库程序集部署到应用。
1. 编译并运行应用。 应用项目文件中的 `<ItemGroup>` 引用类库的程序集 (.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll)（编译时引用）。 有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。

   ```xml
   <ItemGroup>
     <Reference Include=".\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll">
       <HintPath>.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll</HintPath>
       <SpecificVersion>False</SpecificVersion>
     </Reference>
   </ItemGroup>
   ```
1. 观察到索引页呈现的服务配置键值与类库的 `ServiceKeyInjection.Configure` 方法设置的值匹配。

**从运行时存储部署的程序集激活**

1. StartupDiagnostics 项目使用 [PowerShell](/powershell/scripting/powershell-scripting) 修改其 StartupDiagnostics.deps.json 文件。 默认情况下，Windows 7 SP1 和 Windows Server 2008 R2 SP1 及以后版本的 Windows 上安装有 PowerShell。 若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core)。
1. 构建 StartupDiagnostics 项目。 构建项目后，会自动生成项目文件中的构建目标：
   * 触发 PowerShell 脚本以修改 StartupDiagnostics.deps.json 文件。
   * 将 StartupDiagnostics.deps.json 文件移动到用户配置文件的 additionalDeps 文件夹。
1. 在承载启动目录的命令提示符处执行 `dotnet store` 命令，将程序集及其依赖项存储在用户配置文件的运行时存储中：

   ```console
   dotnet store --manifest StartupDiagnostics.csproj --runtime <RID>
   ```
   对于 Windows，该命令使用 `win7-x64` [运行时标识符 (RID)](/dotnet/core/rid-catalog)。 为其他运行时提供承载启动时，请替换为正确的 RID。
1. 设置环境变量：
   * 将程序集名称 StartupDiagnostics 的添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。
   * 在 Windows 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`。 在 macOS/Linux 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`，其中 `<USER>` 是包含承载启动的用户配置文件。
1. 运行示例应用。
1. 请求 `/services` 终结点以查看应用的注册服务。 请求 `/diag` 终结点以查看诊断信息。
