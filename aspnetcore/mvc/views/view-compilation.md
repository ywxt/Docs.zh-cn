---
title: ASP.NET Core 中的 Razor 文件编译和预编译
author: rick-anderson
description: 了解预编译 Razor 文件的好处以及如何在 ASP.NET Core 应用中完成 Razor 文件预编译。
manager: wpickett
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-compilation
ms.openlocfilehash: 03b11116a15c291452acd878e32cd015dc553dcc
ms.sourcegitcommit: 24c32648ab0c6f0be15333d7c23c1bf680858c43
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
ms.locfileid: "34336273"
---
# <a name="razor-file-compilation-in-aspnet-core"></a>ASP.NET Core 中的 Razor 文件编译

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="= aspnetcore-1.1"
调用相关的 MVC 视图时，Razor 文件在运行时进行编译。 不支持在生成时发布 Razor 文件。 可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。
::: moniker-end
::: moniker range="= aspnetcore-2.0"
调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。 不支持在生成时发布 Razor 文件。 可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。 在生成时和发布时使用 [Razor SDK](xref:mvc/razor-pages/sdk) 编译 Razor 文件。
::: moniker-end

## <a name="precompilation-considerations"></a>预编译注意事项

以下是预编译 Razor 文件的意外后果：

* 发布捆绑包更小
* 启动速度更快
* 无法编辑 Razor 文件&mdash;关联内容不会出现在发布捆绑包中。

## <a name="deploy-precompiled-files"></a>部署预编译文件

::: moniker range=">= aspnetcore-2.1"
Razor SDK 默认启用 Razor 文件的生成时和发布时编译。 Razor 文件更新后，支持在生成时编辑这些文件。 默认情况下，仅通过应用部署编译的 Views.dll 而不部署 cshtml 文件。

> [!IMPORTANT]
> 仅当项目文件中未设置特定于预编译的属性时，Razor SDK 才有效。 例如，通过将 .csproj 文件的 `MvcRazorCompileOnPublish` 属性设置为 `true` 来禁用 Razor SDK。
::: moniker-end

::: moniker range="= aspnetcore-2.0"
如果项目面向 .NET Framework，请安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包：

[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]

如果项目面向 .NET Core，则无需进行任何更改。

默认情况下，ASP.NET Core 2.x 项目模板将 `MvcRazorCompileOnPublish` 属性隐式设置为 `true`。 因此，可以从 .csproj 文件中安全地删除此元素。

> [!IMPORTANT]
> 在 ASP.NET Core 2.0 中执行[独立部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) 时，无法使用 Razor 文件预编译。
::: moniker-end

::: moniker range="= aspnetcore-1.1"
将 `MvcRazorCompileOnPublish` 属性设置为 `true`，然后安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包。 以下 .csproj 示例突出显示了这些设置：

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]
::: moniker-end

::: moniker range="<= aspnetcore-2.0"
使用 [.NET Core CLI 发布命令](/dotnet/core/tools/dotnet-publish)，让应用做好[框架依赖型部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)的准备。 例如，在项目根目录中执行以下命令：

```console
dotnet publish -c Release
```

预编译成功后，将生成包含已编译 Razor 文件的 <project_name>.PrecompiledViews.dll 文件。 例如，以下屏幕截图描述了 WebApplication1.PrecompiledViews.dll 中 Index.cshtml 的内容：

![DLL 中的 Razor 视图](view-compilation/_static/razor-views-in-dll.png)
::: moniker-end

## <a name="additional-resources"></a>其他资源

::: moniker range="= aspnetcore-1.1"
* <xref:mvc/views/overview>
::: moniker-end

::: moniker range="= aspnetcore-2.0"
* <xref:mvc/razor-pages/index>
* <xref:mvc/views/overview>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"
* <xref:mvc/razor-pages/index>
* <xref:mvc/views/overview>
* <xref:mvc/razor-pages/sdk>
::: moniker-end