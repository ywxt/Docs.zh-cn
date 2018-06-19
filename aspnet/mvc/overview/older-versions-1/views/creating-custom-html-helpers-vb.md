---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 创建自定义 HTML 帮助程序 (VB) |Microsoft 文档
author: microsoft
description: 本教程的目标是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。 通过利用 HTML 帮助程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 6980026e2653eacb71697f9b34def9bc38638726
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871501"
---
<a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="81382-104">创建自定义 HTML 帮助程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="81382-104">Creating Custom HTML Helpers (VB)</span></span>
====================
<span data-ttu-id="81382-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="81382-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="81382-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="81382-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="81382-107">本教程的目标是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。</span><span class="sxs-lookup"><span data-stu-id="81382-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="81382-108">通过利用 HTML 帮助器，可以减少的你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置需要很长时间。</span><span class="sxs-lookup"><span data-stu-id="81382-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="81382-109">本教程的目标是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。</span><span class="sxs-lookup"><span data-stu-id="81382-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="81382-110">通过利用 HTML 帮助器，可以减少的你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置需要很长时间。</span><span class="sxs-lookup"><span data-stu-id="81382-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="81382-111">在本教程的第一部分，我介绍一些现有 ASP.NET MVC framework 附带的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="81382-112">接下来，我介绍了两种方法可以创建自定义 HTML 帮助： 我介绍如何创建共享的方法，以及通过创建扩展方法创建自定义 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="81382-113">了解 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="81382-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="81382-114">HTML 帮助程序是仅返回一个字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="81382-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="81382-115">字符串可以表示任何类型的所需的内容。</span><span class="sxs-lookup"><span data-stu-id="81382-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="81382-116">例如，你可以使用 HTML 帮助器来呈现类似于 HTML 的标准 HTML 标记`<input>`和`<img>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="81382-117">此外可以使用 HTML 帮助器来呈现更复杂的内容，如选项卡条或一个 HTML 表的数据库数据。</span><span class="sxs-lookup"><span data-stu-id="81382-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="81382-118">ASP.NET MVC framework 包括以下一组标准 HTML 帮助器 （这不是完整列表）：</span><span class="sxs-lookup"><span data-stu-id="81382-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="81382-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="81382-119">Html.ActionLink()</span></span>
- <span data-ttu-id="81382-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="81382-120">Html.BeginForm()</span></span>
- <span data-ttu-id="81382-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="81382-121">Html.CheckBox()</span></span>
- <span data-ttu-id="81382-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="81382-122">Html.DropDownList()</span></span>
- <span data-ttu-id="81382-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="81382-123">Html.EndForm()</span></span>
- <span data-ttu-id="81382-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="81382-124">Html.Hidden()</span></span>
- <span data-ttu-id="81382-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="81382-125">Html.ListBox()</span></span>
- <span data-ttu-id="81382-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="81382-126">Html.Password()</span></span>
- <span data-ttu-id="81382-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="81382-127">Html.RadioButton()</span></span>
- <span data-ttu-id="81382-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="81382-128">Html.TextArea()</span></span>
- <span data-ttu-id="81382-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="81382-129">Html.TextBox()</span></span>

<span data-ttu-id="81382-130">例如，考虑列表 1 中的窗体。</span><span class="sxs-lookup"><span data-stu-id="81382-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="81382-131">此窗体将呈现的两个标准 HTML 帮助器 （请参见图 1） 的帮助。</span><span class="sxs-lookup"><span data-stu-id="81382-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="81382-132">此窗体使用`Html.BeginForm()`和`Html.TextBox()`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="81382-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>


<span data-ttu-id="81382-133">[![页呈现的 HTML 帮助器](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="81382-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="81382-134">**图 01**： 页上呈现的 HTML 帮助器 ([单击以查看实际尺寸的图像](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="81382-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>


<span data-ttu-id="81382-135">**列表 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="81382-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="81382-136">`Html.BeginForm()`帮助器方法用于创建的开始和结束 HTML`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="81382-137">请注意，`Html.BeginForm()`方法调用在中使用语句。</span><span class="sxs-lookup"><span data-stu-id="81382-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="81382-138">使用语句可确保`<form>`标记使用的结尾处获取结束块。</span><span class="sxs-lookup"><span data-stu-id="81382-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="81382-139">如果你愿意，而不是创建 using 块中，你可以调用 Html.EndForm() 帮助器方法来关闭`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="81382-140">使用任何方法来创建打开和关闭`<form>`看起来最直观的标记。</span><span class="sxs-lookup"><span data-stu-id="81382-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="81382-141">`Html.TextBox()`帮助器方法列表 1 中使用以呈现 HTML`<input>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="81382-142">如果在你的浏览器中选择查看源你看到列出 2 中的 HTML 源文件。</span><span class="sxs-lookup"><span data-stu-id="81382-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="81382-143">请注意源包含标准的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="81382-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81382-144">请注意，`Html.TextBox()`帮助器呈现的 HTML`<%= %>`标记而不是`<% %>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="81382-145">如果不包含等号，然后执行任何操作获取呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="81382-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="81382-146">ASP.NET MVC framework 包含一小部分的帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="81382-147">最有可能，你将需要扩展的自定义 HTML 帮助器 MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="81382-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="81382-148">在本教程的其余部分中，你了解两种方法可以创建自定义 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="81382-149">**列出 2 – `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="81382-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="81382-150">使用共享方法创建 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="81382-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="81382-151">创建新的 HTML 帮助器的最简单方法是创建一个共享的方法来返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="81382-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="81382-152">例如，假设你决定创建新的 HTML 帮助器上呈现 HTML`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="81382-153">可以使用在列出 2 中的类来呈现`<label>`。</span><span class="sxs-lookup"><span data-stu-id="81382-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="81382-154">**列出 2 – `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="81382-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="81382-155">无需进行任何特殊有关列出 2 中的类。</span><span class="sxs-lookup"><span data-stu-id="81382-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="81382-156">`Label()`方法只需返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="81382-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="81382-157">已修改的索引视图，列出 3 中使用`LabelHelper`呈现 HTML`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="81382-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="81382-158">请注意，则视图包括`<%@ imports %>`导入 Application1.Helpers 命名空间的指令。</span><span class="sxs-lookup"><span data-stu-id="81382-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="81382-159">**列出 2 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="81382-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="81382-160">使用扩展方法中创建 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="81382-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="81382-161">如果你想要创建 HTML 帮助程序，只需工作诸如标准的 HTML 帮助器，它们包含在 ASP.NET MVC framework 中，则需要创建扩展方法。</span><span class="sxs-lookup"><span data-stu-id="81382-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="81382-162">扩展方法使你能够添加到现有类的新方法。</span><span class="sxs-lookup"><span data-stu-id="81382-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="81382-163">在创建一个 HTML 帮助器方法时，你添加到的新方法`HtmlHelper`由视图的 Html 属性表示的类。</span><span class="sxs-lookup"><span data-stu-id="81382-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="81382-164">列出 3 中的 Visual Basic 模块将添加名为的扩展方法`Label()`到`HtmlHelper`类。</span><span class="sxs-lookup"><span data-stu-id="81382-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="81382-165">有一些你应注意到有关此模块的内容。</span><span class="sxs-lookup"><span data-stu-id="81382-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="81382-166">首先，请注意该模块用修饰`<Extension()>`属性。</span><span class="sxs-lookup"><span data-stu-id="81382-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="81382-167">若要使用此属性，必须导入`System.Runtime.CompilerServices`命名空间</span><span class="sxs-lookup"><span data-stu-id="81382-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="81382-168">其次，请注意，第一个参数`Label()`方法表示`HtmlHelper`类。</span><span class="sxs-lookup"><span data-stu-id="81382-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="81382-169">扩展方法的第一个参数指示该扩展方法所扩展的类。</span><span class="sxs-lookup"><span data-stu-id="81382-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="81382-170">**列出 3 – `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="81382-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="81382-171">创建扩展方法，并在成功生成你的应用程序后，该扩展方法将出现在 Visual Studio Intellisense，就像所有其他方法的类 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="81382-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="81382-172">唯一的区别是方法用特殊符号旁边 （图标的向下箭头） 显示该扩展。</span><span class="sxs-lookup"><span data-stu-id="81382-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="81382-173">[![使用 Html.Label() 扩展方法](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="81382-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="81382-174">**图 02**： 使用 Html.Label() 扩展方法 ([单击以查看实际尺寸的图像](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="81382-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>


<span data-ttu-id="81382-175">已修改的索引视图，列出 4 中使用 Html.Label() 扩展方法来呈现的所有其&lt;标签&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="81382-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="81382-176">**列出 4 – `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="81382-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="81382-177">总结</span><span class="sxs-lookup"><span data-stu-id="81382-177">Summary</span></span>

<span data-ttu-id="81382-178">在本教程中，您学习了两种方法可以创建自定义 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="81382-179">首先，您学习了如何创建自定义`Label()`通过创建共享的方法的 HTML 帮助程序返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="81382-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="81382-180">接下来，您学习了如何创建自定义`Label()`通过上创建的扩展方法的 HTML 帮助器方法`HtmlHelper`类。</span><span class="sxs-lookup"><span data-stu-id="81382-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="81382-181">在本教程中，我侧重于生成一个非常简单的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="81382-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="81382-182">请注意，可根据需要一样复杂 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="81382-183">你可以构建呈现如树视图、 菜单或表的数据库数据的丰富内容的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="81382-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="81382-184">[上一页](asp-net-mvc-views-overview-vb.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="81382-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
