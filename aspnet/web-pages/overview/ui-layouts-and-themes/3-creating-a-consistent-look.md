---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET 网页中创建一致的布局页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 若要使其更高效地创建你的站点的 web 页面，可以创建可重用块的内容 （如页眉和页脚） 的网站，然后你 c...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/10/2014
ms.topic: article
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 2c7631017f7c0fb31f43320c2ab78baddd87b516
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530236"
---
<a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="1b8e5-103">在 ASP.NET Web 页 (Razor) 站点中创建一致的布局</span><span class="sxs-lookup"><span data-stu-id="1b8e5-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="1b8e5-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1b8e5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1b8e5-105">此文章介绍了如何在 ASP.NET Web 页 (Razor) 网站中使用布局页，以创建可重用块的内容 （如页眉和页脚） 并在站点中创建的所有页一致的外观。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="1b8e5-106">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="1b8e5-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="1b8e5-107">如何创建可重用块的内容，例如页眉和页脚。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="1b8e5-108">如何在你使用的布局的站点中创建的所有页一致的外观。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="1b8e5-109">如何将数据在运行时传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="1b8e5-110">这些是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="1b8e5-111">内容块，是包含要插入多个页面的 HTML 格式的内容文件。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="1b8e5-112">包含可以共享网站上的页的 HTML 格式的内容页的布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="1b8e5-113">`RenderPage`， `RenderBody`，和`RenderSection`方法，其作用是告诉 ASP.NET 页元素的插入位置。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="1b8e5-114">`PageData`允许您在共享内容块和布局页之间的数据的字典。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1b8e5-115">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="1b8e5-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1b8e5-116">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1b8e5-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1b8e5-117">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="about-layout-pages"></a><span data-ttu-id="1b8e5-118">有关布局页</span><span class="sxs-lookup"><span data-stu-id="1b8e5-118">About Layout Pages</span></span>

<span data-ttu-id="1b8e5-119">许多网站未在每个页上，如页眉和页脚或告知用户他们在登录框中显示的内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="1b8e5-120">ASP.NET，可以使用内容块可以包含文本、 标记和代码，就像常规 web 页一样创建一个单独的文件。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="1b8e5-121">然后，你可以在想要显示的信息的站点上的其他页中插入该内容块。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="1b8e5-122">这样无需复制并粘贴到每一页的相同的内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="1b8e5-123">创建这样的常见内容还可以更轻松地更新你的站点。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="1b8e5-124">如果你需要更改的内容，你可以仅更新单个文件，并且所做的更改将反映无处不在已插入内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="1b8e5-125">下图显示内容如何阻止工作。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="1b8e5-126">当浏览器从 web 服务器请求页面时，ASP.NET 会将内容块插入点处其中`RenderPage`在主页面中调用方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="1b8e5-127">然后，完成 （合并） 页被发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-127">The finished (merged) page is then sent to the browser.</span></span>

![显示如何 RenderPage 方法将一个引用的页插入到当前页的概念图。](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="1b8e5-129">在此过程中，你将创建引用两个内容块 （页眉和页脚），它们位于单独的文件中的页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="1b8e5-130">在你的站点中的任意页中，可以使用这些相同的内容块。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="1b8e5-131">完成后，你将获得如下页：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-131">When you're done, you'll get a page like this:</span></span>

![显示在浏览器中运行包括对 RenderPage 方法的调用的页面的页面的屏幕截图。](3-creating-a-consistent-look/_static/image2.jpg)

1. <span data-ttu-id="1b8e5-133">在你的网站的根文件夹中，创建名为的文件*Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="1b8e5-134">现有的标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="1b8e5-135">在根文件夹中，创建名为的文件夹*共享*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b8e5-136">常见的做法，用于存储在名为的文件夹中的 web 页之间共享的文件是*共享*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="1b8e5-137">在*共享*文件夹中，创建名为的文件 *\_Header.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="1b8e5-138">任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="1b8e5-139">请注意，文件名是 *\_Header.cshtml*，以下划线 (\_) 作为前缀。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="1b8e5-140">ASP.NET 不会发送到浏览器页面，如果其名称以下划线开头。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="1b8e5-141">这可以防止用户请求 （无意中或其他） 这些页面直接。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="1b8e5-142">它是一个好办法使用下划线名称页中，具有内容块，因为你实际上不希望用户能够请求这些页面 &#8212;它们严格存在要插入到其他页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="1b8e5-143">在*共享*文件夹中，创建名为的文件 *\_Footer.cshtml*和替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="1b8e5-144">在*Index.cshtml*页上，添加到两个调用`RenderPage`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="1b8e5-145">此示例演示如何将内容块插入到网页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="1b8e5-146">你调用`RenderPage`方法并将其传递你想要在该点插入其内容的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="1b8e5-147">在这里，要插入的内容 *\_Header.cshtml*和 *\_Footer.cshtml*文件到*Index.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="1b8e5-148">运行*Index.cshtml*在浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="1b8e5-149">(在 WebMatrix 中，在**文件**工作区中，右键单击该文件，然后选择**在浏览器中启动**。)</span><span class="sxs-lookup"><span data-stu-id="1b8e5-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="1b8e5-150">在浏览器中查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-150">In the browser, view the page source.</span></span> <span data-ttu-id="1b8e5-151">(例如，在 Internet Explorer 中，右击该页，然后单击**查看源**。)</span><span class="sxs-lookup"><span data-stu-id="1b8e5-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="1b8e5-152">这样，你可以查看发送到浏览器，将索引页标记与内容块相结合的网页标记。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="1b8e5-153">下面的示例演示为呈现页面源文件*Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="1b8e5-154">对调用`RenderPage`插入到*Index.cshtml*已被替换为页眉和页脚文件的实际内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="1b8e5-155">创建一致的外观使用布局页</span><span class="sxs-lookup"><span data-stu-id="1b8e5-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="1b8e5-156">到目前为止，你已了解很容易地包含在多个页相同的内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="1b8e5-157">一种创建站点的一致的外观更结构化的方法是使用布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="1b8e5-158">布局页定义的 web 网页、 的结构，但不包含任何实际内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="1b8e5-159">创建布局页后，可以创建包含的内容，然后将它们链接到布局页的网页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="1b8e5-160">这些页面显示时，它们将采用格式根据布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="1b8e5-161">（在这个意义上来说，布局页充当一种类型的其他页中定义的内容的模板。）</span><span class="sxs-lookup"><span data-stu-id="1b8e5-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="1b8e5-162">布局页就像任何 HTML 页中，只是它包含对的调用`RenderBody`方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="1b8e5-163">位置`RenderBody`布局页中的方法确定内容页中的信息将在其中包含。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="1b8e5-164">下图显示了如何在内容页并布局页将合并在运行时生成完成的网页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="1b8e5-165">浏览器请求内容页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-165">The browser requests a content page.</span></span> <span data-ttu-id="1b8e5-166">内容页中，指定要用于该页面的结构的布局页有代码。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="1b8e5-167">在布局页中，内容插入点处其中`RenderBody`调用方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="1b8e5-168">内容块还可以插入到布局页通过调用`RenderPage`方法上, 一节中采用的方式。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="1b8e5-169">完成网页时，则将它发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-169">When the web page is complete, it's sent to the browser.</span></span>

![显示在浏览器中运行包括对 RenderBody 方法的调用的页面的页面的屏幕截图。](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="1b8e5-171">以下过程演示如何创建网页并链接到它的内容页的布局。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="1b8e5-172">在*共享*文件夹中你的网站，创建名为的文件 *\_Layout1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="1b8e5-173">任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="1b8e5-174">你使用`RenderPage`布局页后，可以将插入内容块中的方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="1b8e5-175">布局页可以包含对只有一个调用`RenderBody`方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="1b8e5-176">在*共享*文件夹中，创建名为的文件 *\_Header2.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="1b8e5-177">在根文件夹中，创建一个新文件夹并将其命名*样式*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="1b8e5-178">在*样式*文件夹中，创建名为的文件*Site.css*并添加以下样式定义：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="1b8e5-179">这些样式定义目前仅用于显示布局页中，如何可以使用样式表。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="1b8e5-180">如果你想，你可以定义你自己的这些元素的样式。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="1b8e5-181">在根文件夹中，创建名为的文件*Content1.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="1b8e5-182">这是将使用布局页的页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="1b8e5-183">在页面顶部的代码块指示要用于此内容进行格式设置的布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="1b8e5-184">运行*Content1.cshtml*在浏览器。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="1b8e5-185">呈现的页面使用的格式和样式表中定义 *\_Layout1.cshtml*和中定义的文本 （内容） *Content1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[image]](3-creating-a-consistent-look/_static/image4.jpg)

    <span data-ttu-id="1b8e5-187">您可以重复步骤 6 以创建然后可以共享相同的布局页的其他内容页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b8e5-188">你可以设置你的站点，以便为文件夹中的所有内容页对自动使用相同的布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="1b8e5-189">有关详细信息，请参阅[自定义站点范围的行为的 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906)。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="1b8e5-190">具有多个内容区域的设计布局页</span><span class="sxs-lookup"><span data-stu-id="1b8e5-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="1b8e5-191">内容页可以有多个部分中，这非常有用，如果你想要使用具有多个区域可替换内容的布局。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="1b8e5-192">在内容页中，你为每个部分的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="1b8e5-193">(保持默认部分未命名。)在布局页中，你将添加`RenderBody`方法，以指定的未命名 （默认值） 部分应出现的位置。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="1b8e5-194">然后添加单独`RenderSection`方法以逐一呈现命名的部分。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="1b8e5-195">下图显示 ASP.NET 处理分为多个部分的内容的方式。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="1b8e5-196">每个命名的部分包含在内容页中的部分块中。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="1b8e5-197">(它们在名为`Header`和`List`在示例中。)框架将内容部分插入点处的布局页，其中`RenderSection`调用方法。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="1b8e5-198">未命名 （默认值） 部分插入点处其中`RenderBody`调用方法，如前面所看到。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![显示如何 RenderSection 方法将引用部分插入到当前页的概念图。](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="1b8e5-200">此过程介绍如何创建有多个内容节的内容页以及如何使其使用支持多个内容区域的布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="1b8e5-201">在*共享*文件夹中，创建名为的文件 *\_Layout2.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="1b8e5-202">任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="1b8e5-203">你使用`RenderSection`方法呈现的标头和列表部分。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="1b8e5-204">在根文件夹中，创建名为的文件*Content2.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="1b8e5-205">此内容页包含在页面顶部的代码块。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="1b8e5-206">每个命名的部分包含在部分块中。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="1b8e5-207">页面的其余部分包含 （未命名） 的默认内容部分。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="1b8e5-208">运行*Content2.cshtml*在浏览器。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-208">Run *Content2.cshtml* in a browser.</span></span>

    ![显示在浏览器中运行包括对 RenderSection 方法的调用的页面的页面的屏幕截图。](3-creating-a-consistent-look/_static/image6.jpg)

## <a name="making-content-sections-optional"></a><span data-ttu-id="1b8e5-210">使内容的部分可选</span><span class="sxs-lookup"><span data-stu-id="1b8e5-210">Making Content Sections Optional</span></span>

<span data-ttu-id="1b8e5-211">通常情况下，在内容页中创建的部分必须匹配布局页中定义的部分。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="1b8e5-212">如果发生以下任一情况，你会遇到错误：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="1b8e5-213">内容页包含布局页中没有相应部分的部分。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="1b8e5-214">布局页包含的部分没有任何内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="1b8e5-215">该布局页面包括尝试多次呈现相同的部分的方法调用。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="1b8e5-216">但是，可以通过声明部分是可选中布局页来重写此行为的命名的节。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="1b8e5-217">这样可以定义多个内容页，可以共享布局页，但是，可能会也可能没有特定部分的内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="1b8e5-218">打开*Content2.cshtml*并删除以下部分：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="1b8e5-219">保存页，然后在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="1b8e5-220">显示错误消息，因为内容页面上不提供布局页，即标头部分中定义的节的内容。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![显示如果运行某个页面则会发生的错误的屏幕截图调用 RenderSection 方法但不是提供的相应部分。](3-creating-a-consistent-look/_static/image7.jpg)
3. <span data-ttu-id="1b8e5-222">在*共享*文件夹中，打开 *\_Layout2.cshtml*页上，将以下行：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="1b8e5-223">替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="1b8e5-224">作为替代方法，无法替换下面的代码块生成相同的结果之前的代码行：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="1b8e5-225">运行*Content2.cshtml*再次浏览器。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="1b8e5-226">（如果你仍然使用浏览器中打开此页，你可以只刷新它。）此时将显示页不显示错误，即使该类具有没有标头。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="1b8e5-227">将数据传递给布局页</span><span class="sxs-lookup"><span data-stu-id="1b8e5-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="1b8e5-228">您可能需要在布局页中引用的内容页中定义的数据。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="1b8e5-229">如果是这样，你需要将从内容页的数据传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="1b8e5-230">例如，你可能想要显示的用户的登录状态，或你可能想要显示或隐藏根据用户输入的内容区域。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="1b8e5-231">若要将数据从内容页传递给布局页中，你可以将值放入`PageData`属性的内容页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="1b8e5-232">`PageData`属性是保存你想要在页面之间传递数据的名称/值对的集合。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="1b8e5-233">在布局页中，然后可以读取外的值`PageData`属性。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="1b8e5-234">下面是另一个关系图。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-234">Here's another diagram.</span></span> <span data-ttu-id="1b8e5-235">本示例显示如何使用 ASP.NET`PageData`属性要从内容页的值传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="1b8e5-236">当 ASP.NET 开始生成 web 页面时，它将创建`PageData`集合。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="1b8e5-237">在内容页中，你编写代码以将数据放入`PageData`集合。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="1b8e5-238">中的值`PageData`通过内容页中的其他章节或其他内容块，也可以访问集合。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![演示如何填充 PageData 字典并将该信息传递给布局页内容页的概念图。](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="1b8e5-240">以下过程演示如何将数据从内容页传递给布局页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="1b8e5-241">页运行时，它将显示一个按钮，使用户可以隐藏或显示在布局页中定义的列表。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="1b8e5-242">当用户单击按钮时，它设置中的 true/false （布尔值） 值`PageData`属性。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="1b8e5-243">布局页读取该值，并如果为 false，将隐藏列表。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="1b8e5-244">值还用于在内容页确定是否显示**隐藏列表**按钮或**显示列表**按钮。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[image]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="1b8e5-246">在根文件夹中，创建名为的文件*Content3.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="1b8e5-247">代码将存储中的数据的两条`PageData`属性 &#8212; 网页和 true 或 false 以指定是否显示列表的标题。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="1b8e5-248">请注意，ASP.NET 将允许你放入有条件地使用代码块的页的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="1b8e5-249">例如，`if/else`页的正文中的块确定哪个窗体，具体取决于是否显示`PageData["ShowList"]`设置为 true。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="1b8e5-250">在*共享*文件夹中，创建名为的文件 *\_Layout3.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="1b8e5-251">布局页包括中的表达式`<title>`获取从的标题值的元素`PageData`属性。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="1b8e5-252">它还使用`ShowList`值`PageData`属性来确定是否显示该列表内容块。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="1b8e5-253">在*共享*文件夹中，创建名为的文件 *\_List.cshtml*和任何现有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1b8e5-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="1b8e5-254">运行*Content3.cshtml*在浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="1b8e5-255">在页面左侧上可见的列表将显示的页和**隐藏列表**底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![显示包含列表和一个按钮，将显示为隐藏列表的页的屏幕截图。](3-creating-a-consistent-look/_static/image10.jpg)
5. <span data-ttu-id="1b8e5-257">单击**隐藏列表**。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-257">Click **Hide List**.</span></span> <span data-ttu-id="1b8e5-258">列表将消失，该按钮改为**显示列表**。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-258">The list disappears and the button changes to **Show List**.</span></span>

    ![显示不包含列表和一个按钮，将显示为显示列表页的屏幕截图。](3-creating-a-consistent-look/_static/image11.jpg)
6. <span data-ttu-id="1b8e5-260">单击**显示列表**再次显示按钮和列表。</span><span class="sxs-lookup"><span data-stu-id="1b8e5-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b8e5-261">其他资源</span><span class="sxs-lookup"><span data-stu-id="1b8e5-261">Additional Resources</span></span>


[<span data-ttu-id="1b8e5-262">为 ASP.NET 网页自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="1b8e5-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
