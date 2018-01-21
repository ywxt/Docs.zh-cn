---
title: "有关 ASP.NET 核心 Microsoft.AspNetCore.All metapackage 2.x 及更高版本"
author: Rick-Anderson
description: "Microsoft.AspNetCore.All metapackage 包括所有受支持的 ASP.NET Core 和实体框架核心包，以及其依赖项。"
ms.author: riande
manager: wpickett
ms.date: 09/20/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/metapackage
ms.openlocfilehash: 8a44ee7ebb7e6b0112000429f1f080bceb7dc895
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
#<a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a><span data-ttu-id="bd9d6-103">有关 ASP.NET 核心 Microsoft.AspNetCore.All metapackage 2.x</span><span class="sxs-lookup"><span data-stu-id="bd9d6-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.x</span></span>

<span data-ttu-id="bd9d6-104">此功能需要 ASP.NET Core 2.x 目标.NET 核心 2.x。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-104">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="bd9d6-105">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="bd9d6-105">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="bd9d6-106">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-106">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="bd9d6-107">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-107">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="bd9d6-108">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-108">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span> 

<span data-ttu-id="bd9d6-109">ASP.NET 核心的所有功能 2.x 并且实体框架核心 2.x 包含在`Microsoft.AspNetCore.All`包。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-109">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="bd9d6-110">默认的项目模板使用此程序包。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-110">The default project templates use this package.</span></span>

<span data-ttu-id="bd9d6-111">版本数`Microsoft.AspNetCore.All`metapackage 表示 ASP.NET Core 版本和实体框架 Core 版本 （.NET Core 版本与对齐）。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-111">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version (aligned with the .NET Core version).</span></span>

<span data-ttu-id="bd9d6-112">应用程序使用`Microsoft.AspNetCore.All`metapackage 自动充分利用[.NET 核心运行时存储](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-112">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](https://docs.microsoft.com/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="bd9d6-113">运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-113">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="bd9d6-114">当你使用`Microsoft.AspNetCore.All`metapackage，**没有**资产从引用的 ASP.NET Core NuGet 包与应用程序部署&mdash;.NET 核心运行时存储区包含这些资产。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-114">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="bd9d6-115">预编译运行时存储中的资产以提高应用程序启动时间。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-115">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="bd9d6-116">你可以使用包修整过程删除不使用的包。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-116">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="bd9d6-117">裁剪后的包不在发布的应用程序输出中。</span><span class="sxs-lookup"><span data-stu-id="bd9d6-117">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="bd9d6-118">以下*.csproj*文件引用`Microsoft.AspNetCore.All`metapackage 有关 ASP.NET 核心：</span><span class="sxs-lookup"><span data-stu-id="bd9d6-118">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[Main](..\mvc\views\view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=9)]
