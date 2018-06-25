---
title: ASP.NET Core 中的 Razor 文件编译和预编译
author: rick-anderson
description: 了解预编译 Razor 文件的好处以及如何在 ASP.NET Core 应用中完成 Razor 文件预编译。
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
uid: mvc/views/view-compilation
ms.openlocfilehash: 6ef450a24f57c721021f77f6df5088574caa2645
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274035"
---
# <a name="razor-file-compilation-in-aspnet-core"></a><span data-ttu-id="a1e17-103">ASP.NET Core 中的 Razor 文件编译</span><span class="sxs-lookup"><span data-stu-id="a1e17-103">Razor file compilation in ASP.NET Core</span></span>

<span data-ttu-id="a1e17-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a1e17-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-1.1"
<span data-ttu-id="a1e17-105">调用相关的 MVC 视图时，Razor 文件在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="a1e17-105">A Razor file is compiled at runtime, when the associated MVC view is invoked.</span></span> <span data-ttu-id="a1e17-106">不支持在生成时发布 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-106">Build-time Razor file publishing is unsupported.</span></span> <span data-ttu-id="a1e17-107">可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。</span><span class="sxs-lookup"><span data-stu-id="a1e17-107">Razor files can optionally be compiled at publish time and deployed with the app&mdash;using the precompilation tool.</span></span>
::: moniker-end
::: moniker range="= aspnetcore-2.0"
<span data-ttu-id="a1e17-108">调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="a1e17-108">A Razor file is compiled at runtime, when the associated Razor Page or MVC view is invoked.</span></span> <span data-ttu-id="a1e17-109">不支持在生成时发布 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-109">Build-time Razor file publishing is unsupported.</span></span> <span data-ttu-id="a1e17-110">可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。</span><span class="sxs-lookup"><span data-stu-id="a1e17-110">Razor files can optionally be compiled at publish time and deployed with the app&mdash;using the precompilation tool.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="a1e17-111">调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="a1e17-111">A Razor file is compiled at runtime, when the associated Razor Page or MVC view is invoked.</span></span> <span data-ttu-id="a1e17-112">在生成时和发布时使用 [Razor SDK](xref:razor-pages/sdk) 编译 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-112">Razor files are compiled at both build and publish time using the [Razor SDK](xref:razor-pages/sdk).</span></span>
::: moniker-end

## <a name="precompilation-considerations"></a><span data-ttu-id="a1e17-113">预编译注意事项</span><span class="sxs-lookup"><span data-stu-id="a1e17-113">Precompilation considerations</span></span>

<span data-ttu-id="a1e17-114">以下是预编译 Razor 文件的意外后果：</span><span class="sxs-lookup"><span data-stu-id="a1e17-114">The following are side effects of precompiling Razor files:</span></span>

* <span data-ttu-id="a1e17-115">发布捆绑包更小</span><span class="sxs-lookup"><span data-stu-id="a1e17-115">A smaller published bundle</span></span>
* <span data-ttu-id="a1e17-116">启动速度更快</span><span class="sxs-lookup"><span data-stu-id="a1e17-116">A faster startup time</span></span>
* <span data-ttu-id="a1e17-117">无法编辑 Razor 文件&mdash;关联内容不会出现在发布捆绑包中。</span><span class="sxs-lookup"><span data-stu-id="a1e17-117">You can't edit Razor files&mdash;the associated content is absent from the published bundle.</span></span>

## <a name="deploy-precompiled-files"></a><span data-ttu-id="a1e17-118">部署预编译文件</span><span class="sxs-lookup"><span data-stu-id="a1e17-118">Deploy precompiled files</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="a1e17-119">Razor SDK 默认启用 Razor 文件的生成时和发布时编译。</span><span class="sxs-lookup"><span data-stu-id="a1e17-119">Build- and publish-time compilation of Razor files is enabled by default by the Razor SDK.</span></span> <span data-ttu-id="a1e17-120">Razor 文件更新后，支持在生成时编辑这些文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-120">Editing Razor files after they're updated is supported at build time.</span></span> <span data-ttu-id="a1e17-121">默认情况下，仅通过应用部署编译的 Views.dll 而不部署 cshtml 文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-121">By default, only the compiled *Views.dll* and no *.cshtml* files are deployed with your app.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e17-122">仅当项目文件中未设置特定于预编译的属性时，Razor SDK 才有效。</span><span class="sxs-lookup"><span data-stu-id="a1e17-122">The Razor SDK is effective only when no precompilation-specific properties are set in the project file.</span></span> <span data-ttu-id="a1e17-123">例如，通过将 .csproj 文件的 `MvcRazorCompileOnPublish` 属性设置为 `true` 来禁用 Razor SDK。</span><span class="sxs-lookup"><span data-stu-id="a1e17-123">For instance, setting the *.csproj* file's `MvcRazorCompileOnPublish` property to `true` disables the Razor SDK.</span></span>
::: moniker-end

::: moniker range="= aspnetcore-2.0"
<span data-ttu-id="a1e17-124">如果项目面向 .NET Framework，请安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="a1e17-124">If your project targets .NET Framework, install the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet package:</span></span>

<span data-ttu-id="a1e17-125">[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]</span><span class="sxs-lookup"><span data-stu-id="a1e17-125">[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]</span></span>

<span data-ttu-id="a1e17-126">如果项目面向 .NET Core，则无需进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="a1e17-126">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="a1e17-127">默认情况下，ASP.NET Core 2.x 项目模板将 `MvcRazorCompileOnPublish` 属性隐式设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="a1e17-127">The ASP.NET Core 2.x project templates implicitly set the `MvcRazorCompileOnPublish` property to `true` by default.</span></span> <span data-ttu-id="a1e17-128">因此，可以从 .csproj 文件中安全地删除此元素。</span><span class="sxs-lookup"><span data-stu-id="a1e17-128">Consequently, this element can be safely removed from the *.csproj* file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e17-129">在 ASP.NET Core 2.0 中执行[独立部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) 时，无法使用 Razor 文件预编译。</span><span class="sxs-lookup"><span data-stu-id="a1e17-129">Razor file precompilation is unavailable when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span>
::: moniker-end

::: moniker range="= aspnetcore-1.1"
<span data-ttu-id="a1e17-130">将 `MvcRazorCompileOnPublish` 属性设置为 `true`，然后安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a1e17-130">Set the `MvcRazorCompileOnPublish` property to `true`, and install the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet package.</span></span> <span data-ttu-id="a1e17-131">以下 .csproj 示例突出显示了这些设置：</span><span class="sxs-lookup"><span data-stu-id="a1e17-131">The following *.csproj* sample highlights these settings:</span></span>

<span data-ttu-id="a1e17-132">[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]</span><span class="sxs-lookup"><span data-stu-id="a1e17-132">[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]</span></span>
::: moniker-end

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="a1e17-133">使用 [.NET Core CLI 发布命令](/dotnet/core/tools/dotnet-publish)，让应用做好[框架依赖型部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)的准备。</span><span class="sxs-lookup"><span data-stu-id="a1e17-133">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) with the [.NET Core CLI publish command](/dotnet/core/tools/dotnet-publish).</span></span> <span data-ttu-id="a1e17-134">例如，在项目根目录中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="a1e17-134">For example, execute the following command at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="a1e17-135">预编译成功后，将生成包含已编译 Razor 文件的 <project_name>.PrecompiledViews.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="a1e17-135">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor files, is produced when precompilation succeeds.</span></span> <span data-ttu-id="a1e17-136">例如，以下屏幕截图描述了 WebApplication1.PrecompiledViews.dll 中 Index.cshtml 的内容：</span><span class="sxs-lookup"><span data-stu-id="a1e17-136">For example, the screenshot below depicts the contents of *Index.cshtml* within *WebApplication1.PrecompiledViews.dll*:</span></span>

![DLL 中的 Razor 视图](view-compilation/_static/razor-views-in-dll.png)
::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="a1e17-138">其他资源</span><span class="sxs-lookup"><span data-stu-id="a1e17-138">Additional resources</span></span>

::: moniker range="= aspnetcore-1.1"
* <xref:mvc/views/overview>
::: moniker-end

::: moniker range="= aspnetcore-2.0"
* <xref:razor-pages/index>
* <xref:mvc/views/overview>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"
* <xref:razor-pages/index>
* <xref:mvc/views/overview>
* <xref:razor-pages/sdk>
::: moniker-end