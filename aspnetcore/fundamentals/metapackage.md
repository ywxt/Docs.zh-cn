---
title: ASP.NET Core 2.x 及更高版本的 Microsoft.AspNetCore.All 元包
author: Rick-Anderson
description: Microsoft.AspNetCore.All 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包及其依赖关系。
manager: wpickett
monikerRange: = aspnetcore-2.0
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: 4c11f15e659565325bfe8b8d91188b62177b251d
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a>ASP.NET Core 2.x 的 Microsoft.AspNetCore.All 元包

此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。

ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：

* ASP.NET Core 团队支持的所有包。
* Entity Framework Core 支持的所有包。 
* ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。 

`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。 定目标到 ASP.NET Core 2.0 的默认项目模板使用此包。

`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本（与 .NET Core 版本对齐）。

使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)。 此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。 使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。 运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。

可使用包修整过程来删除不使用的包。 已发布的应用程序输出中排除了修整的包。

以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：

[!code-xml[](../mvc/views/view-compilation/sample/MvcRazorCompileOnPublish2.csproj?highlight=9)]
