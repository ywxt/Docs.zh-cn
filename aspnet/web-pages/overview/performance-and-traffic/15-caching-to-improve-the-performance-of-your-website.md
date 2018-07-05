---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 在 ASP.NET Web 中缓存数据页 (Razor) 站点的更好的性能 |Microsoft Docs
author: tfitzmac
description: 你可以加快你的网站通过存储程序，即缓存的结果通常会需要大量时间来检索或处理的数据...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2014
ms.topic: article
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 4134c80d7eed4752c90a06aab796a0fd8c2a9782
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383404"
---
<a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a><span data-ttu-id="de90d-103">更好的性能的缓存的 ASP.NET Web Pages (Razor) 站点中的数据</span><span class="sxs-lookup"><span data-stu-id="de90d-103">Caching Data in an ASP.NET Web Pages (Razor) Site for Better Performance</span></span>
====================
<span data-ttu-id="de90d-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="de90d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="de90d-105">本文介绍如何使用缓存信息的帮助程序进行更快的性能，在 ASP.NET Web Pages (Razor) 的网站中。</span><span class="sxs-lookup"><span data-stu-id="de90d-105">This article explains how to use a helper to cache information for faster performance in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="de90d-106">可以通过存储来加快你的网站&#8212;，即缓存&#8212;的数据，通常那样会花费相当长的时间来检索或处理并不经常更改的结果。</span><span class="sxs-lookup"><span data-stu-id="de90d-106">You can speed up your website by having it store &#8212; that is, cache &#8212; the results of data that ordinarily would take considerable time to retrieve or process and that does not change often.</span></span>
> 
> <span data-ttu-id="de90d-107">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="de90d-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="de90d-108">如何使用缓存来提高你的网站的响应能力。</span><span class="sxs-lookup"><span data-stu-id="de90d-108">How to use caching to improve the responsiveness of your website.</span></span>
> 
> <span data-ttu-id="de90d-109">下面是在本文中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="de90d-109">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="de90d-110">`WebCache`帮助器。</span><span class="sxs-lookup"><span data-stu-id="de90d-110">The `WebCache` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="de90d-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="de90d-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="de90d-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="de90d-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="de90d-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="de90d-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="de90d-114">每次有人从您的网站请求页面时，web 服务器必须执行一些操作才能完成请求。</span><span class="sxs-lookup"><span data-stu-id="de90d-114">Every time someone requests a page from your site, the web server has to do some work in order to fulfill the request.</span></span> <span data-ttu-id="de90d-115">对于某些页面中，服务器可能需要执行需要 （相对） 长时间，如从数据库检索数据的任务。</span><span class="sxs-lookup"><span data-stu-id="de90d-115">For some of your pages, the server might have to perform tasks that take a (comparatively) long time, such as retrieving data from a database.</span></span> <span data-ttu-id="de90d-116">即使这些任务不采用长绝对意义上讲，如果您的网站遇到大量流量，一整个系列的会导致 web 服务器来执行复杂的或速度缓慢的任务的单个请求最多可添加了大量工作。</span><span class="sxs-lookup"><span data-stu-id="de90d-116">Even if these tasks don't take long in absolute terms, if your site experiences a lot of traffic, a whole series of individual requests that cause the web server to perform the complicated or slow task can add up to a lot of work.</span></span> <span data-ttu-id="de90d-117">这最终会影响站点的性能。</span><span class="sxs-lookup"><span data-stu-id="de90d-117">This can ultimately affect the performance of the site.</span></span>

<span data-ttu-id="de90d-118">若要提高此类情况下在你性能的一种方法是网站的缓存数据。</span><span class="sxs-lookup"><span data-stu-id="de90d-118">One way to improve the performance of your website in circumstances like this is to cache data.</span></span> <span data-ttu-id="de90d-119">如果你的站点获取重复的请求相同的信息，和不需为每个人员修改信息并不是时间敏感的而不是重新提取或重新计算它，您可以一次提取数据，然后将结果存储。</span><span class="sxs-lookup"><span data-stu-id="de90d-119">If your site gets repeated requests for the same information, and the information does not need to be modified for each person, and it's not time sensitive, instead of re-fetching or recalculating it, you can fetch the data once and then store the results.</span></span> <span data-ttu-id="de90d-120">下一次为此，传入某个请求的信息，您只会收到其从缓存。</span><span class="sxs-lookup"><span data-stu-id="de90d-120">The next time a request comes in for that information, you just get it out of the cache.</span></span>

<span data-ttu-id="de90d-121">一般情况下，你将缓存不会频繁更改的信息。</span><span class="sxs-lookup"><span data-stu-id="de90d-121">In general, you cache information that doesn't change frequently.</span></span> <span data-ttu-id="de90d-122">当将信息放在缓存中时，它存储在 web 服务器上的内存中。</span><span class="sxs-lookup"><span data-stu-id="de90d-122">When you put information in the cache, it's stored in memory on the web server.</span></span> <span data-ttu-id="de90d-123">您可以指定它应缓存多长，从秒到几天。</span><span class="sxs-lookup"><span data-stu-id="de90d-123">You can specify how long it should be cached, from seconds to days.</span></span> <span data-ttu-id="de90d-124">当缓存时间到期时，会自动从缓存删除信息。</span><span class="sxs-lookup"><span data-stu-id="de90d-124">When the caching period expires, the information is automatically removed from the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="de90d-125">缓存中的项可能会删除原因以外，它们已过期。</span><span class="sxs-lookup"><span data-stu-id="de90d-125">Entries in the cache might be removed for reasons other than that they've expired.</span></span> <span data-ttu-id="de90d-126">例如，web 服务器可能会暂时内存不足，并且它可以回收内存的一种方法是通过从缓存中引发的条目。</span><span class="sxs-lookup"><span data-stu-id="de90d-126">For example, the web server might temporarily run low on memory, and one way it can reclaim memory is by throwing entries out of the cache.</span></span> <span data-ttu-id="de90d-127">正如您将看到，即使已将信息放入缓存，您必须检查以确保它仍是在需要时。</span><span class="sxs-lookup"><span data-stu-id="de90d-127">As you'll see, even if you've put information into the cache, you have to check to be sure it's still there when you need it.</span></span>


<span data-ttu-id="de90d-128">假设网站有一个显示当前温度和天气预报页面。</span><span class="sxs-lookup"><span data-stu-id="de90d-128">Imagine your website has a page that displays the current temperature and weather forecast.</span></span> <span data-ttu-id="de90d-129">若要获取此类型的信息，可能会向外部服务发送请求。</span><span class="sxs-lookup"><span data-stu-id="de90d-129">To get this type of information, you might send a request to an external service.</span></span> <span data-ttu-id="de90d-130">因为此信息不会更改很多 （在两小时时间段，例如） 由于外部调用需要时间和带宽，那么是的良好候选项的缓存。</span><span class="sxs-lookup"><span data-stu-id="de90d-130">Since this information doesn't change much (within a two-hour time period, for example) and since external calls require time and bandwidth, it's a good candidate for caching.</span></span>

## <a name="adding-caching-to-a-page"></a><span data-ttu-id="de90d-131">添加到页面缓存</span><span class="sxs-lookup"><span data-stu-id="de90d-131">Adding Caching to a Page</span></span>

<span data-ttu-id="de90d-132">ASP.NET 包括`WebCache`帮助器，轻松地向站点添加缓存，并将数据添加到缓存。</span><span class="sxs-lookup"><span data-stu-id="de90d-132">ASP.NET includes a `WebCache` helper that makes it easy to add caching to your site and add data to the cache.</span></span> <span data-ttu-id="de90d-133">在此过程中，你将创建一个页面，缓存的当前时间。</span><span class="sxs-lookup"><span data-stu-id="de90d-133">In this procedure, you'll create a page that caches the current time.</span></span> <span data-ttu-id="de90d-134">这不是实际的示例中，由于当前时间是内容的情况下，会更改，而且并不复杂计算。</span><span class="sxs-lookup"><span data-stu-id="de90d-134">This isn't a real-world example, since the current time is something that does change often, and that moreover isn't complex to calculate.</span></span> <span data-ttu-id="de90d-135">但是，它是为了说明中的缓存的好方法。</span><span class="sxs-lookup"><span data-stu-id="de90d-135">However, it's a good way to illustrate caching in action.</span></span>

1. <span data-ttu-id="de90d-136">添加一个名为的新页*WebCache.cshtml*到网站。</span><span class="sxs-lookup"><span data-stu-id="de90d-136">Add a new page named *WebCache.cshtml* to the website.</span></span>
2. <span data-ttu-id="de90d-137">将以下代码和标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="de90d-137">Add the following code and markup to the page:</span></span>

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    <span data-ttu-id="de90d-138">当您缓存数据时，您将其放入缓存使用的名称这是唯一的网站。</span><span class="sxs-lookup"><span data-stu-id="de90d-138">When you cache data, you put it into the cache using a name this is unique across the website.</span></span> <span data-ttu-id="de90d-139">在这种情况下，将使用名为某个缓存项`CachedTime`。</span><span class="sxs-lookup"><span data-stu-id="de90d-139">In this case, you'll use a cache entry named `CachedTime`.</span></span> <span data-ttu-id="de90d-140">这是`cacheItemKey`代码示例中所示。</span><span class="sxs-lookup"><span data-stu-id="de90d-140">This is the `cacheItemKey` shown in the code example.</span></span>

    <span data-ttu-id="de90d-141">代码首先读取`CachedTime`缓存条目。</span><span class="sxs-lookup"><span data-stu-id="de90d-141">The code first reads the `CachedTime` cache entry.</span></span> <span data-ttu-id="de90d-142">如果 （即，如果缓存条目不为 null） 返回一个值，则代码只是将时间变量的值设置为缓存数据。</span><span class="sxs-lookup"><span data-stu-id="de90d-142">If a value is returned (that is, if the cache entry isn't null), the code just sets the value of the time variable to the cache data.</span></span>

    <span data-ttu-id="de90d-143">但是，如果不存在的缓存项 （即，它为 null），代码设置的时间值、 将其添加到缓存中，并设置为 1 分钟的到期值。</span><span class="sxs-lookup"><span data-stu-id="de90d-143">However, if the cache entry doesn't exist (that is, it's null), the code sets the time value, adds it to the cache, and sets an expiration value to one minute.</span></span> <span data-ttu-id="de90d-144">1 分钟之后，该缓存项将被放弃。</span><span class="sxs-lookup"><span data-stu-id="de90d-144">After one minute, the cache entry is discarded.</span></span> <span data-ttu-id="de90d-145">（在缓存中的项的默认过期值是 20 分钟。）该命令`WebCache.Set(cacheItemKey, time, 1, false)`演示如何将当前的时间值添加到缓存并设置为 1 分钟的到期日期。</span><span class="sxs-lookup"><span data-stu-id="de90d-145">(The default expiration value for an item in the cache is 20 minutes.) The command `WebCache.Set(cacheItemKey, time, 1, false)` shows how to add the current time value to the cache and set its expiration to 1 minute.</span></span> <span data-ttu-id="de90d-146">设置*slidingExpiration*参数`false`意味着每次请求时它不续订过期时间。</span><span class="sxs-lookup"><span data-stu-id="de90d-146">Setting the *slidingExpiration* parameter to `false` means the expiration time is not renewed each time it is requested.</span></span> <span data-ttu-id="de90d-147">完全在 1 分钟后它最初添加到缓存到期时间。</span><span class="sxs-lookup"><span data-stu-id="de90d-147">It will expire exactly 1 minute after it was originally added to the cache.</span></span> <span data-ttu-id="de90d-148">如果将此值设置为`true`1 分钟到期时间从缓存中请求的值每次重置。</span><span class="sxs-lookup"><span data-stu-id="de90d-148">If you set this value to `true` the 1 minute expiration time is reset each time the value is requested from the cache.</span></span>

    <span data-ttu-id="de90d-149">此代码说明了在缓存数据时应始终使用的模式。</span><span class="sxs-lookup"><span data-stu-id="de90d-149">This code illustrates the pattern you should always use when you cache data.</span></span> <span data-ttu-id="de90d-150">您从缓存中获取的内容之前，始终先检查是否`WebCache.Get`方法已返回 null。</span><span class="sxs-lookup"><span data-stu-id="de90d-150">Before you get something out of the cache, always check first whether the `WebCache.Get` method has returned null.</span></span> <span data-ttu-id="de90d-151">请记住该缓存项可能已过期，或可能被删除，出于其他某种原因，因此永远不会保证任何给定的项目存在于缓存中。</span><span class="sxs-lookup"><span data-stu-id="de90d-151">Remember that the cache entry might have expired or might have been removed for some other reason, so any given entry is never guaranteed to be in the cache.</span></span>
3. <span data-ttu-id="de90d-152">运行*WebCache.cshtml*在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="de90d-152">Run *WebCache.cshtml* in a browser.</span></span> <span data-ttu-id="de90d-153">(请确保的页中选择**文件**工作区之前运行它。)第一次请求页上，时间数据不在缓存中，和的代码具有要添加到缓存的时间值。</span><span class="sxs-lookup"><span data-stu-id="de90d-153">(Make sure the page is selected in the **Files** workspace before you run it.) The first time you request the page, the time data isn't in the cache, and the code has to add the time value to the cache.</span></span>

    ![缓存-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. <span data-ttu-id="de90d-155">刷新*WebCache.cshtml*在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="de90d-155">Refresh *WebCache.cshtml* in the browser.</span></span> <span data-ttu-id="de90d-156">这一次，时间数据是在缓存中。</span><span class="sxs-lookup"><span data-stu-id="de90d-156">This time, the time data is in the cache.</span></span> <span data-ttu-id="de90d-157">请注意，自上次查看页面以来尚未更改的时间。</span><span class="sxs-lookup"><span data-stu-id="de90d-157">Notice that the time hasn't changed since the last time you viewed the page.</span></span>

    ![缓存 2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. <span data-ttu-id="de90d-159">稍等片刻，在清空缓存，并刷新页。</span><span class="sxs-lookup"><span data-stu-id="de90d-159">Wait one minute for the cache to be emptied, and then refresh the page.</span></span> <span data-ttu-id="de90d-160">页面再次指示时间数据并不在缓存中，找到并更新的时间添加到缓存。</span><span class="sxs-lookup"><span data-stu-id="de90d-160">The page again indicates that the time data wasn't found in the cache, and the updated time is added to the cache.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="de90d-161">其他资源</span><span class="sxs-lookup"><span data-stu-id="de90d-161">Additional Resources</span></span>


- [<span data-ttu-id="de90d-162">在图表中显示数据</span><span class="sxs-lookup"><span data-stu-id="de90d-162">Displaying Data in a Chart</span></span>](https://go.microsoft.com/fwlink/?LinkId=202895)
- <span data-ttu-id="de90d-163">[WebCache API 参考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="de90d-163">[WebCache API reference](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span></span>
