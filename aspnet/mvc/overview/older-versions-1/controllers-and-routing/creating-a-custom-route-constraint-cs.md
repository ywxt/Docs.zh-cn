---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: 创建自定义路由约束 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何创建自定义路由约束。 我们实现一个简单的自定义的约束，可防止路由匹配 w...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 0a0b6b706fdb212a745346ffaefc118e85c2a245
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831055"
---
<a name="creating-a-custom-route-constraint-c"></a><span data-ttu-id="00f81-104">创建自定义路由约束 (C#)</span><span class="sxs-lookup"><span data-stu-id="00f81-104">Creating a Custom Route Constraint (C#)</span></span>
====================
<span data-ttu-id="00f81-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="00f81-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="00f81-106">Stephen Walther 演示了如何创建自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="00f81-107">我们实现简单的自定义约束，以防止浏览器请求进行从远程计算机时要匹配的路由。</span><span class="sxs-lookup"><span data-stu-id="00f81-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>


<span data-ttu-id="00f81-108">本教程的目的是演示如何创建自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="00f81-109">自定义路由约束，可防止路由除非匹配某些自定义的条件匹配。</span><span class="sxs-lookup"><span data-stu-id="00f81-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="00f81-110">在本教程中，我们将创建本地主机路由约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="00f81-111">本地主机路由约束只匹配来自本地计算机的请求。</span><span class="sxs-lookup"><span data-stu-id="00f81-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="00f81-112">从在 Internet 上的远程请求都不匹配。</span><span class="sxs-lookup"><span data-stu-id="00f81-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="00f81-113">通过实现 IRouteConstraint 接口实现自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="00f81-114">这是一个极其简单接口，用于描述一个方法：</span><span class="sxs-lookup"><span data-stu-id="00f81-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="00f81-115">该方法返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="00f81-115">The method returns a Boolean value.</span></span> <span data-ttu-id="00f81-116">如果返回 false，与约束关联的路由不会与浏览器请求匹配。</span><span class="sxs-lookup"><span data-stu-id="00f81-116">If you return false, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="00f81-117">在列表 1 中包含的 Localhost 约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="00f81-118">**代码清单 1-LocalhostConstraint.cs**</span><span class="sxs-lookup"><span data-stu-id="00f81-118">**Listing 1 - LocalhostConstraint.cs**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="00f81-119">在列表 1 中的约束利用由 HttpRequest 类公开的 IsLocal 属性。</span><span class="sxs-lookup"><span data-stu-id="00f81-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="00f81-120">该请求的 IP 地址是任一 127.0.0.1 或请求的 IP 是服务器的 IP 地址相同时，此属性返回 true。</span><span class="sxs-lookup"><span data-stu-id="00f81-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="00f81-121">使用 Global.asax 文件中定义的路由中的自定义约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="00f81-122">代码清单 2 中的 Global.asax 文件使用 Localhost 约束以防止任何人请求管理页，除非它们从本地服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="00f81-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="00f81-123">例如，从远程服务器进行时，将失败 /Admin/DeleteAll 的请求。</span><span class="sxs-lookup"><span data-stu-id="00f81-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="00f81-124">**代码清单 2-Global.asax**</span><span class="sxs-lookup"><span data-stu-id="00f81-124">**Listing 2 - Global.asax**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="00f81-125">管理路由的定义中使用 Localhost 约束。</span><span class="sxs-lookup"><span data-stu-id="00f81-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="00f81-126">此路由不会由远程浏览器请求匹配。</span><span class="sxs-lookup"><span data-stu-id="00f81-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="00f81-127">但请注意，在 Global.asax 中定义其他路由可能与相同的请求匹配。</span><span class="sxs-lookup"><span data-stu-id="00f81-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="00f81-128">请务必了解约束匹配的请求阻止特定路由，并不是所有路由在 Global.asax 文件中都定义。</span><span class="sxs-lookup"><span data-stu-id="00f81-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="00f81-129">请注意，默认路由已被注释掉从代码清单 2 中的 Global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="00f81-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="00f81-130">如果包含默认路由，默认路由将匹配的管理控制器的请求。</span><span class="sxs-lookup"><span data-stu-id="00f81-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="00f81-131">在这种情况下，远程用户仍可以调用的管理控制器的操作，即使它们的请求不匹配的管理路由。</span><span class="sxs-lookup"><span data-stu-id="00f81-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="00f81-132">[上一页](creating-a-route-constraint-cs.md)
> [下一页](asp-net-mvc-controller-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="00f81-132">[Previous](creating-a-route-constraint-cs.md)
[Next](asp-net-mvc-controller-overview-vb.md)</span></span>
