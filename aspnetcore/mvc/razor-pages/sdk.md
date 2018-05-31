---
title: ASP.NET Core Razor SDK
author: Rick-Anderson
description: 了解 ASP.NET Core 中的 Razor 页面如何使基于页面的编码方式比使用 MVC 更简单高效。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: mvc/razor-pages/sdk
ms.openlocfilehash: cf0e1873c7ce500ce3b8ad2b3367555bdc41a576
ms.sourcegitcommit: 466300d32f8c33e64ee1b419a2cbffe702863cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2018
ms.locfileid: "34555529"
---
# <a name="aspnet-core-razor-sdk"></a>ASP.NET Core Razor SDK

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[](~/includes/2.1-SDK.md)] 包含 `Microsoft.NET.Sdk.Razor` MSBuild SDK (Razor SDK)。 Razor SDK：

* 针对基于 ASP.NET Core MVC 的项目，围绕包含 [Razor](xref:mvc/views/razor) 文件的项目的生成、打包和发布设定了体验标准。
* 包含一组预定义的目标、属性和项目，它们允许自定义 Razor 文件的编译。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/2.1-SDK.md)]

## <a name="using-the-razor-sdk"></a>使用 Razor SDK

大多数 Web 应用无需明确引用 Razor SDK。 

要使用 Razor SDK 来生成包含 Razor 视图或 Razor 页面的类库，请执行以下操作：

* 使用 `Microsoft.NET.Sdk.Razor` 而非 `Microsoft.NET.Sdk`：
```xml
<Project SDK="Microsoft.NET.Sdk.Razor">
  ...
</Project>
```

* 通常需要对 `Microsoft.AspNetCore.Mvc` 的包引用以引入生成和编译 Razor 页面和 Razor 视图所需的其他依赖项。 至少，项目需要将包引用添加到：

    * `Microsoft.AspNetCore.Razor.Design` 
    * `Microsoft.AspNetCore.Mvc.Razor.Extensions`
    
 前面的包包含在 `Microsoft.AspNetCore.Mvc` 中。 以下标记显示了使用 Razor SDK 为 ASP.NET Core Razor 页面应用生成 Razor 文件的基本 .csproj 文件：
    
 [!code-xml[Main](sdk/sample/RazorSDK.csproj)]

### <a name="properties"></a>属性

以下属性控制项目生成过程中 Razor 的 SDK 行为：

* `RazorCompileOnBuild`：为 `true` 时，在生成项目过程中，编译并发出 Razor 程序集。 默认为 `true`。
* `RazorCompileOnPublish`：为 `true` 时，在发布项目过程中，编译并发出 Razor 程序集。 默认为 `true`。

以下属性和项用于配置 Razor SDK 的输入和输出：

| 项                                         | 描述                                                                   |
| ------------                                  | -------------                                                                 |
| RazorGenerate                                 | 输入到代码生成目标的项元素（.cshtml 文件）。 |
| RazorCompile                                  | 输入到 Razor 编译目标的项元素（.cs 文件）。 使用此 ItemGroup 指定要编译到 Razor 程序集中的其他文件。 |
| RazorTargetAssemblyAttribute                  | 用于编码生成 Razor 程序集属性的项元素。 例如:  <br />`<RazorAssemblyAttribute ` <br />  `Include="System.Reflection.AssemblyMetadataAttribute"`<br />`  _Parameter1="BuildSource" _Parameter2="https://docs.asp.net/">` |
| RazorEmbeddedResource                         | 作为嵌入的资源添加到生成的 Razor 程序集中的项元素 |

| 属性                                      | 描述                                                                   |
| ------------                                  | -------------                                                                 |
| RazorTargetName                               | Razor 生成的程序集的文件名（不含扩展名）。 | 
| RazorOutputPath                               | Razor 输出目录。                                      |
| RazorCompileToolset                           | 用于确定用于生成 Razor 程序集的工具集。 有效值为 `Implicit` 和 `PrecompilationTool`。 |
| EnableDefaultContentItems                     | 为 `true` 时，包括某些文件类型（例如 .cshtml 文件）作为项目中内容。 当通过 Microsoft.NET.Sdk.Web 引用时，还包括 wwwroot 下的所有文件和配置文件。         |
| EnableDefaultRazorGenerateItems               | 为 `true` 时，包括 `RazorGenerate` 项中 `Content` 项的 .cshtml 文件。 |
| GenerateRazorTargetAssemblyInfo               | 为 `true` 时，生成 .cs 文件（其中包含由 `RazorAssemblyAttribute` 指定的属性），并将其包含在编译输出中。 |
| EnableDefaultRazorTargetAssemblyInfoAttributes | 为 `true` 时，将一组默认的程序集属性添加到 `RazorAssemblyAttribute`。 |
| CopyRazorGenerateFilesToPublishDirectory       | 为 `true` 时，将 RazorGenerate 项 (.cshtml) 文件复制到发布目录。 如果在生成时或发布时参与编译，则通常发布的应用程序无需 Razor 文件。 默认为 `false`。 |
| CopyRefAssembliesToPublishDirectory            | 为 `true` 时，将引用程序集项复制到发布目录。 如果在生成时或发布时出现 Razor 编译，则通常发布的应用程序无需引用程序集。 如果发布的应用程序需要运行时编译（例如，在运行时修改 cshtml 文件或使用嵌入的视图），则设置为 `true`。 默认为 `false`。 |
| IncludeRazorContentInPack                      | 为 `true` 时，所有 Razor 内容项（.cshtml 文件）将标记为包含在生成的 NuGet 包中。 默认为 `false`。 |
| EmbedRazorGenerateSources | 为 `true` 时，将 RazorGenerate (.cshtml) 项作为嵌入的文件添加到生成的 Razor 程序集中。 默认为 `false`。 |
| UseRazorBuildServer                           | 为 `true` 时，使用永久生成服务器进程来卸载代码生成工作。 默认值为 `UseSharedCompilation`。 |

### <a name="targets"></a>目标
Razor SDK 定义两个主要目标：

* `RazorGenerate` - 代码从 RazorGenerate 项元素生成 .cs 文件。 使用 `RazorGenerateDependsOn` 属性指定可在此目标之前或之后运行的其他目标。
* `RazorCompile` - 将生成的 .cs 文件编译到 Razor 程序集中。 使用 `RazorCompileDependsOn` 指定可在此目标之前或之后运行的其他目标。
