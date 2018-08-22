---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态类型化。 强类型视图 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 41a47f0f6e5fd900e8bf35c37ed98566fe416ace
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824458"
---
<a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="67a3b-103">动态类型化。</span><span class="sxs-lookup"><span data-stu-id="67a3b-103">Dynamic v.</span></span> <span data-ttu-id="67a3b-104">强类型化的视图</span><span class="sxs-lookup"><span data-stu-id="67a3b-104">Strongly Typed Views</span></span>
====================
<span data-ttu-id="67a3b-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="67a3b-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="67a3b-106">有三种方法将信息从控制器传递到 ASP.NET MVC 3 中的视图：</span><span class="sxs-lookup"><span data-stu-id="67a3b-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="67a3b-107">作为强类型化的模型对象。</span><span class="sxs-lookup"><span data-stu-id="67a3b-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="67a3b-108">为动态类型 (使用@model动态)</span><span class="sxs-lookup"><span data-stu-id="67a3b-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="67a3b-109">使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="67a3b-109">Using the ViewBag</span></span>

<span data-ttu-id="67a3b-110">我编写了一个简单的 MVC 3 顶部博客应用程序进行比较和对比动态和强类型化视图。</span><span class="sxs-lookup"><span data-stu-id="67a3b-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="67a3b-111">在控制器启动与一系列简单的博客：</span><span class="sxs-lookup"><span data-stu-id="67a3b-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="67a3b-112">IndexNotStonglyTyped() 方法中右键单击并添加 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="67a3b-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="67a3b-113">[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="67a3b-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="67a3b-114">请确保**创建强类型化视图**框未选中。</span><span class="sxs-lookup"><span data-stu-id="67a3b-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="67a3b-115">生成的视图不包含很多：</span><span class="sxs-lookup"><span data-stu-id="67a3b-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="67a3b-116">因为我们使用的动态和不是强类型化的视图，intellisense 不会帮助我们。</span><span class="sxs-lookup"><span data-stu-id="67a3b-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="67a3b-117">已完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="67a3b-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="67a3b-118">[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="67a3b-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="67a3b-119">现在我们将添加一个强类型化的视图。</span><span class="sxs-lookup"><span data-stu-id="67a3b-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="67a3b-120">将以下代码添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="67a3b-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="67a3b-121">请注意，它是完全相同返回 View(topBlogs);调用作为非强类型视图。</span><span class="sxs-lookup"><span data-stu-id="67a3b-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="67a3b-122">右键单击的内部*StonglyTypedIndex()* ，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="67a3b-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="67a3b-123">这次请选择**博客**模型类，然后选择**列表**为基架模板。</span><span class="sxs-lookup"><span data-stu-id="67a3b-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="67a3b-124">[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="67a3b-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="67a3b-125">在新的视图模板中，我们将获得 intellisense 支持。</span><span class="sxs-lookup"><span data-stu-id="67a3b-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="67a3b-126">[![7002.intellesince [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="67a3b-126">[![7002.intellesince[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="67a3b-127">可以下载 c# 项目[此处](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)。</span><span class="sxs-lookup"><span data-stu-id="67a3b-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
