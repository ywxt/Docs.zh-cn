---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 使用 TagBuilder 类来生成 HTML 帮助器 (C#) |Microsoft 文档
author: StephenWalther
description: Stephen Walther 向你介绍 TagBuilder 类命名为 ASP.NET MVC framework 中的一个有用的实用工具类。 你可以轻松地使用 TagBuilder 类...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c0e8e4e3a733f2cc8690dc85e3006bce6c661d2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870383"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="3f57d-104">使用 TagBuilder 类来生成 HTML 帮助器 (C#)</span><span class="sxs-lookup"><span data-stu-id="3f57d-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="3f57d-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="3f57d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="3f57d-106">Stephen Walther 向你介绍 TagBuilder 类命名为 ASP.NET MVC framework 中的一个有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="3f57d-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="3f57d-107">TagBuilder 类可用于轻松生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="3f57d-108">ASP.NET MVC framework 包括一个名为生成 HTML 帮助器时，可以使用 TagBuilder 类的有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="3f57d-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="3f57d-109">TagBuilder 类，如所示的类名称，可以轻松地生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="3f57d-110">此简易教程，你将获得 TagBuilder 类的概述并了解如何使用此类时生成简单的 HTML 帮助器上呈现 HTML &lt;img&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="3f57d-111">TagBuilder 类概述</span><span class="sxs-lookup"><span data-stu-id="3f57d-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="3f57d-112">TagBuilder 类包含在 System.Web.Mvc 命名空间。</span><span class="sxs-lookup"><span data-stu-id="3f57d-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="3f57d-113">它具有五个方法：</span><span class="sxs-lookup"><span data-stu-id="3f57d-113">It has five methods:</span></span>

- <span data-ttu-id="3f57d-114">AddCssClass()-可以添加一个新*类 =""* 属性设为标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="3f57d-115">GenerateId()-可以向标记添加 id 属性。</span><span class="sxs-lookup"><span data-stu-id="3f57d-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="3f57d-116">此方法将自动替换 id 中的句点 （默认情况下，期间将被下划线取代）</span><span class="sxs-lookup"><span data-stu-id="3f57d-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="3f57d-117">MergeAttribute()-可以将属性添加到一个标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="3f57d-118">有多个重载此方法。</span><span class="sxs-lookup"><span data-stu-id="3f57d-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="3f57d-119">SetInnerText()-可设置内部标记的文本。</span><span class="sxs-lookup"><span data-stu-id="3f57d-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="3f57d-120">内部文本是 HTML 编码自动。</span><span class="sxs-lookup"><span data-stu-id="3f57d-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="3f57d-121">Tostring （）-可呈现标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="3f57d-122">你可以指定是否想要创建的正常标记、 开始标记、 结束标记或自结束标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="3f57d-123">TagBuilder 类具有四个重要属性：</span><span class="sxs-lookup"><span data-stu-id="3f57d-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="3f57d-124">属性 – 表示的所有标记的属性。</span><span class="sxs-lookup"><span data-stu-id="3f57d-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="3f57d-125">IdAttributeDotReplacement-表示 GenerateId() 方法用于替换的句号 （默认值是一个下划线） 的字符。</span><span class="sxs-lookup"><span data-stu-id="3f57d-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="3f57d-126">InnerHTML-表示标记的内部内容。</span><span class="sxs-lookup"><span data-stu-id="3f57d-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="3f57d-127">将字符串分配给此属性*不*的字符串进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="3f57d-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="3f57d-128">标记名 – 表示标记的名称。</span><span class="sxs-lookup"><span data-stu-id="3f57d-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="3f57d-129">这些方法和属性为你提供的所有基本的方法和你需要生成的 HTML 标记的属性。</span><span class="sxs-lookup"><span data-stu-id="3f57d-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="3f57d-130">实际上，不需要使用 TagBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="3f57d-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="3f57d-131">你可以改为使用 StringBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="3f57d-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="3f57d-132">但是，TagBuilder 类使您的生活略微简化。</span><span class="sxs-lookup"><span data-stu-id="3f57d-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="3f57d-133">创建一个映像 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="3f57d-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="3f57d-134">当你创建 TagBuilder 类的实例时，您传递你想要对 TagBuilder 构造函数生成的标记的名称。</span><span class="sxs-lookup"><span data-stu-id="3f57d-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="3f57d-135">接下来，你可以调用等 AddCssClass 和 MergeAttribute() 方法修改的属性标记的方法。</span><span class="sxs-lookup"><span data-stu-id="3f57d-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="3f57d-136">最后，你可以调用要呈现标记的 tostring （） 方法。</span><span class="sxs-lookup"><span data-stu-id="3f57d-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="3f57d-137">例如，清单 1 包含一个图像 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3f57d-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="3f57d-138">映像帮助程序通过实现的内部表示为 HTML TagBuilder &lt;img&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="3f57d-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="3f57d-139">**列表 1-Helpers\ImageHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="3f57d-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="3f57d-140">列表 1 中的类包含名为映像的两个静态重载的方法。</span><span class="sxs-lookup"><span data-stu-id="3f57d-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="3f57d-141">当调用 Image() 方法时，您可以传递一个对象表示一组的 HTML 特性，或不该对象。</span><span class="sxs-lookup"><span data-stu-id="3f57d-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="3f57d-142">请注意如何 TagBuilder.MergeAttribute() 方法用于将单独的属性，如 src 属性添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="3f57d-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="3f57d-143">请注意，此外，如何 TagBuilder.MergeAttributes() 方法用于将特性的集合添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="3f57d-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="3f57d-144">MergeAttributes() 方法接受一个字典&lt;字符串、 对象&gt;参数。</span><span class="sxs-lookup"><span data-stu-id="3f57d-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="3f57d-145">RouteValueDictionary 类用于将转换表示的属性转换为字典的集合的对象&lt;字符串、 对象&gt;。</span><span class="sxs-lookup"><span data-stu-id="3f57d-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="3f57d-146">创建的映像帮助程序后，你可以在就像任何其他标准 HTML 帮助你 ASP.NET MVC 视图中使用的帮助器。</span><span class="sxs-lookup"><span data-stu-id="3f57d-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="3f57d-147">列出 2 中的视图使用 Image helper 两次显示 Xbox 同一个映像 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="3f57d-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="3f57d-148">Image() 帮助器称为使用或不 HTML 属性集合。</span><span class="sxs-lookup"><span data-stu-id="3f57d-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="3f57d-149">**列出 2-Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="3f57d-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


<span data-ttu-id="3f57d-150">[![新项目对话框](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3f57d-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="3f57d-151">**图 01**： 使用 Image helper ([单击以查看实际尺寸的图像](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="3f57d-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>


<span data-ttu-id="3f57d-152">请注意，你必须导入与 Index.aspx 视图顶部的映像帮助器关联的命名空间。</span><span class="sxs-lookup"><span data-stu-id="3f57d-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="3f57d-153">使用以下指令，帮助器是导入：</span><span class="sxs-lookup"><span data-stu-id="3f57d-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="3f57d-154">[上一页](creating-custom-html-helpers-cs.md)
> [下一页](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3f57d-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>
