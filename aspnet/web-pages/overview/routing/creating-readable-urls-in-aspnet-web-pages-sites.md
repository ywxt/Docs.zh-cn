---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 在 ASP.NET 网页中创建可读的 Url 页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本指南介绍了一个 ASP.NET Web 页 (Razor) 的网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 中的路由。 你的将...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 7858b7cbd6dccafb2867ed9a1d102561e211e435
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529746"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="9a720-104">在 ASP.NET Web 页 (Razor) 站点中创建可读的 Url</span><span class="sxs-lookup"><span data-stu-id="9a720-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="9a720-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9a720-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9a720-106">本指南介绍了一个 ASP.NET Web 页 (Razor) 的网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 中的路由。</span><span class="sxs-lookup"><span data-stu-id="9a720-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="9a720-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="9a720-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9a720-108">如何 ASP.NET 使用路由来允许你使用更具可读性且更可搜索的 Url。</span><span class="sxs-lookup"><span data-stu-id="9a720-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9a720-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="9a720-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9a720-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="9a720-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="9a720-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="9a720-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="about-routing"></a><span data-ttu-id="9a720-112">有关路由</span><span class="sxs-lookup"><span data-stu-id="9a720-112">About Routing</span></span>

<span data-ttu-id="9a720-113">在你的站点中的页面的 Url 可以影响以及站点的工作原理。</span><span class="sxs-lookup"><span data-stu-id="9a720-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="9a720-114">URL 的&quot;友好&quot;可以更加轻松让人有机会使用站点。</span><span class="sxs-lookup"><span data-stu-id="9a720-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="9a720-115">它还可帮助搜索引擎搜索引擎优化 (SEO) 站点。</span><span class="sxs-lookup"><span data-stu-id="9a720-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="9a720-116">ASP.NET 网站包括能够自动使用友好的 Url。</span><span class="sxs-lookup"><span data-stu-id="9a720-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="9a720-117">ASP.NET，可以创建有意义描述用户的操作，而不是仅指向服务器上的文件的 Url。</span><span class="sxs-lookup"><span data-stu-id="9a720-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="9a720-118">请考虑这些 Url 的虚构博客：</span><span class="sxs-lookup"><span data-stu-id="9a720-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="9a720-119">比较以下到这些 Url:</span><span class="sxs-lookup"><span data-stu-id="9a720-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="9a720-120">在第一个对，用户必须知道使用显示博客*blog.cshtml*页，然后将必须构造查询字符串，可获取正确的类别或日期范围。</span><span class="sxs-lookup"><span data-stu-id="9a720-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="9a720-121">更易于理解和创建的第二个示例集。</span><span class="sxs-lookup"><span data-stu-id="9a720-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="9a720-122">第一个示例的 Url 也点直接到特定的文件 (*blog.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="9a720-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="9a720-123">如果出于某种原因博客移到另一个文件夹的服务器上，或者如果博客已重新，改为使用不同的页，则链接将是错误的。</span><span class="sxs-lookup"><span data-stu-id="9a720-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="9a720-124">第二个组 Url 未指向特定页，因此，即使的博客实现或位置发生更改，Url 将仍将有效。</span><span class="sxs-lookup"><span data-stu-id="9a720-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="9a720-125">在 ASP.NET Web 页中，您可以创建类似于上面的示例中的更友好 Url 因为 ASP.NET 使用*路由*。</span><span class="sxs-lookup"><span data-stu-id="9a720-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="9a720-126">路由可以完成请求指向的页 （或页） 的 URL 从创建逻辑映射。</span><span class="sxs-lookup"><span data-stu-id="9a720-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="9a720-127">因为映射被逻辑 （不是物理，到特定文件），路由提供极其灵活地为您的网站定义 Url 的方式。</span><span class="sxs-lookup"><span data-stu-id="9a720-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="9a720-128">路由的工作原理</span><span class="sxs-lookup"><span data-stu-id="9a720-128">How Routing Works</span></span>

<span data-ttu-id="9a720-129">当 ASP.NET 处理的请求时，它会读取来确定如何将其路由的 URL。</span><span class="sxs-lookup"><span data-stu-id="9a720-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="9a720-130">ASP.NET 尝试匹配三个部分，将从左到右，磁盘上的文件的 URL。</span><span class="sxs-lookup"><span data-stu-id="9a720-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="9a720-131">如果没有匹配项，则将在 URL 中剩余的任何内容传递给页作为*路径信息*。</span><span class="sxs-lookup"><span data-stu-id="9a720-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="9a720-132">假设有人进行使用此 URL 的请求：</span><span class="sxs-lookup"><span data-stu-id="9a720-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="9a720-133">搜索如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a720-133">The search goes like this:</span></span>

1. <span data-ttu-id="9a720-134">是否存在的文件的路径和名称 */a/b/c.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="9a720-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="9a720-135">如果是这样，运行该页面，并向其传递任何信息。</span><span class="sxs-lookup"><span data-stu-id="9a720-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="9a720-136">否则为...</span><span class="sxs-lookup"><span data-stu-id="9a720-136">Otherwise ...</span></span>
2. <span data-ttu-id="9a720-137">是否存在的文件的路径和名称 */a/b.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="9a720-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="9a720-138">如果因此，运行该页面，并将值传递`c`到它。</span><span class="sxs-lookup"><span data-stu-id="9a720-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="9a720-139">否则为...</span><span class="sxs-lookup"><span data-stu-id="9a720-139">Otherwise …</span></span>
3. <span data-ttu-id="9a720-140">是否存在的文件的路径和名称 */a.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="9a720-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="9a720-141">如果因此，运行该页面，并将值传递`b/c`到它。</span><span class="sxs-lookup"><span data-stu-id="9a720-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="9a720-142">如果搜索已找到不精确的匹配项 *.cshtml*其指定文件夹中的文件，ASP.NET 将继续进行反过来查找这些文件：</span><span class="sxs-lookup"><span data-stu-id="9a720-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="9a720-143">*/a/b/c/default.cshtml* （任何路径信息）。</span><span class="sxs-lookup"><span data-stu-id="9a720-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="9a720-144">*/a/b/c/index.cshtml* （任何路径信息）。</span><span class="sxs-lookup"><span data-stu-id="9a720-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="9a720-145">为了清楚起见，特定页的请求 (即，包括请求 *.cshtml*文件扩展名) 就像你预期一样工作。</span><span class="sxs-lookup"><span data-stu-id="9a720-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="9a720-146">请求喜欢`http://www.contoso.com/a/b.cshtml`将运行页面*b.cshtml*正常。</span><span class="sxs-lookup"><span data-stu-id="9a720-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>


<span data-ttu-id="9a720-147">在页上，你可以通过该页面的路径信息`UrlData`属性，它是一个字典。</span><span class="sxs-lookup"><span data-stu-id="9a720-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="9a720-148">假设你有一个名为文件*ViewCustomers.cshtml*和你的站点获取此请求：</span><span class="sxs-lookup"><span data-stu-id="9a720-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="9a720-149">如上面的规则中所述，请求将转到你的页面。</span><span class="sxs-lookup"><span data-stu-id="9a720-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="9a720-150">在页上，可以使用类似如下的代码，获取和显示的路径信息 (在此情况下，值&quot;1000年&quot;):</span><span class="sxs-lookup"><span data-stu-id="9a720-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="9a720-151">由于路由不涉及完整的文件名，可能存在多义性如果必须具有相同的页名称但不同的文件名扩展 (例如， *MyPage.cshtml*和*MyPage.html*).</span><span class="sxs-lookup"><span data-stu-id="9a720-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="9a720-152">为了避免出现路由问题，最好是若要确保你不包含其名称仅在其扩展名不同的站点中的页。</span><span class="sxs-lookup"><span data-stu-id="9a720-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="9a720-153">其他资源</span><span class="sxs-lookup"><span data-stu-id="9a720-153">Additional Resources</span></span>

<span data-ttu-id="9a720-154">[WebMatrix-Url、 UrlData 和路由 SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。</span><span class="sxs-lookup"><span data-stu-id="9a720-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="9a720-155">由 Mike Brind 此博客文章提供有关路由的工作方式中的 ASP.NET Web Pages 某些其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="9a720-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
