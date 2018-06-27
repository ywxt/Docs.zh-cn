---
title: 在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用
author: guardrex
description: 了解如何使用 IHostingStartup 从外部程序集增强 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: bd9605dd8efee2c3ba8bc82a81554cace40630be
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278078"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a>在 ASP.NET Core 中使用 IHostingStartup 从外部程序集增强应用

作者：[Luke Latham](https://github.com/guardrex)

通过 [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 实现，可在启动时从应用 `Startup` 类之外的外部程序集向应用添加增强功能。 例如，外部工具库可以使用 `IHostingStartup` 实现为应用提供其他配置提供程序或服务。 ASP.NET Core 2.0 及更高版本提供 `IHostingStartup`。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="discover-loaded-hosting-startup-assemblies"></a>发现加载的承载启动程序集

若要发现应用或库加载的承载启动程序集，请启用日志记录并检查应用程序日志。 记录加载程序集时发生的错误。 会在调试级别记录加载的承载启动程序集，并记录所有错误。

示例应用将 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 读入 `string` 数组并在应用的索引页中显示结果：

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a>禁用承载启动程序集的自动加载

有两种方法可用于禁用承载启动程序集的自动加载：

* 设置[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。
* 设置 `ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。

当主机设置或环境变量设置为 `true` 或 `1` 时，不会自动加载承载启动程序集。 如果同时设置了两者，则行为由主机设置控制。

如果使用主机设置或环境变量来禁用承载启动程序集，将实现全局性禁用，并可能会禁用应用的多个特征。 当前无法选择性地禁用由库添加的承载启动程序集，除非库提供自己的配置选项。 未来的一个版本将提供选择性禁用承载启动程序集的功能（请参阅 [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)）。

## <a name="implement-ihostingstartup"></a>实现 IHostingStartup

### <a name="create-the-assembly"></a>创建程序集

`IHostingStartup` 增强功能基于没有入口点的控制台应用部署为程序集。 程序集引用 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 包：

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupEnhancement.csproj)]

生成 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 时，[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性将类标识为 `IHostingStartup` 的实现，用于加载和执行。 在下面的示例中，命名空间为 `StartupEnhancement`，类为 `StartupEnhancementHostingStartup`：

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet1)]

类实现 `IHostingStartup`。 类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。 用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

生成 `IHostingStartup` 项目时，依赖项文件 (\*.deps.json) 将程序集的 `runtime` 位置设为 bin 文件夹：

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

仅显示部分文件。 示例中程序集的名称是 `StartupEnhancement`。

### <a name="update-the-dependencies-file"></a>更新依赖项文件

运行时位置在 \*.deps.json 文件中指定。 若要激活增强功能，`runtime` 元素必须指定增强功能运行时程序集的位置。 将 `runtime` 位置的前缀设为 `lib/<TARGET_FRAMEWORK_MONIKER>/`：

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

在示例应用中，\*.deps.json 文件的修改由 [PowerShell](/powershell/scripting/powershell-scripting) 脚本执行。 PowerShell 脚本由项目文件中的生成目标自动触发。

### <a name="enhancement-activation"></a>增强功能激活

**放置程序集文件**

`IHostingStartup` 实现的程序集文件必须以 bin 方式部署在应用中或放置在[运行时存储](/dotnet/core/deploying/runtime-store)中：

若要实现按用户使用，将程序集放入用户配置文件的运行时存储：

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

若要实现全局使用，将程序集放入 .NET Core 安装的运行时存储：

```
<DRIVE>\Program Files\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

将程序集部署到运行时存储时，可能也会部署符号文件，但增强功能的运行无需此文件。

**放置依赖项文件**

该实现的 \*.deps.json 文件必须位于可访问的位置。

若要实现按用户使用，将文件置于用户配置文件 `.dotnet` 设置的 `additonalDeps`文件夹中：

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

若要实现全局使用，将文件置于 .NET Core 安装的 `additonalDeps` 文件夹中：

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

共享框架版本反映目标应用使用的共享运行时的版本。 共享运行时显示在 \*.runtimeconfig.json 文件中。 在示例应用中，共享运行时在 HostingStartupSample.runtimeconfig.json 文件中指定。

**设置环境变量**

在使用该增强功能的应用的上下文中设置以下环境变量。

ASPNETCORE_HOSTINGSTARTUPASSEMBLIES

仅扫描承载启动程序集以查找 `HostingStartupAttribute`。 在此环境变量中提供实现的程序集名称。 示例应用将此值设置为 `StartupDiagnostics`。

还可使用[承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)主机配置设置来设置此值。

存在多个托管启动程序集时，将按列出程序集的顺序执行 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法。

DOTNET_ADDITIONAL_DEPS

实现的 \*.deps.json 文件的位置。

如果将文件放置在用户配置文件的 .dotnet 文件夹中以实现按用户使用：

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

如果将文件放置在 .NET Core 安装中以实现全局使用，则提供该文件的完整路径：

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

示例应用将此值设置为：

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。

## <a name="sample-app"></a>示例应用

[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）使用 `IHostingStartup` 创建一个诊断工具。 该工具在启动时将两个中间件添加到应用，用于提供诊断信息：

* 已注册服务
* 地址：方案、主机、基路径、路径、查询字符串
* 连接：远程 IP、远程端口、本地 IP、本地端口、客户端证书
* 请求标头
* 环境变量

运行示例：

1. 启动诊断项目使用 [PowerShell](/powershell/scripting/powershell-scripting) 修改其 StartupDiagnostics.deps.json 文件。 默认情况下，Windows 7 SP1 和 Windows Server 2008 R2 SP1 及以后版本的 Windows OS 上安装有 PowerShell。 若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell)。
2. 生成启动诊断项目。 项目文件中的生成目标：
   * 将程序集和符号文件移动到用户配置文件的运行时存储。
   * 触发 PowerShell 脚本以修改 StartupDiagnostics.deps.json 文件。
   * 将 StartupDiagnostics.deps.json 文件移动到用户配置文件的 `additionalDeps` 文件夹。
3. 设置环境变量：
    * `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`
    * `DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`
4. 运行示例应用。
5. 请求 `/services` 终结点以查看应用的注册服务。 请求 `/diag` 终结点以查看诊断信息。
