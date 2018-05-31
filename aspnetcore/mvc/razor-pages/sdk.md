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
# <a name="aspnet-core-razor-sdk"></a><span data-ttu-id="53a34-103">ASP.NET Core Razor SDK</span><span class="sxs-lookup"><span data-stu-id="53a34-103">ASP.NET Core Razor SDK</span></span>

<span data-ttu-id="53a34-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="53a34-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="53a34-105">[!INCLUDE[](~/includes/2.1-SDK.md)] 包含 `Microsoft.NET.Sdk.Razor` MSBuild SDK (Razor SDK)。</span><span class="sxs-lookup"><span data-stu-id="53a34-105">The [!INCLUDE[](~/includes/2.1-SDK.md)] includes the `Microsoft.NET.Sdk.Razor` MSBuild SDK (Razor SDK).</span></span> <span data-ttu-id="53a34-106">Razor SDK：</span><span class="sxs-lookup"><span data-stu-id="53a34-106">The Razor SDK:</span></span>

* <span data-ttu-id="53a34-107">针对基于 ASP.NET Core MVC 的项目，围绕包含 [Razor](xref:mvc/views/razor) 文件的项目的生成、打包和发布设定了体验标准。</span><span class="sxs-lookup"><span data-stu-id="53a34-107">Standardizes the experience around building, packaging, and publishing projects containing [Razor](xref:mvc/views/razor) files for ASP.NET Core MVC-based projects.</span></span>
* <span data-ttu-id="53a34-108">包含一组预定义的目标、属性和项目，它们允许自定义 Razor 文件的编译。</span><span class="sxs-lookup"><span data-stu-id="53a34-108">Includes a set of predefined targets, properties, and items that allow customizing the compilation of Razor files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53a34-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="53a34-109">Prerequisites</span></span>

[!INCLUDE[](~/includes/2.1-SDK.md)]

## <a name="using-the-razor-sdk"></a><span data-ttu-id="53a34-110">使用 Razor SDK</span><span class="sxs-lookup"><span data-stu-id="53a34-110">Using the Razor SDK</span></span>

<span data-ttu-id="53a34-111">大多数 Web 应用无需明确引用 Razor SDK。</span><span class="sxs-lookup"><span data-stu-id="53a34-111">Most web apps don't need to expressly reference the Razor SDK.</span></span> 

<span data-ttu-id="53a34-112">要使用 Razor SDK 来生成包含 Razor 视图或 Razor 页面的类库，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="53a34-112">To use the Razor SDK to build class libraries containing Razor views or Razor Pages:</span></span>

* <span data-ttu-id="53a34-113">使用 `Microsoft.NET.Sdk.Razor` 而非 `Microsoft.NET.Sdk`：</span><span class="sxs-lookup"><span data-stu-id="53a34-113">Use `Microsoft.NET.Sdk.Razor` instead of `Microsoft.NET.Sdk`:</span></span>
```xml
<Project SDK="Microsoft.NET.Sdk.Razor">
  ...
</Project>
```

* <span data-ttu-id="53a34-114">通常需要对 `Microsoft.AspNetCore.Mvc` 的包引用以引入生成和编译 Razor 页面和 Razor 视图所需的其他依赖项。</span><span class="sxs-lookup"><span data-stu-id="53a34-114">Typically a package reference to `Microsoft.AspNetCore.Mvc` is required to bring in additional dependencies required to build and compile Razor Pages and Razor views.</span></span> <span data-ttu-id="53a34-115">至少，项目需要将包引用添加到：</span><span class="sxs-lookup"><span data-stu-id="53a34-115">At minimum, your project needs to add package references to:</span></span>

    * `Microsoft.AspNetCore.Razor.Design` 
    * `Microsoft.AspNetCore.Mvc.Razor.Extensions`
    
 <span data-ttu-id="53a34-116">前面的包包含在 `Microsoft.AspNetCore.Mvc` 中。</span><span class="sxs-lookup"><span data-stu-id="53a34-116">The preceding packages are included in `Microsoft.AspNetCore.Mvc`.</span></span> <span data-ttu-id="53a34-117">以下标记显示了使用 Razor SDK 为 ASP.NET Core Razor 页面应用生成 Razor 文件的基本 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="53a34-117">The following markup shows a basic *.csproj* file that uses the Razor SDK to build Razor files for an ASP.NET Core Razor Pages app:</span></span>
    
 [!code-xml[Main](sdk/sample/RazorSDK.csproj)]

### <a name="properties"></a><span data-ttu-id="53a34-118">属性</span><span class="sxs-lookup"><span data-stu-id="53a34-118">Properties</span></span>

<span data-ttu-id="53a34-119">以下属性控制项目生成过程中 Razor 的 SDK 行为：</span><span class="sxs-lookup"><span data-stu-id="53a34-119">The following properties control the Razor's SDK behavior as part of a project build:</span></span>

* <span data-ttu-id="53a34-120">`RazorCompileOnBuild`：为 `true` 时，在生成项目过程中，编译并发出 Razor 程序集。</span><span class="sxs-lookup"><span data-stu-id="53a34-120">`RazorCompileOnBuild` : When `true`, compiles and emits the Razor assembly as part of building the project.</span></span> <span data-ttu-id="53a34-121">默认为 `true`。</span><span class="sxs-lookup"><span data-stu-id="53a34-121">Defaults to `true`.</span></span>
* <span data-ttu-id="53a34-122">`RazorCompileOnPublish`：为 `true` 时，在发布项目过程中，编译并发出 Razor 程序集。</span><span class="sxs-lookup"><span data-stu-id="53a34-122">`RazorCompileOnPublish` : When `true`, compiles and emits the Razor assembly as part of publishing the project.</span></span> <span data-ttu-id="53a34-123">默认为 `true`。</span><span class="sxs-lookup"><span data-stu-id="53a34-123">Defaults to `true`.</span></span>

<span data-ttu-id="53a34-124">以下属性和项用于配置 Razor SDK 的输入和输出：</span><span class="sxs-lookup"><span data-stu-id="53a34-124">The following properties and items are used to configure inputs and output to the Razor SDK:</span></span>

| <span data-ttu-id="53a34-125">项</span><span class="sxs-lookup"><span data-stu-id="53a34-125">Items</span></span>                                         | <span data-ttu-id="53a34-126">描述</span><span class="sxs-lookup"><span data-stu-id="53a34-126">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="53a34-127">RazorGenerate</span><span class="sxs-lookup"><span data-stu-id="53a34-127">RazorGenerate</span></span>                                 | <span data-ttu-id="53a34-128">输入到代码生成目标的项元素（.cshtml 文件）。</span><span class="sxs-lookup"><span data-stu-id="53a34-128">Item elements (*.cshtml* files) that are inputs to code generation targets.</span></span> |
| <span data-ttu-id="53a34-129">RazorCompile</span><span class="sxs-lookup"><span data-stu-id="53a34-129">RazorCompile</span></span>                                  | <span data-ttu-id="53a34-130">输入到 Razor 编译目标的项元素（.cs 文件）。</span><span class="sxs-lookup"><span data-stu-id="53a34-130">Item elements (.cs files) that are inputs to  Razor compilation targets.</span></span> <span data-ttu-id="53a34-131">使用此 ItemGroup 指定要编译到 Razor 程序集中的其他文件。</span><span class="sxs-lookup"><span data-stu-id="53a34-131">Use this ItemGroup to specify additional files to be compiled into the Razor assembly.</span></span> |
| <span data-ttu-id="53a34-132">RazorTargetAssemblyAttribute</span><span class="sxs-lookup"><span data-stu-id="53a34-132">RazorTargetAssemblyAttribute</span></span>                  | <span data-ttu-id="53a34-133">用于编码生成 Razor 程序集属性的项元素。</span><span class="sxs-lookup"><span data-stu-id="53a34-133">Item elements used to code generate attributes for the Razor assembly.</span></span> <span data-ttu-id="53a34-134">例如:</span><span class="sxs-lookup"><span data-stu-id="53a34-134">For example:</span></span>  <br />`<RazorAssemblyAttribute ` <br />  `Include="System.Reflection.AssemblyMetadataAttribute"`<br />`  _Parameter1="BuildSource" _Parameter2="https://docs.asp.net/">` |
| <span data-ttu-id="53a34-135">RazorEmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="53a34-135">RazorEmbeddedResource</span></span>                         | <span data-ttu-id="53a34-136">作为嵌入的资源添加到生成的 Razor 程序集中的项元素</span><span class="sxs-lookup"><span data-stu-id="53a34-136">Item elements added as embedded resources to the generated Razor assembly</span></span> |

| <span data-ttu-id="53a34-137">属性</span><span class="sxs-lookup"><span data-stu-id="53a34-137">Property</span></span>                                      | <span data-ttu-id="53a34-138">描述</span><span class="sxs-lookup"><span data-stu-id="53a34-138">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="53a34-139">RazorTargetName</span><span class="sxs-lookup"><span data-stu-id="53a34-139">RazorTargetName</span></span>                               | <span data-ttu-id="53a34-140">Razor 生成的程序集的文件名（不含扩展名）。</span><span class="sxs-lookup"><span data-stu-id="53a34-140">File name (without extension) of the assembly produced by Razor.</span></span> | 
| <span data-ttu-id="53a34-141">RazorOutputPath</span><span class="sxs-lookup"><span data-stu-id="53a34-141">RazorOutputPath</span></span>                               | <span data-ttu-id="53a34-142">Razor 输出目录。</span><span class="sxs-lookup"><span data-stu-id="53a34-142">The Razor output directory.</span></span>                                      |
| <span data-ttu-id="53a34-143">RazorCompileToolset</span><span class="sxs-lookup"><span data-stu-id="53a34-143">RazorCompileToolset</span></span>                           | <span data-ttu-id="53a34-144">用于确定用于生成 Razor 程序集的工具集。</span><span class="sxs-lookup"><span data-stu-id="53a34-144">Used to determine the toolset used to build the Razor assembly.</span></span> <span data-ttu-id="53a34-145">有效值为 `Implicit` 和 `PrecompilationTool`。</span><span class="sxs-lookup"><span data-stu-id="53a34-145">Valid values are `Implicit`, , and `PrecompilationTool`.</span></span> |
| <span data-ttu-id="53a34-146">EnableDefaultContentItems</span><span class="sxs-lookup"><span data-stu-id="53a34-146">EnableDefaultContentItems</span></span>                     | <span data-ttu-id="53a34-147">为 `true` 时，包括某些文件类型（例如 .cshtml 文件）作为项目中内容。</span><span class="sxs-lookup"><span data-stu-id="53a34-147">When `true`, includes certain file types, such as *.cshtml* files, as content in the project.</span></span> <span data-ttu-id="53a34-148">当通过 Microsoft.NET.Sdk.Web 引用时，还包括 wwwroot 下的所有文件和配置文件。</span><span class="sxs-lookup"><span data-stu-id="53a34-148">When referenced via Microsoft.NET.Sdk.Web, also includes all files under *wwwroot*, and config files.</span></span>         |
| <span data-ttu-id="53a34-149">EnableDefaultRazorGenerateItems</span><span class="sxs-lookup"><span data-stu-id="53a34-149">EnableDefaultRazorGenerateItems</span></span>               | <span data-ttu-id="53a34-150">为 `true` 时，包括 `RazorGenerate` 项中 `Content` 项的 .cshtml 文件。</span><span class="sxs-lookup"><span data-stu-id="53a34-150">When `true`, includes *.cshtml* files from `Content` items in `RazorGenerate` items.</span></span> |
| <span data-ttu-id="53a34-151">GenerateRazorTargetAssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="53a34-151">GenerateRazorTargetAssemblyInfo</span></span>               | <span data-ttu-id="53a34-152">为 `true` 时，生成 .cs 文件（其中包含由 `RazorAssemblyAttribute` 指定的属性），并将其包含在编译输出中。</span><span class="sxs-lookup"><span data-stu-id="53a34-152">When `true`, generates a *.cs* file containing attributes specified by `RazorAssemblyAttribute` and includes it in the compile output.</span></span> |
| <span data-ttu-id="53a34-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span><span class="sxs-lookup"><span data-stu-id="53a34-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span></span> | <span data-ttu-id="53a34-154">为 `true` 时，将一组默认的程序集属性添加到 `RazorAssemblyAttribute`。</span><span class="sxs-lookup"><span data-stu-id="53a34-154">When `true`, adds a default set of assembly attributes to `RazorAssemblyAttribute`.</span></span> |
| <span data-ttu-id="53a34-155">CopyRazorGenerateFilesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="53a34-155">CopyRazorGenerateFilesToPublishDirectory</span></span>       | <span data-ttu-id="53a34-156">为 `true` 时，将 RazorGenerate 项 (.cshtml) 文件复制到发布目录。</span><span class="sxs-lookup"><span data-stu-id="53a34-156">When `true`, copies RazorGenerate items (*.cshtml*) files to the publish directory.</span></span> <span data-ttu-id="53a34-157">如果在生成时或发布时参与编译，则通常发布的应用程序无需 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="53a34-157">Typically Razor files are not needed for a published application if they participate in compilation at build-time or publish-time.</span></span> <span data-ttu-id="53a34-158">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="53a34-158">Defaults to `false`.</span></span> |
| <span data-ttu-id="53a34-159">CopyRefAssembliesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="53a34-159">CopyRefAssembliesToPublishDirectory</span></span>            | <span data-ttu-id="53a34-160">为 `true` 时，将引用程序集项复制到发布目录。</span><span class="sxs-lookup"><span data-stu-id="53a34-160">When `true`, copy reference assembly items to the publish directory.</span></span> <span data-ttu-id="53a34-161">如果在生成时或发布时出现 Razor 编译，则通常发布的应用程序无需引用程序集。</span><span class="sxs-lookup"><span data-stu-id="53a34-161">Typically reference assemblies are not needed for a published application if Razor compilation occurs at build-time or publish-time.</span></span> <span data-ttu-id="53a34-162">如果发布的应用程序需要运行时编译（例如，在运行时修改 cshtml 文件或使用嵌入的视图），则设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="53a34-162">Set to `true`, if your published application requires runtime compilation, for example, modifies cshtml files at runtime, or uses embedded views.</span></span> <span data-ttu-id="53a34-163">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="53a34-163">Defaults to `false`.</span></span> |
| <span data-ttu-id="53a34-164">IncludeRazorContentInPack</span><span class="sxs-lookup"><span data-stu-id="53a34-164">IncludeRazorContentInPack</span></span>                      | <span data-ttu-id="53a34-165">为 `true` 时，所有 Razor 内容项（.cshtml 文件）将标记为包含在生成的 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="53a34-165">When `true`, all Razor content items (*.cshtml* files) will be marked for inclusion in the generated NuGet package.</span></span> <span data-ttu-id="53a34-166">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="53a34-166">Defaults to `false`.</span></span> |
| <span data-ttu-id="53a34-167">EmbedRazorGenerateSources</span><span class="sxs-lookup"><span data-stu-id="53a34-167">EmbedRazorGenerateSources</span></span> | <span data-ttu-id="53a34-168">为 `true` 时，将 RazorGenerate (.cshtml) 项作为嵌入的文件添加到生成的 Razor 程序集中。</span><span class="sxs-lookup"><span data-stu-id="53a34-168">When `true`, adds RazorGenerate (*.cshtml*) items as embedded files to the generated Razor assembly.</span></span> <span data-ttu-id="53a34-169">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="53a34-169">Defaults to `false`.</span></span> |
| <span data-ttu-id="53a34-170">UseRazorBuildServer</span><span class="sxs-lookup"><span data-stu-id="53a34-170">UseRazorBuildServer</span></span>                           | <span data-ttu-id="53a34-171">为 `true` 时，使用永久生成服务器进程来卸载代码生成工作。</span><span class="sxs-lookup"><span data-stu-id="53a34-171">When `true`, uses a persistent build server process to offload code generation work.</span></span> <span data-ttu-id="53a34-172">默认值为 `UseSharedCompilation`。</span><span class="sxs-lookup"><span data-stu-id="53a34-172">Defaults to the value of `UseSharedCompilation`.</span></span> |

### <a name="targets"></a><span data-ttu-id="53a34-173">目标</span><span class="sxs-lookup"><span data-stu-id="53a34-173">Targets</span></span>
<span data-ttu-id="53a34-174">Razor SDK 定义两个主要目标：</span><span class="sxs-lookup"><span data-stu-id="53a34-174">The Razor SDK defines two primary targets:</span></span>

* <span data-ttu-id="53a34-175">`RazorGenerate` - 代码从 RazorGenerate 项元素生成 .cs 文件。</span><span class="sxs-lookup"><span data-stu-id="53a34-175">`RazorGenerate` - Code generates *.cs* files from RazorGenerate item elements.</span></span> <span data-ttu-id="53a34-176">使用 `RazorGenerateDependsOn` 属性指定可在此目标之前或之后运行的其他目标。</span><span class="sxs-lookup"><span data-stu-id="53a34-176">Use `RazorGenerateDependsOn` property to specify additional targets that can run before or after this target.</span></span>
* <span data-ttu-id="53a34-177">`RazorCompile` - 将生成的 .cs 文件编译到 Razor 程序集中。</span><span class="sxs-lookup"><span data-stu-id="53a34-177">`RazorCompile` - Compiles generated *.cs* files in to a Razor assembly.</span></span> <span data-ttu-id="53a34-178">使用 `RazorCompileDependsOn` 指定可在此目标之前或之后运行的其他目标。</span><span class="sxs-lookup"><span data-stu-id="53a34-178">Use `RazorCompileDependsOn` to specify additional targets that can run before or after this target.</span></span>
