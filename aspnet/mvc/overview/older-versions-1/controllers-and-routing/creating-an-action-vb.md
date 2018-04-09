---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 创建操作 (VB) |Microsoft 文档
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被某项操作的要求。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: c77e4738444c61d60bdd78a50b36f98be41fc271
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-an-action-vb"></a><span data-ttu-id="9df6f-104">创建操作 (VB)</span><span class="sxs-lookup"><span data-stu-id="9df6f-104">Creating an Action (VB)</span></span>
====================
<span data-ttu-id="9df6f-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9df6f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9df6f-106">了解如何向 ASP.NET MVC 控制器中添加新操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="9df6f-107">了解有关该方法将被某项操作的要求。</span><span class="sxs-lookup"><span data-stu-id="9df6f-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="9df6f-108">本教程旨在说明如何创建新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="9df6f-109">你将了解操作方法的要求。</span><span class="sxs-lookup"><span data-stu-id="9df6f-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="9df6f-110">你还了解了如何防止将方法公开为一个操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="9df6f-111">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="9df6f-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="9df6f-112">通过将新方法添加到控制器可将新的操作添加到控制器中。</span><span class="sxs-lookup"><span data-stu-id="9df6f-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="9df6f-113">例如，列表 1 中的控制器包含名为 index （） 的操作和名为 SayHello() 操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="9df6f-114">作为操作公开这两种方法。</span><span class="sxs-lookup"><span data-stu-id="9df6f-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="9df6f-115">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="9df6f-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="9df6f-116">以便公开到为操作 universe，方法必须满足某些要求：</span><span class="sxs-lookup"><span data-stu-id="9df6f-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="9df6f-117">该方法必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="9df6f-117">The method must be public.</span></span>
- <span data-ttu-id="9df6f-118">该方法不能为静态方法。</span><span class="sxs-lookup"><span data-stu-id="9df6f-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="9df6f-119">该方法不能为扩展方法。</span><span class="sxs-lookup"><span data-stu-id="9df6f-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="9df6f-120">该方法不能为构造函数、 getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="9df6f-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="9df6f-121">该方法不能有开放式泛型类型。</span><span class="sxs-lookup"><span data-stu-id="9df6f-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="9df6f-122">该方法不是控制器的基本类的方法。</span><span class="sxs-lookup"><span data-stu-id="9df6f-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="9df6f-123">方法不能包含**ref**或**出**参数。</span><span class="sxs-lookup"><span data-stu-id="9df6f-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="9df6f-124">请注意，有的控制器操作的返回类型没有限制。</span><span class="sxs-lookup"><span data-stu-id="9df6f-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="9df6f-125">控制器操作可以返回一个字符串，DateTime 或 void 随机类的实例。</span><span class="sxs-lookup"><span data-stu-id="9df6f-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="9df6f-126">ASP.NET MVC framework 将转换并不是转换为字符串操作结果的任何返回类型，并呈现到浏览器的字符串。</span><span class="sxs-lookup"><span data-stu-id="9df6f-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="9df6f-127">当添加不违反到控制器的这些要求的任何方法时，该方法将公开为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="9df6f-128">此处必须小心。</span><span class="sxs-lookup"><span data-stu-id="9df6f-128">Be careful here.</span></span> <span data-ttu-id="9df6f-129">连接到 Internet 的任何人都可以调用的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="9df6f-130">例如，不要创建 DeleteMyWebsite() 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9df6f-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="9df6f-131">防止调用公共方法</span><span class="sxs-lookup"><span data-stu-id="9df6f-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="9df6f-132">如果你需要创建一个公共方法中了控制器类并且你不想要公开的控制器操作作为方法，则可以防止使用调用该方法&lt;NonAction&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="9df6f-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="9df6f-133">例如，清单 2 中的控制器包含一个名为 CompanySecrets() 用修饰的公共方法&lt;NonAction&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="9df6f-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="9df6f-134">**Listing 2 - Controllers\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="9df6f-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="9df6f-135">如果你尝试通过在你的浏览器的地址栏中键入 /Work/CompanySecrets 调用 CompanySecrets() 控制器操作然后将图 1 中获得的错误消息。</span><span class="sxs-lookup"><span data-stu-id="9df6f-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


<span data-ttu-id="9df6f-136">[![调用 NonAction 方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9df6f-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="9df6f-137">**图 01**： 调用 NonAction 方法 ([单击以查看实际尺寸的图像](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9df6f-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9df6f-138">[上一页](creating-a-controller-vb.md)
> [下一页](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9df6f-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
