---
title: ASP.NET Core 中的 Razor 视图编译和预编译
author: rick-anderson
description: 了解如何在 ASP.NET Core 应用中启用 MVC Razor 视图编译和预编译。
manager: wpickett
ms.author: riande
ms.date: 12/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-compilation
ms.openlocfilehash: 013ca0d149c6415b5e6825aa5a48e93ae48f6728
ms.sourcegitcommit: 0063338c2e130409081bb60fcffa0c3f190cd46a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
# <a name="razor-file-cshtml-compilation-in-aspnet-core"></a>ASP.NET Core 中的 Razor 文件 (.cshtml) 编译

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

调用视图时，Razor 视图在运行时进行编译。 ASP.NET Core 2.1.0 或更高版本使用 [Razor Sdk](/aspnetcore/mvc/razor-pages/sdk) 在生成时和发布时编译视图。 在 ASP.NET Core 1.1 和 ASP.NET Core 2.0 中，可以选择在发布时编译视图并通过 &mdash; 应用使用预编译工具进行部署。 



预编译注意事项：

* 预编译视图生成的发布捆绑包更小，启动速度更快。
* 在预编译视图之后，无法编辑 Razor 文件。 已编辑的视图不会出现在发布捆绑包中。 

部署预编译的视图：

# <a name="aspnet-core-21tabaspnetcore21"></a>[ASP.NET Core 2.1](#tab/aspnetcore21/)
Razor Sdk 默认启用 Razor 文件的生成时和发布时编译。 Razor 文件更新后，支持在生成时编辑这些文件。 默认情况下，仅通过应用程序部署编译的 Views.dll 而不部署 cshtml 文件。 
    
> [!IMPORTANT]
> 仅当项目文件中未设置特定于预编译的属性时，Razor Sdk 才有效。 例如，在 .csproj 文件中设置 `MvcRazorCompileOnPublish` 将禁用 Razor Sdk。

# <a name="aspnet-core-20tabaspnetcore20"></a>[ASP.NET Core 2.0](#tab/aspnetcore20/)

如果项目面向 .NET Framework，请添加对 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) 的包引用：

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

如果项目面向 .NET Core，则无需进行任何更改。

默认情况下，ASP.NET Core 2.x 项目模板将 `MvcRazorCompileOnPublish` 隐式设置为 `true`，这意味着可以从 .csproj 文件安全地删除此节点。
    
> [!IMPORTANT]
> 在 ASP.NET Core 2.0 中执行[独立部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) 时，Razor 视图预编译不可用。 

使用 [.NET Core CLI 发布命令](/dotnet/core/tools/dotnet-publish)，让应用做好[框架依赖型部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)的准备。 例如，在项目根目录中执行以下命令：

```console
dotnet publish -c Release
```

预编译成功后，将生成包含已编译 Razor 视图的 <project_name> .PrecompiledViews.dll 文件。 例如，以下屏幕截图描述了 WebApplication1.PrecompiledViews.dll 中 Index.cshtml 的内容：

![DLL 中的 Razor 视图](view-compilation/_static/razor-views-in-dll.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

将 `MvcRazorCompileOnPublish` 设置为 `true`，并添加对 `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` 的包引用。 以下 .csproj 示例突出显示了这些设置：

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=5,12)]

---

