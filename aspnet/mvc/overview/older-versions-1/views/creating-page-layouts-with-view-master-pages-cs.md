---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 创建视图母版页 (C#) 中使用的页面布局 |Microsoft 文档
author: microsoft
description: 在本教程中，您将学习如何在你的应用程序中创建多个页的常用页面布局，通过利用视图母版页。 你可以使用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 82500a311e1110713a60604027d018ba16539b65
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871241"
---
<a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="596a8-104">创建视图母版页 (C#) 中使用的页面布局</span><span class="sxs-lookup"><span data-stu-id="596a8-104">Creating Page Layouts with View Master Pages (C#)</span></span>
====================
<span data-ttu-id="596a8-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="596a8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="596a8-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="596a8-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="596a8-107">在本教程中，您将学习如何在你的应用程序中创建多个页的常用页面布局，通过利用视图母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="596a8-108">你可用于视图的母版页，例如，定义两列的页面布局和为所有 web 应用程序中的页，都使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="596a8-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>


## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="596a8-109">创建视图母版页中使用的页面布局</span><span class="sxs-lookup"><span data-stu-id="596a8-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="596a8-110">在本教程中，您将学习如何在你的应用程序中创建多个页的常用页面布局，通过利用视图母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="596a8-111">你可用于视图的母版页，例如，定义两列的页面布局和为所有 web 应用程序中的页，都使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="596a8-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="596a8-112">你还可以利用视图的母版页跨应用程序中的多个页共享公共内容。</span><span class="sxs-lookup"><span data-stu-id="596a8-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="596a8-113">例如，你可以在视图的母版页中放置您的网站徽标、 导航链接和横幅播发。</span><span class="sxs-lookup"><span data-stu-id="596a8-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="596a8-114">这样一来，你的应用程序中每页将自动显示此内容。</span><span class="sxs-lookup"><span data-stu-id="596a8-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="596a8-115">在本教程中，您将学习如何创建新视图母版页和创建新视图内容页基于母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="596a8-116">创建视图的母版页</span><span class="sxs-lookup"><span data-stu-id="596a8-116">Creating a View Master Page</span></span>

<span data-ttu-id="596a8-117">让我们首先创建定义两列布局视图母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="596a8-118">你将添加新视图母版页到 MVC 项目，请右键单击 Views\Shared 文件夹中，选择菜单选项**添加、 新项**，并选择**MVC 视图母版页**模板 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="596a8-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>


<span data-ttu-id="596a8-119">[![添加视图的母版页](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="596a8-120">**图 01**： 添加视图的母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="596a8-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="596a8-121">应用程序中，可以创建多个视图母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="596a8-122">每个视图的母版页可以定义不同的页面布局。</span><span class="sxs-lookup"><span data-stu-id="596a8-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="596a8-123">例如，您可能希望某些页具有两列布局和其他页面具有三列布局。</span><span class="sxs-lookup"><span data-stu-id="596a8-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="596a8-124">视图的母版页看起来非常相似的标准的 ASP.NET MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="596a8-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="596a8-125">但是，与普通视图中，不同视图的母版页包含一个或多个`<asp:ContentPlaceHolder>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="596a8-126">`<contentplaceholder>`使用标记来标记的区域的主控页可以在单个内容页面中重写。</span><span class="sxs-lookup"><span data-stu-id="596a8-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="596a8-127">例如，列表 1 中的视图母版页定义两列布局。</span><span class="sxs-lookup"><span data-stu-id="596a8-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="596a8-128">它包含两个`<contentplaceholder>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="596a8-129">一个`<ContentPlaceHolder>`为每个列。</span><span class="sxs-lookup"><span data-stu-id="596a8-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="596a8-130">**列表 1 – `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="596a8-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="596a8-131">列表 1 中的母版页包含两个视图的正文`<div>`对应于两个列的标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="596a8-132">级联样式表列类应用于这两`<div>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="596a8-133">此类声明顶部的主控页的样式表中定义。</span><span class="sxs-lookup"><span data-stu-id="596a8-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="596a8-134">你可以预览视图母版页通过切换到设计视图中的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="596a8-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="596a8-135">单击左下角的源代码编辑器的设计选项卡 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="596a8-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>


<span data-ttu-id="596a8-136">[![预览母版页设计器中](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="596a8-137">**图 02**： 预览设计器中的母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="596a8-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>


### <a name="creating-a-view-content-page"></a><span data-ttu-id="596a8-138">创建视图内容页</span><span class="sxs-lookup"><span data-stu-id="596a8-138">Creating a View Content Page</span></span>

<span data-ttu-id="596a8-139">创建视图的母版页后，你可以创建一个或多个视图基于视图母版页的内容页。</span><span class="sxs-lookup"><span data-stu-id="596a8-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="596a8-140">例如，可以通过右键单击 Views\Home 文件夹中，创建主控制器的索引视图内容页选择**添加、 新项**，选择**MVC 视图内容页**模板中，输入名称 Index.aspx，并单击**添加**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="596a8-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>


<span data-ttu-id="596a8-141">[![添加视图内容页](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="596a8-142">**图 03**： 添加视图内容页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="596a8-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>


<span data-ttu-id="596a8-143">单击添加按钮后，新出现一个对话框，使您能够选择视图的母版页要视图内容页相关联 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="596a8-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="596a8-144">你可以导航到我们在上一节中创建 Site.master 视图母版页上。</span><span class="sxs-lookup"><span data-stu-id="596a8-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>


<span data-ttu-id="596a8-145">[![选择母版页](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="596a8-146">**图 04**： 选择母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="596a8-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>


<span data-ttu-id="596a8-147">创建新视图内容页基于 Site.master 主控页后，你将收到列出 2 中的文件。</span><span class="sxs-lookup"><span data-stu-id="596a8-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="596a8-148">**列出 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="596a8-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="596a8-149">请注意，此视图包含`<asp:Content>`对应于每个标记`<asp:ContentPlaceHolder>`视图母版页中的标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="596a8-150">每个`<asp:Content>`标记包含指向特定 ContentPlaceHolderID 属性`<asp:ContentPlaceHolder>`，它将重写。</span><span class="sxs-lookup"><span data-stu-id="596a8-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="596a8-151">此外，请注意，列出 2 中的内容视图页不包含任何正常的开始和结束 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="596a8-152">例如，它不包含开始和结束`<html>`或`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="596a8-153">正常的开始和结束标记的所有包含在视图的母版页。</span><span class="sxs-lookup"><span data-stu-id="596a8-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="596a8-154">你想要在视图内容页中显示任何内容必须放在`<asp:Content>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="596a8-155">如果将任何 HTML 或在这些标记之外的其他内容，然后将你尝试查看的页时收到错误。</span><span class="sxs-lookup"><span data-stu-id="596a8-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="596a8-156">无需重写每个`<asp:ContentPlaceHolder>`从母版页的内容视图页中的标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="596a8-157">你只需重写`<asp:ContentPlaceHolder>`标记当你想要将标记替换为特定的内容。</span><span class="sxs-lookup"><span data-stu-id="596a8-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="596a8-158">例如，已修改的索引视图，列出 3 中仅包含两个`<asp:Content>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="596a8-159">每个`<asp:Content>`标记包含一些文本。</span><span class="sxs-lookup"><span data-stu-id="596a8-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="596a8-160">**列出 3 – `Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="596a8-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="596a8-161">请求的视图中列出的 3 时，它将呈现图 5 中的页。</span><span class="sxs-lookup"><span data-stu-id="596a8-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="596a8-162">请注意视图呈现具有两个列的页。</span><span class="sxs-lookup"><span data-stu-id="596a8-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="596a8-163">此外，请注意，从视图内容页中的内容合并视图的母版页的内容</span><span class="sxs-lookup"><span data-stu-id="596a8-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>


<span data-ttu-id="596a8-164">[![索引视图内容页](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="596a8-165">**图 05**: 索引视图内容页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="596a8-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>


### <a name="modifying-view-master-page-content"></a><span data-ttu-id="596a8-166">修改视图母版页页内容</span><span class="sxs-lookup"><span data-stu-id="596a8-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="596a8-167">几乎遇到的一个问题立即时使用视图母版页是修改视图母版页内容，要求不同的视图内容页时的问题。</span><span class="sxs-lookup"><span data-stu-id="596a8-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="596a8-168">例如，你希望每个页中具有唯一的标题将 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="596a8-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="596a8-169">但是，在视图的母版页 （而不是视图内容页声明标题。</span><span class="sxs-lookup"><span data-stu-id="596a8-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="596a8-170">因此，执行自定义方式为每个视图内容页的页标题？</span><span class="sxs-lookup"><span data-stu-id="596a8-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="596a8-171">有两种方法，你可以进行修改的视图内容页显示的标题。</span><span class="sxs-lookup"><span data-stu-id="596a8-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="596a8-172">首先，将分配到的标题属性页面标题`<%@ page %>`指令声明视图内容页顶部。</span><span class="sxs-lookup"><span data-stu-id="596a8-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="596a8-173">例如，如果你想要将页标题"超级极佳 Website"分配给索引视图，然后你可以包括在索引视图的顶部的以下指令：</span><span class="sxs-lookup"><span data-stu-id="596a8-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="596a8-174">索引视图呈现到浏览器中，浏览器标题栏中会显示所需的标题：</span><span class="sxs-lookup"><span data-stu-id="596a8-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>


<span data-ttu-id="596a8-175">[![浏览器标题栏](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="596a8-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>


<span data-ttu-id="596a8-176">没有母版视图页中要工作的标题属性的顺序必须满足的一个重要要求。</span><span class="sxs-lookup"><span data-stu-id="596a8-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="596a8-177">必须包含视图的母版页`<head runat="server">`而不是常规的标记`<head>`标记其标头。</span><span class="sxs-lookup"><span data-stu-id="596a8-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="596a8-178">如果`<head>`标记不包括 runat ="server"属性，则不会显示标题。</span><span class="sxs-lookup"><span data-stu-id="596a8-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="596a8-179">母版页包含所需的默认视图`<head runat="server">`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="596a8-180">从单独的视图内容页修改母版页内容的备用方法是将你想要在修改的区域`<asp:ContentPlaceHolder>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="596a8-181">例如，假设你想要更改不仅标题，而且还由母版视图页呈现的 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="596a8-182">列出 4 中的母版视图页面包含`<asp:ContentPlaceHolder>`中标记其`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="596a8-183">**列出 4 – `Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="596a8-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="596a8-184">请注意，`<asp:ContentPlaceHolder>`列出 4 中的标记包含默认内容： 默认标题和默认 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="596a8-185">如果你不替代这`<asp:ContentPlaceHolder>`标记在单独的视图内容页中，则将显示默认内容。</span><span class="sxs-lookup"><span data-stu-id="596a8-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="596a8-186">列出 5 中的内容视图页重写`<asp:ContentPlaceHolder>`为了显示自定义标题和自定义元标记的标记。</span><span class="sxs-lookup"><span data-stu-id="596a8-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="596a8-187">**列出 5- `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="596a8-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="596a8-188">总结</span><span class="sxs-lookup"><span data-stu-id="596a8-188">Summary</span></span>

<span data-ttu-id="596a8-189">本教程向您提供查看主控页并查看内容页的基本简介。</span><span class="sxs-lookup"><span data-stu-id="596a8-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="596a8-190">您学习了如何创建新视图的母版页和创建基于这些视图内容页。</span><span class="sxs-lookup"><span data-stu-id="596a8-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="596a8-191">我们还检查，您可以如何修改视图母版页从特定视图内容页中的内容。</span><span class="sxs-lookup"><span data-stu-id="596a8-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="596a8-192">[上一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一页](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="596a8-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
