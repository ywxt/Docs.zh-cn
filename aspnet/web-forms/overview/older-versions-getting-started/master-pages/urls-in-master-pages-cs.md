---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: 母版页 (C#) 中的 Url |Microsoft 文档
author: rick-anderson
description: 介绍如何在母版页中的 Url 可以中断由于是在不同的相对目录比内容页的主控页文件。 查看重定基址...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2008
ms.topic: article
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 494338f1a0705c8d7e15bc693ae1ec6362b26d64
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="urls-in-master-pages-c"></a><span data-ttu-id="22240-104">母版页 (C#) 中的 Url</span><span class="sxs-lookup"><span data-stu-id="22240-104">URLs in Master Pages (C#)</span></span>
====================
<span data-ttu-id="22240-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="22240-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="22240-106">[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="22240-106">[Download Code](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip) or [Download PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)</span></span>

> <span data-ttu-id="22240-107">介绍如何在母版页中的 Url 可以中断由于是在不同的相对目录比内容页的主控页文件。</span><span class="sxs-lookup"><span data-stu-id="22240-107">Addresses how URLs in the master page can break due to the master page file being in a different relative directory than the content page.</span></span> <span data-ttu-id="22240-108">重定基址通过 Url 查看 ~ 中以编程方式使用 ResolveUrl 和 ResolveClientUrl 和声明性语法。</span><span class="sxs-lookup"><span data-stu-id="22240-108">Looks at rebasing URLs via ~ in the declarative syntax and using ResolveUrl and ResolveClientUrl programmatically.</span></span> <span data-ttu-id="22240-109">（还查看</span><span class="sxs-lookup"><span data-stu-id="22240-109">(Also look at</span></span>


## <a name="introduction"></a><span data-ttu-id="22240-110">介绍</span><span class="sxs-lookup"><span data-stu-id="22240-110">Introduction</span></span>

<span data-ttu-id="22240-111">在所有示例，我们已了解到目前为止，母版页和内容页具有已位于相同的文件夹 （网站的根文件夹） 中。</span><span class="sxs-lookup"><span data-stu-id="22240-111">In all the examples we've seen thus far, the master and content pages have been located in the same folder (the website's root folder).</span></span> <span data-ttu-id="22240-112">但没有的理由为什么母版页和内容页必须位于同一文件夹中。</span><span class="sxs-lookup"><span data-stu-id="22240-112">But there's no reason why the master and content pages must be in the same folder.</span></span> <span data-ttu-id="22240-113">当然，你可以在子文件夹中创建内容页。</span><span class="sxs-lookup"><span data-stu-id="22240-113">You can certainly create content pages in subfolders.</span></span> <span data-ttu-id="22240-114">同样，你可能创建`~/MasterPages/`放置你的站点的主控页的文件夹。</span><span class="sxs-lookup"><span data-stu-id="22240-114">Similarly, you might create a `~/MasterPages/` folder where you place your site's master pages.</span></span>

<span data-ttu-id="22240-115">在将母版页和内容页放在不同的文件夹中的一个潜在的问题涉及中断的 Url。</span><span class="sxs-lookup"><span data-stu-id="22240-115">One potential issue with placing master and content pages in different folders involves broken URLs.</span></span> <span data-ttu-id="22240-116">如果母版页包含超链接、 图像或其他元素中的相对 Url，该链接将驻留在不同的文件夹中的内容页无效。</span><span class="sxs-lookup"><span data-stu-id="22240-116">If the master page contains relative URLs in hyperlinks, images, or other elements, the link will be invalid for content pages that reside in a different folder.</span></span> <span data-ttu-id="22240-117">在本教程中，我们将检查此问题以及解决方法的源。</span><span class="sxs-lookup"><span data-stu-id="22240-117">In this tutorial we examine the source of this problem as well as workarounds.</span></span>

## <a name="the-problem-with-relative-urls"></a><span data-ttu-id="22240-118">使用相对 Url 问题</span><span class="sxs-lookup"><span data-stu-id="22240-118">The Problem with Relative URLs</span></span>

<span data-ttu-id="22240-119">在网页上的 URL 被认为是*相对 URL*如果它指向该资源的位置是相对于网站的文件夹结构中的网页的位置。</span><span class="sxs-lookup"><span data-stu-id="22240-119">A URL on a web page is said to be a *relative URL* if the location of the resource it points to is relative to the web page's location in the website's folder structure.</span></span> <span data-ttu-id="22240-120">任何不以前导正斜杠开头的 URL (`/`) 或协议 (如`http://`) 是相对的因为在网页上包含的 URL 的位置上基于浏览器会得到解决。</span><span class="sxs-lookup"><span data-stu-id="22240-120">Any URL that does not start with a leading forward slash (`/`) or a protocol (such as `http://`) is relative because it is resolved by the browser based on the location of the web page that contains the URL.</span></span>

<span data-ttu-id="22240-121">例如，我们的网站具有`~/Images/`具有单个图像文件，文件夹`PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-121">For example, our website has an `~/Images/` folder with a single image file, `PoweredByASPNET.gif`.</span></span> <span data-ttu-id="22240-122">主控页文件`Site.master`具有`<img>`中的元素`footerContent`区域替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="22240-122">The master page file `Site.master` has an `<img>` element in the `footerContent` region with the following markup:</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

<span data-ttu-id="22240-123">`src`属性中的值`<img>`元素是相对 URL，因为它不以开头`/`或`http://`。</span><span class="sxs-lookup"><span data-stu-id="22240-123">The `src` attribute value in the `<img>` element is a relative URL because it does not start with `/` or `http://`.</span></span> <span data-ttu-id="22240-124">简单地说，`src`属性值将告诉浏览器中看起来都`Images`名为的文件的子文件夹`PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-124">In short, the `src` attribute value tells the browser to look in the `Images` subfolder for a file named `PoweredByASPNET.gif`.</span></span>

<span data-ttu-id="22240-125">当来访内容页时，上述标记被直接发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="22240-125">When visiting a content page, the above markup is sent directly to the browser.</span></span> <span data-ttu-id="22240-126">花一些时间，请访问`About.aspx`和查看发送到浏览器的 HTML 源文件。</span><span class="sxs-lookup"><span data-stu-id="22240-126">Take a moment to visit `About.aspx` and view the HTML source sent to the browser.</span></span> <span data-ttu-id="22240-127">你将找到母版页中的确切相同标记已发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="22240-127">You will find that the exact same markup in the master page was sent to the browser.</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

<span data-ttu-id="22240-128">如果内容页位于根文件夹中 (因为是`About.aspx`) 一切会按预期行为，因为没有方式`Images`相对于根文件夹的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="22240-128">If the content page is in the root folder (as is `About.aspx`) everything works as expected because there is an `Images` subfolder relative to the root folder.</span></span> <span data-ttu-id="22240-129">但是，操作将分解内容页是否比主控页的其他文件夹中。</span><span class="sxs-lookup"><span data-stu-id="22240-129">However, things break down if the content page is in a different folder than the master page.</span></span> <span data-ttu-id="22240-130">若要说明这一点，创建名为的子`Admin`。</span><span class="sxs-lookup"><span data-stu-id="22240-130">To illustrate this, create a subfolder named `Admin`.</span></span> <span data-ttu-id="22240-131">接下来，添加一个名为的内容页`Default.aspx`到`Admin`文件夹，并确保将绑定到的新页`Site.master`母版页。</span><span class="sxs-lookup"><span data-stu-id="22240-131">Next, add a content page named `Default.aspx` to the `Admin` folder, making sure to bind the new page to the `Site.master` master page.</span></span>

> [!NOTE]
> <span data-ttu-id="22240-132">在[*母版页中指定的标题、 Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中我们创建一个名为的自定义的基本页类`BasePage`，自动设置内容页的标题 (如果它不显式指定了）。</span><span class="sxs-lookup"><span data-stu-id="22240-132">In the [*Specifying the Title, Meta Tags, and Other HTML Headers in the Master Page*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) tutorial we created a custom base page class named `BasePage` that automatically set the content page's title (if it was not explicitly assigned).</span></span> <span data-ttu-id="22240-133">不要忘记将具有新创建的页面的代码隐藏类派生自`BasePage`，以便它可以利用此功能。</span><span class="sxs-lookup"><span data-stu-id="22240-133">Don't forget to have the newly created page's code-behind class derive from `BasePage` so that it can utilize this functionality.</span></span>


<span data-ttu-id="22240-134">创建此内容页后，你的解决方案资源管理器应类似于图 1。</span><span class="sxs-lookup"><span data-stu-id="22240-134">After you have created this content page, your Solution Explorer should look similar to Figure 1.</span></span>


![一个新文件夹和 ASP.NET 网页添加到项目](urls-in-master-pages-cs/_static/image1.png)

<span data-ttu-id="22240-136">**图 01**： 一个新文件夹和 ASP.NET 网页添加到项目</span><span class="sxs-lookup"><span data-stu-id="22240-136">**Figure 01**: A New Folder and ASP.NET Page Have Been Added to the Project</span></span>


<span data-ttu-id="22240-137">接下来，更新`Web.sitemap`文件以包括新`<siteMapNode>`本课程中的条目。</span><span class="sxs-lookup"><span data-stu-id="22240-137">Next, update the `Web.sitemap` file to include a new `<siteMapNode>` entry for this lesson.</span></span> <span data-ttu-id="22240-138">下面的 XML 演示完整`Web.sitemap`标记，现在包括添加第三个`<siteMapNode>`元素。</span><span class="sxs-lookup"><span data-stu-id="22240-138">The following XML shows the complete `Web.sitemap` markup, which now includes the addition of a third `<siteMapNode>` element.</span></span>


[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

<span data-ttu-id="22240-139">新创建`Default.aspx`页应具有与在四个 ContentPlaceHolders 相对应的四个内容控件`Site.master`。</span><span class="sxs-lookup"><span data-stu-id="22240-139">The newly created `Default.aspx` page should have four Content controls corresponding to the four ContentPlaceHolders in `Site.master`.</span></span> <span data-ttu-id="22240-140">将一些文本添加到内容控件引用`MainContent`ContentPlaceHolder，然后访问通过浏览器页面。</span><span class="sxs-lookup"><span data-stu-id="22240-140">Add some text to the Content control referencing the `MainContent` ContentPlaceHolder and then visit the page through a browser.</span></span> <span data-ttu-id="22240-141">如图 2 所示，找不到浏览器`PoweredByASPNET.gif`图像文件。</span><span class="sxs-lookup"><span data-stu-id="22240-141">As Figure 2 shows, the browser cannot find the `PoweredByASPNET.gif` image file.</span></span> <span data-ttu-id="22240-142">这是怎么回事？</span><span class="sxs-lookup"><span data-stu-id="22240-142">What's going on here?</span></span>

<span data-ttu-id="22240-143">`~/Admin/Default.aspx`内容页会发送相同 HTML`footerContent`区域，如已`About.aspx`页：</span><span class="sxs-lookup"><span data-stu-id="22240-143">The `~/Admin/Default.aspx` content page is sent the same HTML for the `footerContent` region as was the `About.aspx` page:</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

<span data-ttu-id="22240-144">因为`<img>`元素的`src`属性是相对 URL，浏览器会尝试查找`Images`相对于，网页的文件夹位置的文件夹。</span><span class="sxs-lookup"><span data-stu-id="22240-144">Because the `<img>` element's `src` attribute is a relative URL, the browser attempts to look for an `Images` folder relative to the web page's folder location.</span></span> <span data-ttu-id="22240-145">换而言之，浏览器查找映像文件`Admin/Images/PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-145">In other words, the browser is looking for the image file `Admin/Images/PoweredByASPNET.gif`.</span></span>


<span data-ttu-id="22240-146">[![找不到 PoweredByASPNET.gif 图像文件](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="22240-146">[![The PoweredByASPNET.gif Image File Cannot Be Found](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)</span></span>

<span data-ttu-id="22240-147">**图 02**:`PoweredByASPNET.gif`映像找不到文件 ([单击以查看实际尺寸的图像](urls-in-master-pages-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="22240-147">**Figure 02**: The `PoweredByASPNET.gif` Image File Cannot Be Found  ([Click to view full-size image](urls-in-master-pages-cs/_static/image4.png))</span></span>


### <a name="replacing-relative-urls-with-absolute-urls"></a><span data-ttu-id="22240-148">将替换为绝对 Url 的相对 Url</span><span class="sxs-lookup"><span data-stu-id="22240-148">Replacing Relative URLs with Absolute URLs</span></span>

<span data-ttu-id="22240-149">相对 URL 相反*绝对 URL*，这是一个以正斜杠开头 (`/`) 或如协议`http://`。</span><span class="sxs-lookup"><span data-stu-id="22240-149">The opposite of a relative URL is an *absolute URL*, which is one that starts with a forward slash (`/`) or a protocol such as `http://`.</span></span> <span data-ttu-id="22240-150">绝对 URL 指定从已知的固定点资源的位置，因为相同的绝对 URL 是在任何 web 页面，而不考虑网站的文件夹结构中的网页的位置中有效。</span><span class="sxs-lookup"><span data-stu-id="22240-150">Because an absolute URL specifies the location of a resource from a known fixed point, the same absolute URL is valid in any web page, regardless of the web page's location in the website's folder structure.</span></span>

<span data-ttu-id="22240-151">若要解决与图 2 所示的图像无效，我们需要更新`<img>`元素的`src`属性，以便它使用而不是一个相对的绝对 URL。</span><span class="sxs-lookup"><span data-stu-id="22240-151">To remedy the broken image shown in Figure 2, we need to update the `<img>` element's `src` attribute so that it uses an absolute URL instead of a relative one.</span></span> <span data-ttu-id="22240-152">若要确定正确的绝对 URL，访问你的网站中的 web 页的某个并检查地址栏中。</span><span class="sxs-lookup"><span data-stu-id="22240-152">To determine the correct absolute URL, visit one of the web pages in your website and examine the Address bar.</span></span> <span data-ttu-id="22240-153">如图 2 中的地址栏显示，web 应用程序的完全限定的路径是`http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`。</span><span class="sxs-lookup"><span data-stu-id="22240-153">As the Address bar in Figure 2 shows, the fully qualified path to the web application is `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`.</span></span> <span data-ttu-id="22240-154">因此，我们无法更新`<img>`元素的`src`属性设为以下两个绝对 url:</span><span class="sxs-lookup"><span data-stu-id="22240-154">Therefore, we could update the `<img>` element's `src` attribute to either of the following two absolute URLs:</span></span>

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

<span data-ttu-id="22240-155">花一些时间来更新`<img>`元素的`src`属性设为使用上面所示的形式之一的绝对 URL，然后访问`~/Admin/Default.aspx`通过浏览器的页。</span><span class="sxs-lookup"><span data-stu-id="22240-155">Take a moment to update the `<img>` element's `src` attribute to an absolute URL using one of the forms shown above and then visit the `~/Admin/Default.aspx` page through a browser.</span></span> <span data-ttu-id="22240-156">此时浏览器将正确查找并显示`PoweredByASPNET.gif`图像文件 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="22240-156">This time the browser will correctly find and display the `PoweredByASPNET.gif` image file (see Figure 3).</span></span>


<span data-ttu-id="22240-157">[![PoweredByASPNET.gif 映像是现在显示](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="22240-157">[![The PoweredByASPNET.gif Image is Now Displayed](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)</span></span>

<span data-ttu-id="22240-158">**图 03**:`PoweredByASPNET.gif`映像是现在显示 ([单击以查看实际尺寸的图像](urls-in-master-pages-cs/_static/image7.png))</span><span class="sxs-lookup"><span data-stu-id="22240-158">**Figure 03**: The `PoweredByASPNET.gif` Image is Now Displayed  ([Click to view full-size image](urls-in-master-pages-cs/_static/image7.png))</span></span>


<span data-ttu-id="22240-159">在中的绝对 URL 进行硬编码，它将紧密到网站的服务器和文件夹位置，这可能会更改标你 HTML。</span><span class="sxs-lookup"><span data-stu-id="22240-159">While hard coding in the absolute URL works, it tightly couples your HTML to the website's server and folder location, which may change.</span></span> <span data-ttu-id="22240-160">使用窗体的绝对 URL`http://localhost:3908/...`操作很脆弱，因为端口号前面`localhost`则会自动选择每次启动 Visual Studio 的内置 ASP.NET 开发 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="22240-160">Using an absolute URL of the form `http://localhost:3908/...` is brittle because the port number preceding `localhost` is selected automatically each time Visual Studio's built-in ASP.NET Development Web Server is started.</span></span> <span data-ttu-id="22240-161">同样，`http://localhost`一部分才有效，在进行本地测试。</span><span class="sxs-lookup"><span data-stu-id="22240-161">Similarly, the `http://localhost` part is only valid when testing locally.</span></span> <span data-ttu-id="22240-162">后的代码部署到生产服务器中，URL 基将更改为其他事情，如`http://www.yourserver.com`。</span><span class="sxs-lookup"><span data-stu-id="22240-162">Once the code is deployed to a production server, the URL base will change to something else, like `http://www.yourserver.com`.</span></span> <span data-ttu-id="22240-163">在窗体中的绝对 URL`/ASPNET_MasterPages_Tutorial_04_CS/...`因为此应用程序路径开发和生产服务器之间不同，通常还面临相同易。</span><span class="sxs-lookup"><span data-stu-id="22240-163">The absolute URL in the form `/ASPNET_MasterPages_Tutorial_04_CS/...` also suffers from the same brittleness because oftentimes this application path differs between development and production servers.</span></span>

<span data-ttu-id="22240-164">好消息是 ASP.NET 提供一个用于生成有效的相对 URL，在运行时方法。</span><span class="sxs-lookup"><span data-stu-id="22240-164">The good news is that ASP.NET offers a method for generating a valid relative URL at runtime.</span></span>

## <a name="usingandresolveclienturl"></a><span data-ttu-id="22240-165">使用`~`和`ResolveClientUrl`</span><span class="sxs-lookup"><span data-stu-id="22240-165">Using`~`and`ResolveClientUrl`</span></span>

<span data-ttu-id="22240-166">而是不是绝对 URL 进行硬编码，ASP.NET 将允许页开发人员使用波形符 (`~`) 以指示 web 应用程序的根目录。</span><span class="sxs-lookup"><span data-stu-id="22240-166">Rather than hard code an absolute URL, ASP.NET allows page developers to use the tilde (`~`) to indicate the root of the web application.</span></span> <span data-ttu-id="22240-167">例如，在本教程前面我使用了表示法`~/Admin/Default.aspx`文本中指`Default.aspx`页面`Admin`文件夹。</span><span class="sxs-lookup"><span data-stu-id="22240-167">For example, earlier in this tutorial I used the notation `~/Admin/Default.aspx` in the text to refer to the `Default.aspx` page in the `Admin` folder.</span></span> <span data-ttu-id="22240-168">`~`指示`Admin`文件夹是 web 应用程序的根的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="22240-168">The `~` indicates that the `Admin` folder is a subfolder of the web application's root.</span></span>

<span data-ttu-id="22240-169">`Control`类的[`ResolveClientUrl`方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx)采用 URL 和到相应控件所驻留的网页的相对 URL 对其进行修改。</span><span class="sxs-lookup"><span data-stu-id="22240-169">The `Control` class's [`ResolveClientUrl` method](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) takes a URL and modifies it to a relative URL appropriate for the web page on which the control resides.</span></span> <span data-ttu-id="22240-170">例如，调用`ResolveClientUrl("~/Images/PoweredByASPNET.gif")`从`About.aspx`返回`Images/PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-170">For example, calling `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` from `About.aspx` returns `Images/PoweredByASPNET.gif`.</span></span> <span data-ttu-id="22240-171">调用从`~/Admin/Default.aspx`，但是，返回`../Images/PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-171">Calling it from `~/Admin/Default.aspx`, however, returns `../Images/PoweredByASPNET.gif`.</span></span>

> [!NOTE]
> <span data-ttu-id="22240-172">因为所有 ASP.NET 服务器控件都派生自`Control`类，所有服务器控件都有权访问`ResolveClientUrl`方法。</span><span class="sxs-lookup"><span data-stu-id="22240-172">Because all ASP.NET server controls derive from the `Control` class, all server controls have access to the `ResolveClientUrl` method.</span></span> <span data-ttu-id="22240-173">即使`Page`类派生自`Control`类，这意味着你可以使用此方法直接从 ASP.NET 页的代码隐藏类。</span><span class="sxs-lookup"><span data-stu-id="22240-173">Even the `Page` class derives from the `Control` class, meaning that you can use this method directly from your ASP.NET pages' code-behind classes.</span></span>


### <a name="usingin-the-declarative-markup"></a><span data-ttu-id="22240-174">使用`~`中的声明性的标记</span><span class="sxs-lookup"><span data-stu-id="22240-174">Using`~`in the Declarative Markup</span></span>

<span data-ttu-id="22240-175">多个 ASP.NET Web 控件，包括 URL 相关的属性： 超链接控件具有`NavigateUrl`属性; 图像控件具有`ImageUrl`属性; 依次类推。</span><span class="sxs-lookup"><span data-stu-id="22240-175">Several ASP.NET Web controls include URL-related properties: the HyperLink control has a `NavigateUrl` property; the Image control has an `ImageUrl` property; and so on.</span></span> <span data-ttu-id="22240-176">呈现时，这些控件将传递到其 URL 相关的属性值`ResolveClientUrl`。</span><span class="sxs-lookup"><span data-stu-id="22240-176">When rendered, these controls pass their URL-related property values to `ResolveClientUrl`.</span></span> <span data-ttu-id="22240-177">因此，如果这些属性包含`~`若要指示 web 应用程序的根目录，URL 将修改为有效的相对 URL。</span><span class="sxs-lookup"><span data-stu-id="22240-177">Consequently, if these properties contain a `~` to indicate the root of the web application, the URL will be modified to a valid relative URL.</span></span>

<span data-ttu-id="22240-178">请记住，只有 ASP.NET 服务器控件转换`~`在其 URL 相关的属性。</span><span class="sxs-lookup"><span data-stu-id="22240-178">Keep in mind that only ASP.NET server controls transform the `~` in their URL-related properties.</span></span> <span data-ttu-id="22240-179">如果`~`显示在静态 HTML 标记中，例如`<img src="~/Images/PoweredByASPNET.gif" />`，ASP.NET 引擎将发送`~`到浏览器的其余部分的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="22240-179">If a `~` appears in static HTML markup, such as `<img src="~/Images/PoweredByASPNET.gif" />`, the ASP.NET engine sends the `~` to the browser along with the rest of the HTML content.</span></span> <span data-ttu-id="22240-180">浏览器假定`~`是 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="22240-180">The browser assumes that the `~` is part of the URL.</span></span> <span data-ttu-id="22240-181">例如，如果浏览器收到标记`<img src="~/Images/PoweredByASPNET.gif" />`它假定有一个名为子`~`，该子文件夹`Images`包含图像文件`PoweredByASPNET.gif`。</span><span class="sxs-lookup"><span data-stu-id="22240-181">For example, if the browser receives the markup `<img src="~/Images/PoweredByASPNET.gif" />` it assumes there is a subfolder named `~` with a subfolder `Images` that contains the image file `PoweredByASPNET.gif`.</span></span>

<span data-ttu-id="22240-182">若要解决问题中的图像标记`Site.master`，将现有`<img>`与 ASP.NET 映像 Web 控件的元素。</span><span class="sxs-lookup"><span data-stu-id="22240-182">To fix the image markup in `Site.master`, replace the existing `<img>` element with an ASP.NET Image Web control.</span></span> <span data-ttu-id="22240-183">设置映像 Web 控件的`ID`到`PoweredByImage`，将其`ImageUrl`属性`~/Images/PoweredByASPNET.gif`，并将其`AlternateText`"提供支持的 asp.net ！"的属性</span><span class="sxs-lookup"><span data-stu-id="22240-183">Set the Image Web control's `ID` to `PoweredByImage`, its `ImageUrl` property to `~/Images/PoweredByASPNET.gif`, and its `AlternateText` property to "Powered by ASP.NET!"</span></span>


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="22240-184">对母版页进行此更改后, 重新访问`~/Admin/Default.aspx`再次页。</span><span class="sxs-lookup"><span data-stu-id="22240-184">After making this change to the master page, revisit the `~/Admin/Default.aspx` page again.</span></span> <span data-ttu-id="22240-185">这一次`PoweredByASPNET.gif`的页中出现的图像文件 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="22240-185">This time the `PoweredByASPNET.gif` image file appears in the page (see Figure 3).</span></span> <span data-ttu-id="22240-186">当映像 Web 控件是呈现使用`ResolveClientUrl`方法解决其`ImageUrl`属性值。</span><span class="sxs-lookup"><span data-stu-id="22240-186">When the Image Web control is rendered it uses the `ResolveClientUrl` method to resolve its `ImageUrl` property value.</span></span> <span data-ttu-id="22240-187">在`~/Admin/Default.aspx``ImageUrl`将转换为适当的相对 URL，为以下代码段的 HTML 源所示：</span><span class="sxs-lookup"><span data-stu-id="22240-187">In `~/Admin/Default.aspx` the `ImageUrl` is converted into an appropriate relative URL, as the following snippet of HTML source shows:</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> <span data-ttu-id="22240-188">除了在基于 URL 的 Web 控件属性，在使用`~`还可在调用时`Response.Redirect`和`Server.MapPath`方法，以及其他。</span><span class="sxs-lookup"><span data-stu-id="22240-188">In addition to being used in URL-based Web control properties, the `~` can also be used when calling the `Response.Redirect` and `Server.MapPath` methods, among others.</span></span> <span data-ttu-id="22240-189">此外，`ResolveClientUrl`可能直接从 ASP.NET 或母版页的声明性标记，调用方法，如果需要请参阅[Fritz 透视](https://www.pluralsight.com/blogs/fritz/)的博客文章[使用`ResolveClientUrl`标记中](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)。</span><span class="sxs-lookup"><span data-stu-id="22240-189">Also, the `ResolveClientUrl` method may be invoked directly from an ASP.NET or master page's declarative markup, if needed; see [Fritz Onion](https://www.pluralsight.com/blogs/fritz/)'s blog entry [Using `ResolveClientUrl` in Markup](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx).</span></span>


## <a name="fixing-the-master-pages-remaining-relative-urls"></a><span data-ttu-id="22240-190">修复母版页的剩余相对 Url</span><span class="sxs-lookup"><span data-stu-id="22240-190">Fixing the Master Page's Remaining Relative URLs</span></span>

<span data-ttu-id="22240-191">除了`<img>`中的元素`footerContent`我们只需固定、 母版页包含需要我们关注的一个更相对 URL。</span><span class="sxs-lookup"><span data-stu-id="22240-191">In addition to the `<img>` element in the `footerContent` that we just fixed, the master page contains one more relative URL that requires our attention.</span></span> <span data-ttu-id="22240-192">`topContent`区域包括链接"Master 页教程，"用于指向`Default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="22240-192">The `topContent` region includes the link "Master Pages Tutorials," which points to `Default.aspx`.</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

<span data-ttu-id="22240-193">由于此 URL 是相对的它将发送到用户`Default.aspx`他们访问的内容页的文件夹中的页。</span><span class="sxs-lookup"><span data-stu-id="22240-193">Because this URL is relative, it will send the user to the `Default.aspx` page in the folder of the content page they are visiting.</span></span> <span data-ttu-id="22240-194">能够始终指向此链接`Default.aspx`我们需要更换的根文件夹中`<a>`元素与超链接 Web 控件，以便我们可以使用`~`表示法。</span><span class="sxs-lookup"><span data-stu-id="22240-194">To have this link always point to `Default.aspx` in the root folder we need to replace the `<a>` element with a HyperLink Web control so that we can use the `~` notation.</span></span>

<span data-ttu-id="22240-195">删除`<a>`元素标记并在该处添加超链接控件。</span><span class="sxs-lookup"><span data-stu-id="22240-195">Remove the `<a>` element markup and add a HyperLink control in its place.</span></span> <span data-ttu-id="22240-196">设置超链接的`ID`到`lnkHome`，将其`NavigateUrl`属性`~/Default.aspx`，并将其`Text`属性设置为"Master 页教程"。</span><span class="sxs-lookup"><span data-stu-id="22240-196">Set the HyperLink's `ID` to `lnkHome`, its `NavigateUrl` property to `~/Default.aspx`, and its `Text` property to "Master Pages Tutorials."</span></span>


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

<span data-ttu-id="22240-197">就这么简单！</span><span class="sxs-lookup"><span data-stu-id="22240-197">That's it!</span></span> <span data-ttu-id="22240-198">此时所有母版页和内容页，而不考虑哪些文件夹内容页呈现时，我们母版页中的 Url 正确基于位于中。</span><span class="sxs-lookup"><span data-stu-id="22240-198">At this point all the URLs in our master page are properly based when rendered by a content page regardless of what folders the master page and content page are located in.</span></span>

### <a name="automatic-url-resolution-in-theheadsection"></a><span data-ttu-id="22240-199">中的自动 URL 解析`<head>`部分</span><span class="sxs-lookup"><span data-stu-id="22240-199">Automatic URL Resolution in the`<head>`Section</span></span>

<span data-ttu-id="22240-200">在[*创建站点范围布局使用 Master 页*](creating-a-site-wide-layout-using-master-pages-cs.md)教程，我们添加`<link>`到`Styles.css`文件中`<head>`区域：</span><span class="sxs-lookup"><span data-stu-id="22240-200">In the [*Creating a Site-Wide Layout Using Master Pages*](creating-a-site-wide-layout-using-master-pages-cs.md) tutorial we added a `<link>` to the `Styles.css` file in the `<head>` region:</span></span>


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

<span data-ttu-id="22240-201">虽然`<link>`元素的`href`属性是相对的它会自动转换为在运行时正确的路径。</span><span class="sxs-lookup"><span data-stu-id="22240-201">While the `<link>` element's `href` attribute is relative, it's automatically converted to an appropriate path at runtime.</span></span> <span data-ttu-id="22240-202">如我们所述[*母版页中指定的标题、 Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中，`<head>`区域是实际的服务器端控件，从而使其能够修改其内部控件呈现时的内容。</span><span class="sxs-lookup"><span data-stu-id="22240-202">As we discussed in the [*Specifying the Title, Meta Tags, and Other HTML Headers in the Master Page*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) tutorial, the `<head>` region is actually a server-side control, which enables it to modify the contents of its inner controls when it is rendered.</span></span>

<span data-ttu-id="22240-203">若要验证这一点，重新访问`~/Admin/Default.aspx`页面，查看发送到浏览器的 HTML 源文件。</span><span class="sxs-lookup"><span data-stu-id="22240-203">To verify this, revisit the `~/Admin/Default.aspx` page and view the HTML source sent to the browser.</span></span> <span data-ttu-id="22240-204">如下面的代码段所示，`<link>`元素的`href`属性自动修改为适当的相对 URL， `../Styles.css`。</span><span class="sxs-lookup"><span data-stu-id="22240-204">As the snippet below illustrates, the `<link>` element's `href` attribute has been automatically modified to an appropriate relative URL, `../Styles.css`.</span></span>


[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a><span data-ttu-id="22240-205">总结</span><span class="sxs-lookup"><span data-stu-id="22240-205">Summary</span></span>

<span data-ttu-id="22240-206">母版页经常包括链接、 图像和其他必须通过 URL 指定的外部资源。</span><span class="sxs-lookup"><span data-stu-id="22240-206">Master pages very often include links, images, and other external resources that must be specified via a URL.</span></span> <span data-ttu-id="22240-207">因为主控页和内容页可能不存在的相同文件夹中，务必 abstain 从使用相对 Url。</span><span class="sxs-lookup"><span data-stu-id="22240-207">Because the master page and content pages might not exist in the same folder, it is important to abstain from using relative URLs.</span></span> <span data-ttu-id="22240-208">可以使用硬编码的绝对 Url 时，因此紧密到 web 应用程序中利用的绝对 URL。</span><span class="sxs-lookup"><span data-stu-id="22240-208">While it is possible to use hard coded absolute URLs, doing so tightly couples the absolute URL to the web application.</span></span> <span data-ttu-id="22240-209">如果发生更改的绝对 URL-通常时那样移动或部署 web 应用程序-你将需要记住以返回并更新绝对 Url。</span><span class="sxs-lookup"><span data-stu-id="22240-209">If the absolute URL changes - as it often does when moving or deploying a web application - you'll have to remember to go back and update the absolute URLs.</span></span>

<span data-ttu-id="22240-210">理想的方法是使用波形符 (`~`) 以指示应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="22240-210">The ideal approach is to use the tilde (`~`) to indicate the application root.</span></span> <span data-ttu-id="22240-211">包含与 URL 相关的属性的 ASP.NET Web 控件映射`~`为在运行时应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="22240-211">ASP.NET Web controls that contain URL-related properties map the `~` to the application root at runtime.</span></span> <span data-ttu-id="22240-212">在内部，Web 控件使用`Control`类的`ResolveClientUrl`方法来生成有效的相对 URL。</span><span class="sxs-lookup"><span data-stu-id="22240-212">Internally, the Web controls use the `Control` class's `ResolveClientUrl` method to generate a valid relative URL.</span></span> <span data-ttu-id="22240-213">此方法是公用的且可从每个服务器控件 (包括`Page`类)，因此你可以使用它以编程方式从你的代码隐藏类，如果需要。</span><span class="sxs-lookup"><span data-stu-id="22240-213">This method is public and available from every server control (including the `Page` class), so you can use it programmatically from your code-behind classes, if needed.</span></span>

<span data-ttu-id="22240-214">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="22240-214">Happy Programming!</span></span>

### <a name="further-reading"></a><span data-ttu-id="22240-215">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="22240-215">Further Reading</span></span>

<span data-ttu-id="22240-216">在本教程中讨论的主题的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="22240-216">For more information on the topics discussed in this tutorial, refer to the following resources:</span></span>

- [<span data-ttu-id="22240-217">在 ASP.NET 母版页</span><span class="sxs-lookup"><span data-stu-id="22240-217">Master Pages in ASP.NET</span></span>](http://www.odetocode.com/Articles/419.aspx)
- [<span data-ttu-id="22240-218">母版页中的 URL 重定基址</span><span class="sxs-lookup"><span data-stu-id="22240-218">URL Rebasing in a Master Page</span></span>](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [<span data-ttu-id="22240-219">使用`ResolveClientUrl`标记中</span><span class="sxs-lookup"><span data-stu-id="22240-219">Using `ResolveClientUrl` in Markup</span></span>](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a><span data-ttu-id="22240-220">关于作者</span><span class="sxs-lookup"><span data-stu-id="22240-220">About the Author</span></span>

<span data-ttu-id="22240-221">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个 ASP/ASP.NET 丛书和 4GuysFromRolla.com 创始人，具有已使用 Microsoft Web 技术自 1998 年。</span><span class="sxs-lookup"><span data-stu-id="22240-221">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of multiple ASP/ASP.NET books and founder of 4GuysFromRolla.com, has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="22240-222">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="22240-222">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="22240-223">最新书籍是[ *Sam 教授自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="22240-223">His latest book is [*Sams Teach Yourself ASP.NET 3.5 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="22240-224">可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过在其博客地址[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。</span><span class="sxs-lookup"><span data-stu-id="22240-224">Scott can be reached at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) or via his blog at [http://ScottOnWriting.NET](http://scottonwriting.net/).</span></span>

### <a name="special-thanks-to"></a><span data-ttu-id="22240-225">特别感谢</span><span class="sxs-lookup"><span data-stu-id="22240-225">Special Thanks To</span></span>

<span data-ttu-id="22240-226">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="22240-226">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="22240-227">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。</span><span class="sxs-lookup"><span data-stu-id="22240-227">If so, drop me a line at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22240-228">[上一页](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [下一页](control-id-naming-in-content-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="22240-228">[Previous](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
[Next](control-id-naming-in-content-pages-cs.md)</span></span>
