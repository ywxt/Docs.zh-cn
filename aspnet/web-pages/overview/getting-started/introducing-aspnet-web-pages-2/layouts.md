---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: 引入的 ASP.NET Web Pages-创建一致的布局 |Microsoft 文档
author: tfitzmac
description: 本教程演示如何使用布局在使用 ASP.NET Web 页的站点上创建一致的外观的页。 它假定你已完成...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: c2d5c4d8ed8a71979c16d484ab90d283a45de537
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30899809"
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="bb983-104">引入了 ASP.NET Web 页-创建一致的布局</span><span class="sxs-lookup"><span data-stu-id="bb983-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>
====================
<span data-ttu-id="bb983-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bb983-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bb983-106">本教程演示如何使用*布局*在使用 ASP.NET Web 页的站点上创建一致的外观的页。</span><span class="sxs-lookup"><span data-stu-id="bb983-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="bb983-107">它假定你已完成通过系列[删除数据库数据中的 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584)。</span><span class="sxs-lookup"><span data-stu-id="bb983-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="bb983-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="bb983-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="bb983-109">布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-109">What a layout page is.</span></span>
> - <span data-ttu-id="bb983-110">如何将布局页与动态内容结合起来。</span><span class="sxs-lookup"><span data-stu-id="bb983-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="bb983-111">如何将值传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-111">How to pass values to a layout page.</span></span>


## <a name="about-layouts"></a><span data-ttu-id="bb983-112">有关布局</span><span class="sxs-lookup"><span data-stu-id="bb983-112">About Layouts</span></span>

<span data-ttu-id="bb983-113">你到目前为止已创建的页具有所有已完成，独立页。</span><span class="sxs-lookup"><span data-stu-id="bb983-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="bb983-114">它们都属于相同的站点中，但它们不具有任何通用元素或标准的外观。</span><span class="sxs-lookup"><span data-stu-id="bb983-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="bb983-115">大多数站点都有一致的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="bb983-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="bb983-116">例如，如果你转到[Microsoft.com/web](https://www.microsoft.com/web/)站点和检查，您了解页面都遵循到总体布局和可视主题：</span><span class="sxs-lookup"><span data-stu-id="bb983-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![显示标头、 导航区域、 内容区域和页脚的布局的 Microsoft.com/web 站点页](layouts/_static/image1.png)

<span data-ttu-id="bb983-118">*低效*方式创建此布局可以是定义标头、 导航栏中和页脚单独在每个页面上。</span><span class="sxs-lookup"><span data-stu-id="bb983-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="bb983-119">你将会将复制的相同标记每个时间。</span><span class="sxs-lookup"><span data-stu-id="bb983-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="bb983-120">如果你想要更改的某些内容 （例如，更新页脚），你将必须单独更改每一页。</span><span class="sxs-lookup"><span data-stu-id="bb983-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="bb983-121">这正是*布局页*进入。</span><span class="sxs-lookup"><span data-stu-id="bb983-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="bb983-122">在 ASP.NET Web 页中，你可以定义你的站点上的页面中提供的总体容器布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="bb983-123">例如，标头、 导航区域中和页脚可以包含布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="bb983-124">布局页包含主要内容的位置的占位符。</span><span class="sxs-lookup"><span data-stu-id="bb983-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="bb983-125">然后，你可以定义包含标记和仅该页面的代码的各个内容页。</span><span class="sxs-lookup"><span data-stu-id="bb983-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="bb983-126">内容页无需是完整的 HTML 页面; 例如：他们甚至不需要具有`<body>`元素。</span><span class="sxs-lookup"><span data-stu-id="bb983-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="bb983-127">它们还具有你想要显示中的内容布局页面是告诉 ASP.NET 的代码行。</span><span class="sxs-lookup"><span data-stu-id="bb983-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="bb983-128">此处是大致介绍了此关系的工作原理的图片：</span><span class="sxs-lookup"><span data-stu-id="bb983-128">Here's a picture that shows roughly how this relationship works:</span></span>

![显示两个内容页和它们容纳布局页的概念图](layouts/_static/image2.png)

<span data-ttu-id="bb983-130">这种交互很容易理解何时在操作中查看它。</span><span class="sxs-lookup"><span data-stu-id="bb983-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="bb983-131">在本教程中，你将更改电影页面要使用的布局。</span><span class="sxs-lookup"><span data-stu-id="bb983-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="bb983-132">添加布局页</span><span class="sxs-lookup"><span data-stu-id="bb983-132">Adding a Layout Page</span></span>

<span data-ttu-id="bb983-133">你首先创建定义一种典型的页面布局有页眉、 页脚和主要内容区域的布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="bb983-134">在 WebPagesMovies 站点中，添加一个名为的 CSHTML 页 *\_Layout.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="bb983-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="bb983-135">前导下划线 ( `_` ) 字符非常重要。</span><span class="sxs-lookup"><span data-stu-id="bb983-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="bb983-136">如果页面的名称以下划线开头，则 ASP.NET 不会直接向浏览器发送该页面。</span><span class="sxs-lookup"><span data-stu-id="bb983-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="bb983-137">此约定，可以定义所需的站点，但该用户不应能够直接请求的页。</span><span class="sxs-lookup"><span data-stu-id="bb983-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="bb983-138">中页面的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bb983-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="bb983-139">如你所见，此标记是只需使用的 HTML`<div>`元素多页以及一个定义三个部分`<div>`元素来保存的三个部分。</span><span class="sxs-lookup"><span data-stu-id="bb983-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="bb983-140">页脚包含 Razor 代码执行少量： `@DateTime.Now.Year`，这将在该位置在页中呈现当前年份。</span><span class="sxs-lookup"><span data-stu-id="bb983-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="bb983-141">请注意，没有名为的样式表的链接*Movies.css*。</span><span class="sxs-lookup"><span data-stu-id="bb983-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="bb983-142">样式表是可在其中定义元素的物理布局的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bb983-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="bb983-143">你将在稍后创建的。</span><span class="sxs-lookup"><span data-stu-id="bb983-143">You'll create that in a moment.</span></span>

<span data-ttu-id="bb983-144">在此唯一不同之功能 *\_Layout.cshtml*页`@Render.Body()`行。</span><span class="sxs-lookup"><span data-stu-id="bb983-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="bb983-145">这是与另一页合并此布局时内容的目的地的占位符。</span><span class="sxs-lookup"><span data-stu-id="bb983-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="bb983-146">添加.css 文件</span><span class="sxs-lookup"><span data-stu-id="bb983-146">Adding a .css File</span></span>

<span data-ttu-id="bb983-147">页上定义的元素的实际排列方式 （即，外观） 的首选的方式是使用级联样式表 (CSS) 规则。</span><span class="sxs-lookup"><span data-stu-id="bb983-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="bb983-148">因此，你将创建 *.css*具有用于将新布局规则的文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="bb983-149">在 WebMatrix 中，选择你的站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="bb983-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="bb983-150">然后在**文件**选项卡的功能区中，单击下的箭头**新建**按钮，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="bb983-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![在新建下，功能区中的新建文件夹选项。](layouts/_static/image3.png)

<span data-ttu-id="bb983-152">将新文件夹命名*样式*。</span><span class="sxs-lookup"><span data-stu-id="bb983-152">Name the new folder *Styles*.</span></span>

![命名新文件夹样式](layouts/_static/image4.png)

<span data-ttu-id="bb983-154">在新*样式*文件夹中，创建名为的文件*Movies.css*。</span><span class="sxs-lookup"><span data-stu-id="bb983-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![创建新的 Movies.css 文件](layouts/_static/image5.png)

<span data-ttu-id="bb983-156">新的内容替换 *.css*替换为以下文件：</span><span class="sxs-lookup"><span data-stu-id="bb983-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="bb983-157">我们不会说过多这些 CSS 规则，只是想说明以下两项操作。</span><span class="sxs-lookup"><span data-stu-id="bb983-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="bb983-158">一个是除了设置字体和大小，规则使用绝对定位来建立的页眉、 页脚和主要内容区域的位置。</span><span class="sxs-lookup"><span data-stu-id="bb983-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="bb983-159">如果你熟悉定位在 CSS 中，你可以阅读[CSS 定位](http://www.w3schools.com/css/css_positioning.asp)教程在 W3Schools 站点。</span><span class="sxs-lookup"><span data-stu-id="bb983-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="bb983-160">其他需要注意的事项，在底部，我们已复制最初的样式规则定义的单独在*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="bb983-161">在中使用这些规则[简介显示数据通过使用 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580)教程，以使`WebGrid`添加到表的条带化的标记帮助器呈现。</span><span class="sxs-lookup"><span data-stu-id="bb983-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="bb983-162">(如果你要使用 *.css*文件有关样式定义，你也可能给整个站点的样式规则中。)</span><span class="sxs-lookup"><span data-stu-id="bb983-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="bb983-163">更新要使用的布局的电影文件</span><span class="sxs-lookup"><span data-stu-id="bb983-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="bb983-164">现在你可以更新你的站点以使用新的布局中的现有文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="bb983-165">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="bb983-166">在顶部，作为第一个代码行，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="bb983-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="bb983-167">该页面现在开始方式如下：</span><span class="sxs-lookup"><span data-stu-id="bb983-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="bb983-168">此一行代码将告诉 ASP.NET，当*电影*页运行时，它应与合并 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="bb983-169">由于*Movies.cshtml*文件现在使用布局页，你可以删除从标记*Movies.cshtml*已处理的页 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="bb983-170">带`<!DOCTYPE>`， `<html>`，和`<body>`开始和结束标记。</span><span class="sxs-lookup"><span data-stu-id="bb983-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="bb983-171">带整个`<head>`元素和其内容，其中包括网格中的样式规则，因为您现在已经获得这些规则 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="bb983-172">当处于它时，更改现有`<h1>`元素`<h2>`元素; 你具有`<h1>`已布局页中的元素。</span><span class="sxs-lookup"><span data-stu-id="bb983-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="bb983-173">更改`<h2>`"列表电影"的文本。</span><span class="sxs-lookup"><span data-stu-id="bb983-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="bb983-174">通常，你不需要在内容页中进行这些种类的更改。</span><span class="sxs-lookup"><span data-stu-id="bb983-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="bb983-175">当你的站点开始与布局页中时，你首先创建内容页，而所有这些元素不。</span><span class="sxs-lookup"><span data-stu-id="bb983-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="bb983-176">在这种情况下，不过，您要转换的独立页到使用一种布局，因此清理的位。</span><span class="sxs-lookup"><span data-stu-id="bb983-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="bb983-177">如果已完成， *Movies.cshtml*页面将如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb983-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="bb983-178">测试布局</span><span class="sxs-lookup"><span data-stu-id="bb983-178">Testing the Layout</span></span>

<span data-ttu-id="bb983-179">现在，你可以看到布局如下所示。</span><span class="sxs-lookup"><span data-stu-id="bb983-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="bb983-180">在 WebMatrix 中，右键单击*Movies.cshtml*页，选择**在浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="bb983-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="bb983-181">当浏览器显示页时，它类似于此页：</span><span class="sxs-lookup"><span data-stu-id="bb983-181">When the browser displays the page, it looks like this page:</span></span>

![使用一种布局呈现电影页](layouts/_static/image6.png)

<span data-ttu-id="bb983-183">ASP.NET 所合并到 Movies.cshtml 页面的内容 *\_Layout.cshtml*页上右`RenderBody`方法。</span><span class="sxs-lookup"><span data-stu-id="bb983-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="bb983-184">和当然 *\_Layout.cshtml*的页引用 *.css*定义查找范围页的文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="bb983-185">更新 AddMovie 页后，可以使用布局</span><span class="sxs-lookup"><span data-stu-id="bb983-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="bb983-186">布局实际好处是，你可以使用它们将所有页在你的网站。</span><span class="sxs-lookup"><span data-stu-id="bb983-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="bb983-187">打开*AddMovie.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="bb983-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="bb983-188">你可能会记住*AddMovie.cshtml*页最初在其中以定义查找范围的验证错误消息中发生一些 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="bb983-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="bb983-189">由于你有 *.css*文件中为你的网站现在，你可以将移动到这些规则 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="bb983-190">从其中移除这些*AddMovie.cshtml*文件并将它们添加到底部*Movies.css*文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="bb983-191">要移动的以下规则：</span><span class="sxs-lookup"><span data-stu-id="bb983-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="bb983-192">现在，进行中的更改相同排序*AddMovie.cshtml*针对*Movies.cshtml* -添加`Layout="~/_Layout.cshtml;`和删除现在是多余的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="bb983-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="bb983-193">更改`<h1>`元素`<h2>`。</span><span class="sxs-lookup"><span data-stu-id="bb983-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="bb983-194">完成后，页面将如下所示此示例：</span><span class="sxs-lookup"><span data-stu-id="bb983-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="bb983-195">运行页面。</span><span class="sxs-lookup"><span data-stu-id="bb983-195">Run the page.</span></span> <span data-ttu-id="bb983-196">现在看起来像此图中：</span><span class="sxs-lookup"><span data-stu-id="bb983-196">Now it looks like this illustration:</span></span>

![使用一种布局呈现的添加电影页](layouts/_static/image7.png)

<span data-ttu-id="bb983-198">你想要对站点中的页面进行类似更改 — *EditMovie.cshtml*和*DeleteMovie.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="bb983-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="bb983-199">但是，在执行之前，你可以另一项更改使其变得更加灵活的布局。</span><span class="sxs-lookup"><span data-stu-id="bb983-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="bb983-200">传递到布局页的标题信息</span><span class="sxs-lookup"><span data-stu-id="bb983-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="bb983-201"> *\_Layout.cshtml*你创建的页具有`<title>`设置为"我的电影站点"的元素。</span><span class="sxs-lookup"><span data-stu-id="bb983-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="bb983-202">大多数浏览器显示为选项卡上的文本的此元素的内容：</span><span class="sxs-lookup"><span data-stu-id="bb983-202">Most browsers display the content of this element as the text on a tab:</span></span>

![该页面的&lt;标题&gt;浏览器选项卡中显示的元素](layouts/_static/image8.png)

<span data-ttu-id="bb983-204">此标题信息才是泛型。</span><span class="sxs-lookup"><span data-stu-id="bb983-204">This title information is generic.</span></span> <span data-ttu-id="bb983-205">假设你想要进行更具体到当前页的标题文本。</span><span class="sxs-lookup"><span data-stu-id="bb983-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="bb983-206">（标题文本也用于按搜索引擎确定你的页面即将。）可以将信息从如下的内容页传递*Movies.cshtml*或*AddMovie.cshtml*到布局页，然后使用该信息以自定义布局页呈现。</span><span class="sxs-lookup"><span data-stu-id="bb983-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="bb983-207">打开*Movies.cshtml*再次页。</span><span class="sxs-lookup"><span data-stu-id="bb983-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="bb983-208">在顶部代码中，添加以下行：</span><span class="sxs-lookup"><span data-stu-id="bb983-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="bb983-209">`Page`上所有可用对象，则 *.cshtml*页，即适用于此目的，一个页，并且其布局之间共享信息。</span><span class="sxs-lookup"><span data-stu-id="bb983-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="bb983-210">打开<em>\_Layout.cshtml</em>页。</span><span class="sxs-lookup"><span data-stu-id="bb983-210">Open the<em>\_Layout.cshtml</em> page.</span></span> <span data-ttu-id="bb983-211">更改`<title>`使它类似于此标记的元素：</span><span class="sxs-lookup"><span data-stu-id="bb983-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="bb983-212">此代码将呈现任何处于`Page.Title`页中的该位置在右侧的属性。</span><span class="sxs-lookup"><span data-stu-id="bb983-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="bb983-213">运行*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="bb983-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="bb983-214">这一次该浏览器选项卡显示你所传递的值作为`Page.Title`:</span><span class="sxs-lookup"><span data-stu-id="bb983-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![浏览器选项卡显示在可动态创建的标题](layouts/_static/image9.png)

<span data-ttu-id="bb983-216">如果您希望在浏览器中查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="bb983-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="bb983-217">你可以看到，`<title>`元素呈现为`<title>List Movies</title>`。</span><span class="sxs-lookup"><span data-stu-id="bb983-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="bb983-218">**Page 对象**</span><span class="sxs-lookup"><span data-stu-id="bb983-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="bb983-219">一个有用的功能`Page`是动态对象-`Title`属性不是固定或保留的名称。</span><span class="sxs-lookup"><span data-stu-id="bb983-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="bb983-220">你可以使用*任何*名称的值为`Page`对象。</span><span class="sxs-lookup"><span data-stu-id="bb983-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="bb983-221">例如，你无法轻易传递标题使用名为的属性`Page.CurrentName`或`Page.MyPage`。</span><span class="sxs-lookup"><span data-stu-id="bb983-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="bb983-222">唯一限制是，名称必须遵循的哪些属性可以命名的一般规则。</span><span class="sxs-lookup"><span data-stu-id="bb983-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="bb983-223">（例如，名称不能包含空格。）</span><span class="sxs-lookup"><span data-stu-id="bb983-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="bb983-224">你可以通过传递任意数目的值`Page`对象。</span><span class="sxs-lookup"><span data-stu-id="bb983-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="bb983-225">如果你想要将影片信息传递给布局页，您无法将值传递通过使用类似`Page.MovieTitle`和`Page.Genre`和`Page.MovieYear`。</span><span class="sxs-lookup"><span data-stu-id="bb983-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="bb983-226">（或是为了存储信息的任何其他名称。）唯一的要求-这是可能明显 — 是你需要使用内容页和布局页中的相同名称。</span><span class="sxs-lookup"><span data-stu-id="bb983-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="bb983-227">使用传递的信息`Page`对象已不再局限于只是要在布局页上显示的文本。</span><span class="sxs-lookup"><span data-stu-id="bb983-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="bb983-228">可以将值传递给布局页中，然后布局页中的代码可以使用的值来确定是否要显示的页上，部分什么 *.css*文件以使用，依次类推。</span><span class="sxs-lookup"><span data-stu-id="bb983-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="bb983-229">在中传递的值`Page`对象像任何其他值在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="bb983-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="bb983-230">它只是值源自于在内容页中，并传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>


<span data-ttu-id="bb983-231">打开*AddMovie.cshtml*页上，并将行添加到提供的标题的代码，顶部*AddMovie.cshtml*页：</span><span class="sxs-lookup"><span data-stu-id="bb983-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="bb983-232">运行*AddMovie.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="bb983-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="bb983-233">你看到的新标题：</span><span class="sxs-lookup"><span data-stu-id="bb983-233">You see the new title there:</span></span>

![浏览器选项卡显示在可动态创建的添加电影标题](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="bb983-235">更新要使用布局的剩余页面</span><span class="sxs-lookup"><span data-stu-id="bb983-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="bb983-236">现在可以在你的站点中完成剩余的页，以便它们使用新的布局。</span><span class="sxs-lookup"><span data-stu-id="bb983-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="bb983-237">打开*EditMovie.cshtml*和*DeleteMovie.cshtml*接下来并在每个进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="bb983-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="bb983-238">添加链接到布局页的代码的行：</span><span class="sxs-lookup"><span data-stu-id="bb983-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="bb983-239">添加行以设置页的标题：</span><span class="sxs-lookup"><span data-stu-id="bb983-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="bb983-240">或：</span><span class="sxs-lookup"><span data-stu-id="bb983-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="bb983-241">删除所有多余的 HTML 标记-基本上，保留内位`<body>`元素 （加上在顶部的代码块）。</span><span class="sxs-lookup"><span data-stu-id="bb983-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="bb983-242">更改`<h1>`元素`<h2>`元素。</span><span class="sxs-lookup"><span data-stu-id="bb983-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="bb983-243">已完成这些更改，测试每个，并确保它正确显示，并且标题正确无误。</span><span class="sxs-lookup"><span data-stu-id="bb983-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="bb983-244">最后，建议有关布局页</span><span class="sxs-lookup"><span data-stu-id="bb983-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="bb983-245">在本教程中，你将创建 *\_Layout.cshtml*页上，使用`RenderBody`方法合并从另一页的内容。</span><span class="sxs-lookup"><span data-stu-id="bb983-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="bb983-246">这是在 Web 页中使用布局的基本模式。</span><span class="sxs-lookup"><span data-stu-id="bb983-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="bb983-247">布局页具有我们未在此处介绍的附加功能。</span><span class="sxs-lookup"><span data-stu-id="bb983-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="bb983-248">例如，可以嵌套布局页-一个布局页又可以引用另一个。</span><span class="sxs-lookup"><span data-stu-id="bb983-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="bb983-249">嵌套的布局可以很有用，如果你正在使用的站点需要不同的布局的小节。</span><span class="sxs-lookup"><span data-stu-id="bb983-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="bb983-250">你还可以使用其他方法 (例如， `RenderSection`) 若要设置名为布局页中的部分。</span><span class="sxs-lookup"><span data-stu-id="bb983-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="bb983-251">布局页的组合和 *.css*文件是功能强大。</span><span class="sxs-lookup"><span data-stu-id="bb983-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="bb983-252">正如你将在下一步的系列教程中看到的在 WebMatrix 中你可以创建基于站点*模板*，它会为你提供了的站点中的预构建的功能。</span><span class="sxs-lookup"><span data-stu-id="bb983-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="bb983-253">模板，可以很好的布局页和 CSS 代码即可创建的网站的外观和具有菜单等功能的用途。</span><span class="sxs-lookup"><span data-stu-id="bb983-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="bb983-254">下面是主页的从基于模板，显示布局页和 CSS 使用的功能的站点的屏幕快照：</span><span class="sxs-lookup"><span data-stu-id="bb983-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![显示标头、 导航区域、 内容区域、 可选部分和登录链接的 WebMatrix 网站模板创建的布局](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="bb983-256">完成列表影片页 （更新为使用布局页）</span><span class="sxs-lookup"><span data-stu-id="bb983-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="bb983-257">完成页列出了添加影片页 （对于布局更新）</span><span class="sxs-lookup"><span data-stu-id="bb983-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="bb983-258">完成删除影片页 （对于布局更新） 的页列表</span><span class="sxs-lookup"><span data-stu-id="bb983-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="bb983-259">完成编辑影片页 （对于布局更新） 的页列表</span><span class="sxs-lookup"><span data-stu-id="bb983-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="bb983-260">接下来</span><span class="sxs-lookup"><span data-stu-id="bb983-260">Coming Up Next</span></span>

<span data-ttu-id="bb983-261">在下一步的教程中，你将了解如何将你的站点发布到 Internet，以便每个人都可以看到它。</span><span class="sxs-lookup"><span data-stu-id="bb983-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb983-262">其他资源</span><span class="sxs-lookup"><span data-stu-id="bb983-262">Additional Resources</span></span>

- <span data-ttu-id="bb983-263">[创建一致的查看](https://go.microsoft.com/fwlink/?LinkID=202891)-提供了更详细地使用布局的项目。</span><span class="sxs-lookup"><span data-stu-id="bb983-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="bb983-264">它还描述如何将值传递到的布局页面中显示或隐藏的某些内容。</span><span class="sxs-lookup"><span data-stu-id="bb983-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="bb983-265">[嵌套具有 Razor 布局页](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)-Mike Brind 博客举例说明如何嵌套布局页。</span><span class="sxs-lookup"><span data-stu-id="bb983-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="bb983-266">（包括的下载页。）</span><span class="sxs-lookup"><span data-stu-id="bb983-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bb983-267">[上一页](deleting-data.md)
> [下一页](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="bb983-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
