---
title: ASP.NET Core MVC 的兼容性版本
author: rick-anderson
description: 了解 ASP.NET Core 中的 Startup 类如何配置服务和应用的请求管道。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 04/20/2018
uid: mvc/compatibility-version
ms.openlocfilehash: bedeeba07dcca19176e779f3541c445e94efcd07
ms.sourcegitcommit: 5a2456cbf429069dc48aaa2823cde14100e4c438
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "41910072"
---
# <a name="compatibility-version-for-aspnet-core-mvc"></a><span data-ttu-id="21f68-103">ASP.NET Core MVC 的兼容性版本</span><span class="sxs-lookup"><span data-stu-id="21f68-103">Compatibility version for ASP.NET Core MVC</span></span>

<span data-ttu-id="21f68-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="21f68-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="21f68-105"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 方法允许应用选择加入或退出 ASP.NET Core MVC 2.1 或更高版本中引入的潜在中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="21f68-105">The <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET Core MVC 2.1 or later.</span></span> <span data-ttu-id="21f68-106">这些潜在的中断行为变更通常取决于 MVC 子系统的行为方式以及运行时调用“代码”的方式。</span><span class="sxs-lookup"><span data-stu-id="21f68-106">These potentially breaking behavior changes are generally in how the MVC subsystem behaves and how **your code** is called by the runtime.</span></span> <span data-ttu-id="21f68-107">通过选择加入，你将获取最新的行为以及 ASP.NET Core 的长期行为。</span><span class="sxs-lookup"><span data-stu-id="21f68-107">By opting in, you get the latest behavior, and the long-term behavior of ASP.NET Core.</span></span>

<span data-ttu-id="21f68-108">以下代码将兼容模式设置为 ASP.NET Core 2.1：</span><span class="sxs-lookup"><span data-stu-id="21f68-108">The following code sets the compatibility mode to ASP.NET Core 2.1:</span></span>

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup.cs?name=snippet1)]

<span data-ttu-id="21f68-109">建议使用最新版本 (`CompatibilityVersion.Version_2_1`) 来测试应用。</span><span class="sxs-lookup"><span data-stu-id="21f68-109">We recommend you test your app using the latest version (`CompatibilityVersion.Version_2_1`).</span></span> <span data-ttu-id="21f68-110">我们预计大多数应用不会使用最新版本进行中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="21f68-110">We anticipate that most apps won't have breaking behavior changes using the latest version.</span></span>

<span data-ttu-id="21f68-111">调用 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` 的应用会被阻止进行 ASP.NET Core 2.1 MVC 和更高的 2.x 版本中引入的潜在中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="21f68-111">Apps that call `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` are protected from potentially breaking behavior changes introduced in the ASP.NET Core 2.1 MVC and later 2.x versions.</span></span> <span data-ttu-id="21f68-112">该阻止操作：</span><span class="sxs-lookup"><span data-stu-id="21f68-112">This protection:</span></span>

* <span data-ttu-id="21f68-113">不适用于所有 2.1 和更高版本的更改，它的目标是潜在地中断 MVC 子系统中的 ASP.NET Core 运行时行为变更。</span><span class="sxs-lookup"><span data-stu-id="21f68-113">Does not apply to all 2.1 and later changes, it's targeted to potentially breaking ASP.NET Core runtime behavior changes in the MVC subsystem.</span></span>
* <span data-ttu-id="21f68-114">不会扩展到下一个主要版本。</span><span class="sxs-lookup"><span data-stu-id="21f68-114">Does not extend to the next major version.</span></span>

<span data-ttu-id="21f68-115">未调用 `SetCompatibilityVersion` 的 ASP.NET Core 2.1 和更高 2.x 版本的应用的默认兼容性是 2.0 兼容性。</span><span class="sxs-lookup"><span data-stu-id="21f68-115">The default compatibility for ASP.NET Core 2.1 and later 2.x apps that do **not** call `SetCompatibilityVersion` is 2.0 compatibility.</span></span> <span data-ttu-id="21f68-116">即，未调用 `SetCompatibilityVersion` 与调用 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` 相同。</span><span class="sxs-lookup"><span data-stu-id="21f68-116">That is, not calling `SetCompatibilityVersion` is the same as calling `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`.</span></span>

<span data-ttu-id="21f68-117">以下代码将兼容模式设置为 ASP.NET Core 2.1（以下行为除外）：</span><span class="sxs-lookup"><span data-stu-id="21f68-117">The following code sets the compatibility mode to ASP.NET Core 2.1, except for the following behaviors:</span></span>

* [<span data-ttu-id="21f68-118">AllowCombiningAuthorizeFilters</span><span class="sxs-lookup"><span data-stu-id="21f68-118">AllowCombiningAuthorizeFilters</span></span>](https://github.com/aspnet/Mvc/blob/master/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)
* [<span data-ttu-id="21f68-119">InputFormatterExceptionPolicy</span><span class="sxs-lookup"><span data-stu-id="21f68-119">InputFormatterExceptionPolicy</span></span>](https://github.com/aspnet/Mvc/blob/master/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup2.cs?name=snippet1)]

<span data-ttu-id="21f68-120">对于遇到中断行为变更的应用，请使用适当的兼容性开关：</span><span class="sxs-lookup"><span data-stu-id="21f68-120">For apps that encounter breaking behavior changes, using the appropriate compatibility switches:</span></span>

* <span data-ttu-id="21f68-121">允许使用最新版本并选择退出特定的中断行为变更。</span><span class="sxs-lookup"><span data-stu-id="21f68-121">Allows you to use the latest release and opt out of specific breaking behavior changes.</span></span>
* <span data-ttu-id="21f68-122">请用些时间更新应用，以便其适用于最新更改。</span><span class="sxs-lookup"><span data-stu-id="21f68-122">Gives you time to update your app so it works with the latest changes.</span></span>

<span data-ttu-id="21f68-123">[MvcOptions](https://github.com/aspnet/Mvc/blob/master/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) 类源注释充分地阐述了更改的内容以及为什么更改对大多数用户来说是一种改进。</span><span class="sxs-lookup"><span data-stu-id="21f68-123">The [MvcOptions](https://github.com/aspnet/Mvc/blob/master/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) class source comments have a good explanation of what changed and why the changes are an improvement for most users.</span></span>

<span data-ttu-id="21f68-124">将来会推出 [ASP.NET Core 3.0 版本](https://github.com/aspnet/Home/wiki/Roadmap)。</span><span class="sxs-lookup"><span data-stu-id="21f68-124">At some future date, there will be an [ASP.NET Core 3.0 version](https://github.com/aspnet/Home/wiki/Roadmap).</span></span> <span data-ttu-id="21f68-125">在 3.0 版本中，将删除兼容性开关支持的旧行为。</span><span class="sxs-lookup"><span data-stu-id="21f68-125">Old behaviors supported by compatibility switches will be removed in the 3.0 version.</span></span> <span data-ttu-id="21f68-126">我们认为这些积极的变化几乎使所有用户受益。</span><span class="sxs-lookup"><span data-stu-id="21f68-126">We feel these are positive changes benefitting nearly all users.</span></span> <span data-ttu-id="21f68-127">现在通过引入这些更改，大多数应用可以立即受益，其他人员将有时间更新其应用。</span><span class="sxs-lookup"><span data-stu-id="21f68-127">By introducing these changes now, most apps can benefit now, and the others will have time to update their apps.</span></span>
