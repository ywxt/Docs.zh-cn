---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: "在 ASP.NET Web 中缓存数据页 (Razor) 站点的更好的性能 |Microsoft 文档"
author: tfitzmac
description: "你可以提高网站的速度进行存储的即缓存-通常会需要很长时间来检索或处理的数据的结果..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2014
ms.topic: article
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 742409219bd3b05f8ddf2c0d5034919fc9bf1d26
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a><span data-ttu-id="c8e19-103">缓存 ASP.NET Web 页 (Razor) 站点中的数据以便更好的性能</span><span class="sxs-lookup"><span data-stu-id="c8e19-103">Caching Data in an ASP.NET Web Pages (Razor) Site for Better Performance</span></span>
====================
<span data-ttu-id="c8e19-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c8e19-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c8e19-105">此文章介绍了如何为更快的性能，在 ASP.NET Web 页 (Razor) 网站中使用的缓存信息的帮助。</span><span class="sxs-lookup"><span data-stu-id="c8e19-105">This article explains how to use a helper to cache information for faster performance in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="c8e19-106">可以通过应用商店和 #8212; 让它来加快你的网站也就是说，缓存和 #8212;通常将需要相当长的时间来检索或处理和，通常不会更改的数据结果。</span><span class="sxs-lookup"><span data-stu-id="c8e19-106">You can speed up your website by having it store &#8212; that is, cache &#8212; the results of data that ordinarily would take considerable time to retrieve or process and that does not change often.</span></span>
> 
> <span data-ttu-id="c8e19-107">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="c8e19-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="c8e19-108">如何使用缓存来改进你的网站的响应能力。</span><span class="sxs-lookup"><span data-stu-id="c8e19-108">How to use caching to improve the responsiveness of your website.</span></span>
> 
> <span data-ttu-id="c8e19-109">这些是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="c8e19-109">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="c8e19-110">`WebCache`帮助器。</span><span class="sxs-lookup"><span data-stu-id="c8e19-110">The `WebCache` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c8e19-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="c8e19-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c8e19-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="c8e19-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="c8e19-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="c8e19-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="c8e19-114">每次有人请求页从您的网站时，web 服务器必须执行某项操作以便满足请求。</span><span class="sxs-lookup"><span data-stu-id="c8e19-114">Every time someone requests a page from your site, the web server has to do some work in order to fulfill the request.</span></span> <span data-ttu-id="c8e19-115">对于某些页面中，服务器可能需要执行需要 （相对较） 长时间，例如从数据库检索数据的任务。</span><span class="sxs-lookup"><span data-stu-id="c8e19-115">For some of your pages, the server might have to perform tasks that take a (comparatively) long time, such as retrieving data from a database.</span></span> <span data-ttu-id="c8e19-116">即使这些任务会长时间采用绝对字词，如果您的网站遇到大量流量，导致对 web 服务器来执行复杂的或速度缓慢任务的各个请求的完整的一系列可针对大量工作。</span><span class="sxs-lookup"><span data-stu-id="c8e19-116">Even if these tasks don't take long in absolute terms, if your site experiences a lot of traffic, a whole series of individual requests that cause the web server to perform the complicated or slow task can add up to a lot of work.</span></span> <span data-ttu-id="c8e19-117">最终，这可能会影响站点的性能。</span><span class="sxs-lookup"><span data-stu-id="c8e19-117">This can ultimately affect the performance of the site.</span></span>

<span data-ttu-id="c8e19-118">提高你在如下情况下的性能的一种方法是网站的缓存数据。</span><span class="sxs-lookup"><span data-stu-id="c8e19-118">One way to improve the performance of your website in circumstances like this is to cache data.</span></span> <span data-ttu-id="c8e19-119">如果你的站点获取重复的请求相同的信息，和信息不需要修改的每个人，并且它不是时间敏感的而不是重新提取或重新计算它，你可以一次提取数据，然后存储结果。</span><span class="sxs-lookup"><span data-stu-id="c8e19-119">If your site gets repeated requests for the same information, and the information does not need to be modified for each person, and it's not time sensitive, instead of re-fetching or recalculating it, you can fetch the data once and then store the results.</span></span> <span data-ttu-id="c8e19-120">下一次请求传入该信息，您只会收到其缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-120">The next time a request comes in for that information, you just get it out of the cache.</span></span>

<span data-ttu-id="c8e19-121">一般情况下，你的缓存不经常更改的信息。</span><span class="sxs-lookup"><span data-stu-id="c8e19-121">In general, you cache information that doesn't change frequently.</span></span> <span data-ttu-id="c8e19-122">当你将信息放在缓存中时，它存储在 web 服务器上的内存中。</span><span class="sxs-lookup"><span data-stu-id="c8e19-122">When you put information in the cache, it's stored in memory on the web server.</span></span> <span data-ttu-id="c8e19-123">你可以指定多长时间它应缓存，从几秒到天。</span><span class="sxs-lookup"><span data-stu-id="c8e19-123">You can specify how long it should be cached, from seconds to days.</span></span> <span data-ttu-id="c8e19-124">当缓存期到期时，信息是自动从缓存中删除。</span><span class="sxs-lookup"><span data-stu-id="c8e19-124">When the caching period expires, the information is automatically removed from the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e19-125">缓存中的条目可能会删除原因以外，它们已过期。</span><span class="sxs-lookup"><span data-stu-id="c8e19-125">Entries in the cache might be removed for reasons other than that they've expired.</span></span> <span data-ttu-id="c8e19-126">例如，web 服务器可能会暂时运行低内存，并且它可以回收的内存的一种方法是通过引发缓存条目。</span><span class="sxs-lookup"><span data-stu-id="c8e19-126">For example, the web server might temporarily run low on memory, and one way it can reclaim memory is by throwing entries out of the cache.</span></span> <span data-ttu-id="c8e19-127">正如你将看到的即使已将信息放入缓存，你必须以确保它仍存在时检查你需要它。</span><span class="sxs-lookup"><span data-stu-id="c8e19-127">As you'll see, even if you've put information into the cache, you have to check to be sure it's still there when you need it.</span></span>


<span data-ttu-id="c8e19-128">假设您的网站已显示的当前温度和天气预报的页面。</span><span class="sxs-lookup"><span data-stu-id="c8e19-128">Imagine your website has a page that displays the current temperature and weather forecast.</span></span> <span data-ttu-id="c8e19-129">若要获取此类型的信息，可能会将请求发送到外部服务中。</span><span class="sxs-lookup"><span data-stu-id="c8e19-129">To get this type of information, you might send a request to an external service.</span></span> <span data-ttu-id="c8e19-130">由于此信息不会更改 （在两小时时间段，例如） 的很多，因为外部调用需要时间和带宽，很好的候选用于缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-130">Since this information doesn't change much (within a two-hour time period, for example) and since external calls require time and bandwidth, it's a good candidate for caching.</span></span>

## <a name="adding-caching-to-a-page"></a><span data-ttu-id="c8e19-131">添加到页缓存</span><span class="sxs-lookup"><span data-stu-id="c8e19-131">Adding Caching to a Page</span></span>

<span data-ttu-id="c8e19-132">ASP.NET 包括`WebCache`帮助程序可以轻松地向网站添加缓存并将数据添加到缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-132">ASP.NET includes a `WebCache` helper that makes it easy to add caching to your site and add data to the cache.</span></span> <span data-ttu-id="c8e19-133">在此过程中，你将创建缓存的当前时间的页。</span><span class="sxs-lookup"><span data-stu-id="c8e19-133">In this procedure, you'll create a page that caches the current time.</span></span> <span data-ttu-id="c8e19-134">这不是现实世界的示例中，由于当前时间，通常情况下，会更改并此外不是计算复杂。</span><span class="sxs-lookup"><span data-stu-id="c8e19-134">This isn't a real-world example, since the current time is something that does change often, and that moreover isn't complex to calculate.</span></span> <span data-ttu-id="c8e19-135">但是，它是一种好方法，用于说明中操作的缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-135">However, it's a good way to illustrate caching in action.</span></span>

1. <span data-ttu-id="c8e19-136">添加一个名为的新页*WebCache.cshtml*到网站。</span><span class="sxs-lookup"><span data-stu-id="c8e19-136">Add a new page named *WebCache.cshtml* to the website.</span></span>
2. <span data-ttu-id="c8e19-137">将下面的代码和标记添加到页中：</span><span class="sxs-lookup"><span data-stu-id="c8e19-137">Add the following code and markup to the page:</span></span>

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    <span data-ttu-id="c8e19-138">当缓存数据时，你将其放入缓存使用名称这是唯一的网站。</span><span class="sxs-lookup"><span data-stu-id="c8e19-138">When you cache data, you put it into the cache using a name this is unique across the website.</span></span> <span data-ttu-id="c8e19-139">在这种情况下，你将使用名为某个缓存项`CachedTime`。</span><span class="sxs-lookup"><span data-stu-id="c8e19-139">In this case, you'll use a cache entry named `CachedTime`.</span></span> <span data-ttu-id="c8e19-140">这是`cacheItemKey`代码示例中所示。</span><span class="sxs-lookup"><span data-stu-id="c8e19-140">This is the `cacheItemKey` shown in the code example.</span></span>

    <span data-ttu-id="c8e19-141">该代码第一次读取`CachedTime`缓存条目。</span><span class="sxs-lookup"><span data-stu-id="c8e19-141">The code first reads the `CachedTime` cache entry.</span></span> <span data-ttu-id="c8e19-142">如果 （即，如果缓存条目不为 null），则返回值，则代码只需将时间变量的值设置为缓存数据。</span><span class="sxs-lookup"><span data-stu-id="c8e19-142">If a value is returned (that is, if the cache entry isn't null), the code just sets the value of the time variable to the cache data.</span></span>

    <span data-ttu-id="c8e19-143">但是，如果该缓存条目不存在 （即，它为 null），代码会设置的时间值，将其添加到缓存中，并将过期记录的值设置为一分钟。</span><span class="sxs-lookup"><span data-stu-id="c8e19-143">However, if the cache entry doesn't exist (that is, it's null), the code sets the time value, adds it to the cache, and sets an expiration value to one minute.</span></span> <span data-ttu-id="c8e19-144">在一分钟后该缓存条目将被丢弃。</span><span class="sxs-lookup"><span data-stu-id="c8e19-144">After one minute, the cache entry is discarded.</span></span> <span data-ttu-id="c8e19-145">（缓存中的项的默认过期值为 20 分钟。）该命令`WebCache.Set(cacheItemKey, time, 1, false)`演示如何向缓存添加当前的时间值并将其过期设置为 1 分钟。</span><span class="sxs-lookup"><span data-stu-id="c8e19-145">(The default expiration value for an item in the cache is 20 minutes.) The command `WebCache.Set(cacheItemKey, time, 1, false)` shows how to add the current time value to the cache and set its expiration to 1 minute.</span></span> <span data-ttu-id="c8e19-146">设置*slidingExpiration*参数`false`意味着的到期时间不续订它请求每次。</span><span class="sxs-lookup"><span data-stu-id="c8e19-146">Setting the *slidingExpiration* parameter to `false` means the expiration time is not renewed each time it is requested.</span></span> <span data-ttu-id="c8e19-147">将过期完全 1 分钟之后它最初添加到缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-147">It will expire exactly 1 minute after it was originally added to the cache.</span></span> <span data-ttu-id="c8e19-148">如果将此值设置为`true`1 分钟到期时间从缓存请求值每次重置。</span><span class="sxs-lookup"><span data-stu-id="c8e19-148">If you set this value to `true` the 1 minute expiration time is reset each time the value is requested from the cache.</span></span>

    <span data-ttu-id="c8e19-149">此代码演示在缓存数据时应始终使用的模式。</span><span class="sxs-lookup"><span data-stu-id="c8e19-149">This code illustrates the pattern you should always use when you cache data.</span></span> <span data-ttu-id="c8e19-150">您将得到缓存之前，始终首先检查是否`WebCache.Get`方法已返回 null。</span><span class="sxs-lookup"><span data-stu-id="c8e19-150">Before you get something out of the cache, always check first whether the `WebCache.Get` method has returned null.</span></span> <span data-ttu-id="c8e19-151">请记住的缓存项可能已到期或可能被删除，由于某种其他原因，因此永远不会保证任何给定的项目是在缓存中。</span><span class="sxs-lookup"><span data-stu-id="c8e19-151">Remember that the cache entry might have expired or might have been removed for some other reason, so any given entry is never guaranteed to be in the cache.</span></span>
3. <span data-ttu-id="c8e19-152">运行*WebCache.cshtml*在浏览器。</span><span class="sxs-lookup"><span data-stu-id="c8e19-152">Run *WebCache.cshtml* in a browser.</span></span> <span data-ttu-id="c8e19-153">(请确保页中选择**文件**工作区之前运行它。)第一次请求页上，时间数据不在缓存中，并且代码具有要添加到缓存的时间值。</span><span class="sxs-lookup"><span data-stu-id="c8e19-153">(Make sure the page is selected in the **Files** workspace before you run it.) The first time you request the page, the time data isn't in the cache, and the code has to add the time value to the cache.</span></span>

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. <span data-ttu-id="c8e19-155">刷新*WebCache.cshtml*浏览器中。</span><span class="sxs-lookup"><span data-stu-id="c8e19-155">Refresh *WebCache.cshtml* in the browser.</span></span> <span data-ttu-id="c8e19-156">这一次，时间数据是在缓存中。</span><span class="sxs-lookup"><span data-stu-id="c8e19-156">This time, the time data is in the cache.</span></span> <span data-ttu-id="c8e19-157">请注意自上次查看页面以来未更改的时间。</span><span class="sxs-lookup"><span data-stu-id="c8e19-157">Notice that the time hasn't changed since the last time you viewed the page.</span></span>

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. <span data-ttu-id="c8e19-159">等待在清空缓存一分钟，然后刷新页面。</span><span class="sxs-lookup"><span data-stu-id="c8e19-159">Wait one minute for the cache to be emptied, and then refresh the page.</span></span> <span data-ttu-id="c8e19-160">页再次指示在缓存中，时间数据找不到和更新的时间被添加到缓存。</span><span class="sxs-lookup"><span data-stu-id="c8e19-160">The page again indicates that the time data wasn't found in the cache, and the updated time is added to the cache.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c8e19-161">其他资源</span><span class="sxs-lookup"><span data-stu-id="c8e19-161">Additional Resources</span></span>


- [<span data-ttu-id="c8e19-162">在图表中显示数据</span><span class="sxs-lookup"><span data-stu-id="c8e19-162">Displaying Data in a Chart</span></span>](https://go.microsoft.com/fwlink/?LinkId=202895)
- <span data-ttu-id="c8e19-163">[WebCache API 参考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="c8e19-163">[WebCache API reference](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span></span>
