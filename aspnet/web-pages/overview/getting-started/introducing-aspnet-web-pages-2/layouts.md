---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: Introducing ASP.NET Web 页面-创建一致布局 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何使用布局来使用 ASP.NET Web Pages 站点上创建一致的外观的页面。 它假定你已完成...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: a6a007678d58547e9987ebda46bd08ae8aea66f7
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021168"
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="8a166-104">ASP.NET 网页简介-创建一致布局</span><span class="sxs-lookup"><span data-stu-id="8a166-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>
====================
<span data-ttu-id="8a166-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8a166-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8a166-106">本教程演示如何使用*布局*使用 ASP.NET Web Pages 站点上创建一致的外观的页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="8a166-107">它假定你已完成通过时序[删除数据库数据在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584)。</span><span class="sxs-lookup"><span data-stu-id="8a166-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="8a166-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="8a166-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="8a166-109">布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-109">What a layout page is.</span></span>
> - <span data-ttu-id="8a166-110">如何结合使用动态内容的布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="8a166-111">如何将值传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-111">How to pass values to a layout page.</span></span>


## <a name="about-layouts"></a><span data-ttu-id="8a166-112">关于布局</span><span class="sxs-lookup"><span data-stu-id="8a166-112">About Layouts</span></span>

<span data-ttu-id="8a166-113">到目前为止您已创建的页面都有过完成后，独立页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="8a166-114">它们都属于相同的站点，但它们不具有任何通用元素或标准外观。</span><span class="sxs-lookup"><span data-stu-id="8a166-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="8a166-115">大多数站点所拥有的一致的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="8a166-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="8a166-116">例如，如果你转到[Microsoft.com/web](https://www.microsoft.com/web/)站点并看看，您看到页面都符合整体布局和视觉主题：</span><span class="sxs-lookup"><span data-stu-id="8a166-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![Microsoft.com/web 站点页面布局的标头、 导航区域中，内容区域和页脚](layouts/_static/image1.png)

<span data-ttu-id="8a166-118">*低效*创建此布局的方法可能是定义标头、 导航栏中和页脚分别在每个页面上。</span><span class="sxs-lookup"><span data-stu-id="8a166-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="8a166-119">您将会复制相同的标记每个时间。</span><span class="sxs-lookup"><span data-stu-id="8a166-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="8a166-120">如果你想要更改某些内容 （例如，更新页脚），必须单独更改每个页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="8a166-121">这正是*布局页*进入。</span><span class="sxs-lookup"><span data-stu-id="8a166-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="8a166-122">ASP.NET Web Pages 中，您可以定义提供站点页面的整体容器布局页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="8a166-123">例如，布局页可以包含页眉、 导航区域中和页脚。</span><span class="sxs-lookup"><span data-stu-id="8a166-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="8a166-124">布局页包括主要内容的位置的占位符。</span><span class="sxs-lookup"><span data-stu-id="8a166-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="8a166-125">然后，您可以定义包含标记和仅该页面的代码的各个内容页。</span><span class="sxs-lookup"><span data-stu-id="8a166-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="8a166-126">内容页面不必是完整的 HTML 页面; 例如：他们甚至不需要具有`<body>`元素。</span><span class="sxs-lookup"><span data-stu-id="8a166-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="8a166-127">它们还具有一行告诉你想要显示中的内容布局页面的 ASP.NET 代码。</span><span class="sxs-lookup"><span data-stu-id="8a166-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="8a166-128">下面是大致显示此关系的工作方式的图片：</span><span class="sxs-lookup"><span data-stu-id="8a166-128">Here's a picture that shows roughly how this relationship works:</span></span>

![显示两个内容页面和布局页容纳其中的概念图](layouts/_static/image2.png)

<span data-ttu-id="8a166-130">这种交互很容易地了解观察它的运行时。</span><span class="sxs-lookup"><span data-stu-id="8a166-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="8a166-131">在本教程中，你将更改您的电影页面要使用的布局。</span><span class="sxs-lookup"><span data-stu-id="8a166-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="8a166-132">添加布局页</span><span class="sxs-lookup"><span data-stu-id="8a166-132">Adding a Layout Page</span></span>

<span data-ttu-id="8a166-133">您将首先创建定义与标头、 页脚和用于显示主要内容区域的典型页面布局的布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="8a166-134">在 WebPagesMovies 站点中，添加名为 CSHTML 页面 *\_Layout.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8a166-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="8a166-135">前导下划线 ( `_` ) 字符非常重要。</span><span class="sxs-lookup"><span data-stu-id="8a166-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="8a166-136">如果页面的名称以下划线开头，ASP.NET 不会直接向浏览器发送该页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="8a166-137">此约定可定义所需的站点，但该用户不能直接请求的页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="8a166-138">中页面的内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="8a166-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="8a166-139">正如您所看到的此标记是只需使用的 HTML`<div>`元素可多页以及一个定义三个部分`<div>`元素，用以存放的三个部分。</span><span class="sxs-lookup"><span data-stu-id="8a166-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="8a166-140">页脚包含少量的 Razor 代码： `@DateTime.Now.Year`，这将在该位置的页中呈现当前年份。</span><span class="sxs-lookup"><span data-stu-id="8a166-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="8a166-141">请注意，没有名为的样式表的链接*Movies.css*。</span><span class="sxs-lookup"><span data-stu-id="8a166-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="8a166-142">样式表是可在其中定义元素的物理布局的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8a166-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="8a166-143">你将在稍后创建的。</span><span class="sxs-lookup"><span data-stu-id="8a166-143">You'll create that in a moment.</span></span>

<span data-ttu-id="8a166-144">在此唯一不寻常的功能 *\_Layout.cshtml*页是`@Render.Body()`行。</span><span class="sxs-lookup"><span data-stu-id="8a166-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="8a166-145">这就是此布局合并与另一页面时内容何处的占位符。</span><span class="sxs-lookup"><span data-stu-id="8a166-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="8a166-146">添加.css 文件</span><span class="sxs-lookup"><span data-stu-id="8a166-146">Adding a .css File</span></span>

<span data-ttu-id="8a166-147">页上定义的元素的实际排列方式 （即，外观） 的首选的方法是使用级联样式表 (CSS) 规则。</span><span class="sxs-lookup"><span data-stu-id="8a166-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="8a166-148">因此将创建 *.css*具有新布局的规则文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="8a166-149">在 WebMatrix 中，选择你的站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="8a166-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="8a166-150">然后在**文件**选项卡的功能区中，单击下的箭头**新建**按钮，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="8a166-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![在功能区下新建的新建文件夹选项。](layouts/_static/image3.png)

<span data-ttu-id="8a166-152">将新文件夹命名*样式*。</span><span class="sxs-lookup"><span data-stu-id="8a166-152">Name the new folder *Styles*.</span></span>

![命名的新文件夹样式](layouts/_static/image4.png)

<span data-ttu-id="8a166-154">在新*样式*文件夹中，创建名为的文件*Movies.css*。</span><span class="sxs-lookup"><span data-stu-id="8a166-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![创建新的 Movies.css 文件](layouts/_static/image5.png)

<span data-ttu-id="8a166-156">新的内容替换为 *.css*具有以下文件：</span><span class="sxs-lookup"><span data-stu-id="8a166-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="8a166-157">我们不会说很多有关这些 CSS 规则，只是想说明两件事情。</span><span class="sxs-lookup"><span data-stu-id="8a166-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="8a166-158">一个是，除了设置字体和大小，这些规则使用绝对定位来指定标头、 页脚和主要内容区域的位置。</span><span class="sxs-lookup"><span data-stu-id="8a166-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="8a166-159">如果您是初次接触定位在 CSS 中，你可以读取[CSS 定位](http://www.w3schools.com/css/css_positioning.asp)W3Schools 站点教程。</span><span class="sxs-lookup"><span data-stu-id="8a166-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="8a166-160">请注意，在底部，我们已复制最初的样式规则中单独定义的另外一点*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="8a166-161">这些规则中使用[简介显示数据通过使用 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580)教程，以使`WebGrid`帮助器呈现添加到表中的条带化的标记。</span><span class="sxs-lookup"><span data-stu-id="8a166-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="8a166-162">(如果您将使用 *.css*文件有关样式定义，您也可能给整个站点的样式规则中。)</span><span class="sxs-lookup"><span data-stu-id="8a166-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="8a166-163">更新要使用布局的电影文件</span><span class="sxs-lookup"><span data-stu-id="8a166-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="8a166-164">现在可以更新站点以使用新的布局中的现有文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="8a166-165">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="8a166-166">在顶部，为第一行代码，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="8a166-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="8a166-167">该页面现在开始方式如下：</span><span class="sxs-lookup"><span data-stu-id="8a166-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="8a166-168">这行代码告诉 ASP.NET，当*电影*页上运行，它应与合并 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="8a166-169">由于*Movies.cshtml*文件现在所使用的布局页，可以删除从标记*Movies.cshtml*已处理的页 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="8a166-170">拿出`<!DOCTYPE>`， `<html>`，和`<body>`开始和结束标记。</span><span class="sxs-lookup"><span data-stu-id="8a166-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="8a166-171">拿出整个`<head>`元素和其内容，包括网格中的样式规则，因为您现在已经获得这些规则 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="8a166-172">既然您在它，请更改现有`<h1>`元素`<h2>`元素; 必须`<h1>`已在布局页面中的元素。</span><span class="sxs-lookup"><span data-stu-id="8a166-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="8a166-173">更改`<h2>`"列表 Movies"的文本。</span><span class="sxs-lookup"><span data-stu-id="8a166-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="8a166-174">通常情况下不会有内容页中进行这些各种更改。</span><span class="sxs-lookup"><span data-stu-id="8a166-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="8a166-175">时使用布局页，可以启动你的站点，请首先创建不包含所有这些元素的内容页面。</span><span class="sxs-lookup"><span data-stu-id="8a166-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="8a166-176">在这种情况下，不过，您会转换为独立页面另一个使用一种布局，因此没有进行一些清理。</span><span class="sxs-lookup"><span data-stu-id="8a166-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="8a166-177">当您结束， *Movies.cshtml*页面将如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a166-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="8a166-178">测试布局</span><span class="sxs-lookup"><span data-stu-id="8a166-178">Testing the Layout</span></span>

<span data-ttu-id="8a166-179">现在可以看到布局如下所示。</span><span class="sxs-lookup"><span data-stu-id="8a166-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="8a166-180">在 WebMatrix 中，右键单击*Movies.cshtml*页，然后选择**浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="8a166-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="8a166-181">当浏览器显示页面时，它会查找此页面所示：</span><span class="sxs-lookup"><span data-stu-id="8a166-181">When the browser displays the page, it looks like this page:</span></span>

![使用一种布局呈现电影页面](layouts/_static/image6.png)

<span data-ttu-id="8a166-183">ASP.NET 已合并到 Movies.cshtml 页的内容 *\_Layout.cshtml*页面，在右此处`RenderBody`方法。</span><span class="sxs-lookup"><span data-stu-id="8a166-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="8a166-184">当然 *\_Layout.cshtml*页上的引用 *.css*文件，用于定义页面的外观。</span><span class="sxs-lookup"><span data-stu-id="8a166-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="8a166-185">正在更新 AddMovie 页后，可以使用布局</span><span class="sxs-lookup"><span data-stu-id="8a166-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="8a166-186">布局的真正优点是可以使用它们的所有页在你的站点中。</span><span class="sxs-lookup"><span data-stu-id="8a166-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="8a166-187">打开*AddMovie.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="8a166-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="8a166-188">你可能会记住*AddMovie.cshtml*页最初在其中以定义查找范围的验证错误消息中发生某些 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="8a166-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="8a166-189">因为必须 *.css*文件中为你的网站现在，可以移动到这些规则 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="8a166-190">从其中移除这些*AddMovie.cshtml*文件，并将其添加到底部*Movies.css*文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="8a166-191">要移动的以下规则：</span><span class="sxs-lookup"><span data-stu-id="8a166-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="8a166-192">现在，进行中的更改的相同排序*AddMovie.cshtml*与针对*Movies.cshtml* — 添加`Layout="~/_Layout.cshtml;`和删除现在是无关的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="8a166-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="8a166-193">更改`<h1>`元素`<h2>`。</span><span class="sxs-lookup"><span data-stu-id="8a166-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="8a166-194">完成后，页上将看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="8a166-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="8a166-195">运行页。</span><span class="sxs-lookup"><span data-stu-id="8a166-195">Run the page.</span></span> <span data-ttu-id="8a166-196">现在看起来类似于此图：</span><span class="sxs-lookup"><span data-stu-id="8a166-196">Now it looks like this illustration:</span></span>

![使用一种布局呈现电影中添加页](layouts/_static/image7.png)

<span data-ttu-id="8a166-198">你想要在站点中的页面进行类似的更改 — *EditMovie.cshtml*并*DeleteMovie.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8a166-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="8a166-199">但是，在执行之前，可使另一项更改使更灵活的布局。</span><span class="sxs-lookup"><span data-stu-id="8a166-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="8a166-200">传递到布局页的标题信息</span><span class="sxs-lookup"><span data-stu-id="8a166-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="8a166-201">*\_Layout.cshtml*创建的页具有`<title>`设置为"My 电影 Site"的元素。</span><span class="sxs-lookup"><span data-stu-id="8a166-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="8a166-202">大多数浏览器将此元素的内容显示为一个选项卡上的文本：</span><span class="sxs-lookup"><span data-stu-id="8a166-202">Most browsers display the content of this element as the text on a tab:</span></span>

![页面的&lt;标题&gt;浏览器选项卡中显示的元素](layouts/_static/image8.png)

<span data-ttu-id="8a166-204">此标题信息是泛型方法。</span><span class="sxs-lookup"><span data-stu-id="8a166-204">This title information is generic.</span></span> <span data-ttu-id="8a166-205">假设你想要将更多特定于当前页的标题文本。</span><span class="sxs-lookup"><span data-stu-id="8a166-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="8a166-206">（标题文本还用于通过搜索引擎确定您的页面的内容。）可以将信息从所示的内容页面传递*Movies.cshtml*或*AddMovie.cshtml*到布局页，然后使用该信息以自定义布局页面呈现。</span><span class="sxs-lookup"><span data-stu-id="8a166-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="8a166-207">打开*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="8a166-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="8a166-208">在顶部代码中，添加以下行：</span><span class="sxs-lookup"><span data-stu-id="8a166-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="8a166-209">`Page`对象是可用于所有 *.cshtml*页，一个用于此目的，即页面和其布局之间共享信息。</span><span class="sxs-lookup"><span data-stu-id="8a166-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="8a166-210">打开<em>\_Layout.cshtml</em>页。</span><span class="sxs-lookup"><span data-stu-id="8a166-210">Open the<em>\_Layout.cshtml</em> page.</span></span> <span data-ttu-id="8a166-211">更改`<title>`元素，使其看起来像此标记：</span><span class="sxs-lookup"><span data-stu-id="8a166-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="8a166-212">此代码将呈现任何处于`Page.Title`坐在该位置的页中的属性。</span><span class="sxs-lookup"><span data-stu-id="8a166-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="8a166-213">运行*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="8a166-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="8a166-214">这一次浏览器选项卡显示您作为值传递`Page.Title`:</span><span class="sxs-lookup"><span data-stu-id="8a166-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![显示标题动态创建一个浏览器选项卡](layouts/_static/image9.png)

<span data-ttu-id="8a166-216">如果您想在浏览器中查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="8a166-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="8a166-217">你可以看到`<title>`元素呈现为`<title>List Movies</title>`。</span><span class="sxs-lookup"><span data-stu-id="8a166-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="8a166-218">**Page 对象**</span><span class="sxs-lookup"><span data-stu-id="8a166-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="8a166-219">一个有用的功能`Page`是它是一个动态对象 —`Title`属性不是固定或保留的名称。</span><span class="sxs-lookup"><span data-stu-id="8a166-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="8a166-220">可以使用*任何*名称的值为`Page`对象。</span><span class="sxs-lookup"><span data-stu-id="8a166-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="8a166-221">例如，可以轻松传递标题使用名为的属性`Page.CurrentName`或`Page.MyPage`。</span><span class="sxs-lookup"><span data-stu-id="8a166-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="8a166-222">唯一的限制是，该名称必须遵循常规的规则来可命名为哪些属性。</span><span class="sxs-lookup"><span data-stu-id="8a166-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="8a166-223">（例如，名称不能包含空格。）</span><span class="sxs-lookup"><span data-stu-id="8a166-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="8a166-224">可以将任意数量的值传递使用`Page`对象。</span><span class="sxs-lookup"><span data-stu-id="8a166-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="8a166-225">如果你想要将电影信息传递给布局页，可以通过使用类似于传递值`Page.MovieTitle`并`Page.Genre`和`Page.MovieYear`。</span><span class="sxs-lookup"><span data-stu-id="8a166-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="8a166-226">（或者是您发明来存储的信息的任何其他名称。）唯一的要求，这是可能明显 — 是，您必须使用内容页和布局页中的相同名称。</span><span class="sxs-lookup"><span data-stu-id="8a166-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="8a166-227">使用传递的信息`Page`对象并不局限于只是要布局页上显示的文本。</span><span class="sxs-lookup"><span data-stu-id="8a166-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="8a166-228">可以将值传递给布局页中，并在布局页面中的代码然后使用的值来确定是否要显示的页上，部分什么 *.css*文件以使用，等等。</span><span class="sxs-lookup"><span data-stu-id="8a166-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="8a166-229">在传递的值`Page`对象是像任何其他值的代码中使用。</span><span class="sxs-lookup"><span data-stu-id="8a166-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="8a166-230">它只是源自在内容页中的值，并传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>


<span data-ttu-id="8a166-231">打开*AddMovie.cshtml*页上，并将行添加到代码提供的标题的顶部*AddMovie.cshtml*页：</span><span class="sxs-lookup"><span data-stu-id="8a166-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="8a166-232">运行*AddMovie.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="8a166-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="8a166-233">请参阅新标题：</span><span class="sxs-lookup"><span data-stu-id="8a166-233">You see the new title there:</span></span>

![显示添加电影标题动态创建一个浏览器选项卡](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="8a166-235">更新剩余页面以使用布局</span><span class="sxs-lookup"><span data-stu-id="8a166-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="8a166-236">现在可以在你的站点中完成剩余的页，以便它们使用新的布局。</span><span class="sxs-lookup"><span data-stu-id="8a166-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="8a166-237">打开*EditMovie.cshtml*并*DeleteMovie.cshtml*又和每个中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="8a166-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="8a166-238">添加链接到的布局页面的代码行：</span><span class="sxs-lookup"><span data-stu-id="8a166-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="8a166-239">添加行以设置页的标题：</span><span class="sxs-lookup"><span data-stu-id="8a166-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="8a166-240">或：</span><span class="sxs-lookup"><span data-stu-id="8a166-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="8a166-241">删除所有多余的 HTML 标记，基本上，将保留内的位`<body>`元素 （加上在顶部的代码块）。</span><span class="sxs-lookup"><span data-stu-id="8a166-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="8a166-242">更改`<h1>`元素为`<h2>`元素。</span><span class="sxs-lookup"><span data-stu-id="8a166-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="8a166-243">完成这些更改，测试每个，并确保它正确显示并且标题正确无误。</span><span class="sxs-lookup"><span data-stu-id="8a166-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="8a166-244">最后，建议有关布局页</span><span class="sxs-lookup"><span data-stu-id="8a166-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="8a166-245">在本教程中创建 *\_Layout.cshtml*页上，使用`RenderBody`方法来合并另一页的内容。</span><span class="sxs-lookup"><span data-stu-id="8a166-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="8a166-246">这是在网页中使用的布局的基本模式。</span><span class="sxs-lookup"><span data-stu-id="8a166-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="8a166-247">布局页中有我们此处未涉及的其他功能。</span><span class="sxs-lookup"><span data-stu-id="8a166-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="8a166-248">例如，可以嵌套布局页中，一个布局页面又可以引用另一个。</span><span class="sxs-lookup"><span data-stu-id="8a166-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="8a166-249">嵌套的布局很有用，如果你正在使用的站点需要不同的布局的小节。</span><span class="sxs-lookup"><span data-stu-id="8a166-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="8a166-250">此外可以使用其他方法 (例如， `RenderSection`) 若要设置名为布局页中的部分。</span><span class="sxs-lookup"><span data-stu-id="8a166-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="8a166-251">布局页的组合并 *.css*文件是功能强大。</span><span class="sxs-lookup"><span data-stu-id="8a166-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="8a166-252">正如您将看到在下一步的系列教程中，在 WebMatrix 中您可以创建基于一个站点*模板*，后者提供了的站点中的预生成的功能。</span><span class="sxs-lookup"><span data-stu-id="8a166-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="8a166-253">模板很好地利用布局页和 CSS 以创建的网站的外观精美且具有菜单等功能。</span><span class="sxs-lookup"><span data-stu-id="8a166-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="8a166-254">下面是主页的从基于模板，显示使用布局页和 CSS 的功能的站点的屏幕截图：</span><span class="sxs-lookup"><span data-stu-id="8a166-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![通过显示标头、 导航区域中，内容区域、 可选部分和登录链接的 WebMatrix 网站模板创建的布局](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="8a166-256">电影页 （已更新为使用布局页） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="8a166-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="8a166-257">完成页的列表添加影片页 （针对布局更新）</span><span class="sxs-lookup"><span data-stu-id="8a166-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="8a166-258">删除电影页 （针对布局更新） 的完整页面列表</span><span class="sxs-lookup"><span data-stu-id="8a166-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="8a166-259">编辑电影页 （针对布局更新） 的完整页面列表</span><span class="sxs-lookup"><span data-stu-id="8a166-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="8a166-260">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="8a166-260">Coming Up Next</span></span>

<span data-ttu-id="8a166-261">在下一步的教程中，您将了解如何将您的网站发布到 Internet，以便每个人都可以查看它。</span><span class="sxs-lookup"><span data-stu-id="8a166-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a166-262">其他资源</span><span class="sxs-lookup"><span data-stu-id="8a166-262">Additional Resources</span></span>

- <span data-ttu-id="8a166-263">[创建一致的查看](https://go.microsoft.com/fwlink/?LinkID=202891)— 提供了更多详细使用信息的布局的项目。</span><span class="sxs-lookup"><span data-stu-id="8a166-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="8a166-264">它还介绍了如何将值传递给布局页的显示或隐藏的部分内容。</span><span class="sxs-lookup"><span data-stu-id="8a166-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="8a166-265">[嵌套使用 Razor 布局页](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)— Mike Brind 博客举例说明如何嵌套布局页。</span><span class="sxs-lookup"><span data-stu-id="8a166-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="8a166-266">（包括页面的下载。）</span><span class="sxs-lookup"><span data-stu-id="8a166-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8a166-267">[上一页](deleting-data.md)
> [下一页](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="8a166-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
