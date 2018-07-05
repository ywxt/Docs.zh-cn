---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 使用 TagBuilder 类用于生成 HTML 帮助程序 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 向您介绍 TagBuilder 类命名为 ASP.NET MVC 框架中的一个有用的实用工具类。 可以轻松地使用到的 TagBuilder 类...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ec50fca1d65d95aaf2baf00c84c080ba98bf333
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383863"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="d1717-104">使用 TagBuilder 类用于生成 HTML 帮助程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="d1717-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="d1717-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="d1717-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="d1717-106">Stephen Walther 向您介绍 TagBuilder 类命名为 ASP.NET MVC 框架中的一个有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="d1717-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="d1717-107">TagBuilder 类可用于轻松生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="d1717-108">ASP.NET MVC 框架包括名为可以使用时生成的 HTML 帮助程序的 TagBuilder 类的有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="d1717-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="d1717-109">TagBuilder 类，如所示的类的名称，使您可以轻松地生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="d1717-110">在本简短教程随附的 TagBuilder 类概述并了解如何构建简单的 HTML 帮助器呈现 HTML 时使用此类&lt;i m g&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="d1717-111">TagBuilder 类概述</span><span class="sxs-lookup"><span data-stu-id="d1717-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="d1717-112">TagBuilder 类都包含在 System.Web.Mvc 命名空间。</span><span class="sxs-lookup"><span data-stu-id="d1717-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="d1717-113">它具有五种方法：</span><span class="sxs-lookup"><span data-stu-id="d1717-113">It has five methods:</span></span>

- <span data-ttu-id="d1717-114">AddCssClass()-可以添加一个新*类 =""* 属性为标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="d1717-115">GenerateId()-可以向标记添加一个 id 属性。</span><span class="sxs-lookup"><span data-stu-id="d1717-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="d1717-116">此方法将自动替换 id 中的句点 （默认情况下，期间将被下划线取代）</span><span class="sxs-lookup"><span data-stu-id="d1717-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="d1717-117">MergeAttribute()-可以将属性添加到一个标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="d1717-118">有多个重载的此方法。</span><span class="sxs-lookup"><span data-stu-id="d1717-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="d1717-119">SetInnerText()-可以设置标记的内部文本。</span><span class="sxs-lookup"><span data-stu-id="d1717-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="d1717-120">内部文本是自动 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="d1717-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="d1717-121">Tostring （）-使您能够呈现标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="d1717-122">您可以指定是否想要创建一个正常的标记、 开始标记、 结束标记或自结束标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="d1717-123">TagBuilder 类具有四个重要属性：</span><span class="sxs-lookup"><span data-stu-id="d1717-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="d1717-124">属性 – 表示的所有标记的属性。</span><span class="sxs-lookup"><span data-stu-id="d1717-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="d1717-125">IdAttributeDotReplacement-表示 GenerateId() 方法用于替换 （默认值为下划线） 的句号的字符。</span><span class="sxs-lookup"><span data-stu-id="d1717-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="d1717-126">InnerHTML-表示标记的内部内容。</span><span class="sxs-lookup"><span data-stu-id="d1717-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="d1717-127">将字符串分配给此属性*却不*的字符串进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="d1717-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="d1717-128">TagName-表示标记的名称。</span><span class="sxs-lookup"><span data-stu-id="d1717-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="d1717-129">这些方法和属性提供的所有基本方法和所需的 HTML 标记生成的属性。</span><span class="sxs-lookup"><span data-stu-id="d1717-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="d1717-130">实际上，不必使用 TagBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="d1717-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="d1717-131">可以改为使用 StringBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="d1717-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="d1717-132">但是，TagBuilder 类使您的生活更简单。</span><span class="sxs-lookup"><span data-stu-id="d1717-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="d1717-133">创建图像的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="d1717-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="d1717-134">创建 TagBuilder 类的实例时，你将传递你想要生成到 TagBuilder 构造函数的标记的名称。</span><span class="sxs-lookup"><span data-stu-id="d1717-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="d1717-135">接下来，您可以调用等 AddCssClass 和 MergeAttribute() 方法，若要修改的属性标记的方法。</span><span class="sxs-lookup"><span data-stu-id="d1717-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="d1717-136">最后，调用 tostring （） 方法以呈现标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="d1717-137">例如，列表 1 中包含的图像的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="d1717-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="d1717-138">图像帮助程序在内部实现与表示 HTML TagBuilder &lt;i m g&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="d1717-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="d1717-139">**代码清单 1-Helpers\ImageHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="d1717-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="d1717-140">在列表 1 中的类包含名为映像的两个静态重载的方法。</span><span class="sxs-lookup"><span data-stu-id="d1717-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="d1717-141">当调用 Image() 方法时，您可以传递或不表示一系列 HTML 特性的对象。</span><span class="sxs-lookup"><span data-stu-id="d1717-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="d1717-142">请注意如何使用 TagBuilder.MergeAttribute() 方法以将各个属性如 src 属性添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="d1717-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="d1717-143">此外，请注意如何使用 TagBuilder.MergeAttributes() 方法向 TagBuilder 添加特性的集合。</span><span class="sxs-lookup"><span data-stu-id="d1717-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="d1717-144">MergeAttributes() 方法接受一个字典&lt;string，object&gt;参数。</span><span class="sxs-lookup"><span data-stu-id="d1717-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="d1717-145">RouteValueDictionary 类用于将表示为一个字典的属性集合的对象转换&lt;string，object&gt;。</span><span class="sxs-lookup"><span data-stu-id="d1717-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="d1717-146">创建图像帮助程序后，您可以就像任何其他标准 HTML 帮助程序一样在 ASP.NET MVC 视图中使用该帮助器。</span><span class="sxs-lookup"><span data-stu-id="d1717-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="d1717-147">代码清单 2 中的视图使用图像帮助程序两次显示 Xbox 的同一个图像 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="d1717-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="d1717-148">Image() 帮助者称为使用或不 HTML 特性集合。</span><span class="sxs-lookup"><span data-stu-id="d1717-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="d1717-149">**代码清单 2-Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="d1717-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


<span data-ttu-id="d1717-150">[![新建项目对话框](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d1717-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="d1717-151">**图 01**： 使用图像帮助程序 ([单击以查看实际尺寸的图像](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d1717-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>


<span data-ttu-id="d1717-152">请注意，必须导入 Index.aspx 视图顶部的图像帮助程序关联的命名空间。</span><span class="sxs-lookup"><span data-stu-id="d1717-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="d1717-153">使用以下指令导入帮助程序：</span><span class="sxs-lookup"><span data-stu-id="d1717-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="d1717-154">[上一页](creating-custom-html-helpers-cs.md)
> [下一页](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d1717-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>
