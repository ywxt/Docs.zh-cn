---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: 使用 TagBuilder 类来生成 HTML 帮助程序 (VB) |Microsoft 文档
author: StephenWalther
description: Stephen Walther 向你介绍 TagBuilder 类命名为 ASP.NET MVC framework 中的一个有用的实用工具类。 你可以轻松地使用 TagBuilder 类...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 2b72e08dff646f66252f210543230186cab6e641
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872226"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="c4007-104">使用 TagBuilder 类来生成 HTML 帮助程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="c4007-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>
====================
<span data-ttu-id="c4007-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c4007-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c4007-106">Stephen Walther 向你介绍 TagBuilder 类命名为 ASP.NET MVC framework 中的一个有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="c4007-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="c4007-107">TagBuilder 类可用于轻松生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="c4007-108">ASP.NET MVC framework 包括一个名为生成 HTML 帮助器时，可以使用 TagBuilder 类的有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="c4007-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="c4007-109">TagBuilder 类，如所示的类名称，可以轻松地生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="c4007-110">此简易教程，你将获得 TagBuilder 类的概述并了解如何使用此类时生成简单的 HTML 帮助器上呈现 HTML &lt;img&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="c4007-111">TagBuilder 类概述</span><span class="sxs-lookup"><span data-stu-id="c4007-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="c4007-112">TagBuilder 类包含在 System.Web.Mvc 命名空间。</span><span class="sxs-lookup"><span data-stu-id="c4007-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="c4007-113">它具有五个方法：</span><span class="sxs-lookup"><span data-stu-id="c4007-113">It has five methods:</span></span>

- <span data-ttu-id="c4007-114">AddCssClass() – 使您能够添加新*类 =""* 属性设为标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="c4007-115">GenerateId() – 可用于向标记添加 id 属性。</span><span class="sxs-lookup"><span data-stu-id="c4007-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="c4007-116">此方法将自动替换 id 中的句点 （默认情况下，期间将被下划线取代）</span><span class="sxs-lookup"><span data-stu-id="c4007-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="c4007-117">MergeAttribute() – 可以将属性添加到一个标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="c4007-118">有多个重载此方法。</span><span class="sxs-lookup"><span data-stu-id="c4007-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="c4007-119">SetInnerText() – 可设置内部标记的文本。</span><span class="sxs-lookup"><span data-stu-id="c4007-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="c4007-120">内部文本是 HTML 编码自动。</span><span class="sxs-lookup"><span data-stu-id="c4007-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="c4007-121">Tostring （） – 使您能够呈现标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="c4007-122">你可以指定是否想要创建的正常标记、 开始标记、 结束标记或自结束标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="c4007-123">TagBuilder 类具有四个重要属性：</span><span class="sxs-lookup"><span data-stu-id="c4007-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="c4007-124">属性 – 表示的所有标记的属性。</span><span class="sxs-lookup"><span data-stu-id="c4007-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="c4007-125">IdAttributeDotReplacement – 表示 GenerateId() 方法用于替换的句号 （默认值是一个下划线） 的字符。</span><span class="sxs-lookup"><span data-stu-id="c4007-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="c4007-126">InnerHTML – 表示标记的内部内容。</span><span class="sxs-lookup"><span data-stu-id="c4007-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="c4007-127">将字符串分配给此属性*不*的字符串进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="c4007-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="c4007-128">TagName – 表示标记的名称。</span><span class="sxs-lookup"><span data-stu-id="c4007-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="c4007-129">这些方法和属性为你提供的所有基本的方法和你需要生成的 HTML 标记的属性。</span><span class="sxs-lookup"><span data-stu-id="c4007-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="c4007-130">实际上，不需要使用 TagBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="c4007-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="c4007-131">你可以改为使用 StringBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="c4007-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="c4007-132">但是，TagBuilder 类使您的生活略微简化。</span><span class="sxs-lookup"><span data-stu-id="c4007-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="c4007-133">创建一个映像 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="c4007-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="c4007-134">当你创建 TagBuilder 类的实例时，您传递你想要对 TagBuilder 构造函数生成的标记的名称。</span><span class="sxs-lookup"><span data-stu-id="c4007-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="c4007-135">接下来，你可以调用等 AddCssClass 和 MergeAttribute() 方法修改的属性标记的方法。</span><span class="sxs-lookup"><span data-stu-id="c4007-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="c4007-136">最后，你可以调用要呈现标记的 tostring （） 方法。</span><span class="sxs-lookup"><span data-stu-id="c4007-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="c4007-137">例如，清单 1 包含一个图像 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="c4007-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="c4007-138">映像帮助程序通过实现的内部表示为 HTML TagBuilder &lt;img&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="c4007-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="c4007-139">**列表 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="c4007-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="c4007-140">列表 1 中的模块包含名为 Image() 的两个重载的方法。</span><span class="sxs-lookup"><span data-stu-id="c4007-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="c4007-141">当调用 Image() 方法时，您可以传递一个对象表示一组的 HTML 特性，或不该对象。</span><span class="sxs-lookup"><span data-stu-id="c4007-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="c4007-142">请注意如何 TagBuilder.MergeAttribute() 方法用于将单独的属性，如 src 属性添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="c4007-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="c4007-143">请注意，此外，如何 TagBuilder.MergeAttributes() 方法用于将特性的集合添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="c4007-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="c4007-144">MergeAttributes() 方法接受一个字典&lt;字符串、 对象&gt;参数。</span><span class="sxs-lookup"><span data-stu-id="c4007-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="c4007-145">RouteValueDictionary 类用于将转换表示的属性转换为字典的集合的对象&lt;字符串、 对象&gt;。</span><span class="sxs-lookup"><span data-stu-id="c4007-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="c4007-146">创建的映像帮助程序后，你可以在就像任何其他标准 HTML 帮助你 ASP.NET MVC 视图中使用的帮助器。</span><span class="sxs-lookup"><span data-stu-id="c4007-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="c4007-147">列出 2 中的视图使用 Image helper 两次显示 Xbox 同一个映像 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="c4007-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="c4007-148">Image() 帮助器称为使用或不 HTML 属性集合。</span><span class="sxs-lookup"><span data-stu-id="c4007-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="c4007-149">**列出 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="c4007-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]


<span data-ttu-id="c4007-150">[![新项目对话框](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c4007-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="c4007-151">**图 01**： 使用 Image helper ([单击以查看实际尺寸的图像](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c4007-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>


<span data-ttu-id="c4007-152">请注意，你必须导入与 Index.aspx 视图顶部的映像帮助器关联的命名空间。</span><span class="sxs-lookup"><span data-stu-id="c4007-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="c4007-153">使用以下指令，帮助器是导入：</span><span class="sxs-lookup"><span data-stu-id="c4007-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="c4007-154">在 Visual Basic 应用程序中，默认命名空间是应用程序的名称相同。</span><span class="sxs-lookup"><span data-stu-id="c4007-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4007-155">[上一页](creating-custom-html-helpers-vb.md)
> [下一页](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c4007-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
