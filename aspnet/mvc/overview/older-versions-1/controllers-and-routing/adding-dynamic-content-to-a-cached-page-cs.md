---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 将动态内容添加到缓存的页面 (C#) |Microsoft Docs
author: microsoft
description: 了解如何混合在同一页中的动态和缓存内容。 缓存后替换使您能够显示动态内容，例如横幅广告 o...
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 5c6d5a223a465a00a08f58a188a16cbf3c310431
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805576"
---
<a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="c7a39-104">将动态内容添加到缓存的页面 (C#)</span><span class="sxs-lookup"><span data-stu-id="c7a39-104">Adding Dynamic Content to a Cached Page (C#)</span></span>
====================
<span data-ttu-id="c7a39-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c7a39-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c7a39-106">了解如何混合在同一页中的动态和缓存内容。</span><span class="sxs-lookup"><span data-stu-id="c7a39-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="c7a39-107">缓存后替换，可显示动态内容，例如横幅广告或中缓存已输出的页的新闻项。</span><span class="sxs-lookup"><span data-stu-id="c7a39-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>


<span data-ttu-id="c7a39-108">通过利用输出缓存，可以极大地提高 ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="c7a39-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="c7a39-109">而不是重新生成页面每次请求页面时，可以生成一次并在多个用户的内存中缓存的页面。</span><span class="sxs-lookup"><span data-stu-id="c7a39-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="c7a39-110">但存在一个问题。</span><span class="sxs-lookup"><span data-stu-id="c7a39-110">But there is a problem.</span></span> <span data-ttu-id="c7a39-111">如果你需要在页中显示动态内容？</span><span class="sxs-lookup"><span data-stu-id="c7a39-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="c7a39-112">例如，假设你想要在页中显示横幅广告。</span><span class="sxs-lookup"><span data-stu-id="c7a39-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="c7a39-113">您不希望被缓存，以便每个用户将看到完全相同的播发，横幅广告。</span><span class="sxs-lookup"><span data-stu-id="c7a39-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="c7a39-114">通过这种方式不会进行任何费用 ！</span><span class="sxs-lookup"><span data-stu-id="c7a39-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="c7a39-115">幸运的是，没有简单的解决方案。</span><span class="sxs-lookup"><span data-stu-id="c7a39-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="c7a39-116">您可以充分利用 ASP.NET 框架调用的一项功能*缓存后替换*。</span><span class="sxs-lookup"><span data-stu-id="c7a39-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="c7a39-117">缓存后替换可以替换已缓存在内存中的页中的动态内容。</span><span class="sxs-lookup"><span data-stu-id="c7a39-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>


<span data-ttu-id="c7a39-118">通常情况下，当缓存页面输出使用 [OutputCache] 属性时，进行了缓存服务器和客户端 （web 浏览器） 上。</span><span class="sxs-lookup"><span data-stu-id="c7a39-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="c7a39-119">当使用缓存后替换时，仅在服务器上缓存页。</span><span class="sxs-lookup"><span data-stu-id="c7a39-119">When you use post-cache substitution, a page is cached only on the server.</span></span>


#### <a name="using-post-cache-substitution"></a><span data-ttu-id="c7a39-120">使用缓存后替换</span><span class="sxs-lookup"><span data-stu-id="c7a39-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="c7a39-121">使用缓存后替换需要两个步骤。</span><span class="sxs-lookup"><span data-stu-id="c7a39-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="c7a39-122">首先，需要定义返回一个字符串，表示你想要在缓存的页面中显示的动态内容的方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="c7a39-123">接下来，您调用 HttpResponse.WriteSubstitution() 方法来将动态内容注入到页面。</span><span class="sxs-lookup"><span data-stu-id="c7a39-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="c7a39-124">例如，假设你想要在缓存上随机显示不同的新闻项。</span><span class="sxs-lookup"><span data-stu-id="c7a39-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="c7a39-125">在列表 1 中的类公开了一个方法，名为 RenderNews() 随机从列表中的三个新闻项返回一个新闻项。</span><span class="sxs-lookup"><span data-stu-id="c7a39-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="c7a39-126">**代码清单 1 – Models\News.cs**</span><span class="sxs-lookup"><span data-stu-id="c7a39-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="c7a39-127">若要充分利用缓存后替换，则调用 HttpResponse.WriteSubstitution() 方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="c7a39-128">WriteSubstitution() 方法设置代码，以替换动态内容的缓存的页面区域。</span><span class="sxs-lookup"><span data-stu-id="c7a39-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="c7a39-129">WriteSubstitution() 方法用于在代码清单 2 中的视图中显示的随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="c7a39-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="c7a39-130">**代码清单 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="c7a39-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="c7a39-131">RenderNews 方法传递给 WriteSubstitution() 方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="c7a39-132">请注意，不会调用 RenderNews 方法 （有没有括号）。</span><span class="sxs-lookup"><span data-stu-id="c7a39-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="c7a39-133">而是对方法的引用被传递给 WriteSubstitution()。</span><span class="sxs-lookup"><span data-stu-id="c7a39-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="c7a39-134">缓存索引视图。</span><span class="sxs-lookup"><span data-stu-id="c7a39-134">The Index view is cached.</span></span> <span data-ttu-id="c7a39-135">该视图返回的清单 3 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="c7a39-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="c7a39-136">请注意，使用会导致要缓存 60 秒的索引视图 [OutputCache] 属性修饰的 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="c7a39-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="c7a39-137">**代码清单 3 – Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="c7a39-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="c7a39-138">即使缓存索引视图，在请求索引页时显示不同的随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="c7a39-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="c7a39-139">当请求索引页时，页所显示的时间将不会更改为 60 秒 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="c7a39-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="c7a39-140">时间不会更改这一事实证明对页进行缓存。</span><span class="sxs-lookup"><span data-stu-id="c7a39-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="c7a39-141">但是，内容注入 WriteSubstitution() 方法-随机新闻项目-更改每个请求。</span><span class="sxs-lookup"><span data-stu-id="c7a39-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="c7a39-142">**图 1 – 将注入中缓存的页面的动态新闻项**</span><span class="sxs-lookup"><span data-stu-id="c7a39-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="c7a39-144">在帮助器方法中使用缓存后替换</span><span class="sxs-lookup"><span data-stu-id="c7a39-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="c7a39-145">充分利用缓存后替换的更简单方法是封装对自定义帮助程序方法内 WriteSubstitution() 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="c7a39-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="c7a39-146">列表 4 中的帮助器方法进行了说明这种方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="c7a39-147">**列表 4 – AdHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="c7a39-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="c7a39-148">列表 4 包含公开两个方法的静态类： RenderBanner() 和 RenderBannerInternal()。</span><span class="sxs-lookup"><span data-stu-id="c7a39-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="c7a39-149">RenderBanner() 方法表示实际的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="c7a39-150">此方法，以便你可以在一个视图，就像任何其他帮助器方法中调用 Html.RenderBanner() 扩展标准的 ASP.NET MVC HtmlHelper 类。</span><span class="sxs-lookup"><span data-stu-id="c7a39-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="c7a39-151">RenderBanner() 方法调用将 RenderBannerInternal() 方法传递给 WriteSubsitution() 方法 HttpResponse.WriteSubstitution() 方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubsitution() method.</span></span>

<span data-ttu-id="c7a39-152">RenderBannerInternal() 方法为私有方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="c7a39-153">此方法不会公开为一个帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="c7a39-154">RenderBannerInternal() 方法随机从列表中的三个横幅广告图像返回一个横幅广告图像。</span><span class="sxs-lookup"><span data-stu-id="c7a39-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="c7a39-155">列表 5 中经过修改的索引视图说明了如何使用 RenderBanner() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="c7a39-156">请注意，额外&lt;%@ 导入 %&gt;指令，则包含要导入 MvcApplication1.Helpers 命名空间的视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="c7a39-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="c7a39-157">如果忘记导入此命名空间，则 RenderBanner() 方法不会显示为 Html 属性上的方法。</span><span class="sxs-lookup"><span data-stu-id="c7a39-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="c7a39-158">**列表 5 – Views\Home\Index.aspx （与 RenderBanner() 方法）**</span><span class="sxs-lookup"><span data-stu-id="c7a39-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="c7a39-159">不同横幅广告时请求由列表 5 中查看呈现的页，将显示的每个请求 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="c7a39-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="c7a39-160">对页进行缓存，但由 RenderBanner() 帮助器方法动态注入横幅广告。</span><span class="sxs-lookup"><span data-stu-id="c7a39-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="c7a39-161">**图 2 – 索引视图显示随机横幅广告**</span><span class="sxs-lookup"><span data-stu-id="c7a39-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="c7a39-163">总结</span><span class="sxs-lookup"><span data-stu-id="c7a39-163">Summary</span></span>

<span data-ttu-id="c7a39-164">本教程介绍了如何动态更新缓存的页面中的内容。</span><span class="sxs-lookup"><span data-stu-id="c7a39-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="c7a39-165">您学习了如何使用 HttpResponse.WriteSubstitution() 方法以启用要注入到缓存的页面中的动态内容。</span><span class="sxs-lookup"><span data-stu-id="c7a39-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="c7a39-166">您还学习了如何封装对 HTML 帮助器方法内 WriteSubstitution() 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="c7a39-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="c7a39-167">利用缓存应尽可能 – 它会对 web 应用程序的性能产生重大影响。</span><span class="sxs-lookup"><span data-stu-id="c7a39-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="c7a39-168">在本教程中所述，您可以充分利用缓存甚至当您需要在页面中显示动态内容时。</span><span class="sxs-lookup"><span data-stu-id="c7a39-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

## 

## 

> [!div class="step-by-step"]
> <span data-ttu-id="c7a39-169">[上一页](improving-performance-with-output-caching-cs.md)
> [下一页](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c7a39-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
