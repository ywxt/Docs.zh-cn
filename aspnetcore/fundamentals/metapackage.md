---
title: ASP.NET Core 2.0 及更高版本的 Microsoft.AspNetCore.All 元包
author: Rick-Anderson
description: Microsoft.AspNetCore.All 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包及其依赖关系。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: fbb76f41f3178ddc4e51faa14edece1869a30cd0
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729072"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a><span data-ttu-id="a7595-103">ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包</span><span class="sxs-lookup"><span data-stu-id="a7595-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.0</span></span>

> [!NOTE]
> <span data-ttu-id="a7595-104">对于面向 ASP.NET Core 2.1 及更高版本的应用程序，建议使用 [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) 而不是此包。</span><span class="sxs-lookup"><span data-stu-id="a7595-104">We recommend applications targeting ASP.NET Core 2.1 and later use the [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) rather than this package.</span></span> <span data-ttu-id="a7595-105">请参阅本文中的[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](#migrate)。</span><span class="sxs-lookup"><span data-stu-id="a7595-105">See [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](#migrate) in this article.</span></span>

<span data-ttu-id="a7595-106">此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。</span><span class="sxs-lookup"><span data-stu-id="a7595-106">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="a7595-107">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="a7595-107">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="a7595-108">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="a7595-108">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="a7595-109">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="a7595-109">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="a7595-110">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a7595-110">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span> 

<span data-ttu-id="a7595-111">`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="a7595-111">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="a7595-112">定目标到 ASP.NET Core 2.0 的默认项目模板使用此包。</span><span class="sxs-lookup"><span data-stu-id="a7595-112">The default project templates targeting ASP.NET Core 2.0 use this package.</span></span>

<span data-ttu-id="a7595-113">`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。</span><span class="sxs-lookup"><span data-stu-id="a7595-113">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="a7595-114">使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)。</span><span class="sxs-lookup"><span data-stu-id="a7595-114">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](https://docs.microsoft.com/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="a7595-115">此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。</span><span class="sxs-lookup"><span data-stu-id="a7595-115">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="a7595-116">使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。</span><span class="sxs-lookup"><span data-stu-id="a7595-116">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="a7595-117">运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。</span><span class="sxs-lookup"><span data-stu-id="a7595-117">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="a7595-118">可使用包修整过程来删除不使用的包。</span><span class="sxs-lookup"><span data-stu-id="a7595-118">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="a7595-119">已发布的应用程序输出中排除了修整的包。</span><span class="sxs-lookup"><span data-stu-id="a7595-119">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="a7595-120">以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：</span><span class="sxs-lookup"><span data-stu-id="a7595-120">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=6)]

<a name="migrate"></a>
## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a><span data-ttu-id="a7595-121">从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="a7595-121">Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App</span></span>

<span data-ttu-id="a7595-122">`Microsoft.AspNetCore.All` 包中包含以下包，而 `Microsoft.AspNetCore.App` 包中不包含以下包。</span><span class="sxs-lookup"><span data-stu-id="a7595-122">The following packages are included in `Microsoft.AspNetCore.All` but not the `Microsoft.AspNetCore.App` package.</span></span> 

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

<span data-ttu-id="a7595-123">要从 `Microsoft.AspNetCore.All` 移到 `Microsoft.AspNetCore.App`，如果应用使用上述包或由这些包引入的包中的任何 API，请在项目中添加对这些包的引用。</span><span class="sxs-lookup"><span data-stu-id="a7595-123">To move from `Microsoft.AspNetCore.All` to `Microsoft.AspNetCore.App`, if your app uses any APIs from the above packages, or packages brought in by those packages, add references to those packages in your project.</span></span>

<span data-ttu-id="a7595-124">不会隐式包含非 `Microsoft.AspNetCore.App` 依赖项的上述包的任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="a7595-124">Any dependencies of the preceding packages that otherwise aren't dependencies of `Microsoft.AspNetCore.App` are not included implicitly.</span></span> <span data-ttu-id="a7595-125">例如:</span><span class="sxs-lookup"><span data-stu-id="a7595-125">For example:</span></span>

* <span data-ttu-id="a7595-126">`StackExchange.Redis` 作为 `Microsoft.Extensions.Caching.Redis` 的依赖项</span><span class="sxs-lookup"><span data-stu-id="a7595-126">`StackExchange.Redis` as a dependency of `Microsoft.Extensions.Caching.Redis`</span></span>
* <span data-ttu-id="a7595-127">`Microsoft.ApplicationInsights` 作为 `Microsoft.AspNetCore.ApplicationInsights.HostingStartup` 的依赖项</span><span class="sxs-lookup"><span data-stu-id="a7595-127">`Microsoft.ApplicationInsights` as a dependency of `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`</span></span>
