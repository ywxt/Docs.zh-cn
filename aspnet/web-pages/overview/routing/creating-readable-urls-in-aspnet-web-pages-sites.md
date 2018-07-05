---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 创建可读 Url 在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本指南介绍了中的 ASP.NET Web Pages (Razor) 网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 的路由。 您的将...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: d027be2924f24c1080deb4ee2deacc235bbd1001
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385743"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="73286-104">在 ASP.NET Web Pages (Razor) 站点中创建可读 Url</span><span class="sxs-lookup"><span data-stu-id="73286-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="73286-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="73286-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="73286-106">本指南介绍了中的 ASP.NET Web Pages (Razor) 网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 的路由。</span><span class="sxs-lookup"><span data-stu-id="73286-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="73286-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="73286-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="73286-108">如何 ASP.NET 使用路由来使您可以用更具可读性和可搜索 Url。</span><span class="sxs-lookup"><span data-stu-id="73286-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="73286-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="73286-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="73286-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="73286-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="73286-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="73286-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="about-routing"></a><span data-ttu-id="73286-112">有关路由</span><span class="sxs-lookup"><span data-stu-id="73286-112">About Routing</span></span>

<span data-ttu-id="73286-113">在你的站点中的页面的 Url 可以影响程度网站正常工作。</span><span class="sxs-lookup"><span data-stu-id="73286-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="73286-114">URL 的&quot;友好&quot;可以更轻松的人们能够使用该站点。</span><span class="sxs-lookup"><span data-stu-id="73286-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="73286-115">它还有助于使用搜索引擎搜索引擎优化 (SEO) 的站点。</span><span class="sxs-lookup"><span data-stu-id="73286-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="73286-116">ASP.NET 网站包括能够自动使用友好的 Url。</span><span class="sxs-lookup"><span data-stu-id="73286-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="73286-117">ASP.NET 允许您创建有意义描述用户操作而不是仅指向服务器上的文件的 Url。</span><span class="sxs-lookup"><span data-stu-id="73286-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="73286-118">请考虑这些 Url 为虚构的博客：</span><span class="sxs-lookup"><span data-stu-id="73286-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="73286-119">比较于以下的这些 Url:</span><span class="sxs-lookup"><span data-stu-id="73286-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="73286-120">在第一对中，用户必须知道使用显示博客*blog.cshtml*页，然后将不得不构造一个查询字符串，获取正确的类别或日期范围。</span><span class="sxs-lookup"><span data-stu-id="73286-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="73286-121">示例的第二个集是更易于理解和创建。</span><span class="sxs-lookup"><span data-stu-id="73286-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="73286-122">在第一个示例 Url 还直接指向特定文件 (*blog.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="73286-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="73286-123">如果出于某种原因博客移到另一个文件夹的服务器上，或者如果博客进行了重新编写为使用不同的页，就是错误的链接。</span><span class="sxs-lookup"><span data-stu-id="73286-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="73286-124">第二个集的 Url 未指向特定页，因此，即使博客实现或位置发生更改，Url 将仍将有效。</span><span class="sxs-lookup"><span data-stu-id="73286-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="73286-125">ASP.NET Web Pages 中，您可以创建类似于上面的示例中的更友好 Url 因为 ASP.NET 使用*路由*。</span><span class="sxs-lookup"><span data-stu-id="73286-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="73286-126">路由从可以完成请求的 URL 为某页 （或页面） 中创建逻辑映射。</span><span class="sxs-lookup"><span data-stu-id="73286-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="73286-127">由于映射逻辑 （不是物理，对特定文件），路由提供了极其灵活地为您的网站定义 Url 的方式。</span><span class="sxs-lookup"><span data-stu-id="73286-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="73286-128">路由的工作原理</span><span class="sxs-lookup"><span data-stu-id="73286-128">How Routing Works</span></span>

<span data-ttu-id="73286-129">当 ASP.NET 处理的请求时，它会读取来确定如何将其路由的 URL。</span><span class="sxs-lookup"><span data-stu-id="73286-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="73286-130">ASP.NET 会尝试匹配三个部分，我们从左到右在磁盘上，文件的 URL。</span><span class="sxs-lookup"><span data-stu-id="73286-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="73286-131">如果没有匹配项，在 URL 中剩余的任何内容传递给与页面*路径信息*。</span><span class="sxs-lookup"><span data-stu-id="73286-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="73286-132">假设有人使用此 URL 的请求：</span><span class="sxs-lookup"><span data-stu-id="73286-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="73286-133">搜索如下所示：</span><span class="sxs-lookup"><span data-stu-id="73286-133">The search goes like this:</span></span>

1. <span data-ttu-id="73286-134">是否有具有的路径和名称的文件 */a/b/c.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="73286-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="73286-135">如果是这样，运行该页面，并向其传递任何信息。</span><span class="sxs-lookup"><span data-stu-id="73286-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="73286-136">否则为...</span><span class="sxs-lookup"><span data-stu-id="73286-136">Otherwise ...</span></span>
2. <span data-ttu-id="73286-137">是否有具有的路径和名称的文件 */a/b.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="73286-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="73286-138">如果因此，运行该页面并将值传递`c`到它。</span><span class="sxs-lookup"><span data-stu-id="73286-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="73286-139">否则为...</span><span class="sxs-lookup"><span data-stu-id="73286-139">Otherwise …</span></span>
3. <span data-ttu-id="73286-140">是否有具有的路径和名称的文件 */a.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="73286-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="73286-141">如果因此，运行该页面并将值传递`b/c`到它。</span><span class="sxs-lookup"><span data-stu-id="73286-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="73286-142">如果找到不精确的搜索匹配的 *.cshtml*其指定文件夹中的文件，ASP.NET 仍继续查找这些文件反过来：</span><span class="sxs-lookup"><span data-stu-id="73286-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="73286-143">*/a/b/c/default.cshtml* （没有路径信息）。</span><span class="sxs-lookup"><span data-stu-id="73286-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="73286-144">*/a/b/c/index.cshtml* （没有路径信息）。</span><span class="sxs-lookup"><span data-stu-id="73286-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="73286-145">为了清楚起见，特定页的请求 (即，请求： 其包括 *.cshtml*文件扩展名) 起作用就像你所期望的一样。</span><span class="sxs-lookup"><span data-stu-id="73286-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="73286-146">所示的请求`http://www.contoso.com/a/b.cshtml`将运行页面*b.cshtml*得很好。</span><span class="sxs-lookup"><span data-stu-id="73286-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>


<span data-ttu-id="73286-147">在页上，就可以通过页面的路径信息`UrlData`属性，它是一个字典。</span><span class="sxs-lookup"><span data-stu-id="73286-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="73286-148">假设您有一个名为文件*ViewCustomers.cshtml*和你的站点获取此请求：</span><span class="sxs-lookup"><span data-stu-id="73286-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="73286-149">上述规则中所述，请求将转到你的页面。</span><span class="sxs-lookup"><span data-stu-id="73286-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="73286-150">在页上，可以使用如下所示的代码，以获取并显示路径信息 (在此情况下，值&quot;1000年&quot;):</span><span class="sxs-lookup"><span data-stu-id="73286-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="73286-151">由于路由不会涉及完整的文件名称，可能存在二义性如果页面具有相同名称但具有不同文件扩展名 (例如， *MyPage.cshtml*并*MyPage.html*).</span><span class="sxs-lookup"><span data-stu-id="73286-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="73286-152">为了避免出现路由问题，最好是确保没有页面的名称仅在其扩展插件中不同的站点中。</span><span class="sxs-lookup"><span data-stu-id="73286-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="73286-153">其他资源</span><span class="sxs-lookup"><span data-stu-id="73286-153">Additional Resources</span></span>

<span data-ttu-id="73286-154">[WebMatrix-Url、 UrlData 和路由 SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。</span><span class="sxs-lookup"><span data-stu-id="73286-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="73286-155">由 Mike Brind 此博客文章提供路由的工作原理 ASP.NET Web Pages 中的某些其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="73286-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
