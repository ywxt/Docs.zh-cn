---
title: ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包
author: Rick-Anderson
description: Microsoft.AspNetCore.All 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包及其依赖关系。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 09/20/2017
uid: fundamentals/metapackage
ms.openlocfilehash: fbc0f5465dc37a612b81c293f1a58b53ea4b2238
ms.sourcegitcommit: cb0c27fa0184f954fce591d417e6ab2a51d8bb22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39123822"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包

> [!NOTE]
> 对于面向 ASP.NET Core 2.1 及更高版本的应用程序，建议使用 [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) 而不是此包。 请参阅本文中的[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](#migrate)。

此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。

ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：

* ASP.NET Core 团队支持的所有包。
* Entity Framework Core 支持的所有包。
* ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。

`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。 定目标到 ASP.NET Core 2.0 的默认项目模板使用此包。

`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。

使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)。 此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。 使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。 运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。

可使用包修整过程来删除不使用的包。 已发布的应用程序输出中排除了修整的包。

以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=6)]

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
