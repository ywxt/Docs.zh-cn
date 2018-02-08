---
title: "Razor 视图编译和预编译"
author: rick-anderson
description: "解释如何在 ASP.NET Core 应用程序中启用 MVC Razor 视图编译和预编译的参考文档。"
manager: wpickett
ms.author: riande
ms.date: 12/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-compilation
ms.openlocfilehash: bd3f4470035b0375fc79aa7caa73b60ba6fc4f53
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="razor-view-compilation-and-precompilation-in-aspnet-core"></a><span data-ttu-id="fa717-103">ASP.NET Core 中的 Razor 视图编译和预编译</span><span class="sxs-lookup"><span data-stu-id="fa717-103">Razor view compilation and precompilation in ASP.NET Core</span></span>

<span data-ttu-id="fa717-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fa717-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fa717-105">调用视图时，Razor 视图在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="fa717-105">Razor views are compiled at runtime when the view is invoked.</span></span> <span data-ttu-id="fa717-106">ASP.NET Core 1.1.0 及更高版本可以选择性地编译 Razor 视图，并将其与应用一起部署&mdash;这个过程称为预编译。</span><span class="sxs-lookup"><span data-stu-id="fa717-106">ASP.NET Core 1.1.0 and higher can optionally compile Razor views and deploy them with the app&mdash;a process known as precompilation.</span></span> <span data-ttu-id="fa717-107">ASP.NET Core 2.x 项目模板默认启用预编译。</span><span class="sxs-lookup"><span data-stu-id="fa717-107">The ASP.NET Core 2.x project templates enable precompilation by default.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa717-108">在 ASP.NET Core 2.0 中执行[独立部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) 时，Razor 视图预编译当前不可用。</span><span class="sxs-lookup"><span data-stu-id="fa717-108">Razor view precompilation is currently unavailable when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span> <span data-ttu-id="fa717-109">2.1 版本发布后，该功能将可用于 SCD。</span><span class="sxs-lookup"><span data-stu-id="fa717-109">The feature will be available for SCDs when 2.1 releases.</span></span> <span data-ttu-id="fa717-110">有关详细信息，请参阅 [View compilation fails when cross-compiling for Linux on Windows](https://github.com/aspnet/MvcPrecompilation/issues/102)（对 Windows 上的 Linux 进行交叉编译时，视图编译失败）。</span><span class="sxs-lookup"><span data-stu-id="fa717-110">For more information, see [View compilation fails when cross-compiling for Linux on Windows](https://github.com/aspnet/MvcPrecompilation/issues/102).</span></span>

<span data-ttu-id="fa717-111">预编译注意事项：</span><span class="sxs-lookup"><span data-stu-id="fa717-111">Precompilation considerations:</span></span>

* <span data-ttu-id="fa717-112">预编译视图生成的发布捆绑包更小，启动速度更快。</span><span class="sxs-lookup"><span data-stu-id="fa717-112">Precompiling views results in a smaller published bundle and faster startup time.</span></span>
* <span data-ttu-id="fa717-113">在预编译视图之后，无法编辑 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="fa717-113">You can't edit Razor files after you precompile views.</span></span> <span data-ttu-id="fa717-114">已编辑的视图不会出现在发布捆绑包中。</span><span class="sxs-lookup"><span data-stu-id="fa717-114">The edited views won't be present in the published bundle.</span></span> 

<span data-ttu-id="fa717-115">部署预编译的视图：</span><span class="sxs-lookup"><span data-stu-id="fa717-115">To deploy precompiled views:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fa717-116">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fa717-116">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="fa717-117">如果项目面向 .NET Framework，请添加对 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) 的包引用：</span><span class="sxs-lookup"><span data-stu-id="fa717-117">If your project targets .NET Framework, include a package reference to [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span></span>

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

<span data-ttu-id="fa717-118">如果项目面向 .NET Core，则无需进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="fa717-118">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="fa717-119">默认情况下，ASP.NET Core 2.x 项目模板将 `MvcRazorCompileOnPublish` 隐式设置为 `true`，这意味着可以从 .csproj 文件安全地删除此节点。</span><span class="sxs-lookup"><span data-stu-id="fa717-119">The ASP.NET Core 2.x project templates implicitly set `MvcRazorCompileOnPublish` to `true` by default, which means this node can be safely removed from the *.csproj* file.</span></span> <span data-ttu-id="fa717-120">如果希望显式设置，那么将 `MvcRazorCompileOnPublish` 属性设置为 `true` 并没有什么坏处。</span><span class="sxs-lookup"><span data-stu-id="fa717-120">If you prefer to be explicit, there's no harm in setting the `MvcRazorCompileOnPublish` property to `true`.</span></span> <span data-ttu-id="fa717-121">以下 .csproj 示例突出显示了此设置：</span><span class="sxs-lookup"><span data-stu-id="fa717-121">The following *.csproj* sample highlights this setting:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fa717-122">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fa717-122">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="fa717-123">将 `MvcRazorCompileOnPublish` 设置为 `true`，并添加对 `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` 的包引用。</span><span class="sxs-lookup"><span data-stu-id="fa717-123">Set `MvcRazorCompileOnPublish` to `true`, and include a package reference to `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`.</span></span> <span data-ttu-id="fa717-124">以下 .csproj 示例突出显示了这些设置：</span><span class="sxs-lookup"><span data-stu-id="fa717-124">The following *.csproj* sample highlights these settings:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish.csproj?highlight=5,12)]

---

<span data-ttu-id="fa717-125">通过执行项目根处的如下命令，为[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)准备应用：</span><span class="sxs-lookup"><span data-stu-id="fa717-125">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) by executing a command such as the following at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="fa717-126">预编译成功后，将生成包含已编译 Razor 视图的 <project_name> .PrecompiledViews.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="fa717-126">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor views, is produced when precompilation succeeds.</span></span> <span data-ttu-id="fa717-127">例如，以下屏幕截图描述了 WebApplication1.PrecompiledViews.dll 中 Index.cshtml 的内容：</span><span class="sxs-lookup"><span data-stu-id="fa717-127">For example, the screenshot below depicts the contents of *Index.cshtml* inside of *WebApplication1.PrecompiledViews.dll*:</span></span>

![DLL 中的 Razor 视图](view-compilation/_static/razor-views-in-dll.png)
