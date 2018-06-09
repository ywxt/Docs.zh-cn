---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态 v。 强类型视图 |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2011
ms.topic: article
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 8a96d43e04a0a50d5176c10c26aa49918a0e56ef
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26504086"
---
<a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="f00f0-103">动态 v。</span><span class="sxs-lookup"><span data-stu-id="f00f0-103">Dynamic v.</span></span> <span data-ttu-id="f00f0-104">强类型化的视图</span><span class="sxs-lookup"><span data-stu-id="f00f0-104">Strongly Typed Views</span></span>
====================
<span data-ttu-id="f00f0-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f00f0-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="f00f0-106">有三种方法将从控制器的信息传递给 ASP.NET MVC 3 中的视图：</span><span class="sxs-lookup"><span data-stu-id="f00f0-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="f00f0-107">作为强类型化的模型对象。</span><span class="sxs-lookup"><span data-stu-id="f00f0-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="f00f0-108">为动态类型 (使用@model动态)</span><span class="sxs-lookup"><span data-stu-id="f00f0-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="f00f0-109">使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="f00f0-109">Using the ViewBag</span></span>

<span data-ttu-id="f00f0-110">我已编写简单的 MVC 3 顶部博客应用程序进行比较和对比动态和强类型化视图。</span><span class="sxs-lookup"><span data-stu-id="f00f0-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="f00f0-111">控制器开头博客的简单列表：</span><span class="sxs-lookup"><span data-stu-id="f00f0-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="f00f0-112">右键单击 IndexNotStonglyTyped() 方法中并添加 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="f00f0-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="f00f0-113">[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f00f0-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="f00f0-114">请确保**创建强类型化视图**不选中复选框。</span><span class="sxs-lookup"><span data-stu-id="f00f0-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="f00f0-115">获得的视图不包含很多：</span><span class="sxs-lookup"><span data-stu-id="f00f0-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="f00f0-116">由于我们要使用动态和不是强类型化的视图，intellisense 不会帮助我们。</span><span class="sxs-lookup"><span data-stu-id="f00f0-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="f00f0-117">已完成的代码所示：</span><span class="sxs-lookup"><span data-stu-id="f00f0-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="f00f0-118">[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f00f0-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="f00f0-119">现在我们将添加一个强类型化的视图。</span><span class="sxs-lookup"><span data-stu-id="f00f0-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="f00f0-120">将以下代码添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="f00f0-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="f00f0-121">请注意它是完全相同返回 View(topBlogs);调用作为非强类型化视图。</span><span class="sxs-lookup"><span data-stu-id="f00f0-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="f00f0-122">右键单击内*StonglyTypedIndex()* 和选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="f00f0-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="f00f0-123">这次请选择**博客**模型类，并选择**列表**作为基架模板。</span><span class="sxs-lookup"><span data-stu-id="f00f0-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="f00f0-124">[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f00f0-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="f00f0-125">在新的视图模板内我们获得 intellisense 支持。</span><span class="sxs-lookup"><span data-stu-id="f00f0-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="f00f0-126">[![7002.intellesince [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f00f0-126">[![7002.intellesince[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="f00f0-127">可以下载 c# 项目[此处](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)。</span><span class="sxs-lookup"><span data-stu-id="f00f0-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
