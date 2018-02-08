---
title: "ASP.NET Core 2.x 及更高版本的 Microsoft.AspNetCore.All 元包"
author: Rick-Anderson
description: "Microsoft.AspNetCore.All 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包及其依赖关系。"
manager: wpickett
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: 07220fdae299723088fa85e452cedff5e5685bd7
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
#<a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a><span data-ttu-id="e5e4b-103">ASP.NET Core 2.x 的 Microsoft.AspNetCore.All 元包</span><span class="sxs-lookup"><span data-stu-id="e5e4b-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.x</span></span>

<span data-ttu-id="e5e4b-104">此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-104">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="e5e4b-105">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="e5e4b-105">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="e5e4b-106">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-106">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="e5e4b-107">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-107">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="e5e4b-108">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-108">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span> 

<span data-ttu-id="e5e4b-109">`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-109">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="e5e4b-110">默认项目模板使用此包。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-110">The default project templates use this package.</span></span>

<span data-ttu-id="e5e4b-111">`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本（与 .NET Core 版本对齐）。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-111">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version (aligned with the .NET Core version).</span></span>

<span data-ttu-id="e5e4b-112">使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-112">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](https://docs.microsoft.com/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="e5e4b-113">此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-113">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="e5e4b-114">使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-114">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="e5e4b-115">运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-115">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="e5e4b-116">可使用包修整过程来删除不使用的包。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-116">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="e5e4b-117">已发布的应用程序输出中排除了修整的包。</span><span class="sxs-lookup"><span data-stu-id="e5e4b-117">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="e5e4b-118">以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：</span><span class="sxs-lookup"><span data-stu-id="e5e4b-118">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[Main](..\mvc\views\view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=9)]
