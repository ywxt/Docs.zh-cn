---
title: ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包
author: Rick-Anderson
description: 不建议在 ASP.NET Core 2.1 及更高版本中使用 Microsoft.AspNetCore.All 元数据包。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 54655f1e1abf0b64d19506334d94cfdb0caf55f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148845"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包

> [!NOTE]
> 对于面向 ASP.NET Core 2.1 及更高版本的应用程序，建议使用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)而不是此包。 请参阅本文中的[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](#migrate)。

此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。

ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：

* ASP.NET Core 团队支持的所有包。
* Entity Framework Core 支持的所有包。
* ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。

`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。 定目标到 ASP.NET Core 2.0 的默认项目模板使用此包。

`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。

使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](/dotnet/core/deploying/runtime-store)。 此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。 使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。 运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。

可使用包修整过程来删除不使用的包。 已发布的应用程序输出中排除了修整的包。

以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a>隐式版本控制

在 ASP.NET Core 2.1 或更高版本中，可以指定 `Microsoft.AspNetCore.All` 包引用但不指定版本。 如果未指定版本，SDK 会指定隐式版本 (`Microsoft.NET.Sdk.Web`)。 建议使用 SDK 指定的隐式版本，而不是在包引用上显式设置版本号。 如果对这种方法有任何疑问，可以在 [Microsoft.AspNetCore.App 隐式版本讨论](https://github.com/aspnet/Docs/issues/6430)上发表 GitHub 评论。

对于便携式应用，隐式版本设置为 `major.minor.0`。 共享框架前滚机制在安装的共享框架的最新兼容版本上运行应用。 为确保在开发、测试和生产中使用相同的版本，请确保在所有环境中都安装相同版本的共享框架。 对于独立应用，将隐式版本号设置为在已安装的 SDK 中捆绑的共享框架的 `major.minor.patch`。

在 `Microsoft.AspNetCore.All` 包引用上指定版本号，不能保证会选择该共享框架版本。 例如，假设指定的版本是“2.1.1”，但安装的是“2.1.3”。 这种情况下，应用将使用"2.1.3"。 不过不建议这样做，你可以禁用前滚（修补程序和/或次要版本）。 有关 dotnet 主机前滚以及如何配置其行为的详细信息，请参阅 [dotnet 主机前滚](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)。

必须在项目文件中将项目的 SDK 设置为 `Microsoft.NET.Sdk.Web`，这样才能使用隐式版本的 `Microsoft.AspNetCore.All`。 指定 `Microsoft.NET.Sdk` SDK（项目文件顶部的 `<Project Sdk="Microsoft.NET.Sdk">`）时，将生成以下警告：

警告 NU1604：项目依赖项 Microsoft.AspNetCore.All 不包括包含下限。请在依赖项版本中包括下限，以确保一致的还原结果。

这是 .NET Core 2.1 SDK 的一个已知问题，将在 .NET Core 2.2 SDK 中修复。

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a>从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App

`Microsoft.AspNetCore.All` 包中包含以下包，而 `Microsoft.AspNetCore.App` 包中不包含以下包。

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

要从 `Microsoft.AspNetCore.All` 移到 `Microsoft.AspNetCore.App`，如果应用使用上述包或由这些包引入的包中的任何 API，请在项目中添加对这些包的引用。

不会隐式包含非 `Microsoft.AspNetCore.App` 依赖项的上述包的任何依赖项。 例如:

* `StackExchange.Redis` 作为 `Microsoft.Extensions.Caching.Redis` 的依赖项
* `Microsoft.ApplicationInsights` 作为 `Microsoft.AspNetCore.ApplicationInsights.HostingStartup` 的依赖项

## <a name="update-aspnet-core-21"></a>更新 ASP.NET Core 2.1

建议迁移到 2.1 及更高版本的 `Microsoft.AspNetCore.App` 元数据包。 要继续使用 `Microsoft.AspNetCore.All` 元数据包并确保部署最新的补丁版本，请执行以下操作：

* 在开发计算机和生成服务器上：安装最新的 [.NET Core SDK](https://www.microsoft.com/net/download)。
* 在部署服务器上：安装最新的 [.NET Core 运行时](https://www.microsoft.com/net/download)。
 在应用程序重启时，应用将前滚到最新安装的版本。
