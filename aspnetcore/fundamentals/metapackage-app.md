---
title: ASP.NET Core 2.1 及更高版本的 Microsoft.AspNetCore.App 元包
author: Rick-Anderson
description: Microsoft.AspNetCore.App 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage-app
ms.openlocfilehash: 7c7f69a6176d3f7982a67106cb823ff42200b50e
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2018
ms.locfileid: "34306616"
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a>ASP.NET Core 2.1 的 Microsoft.AspNetCore.App 元包

此功能需要面向 .NET Core 2.1 及更高版本的 ASP.NET Core 2.1。

ASP.NET Core 的 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [元包](/dotnet/core/packages#metapackages)：

* 不包括第三方依赖项，[Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/)、[Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/) 和 [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/) 除外。 为确保正常使用主要框架功能，这些第三方依赖项均为必要条件。
* 包括 ASP.NET Core 团队支持的所有软件包，包含第三方依赖项的软件包（不包括上文所述）除外。
* 包括 Entity Framework Core 团队支持的所有软件包，包含第三方依赖项的软件包（不包括上文所述）除外。

`Microsoft.AspNetCore.App` 包中包含了 ASP.NET Core 2.1 及更高版本和 Entity Framework Core 2.1 及更高版本的所有功能。 面向 ASP.NET Core 2.1 及更高版本的默认项目模板使用此包。 建议面向 ASP.NET Core 2.1 及更高版本和 Entity Framework Core 2.1 及更高版本的应用程序使用 `Microsoft.AspNetCore.App` 包。

`Microsoft.AspNetCore.App` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。

使用 `Microsoft.AspNetCore.App` 元包可提供用于保护应用的版本限制：

* 如果包含的包对 `Microsoft.AspNetCore.App` 中的包具有可传递的（非直接）依赖项，且这些版本号不同，则 NuGet 将生成错误。
* 添加到应用的其他包无法更改 `Microsoft.AspNetCore.App` 中包含的包版本。
* 版本一致性能确保可靠的体验。 `Microsoft.AspNetCore.App` 旨在防止在同一应用中结合使用未经测试的相关位版本组合。

使用 `Microsoft.AspNetCore.App` 元包的应用程序会自动使用 ASP.NET Core 共享框架。 使用 `Microsoft.AspNetCore.App` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产 &mdash; .NET Core 共享框架包含这些资产。 共享框架中的资产已经过预编译，以便缩短应用程序启动时间。 有关详细信息，请参阅 [.NET Core 分发打包](/dotnet/core/build/distribution-packaging)中的“共享框架”。

以下 .csproj 项目文件引用 ASP.NET Core 的 `Microsoft.AspNetCore.App` 元包：

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>

```

前面的标记表示典型的 ASP.NET Core 2.1 及更高版本模板。 它不会为 `Microsoft.AspNetCore.App` 包引用指定版本号。 如果未指定版本，SDK 会指定[隐式](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md)版本，即 `Microsoft.NET.Sdk.Web`。 建议使用 SDK 指定的隐式版本，而不是在包引用上显式设置版本号。 你可以在 [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430)（Microsoft.AspNetCore.App 隐式版本讨论）发表 GitHub 评论。

对于便携式应用，隐式版本设置为 `major.minor.0`。 共享框架前滚机制将在安装的共享框架的最新兼容版本上运行应用。 为确保在开发、测试和生产中使用相同的版本，请确保在所有环境中都安装相同版本的共享框架。 对于独立应用，将隐式版本号设置为在已安装的 SDK 中捆绑的共享框架的 `major.minor.patch`。

在 `Microsoft.AspNetCore.App` 引用上指定版本号，不能保证将选择该共享框架版本。 例如，假设指定的版本是“2.1.1”，但安装的是“2.1.3”。 这种情况下，应用将使用"2.1.3"。 不过不建议这样做，你可以禁用前滚（修补程序和/或次要版本）。 有关 dotnet 主机前滚以及如何配置其行为的详细信息，请参阅 [dotnet 主机前滚](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)。

`Microsoft.AspNetCore.App` [元包](/dotnet/core/packages#metapackages)不是从 NuGet 更新的传统包。 类似于 `Microsoft.NETCore.App`，`Microsoft.AspNetCore.App` 表示共享运行时，它具有在 NuGet 之外处理的特殊版本控制语义。 有关详细信息，请参阅[包、元包和框架](/dotnet/core/packages)。

如果应用程序之前使用 `Microsoft.AspNetCore.All`，请参阅[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate)。
