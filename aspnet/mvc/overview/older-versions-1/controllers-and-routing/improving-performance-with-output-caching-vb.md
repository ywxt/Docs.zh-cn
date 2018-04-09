---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 使用提高性能输出缓存 (VB) |Microsoft 文档
author: microsoft
description: 在本教程中，你学习如何极大地提高你的 ASP.NET MVC web 应用程序的性能通过利用的输出缓存。 你...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ee933b477307f5c3f2377e112a1a98d3d6bc337
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="98a16-104">使用输出缓存 (VB) 提高性能</span><span class="sxs-lookup"><span data-stu-id="98a16-104">Improving Performance with Output Caching (VB)</span></span>
====================
<span data-ttu-id="98a16-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="98a16-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="98a16-106">在本教程中，你学习如何极大地提高你的 ASP.NET MVC web 应用程序的性能通过利用的输出缓存。</span><span class="sxs-lookup"><span data-stu-id="98a16-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="98a16-107">了解如何缓存，以便不需要创建新的用户调用该操作的每个时间相同的内容的控制器操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="98a16-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>


<span data-ttu-id="98a16-108">本教程旨在说明如何你可以显著地提高性能的 ASP.NET MVC 应用程序利用输出缓存。</span><span class="sxs-lookup"><span data-stu-id="98a16-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="98a16-109">输出缓存可用于缓存的控制器操作返回的内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="98a16-110">这样，相同的内容不需要生成每个调用的相同的控制器操作的时间。</span><span class="sxs-lookup"><span data-stu-id="98a16-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="98a16-111">例如，假设你的 ASP.NET MVC 应用程序名为索引视图中显示的数据库记录列表。</span><span class="sxs-lookup"><span data-stu-id="98a16-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="98a16-112">通常情况下，每个用户时，将调用返回的索引视图中，控制器操作的时间的数据库记录集必须是从数据库中检索通过执行数据库查询。</span><span class="sxs-lookup"><span data-stu-id="98a16-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="98a16-113">如果你充分利用输出缓存的手动，则可以避免执行数据库查询，每次任何用户调用相同的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="98a16-114">可从缓存而不是正在重新生成的控制器操作检索视图。</span><span class="sxs-lookup"><span data-stu-id="98a16-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="98a16-115">你可以避免执行冗余缓存启用适用于 server。</span><span class="sxs-lookup"><span data-stu-id="98a16-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="98a16-116">启用输出缓存</span><span class="sxs-lookup"><span data-stu-id="98a16-116">Enabling Output Caching</span></span>

<span data-ttu-id="98a16-117">启用输出缓存通过添加&lt;OutputCache&gt;属性设为的单个控制器操作或整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="98a16-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="98a16-118">例如，列表 1 中的控制器公开名为 index （） 的操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="98a16-119">Index （） 操作的输出被缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="98a16-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="98a16-120">**列表 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="98a16-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


<span data-ttu-id="98a16-121">在 Beta 版中的 ASP.NET MVC，输出缓存并不适用于的 URL，如[ http://www.MySite.com/ ](http://www.mysite.com/)。</span><span class="sxs-lookup"><span data-stu-id="98a16-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="98a16-122">相反，您必须输入的 URL，如[ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)。</span><span class="sxs-lookup"><span data-stu-id="98a16-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>


<span data-ttu-id="98a16-123">列出 1 中为 10 秒时，将缓存 index （） 操作的输出。</span><span class="sxs-lookup"><span data-stu-id="98a16-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="98a16-124">如果你愿意，你可以指定一个更长的时间的缓存持续时间。</span><span class="sxs-lookup"><span data-stu-id="98a16-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="98a16-125">例如，如果你想要缓存的输出为一天的控制器操作然后你可以指定缓存持续时间为 86400 秒 (60 秒\*60 分钟\*24 小时)。</span><span class="sxs-lookup"><span data-stu-id="98a16-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="98a16-126">没有该内容不能保证将缓存按你指定的时间量。</span><span class="sxs-lookup"><span data-stu-id="98a16-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="98a16-127">当内存资源变得低时，缓存将自动启动退出的内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="98a16-128">列表 1 中的主页控制器返回列出 2 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="98a16-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="98a16-129">无需进行任何特殊有关此视图。</span><span class="sxs-lookup"><span data-stu-id="98a16-129">There is nothing special about this view.</span></span> <span data-ttu-id="98a16-130">索引视图只显示的当前时间 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="98a16-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="98a16-131">**列出 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="98a16-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="98a16-132">**图 1 – 缓存索引视图**</span><span class="sxs-lookup"><span data-stu-id="98a16-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="98a16-134">如果多次通过在你的浏览器的地址栏中输入 URL /Home/索引调用 index （） 操作和重复达到你的浏览器中的刷新/重新加载按钮，然后通过索引视图显示的时间不会更改为 10 秒。</span><span class="sxs-lookup"><span data-stu-id="98a16-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="98a16-135">将显示在同一时间，因为视图缓存。</span><span class="sxs-lookup"><span data-stu-id="98a16-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="98a16-136">请务必了解为每个用户访问你的应用程序会缓存该视图的视图相同。</span><span class="sxs-lookup"><span data-stu-id="98a16-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="98a16-137">将调用该 index （） 操作的任何人将获得索引视图相同的缓存的的版本。</span><span class="sxs-lookup"><span data-stu-id="98a16-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="98a16-138">这意味着大幅减少的 web 服务器提供的索引视图时必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="98a16-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="98a16-139">列出 2 中的视图碰巧执行某些非常简单。</span><span class="sxs-lookup"><span data-stu-id="98a16-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="98a16-140">该视图仅显示当前时间。</span><span class="sxs-lookup"><span data-stu-id="98a16-140">The view just displays the current time.</span></span> <span data-ttu-id="98a16-141">但是，你可以就像轻松缓存此视图显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="98a16-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="98a16-142">在这种情况下，不需要的数据库记录集从数据库中每次调用返回的视图控制器操作检索。</span><span class="sxs-lookup"><span data-stu-id="98a16-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="98a16-143">Caching 可以降低你的 web 服务器和数据库服务器必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="98a16-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="98a16-144">不使用页&lt;%@ OutputCache %&gt;指令中的 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="98a16-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="98a16-145">此指令窜从 Web 窗体世界，并且不应使用 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="98a16-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="98a16-146">在其中缓存内容</span><span class="sxs-lookup"><span data-stu-id="98a16-146">Where Content is Cached</span></span>

<span data-ttu-id="98a16-147">默认情况下，当你使用&lt;OutputCache&gt;属性，内容缓存在三个位置： web 服务器、 任何代理服务器和 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="98a16-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="98a16-148">你可以控制完全其中缓存内容通过修改的 Location 属性&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="98a16-149">可以将位置属性设置为以下值之一：</span><span class="sxs-lookup"><span data-stu-id="98a16-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="98a16-150">·任何</span><span class="sxs-lookup"><span data-stu-id="98a16-150">· Any</span></span>
> 
> <span data-ttu-id="98a16-151">·客户端</span><span class="sxs-lookup"><span data-stu-id="98a16-151">· Client</span></span>
> 
> <span data-ttu-id="98a16-152">·下游</span><span class="sxs-lookup"><span data-stu-id="98a16-152">· Downstream</span></span>
> 
> <span data-ttu-id="98a16-153">·服务器</span><span class="sxs-lookup"><span data-stu-id="98a16-153">· Server</span></span>
> 
> <span data-ttu-id="98a16-154">·无</span><span class="sxs-lookup"><span data-stu-id="98a16-154">· None</span></span>
> 
> <span data-ttu-id="98a16-155">·ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="98a16-155">· ServerAndClient</span></span>


<span data-ttu-id="98a16-156">默认情况下，位置属性具有值任何。</span><span class="sxs-lookup"><span data-stu-id="98a16-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="98a16-157">但是，有一些你可能希望到仅在浏览器上或仅在服务器上缓存的情形。</span><span class="sxs-lookup"><span data-stu-id="98a16-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="98a16-158">例如，如果缓存个性化为每个用户的信息然后你不应缓存服务器上的信息。</span><span class="sxs-lookup"><span data-stu-id="98a16-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="98a16-159">如果您要为不同的用户显示不同的信息，你应该缓存仅在客户端上的信息。</span><span class="sxs-lookup"><span data-stu-id="98a16-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="98a16-160">例如，清单 3 中的控制器公开名为 GetName() 返回当前的用户名称的操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="98a16-161">如果上插座登录到网站并调用 GetName() 操作然后操作返回字符串"Hi 上插座"。</span><span class="sxs-lookup"><span data-stu-id="98a16-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="98a16-162">如果以后，Jill 登录到网站并将调用该 GetName() 操作然后她还将获取字符串"Hi 上插座"。</span><span class="sxs-lookup"><span data-stu-id="98a16-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="98a16-163">上插座最初将调用该控制器操作后，该字符串缓存所有用户在 web 服务器上。</span><span class="sxs-lookup"><span data-stu-id="98a16-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="98a16-164">**列出 3 – Controllers\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="98a16-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="98a16-165">最有可能，列出 3 中的控制器工作不希望的方式。</span><span class="sxs-lookup"><span data-stu-id="98a16-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="98a16-166">你不想要向 Jill 显示消息"Hi 上插座"。</span><span class="sxs-lookup"><span data-stu-id="98a16-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="98a16-167">你应该永远不会缓存服务器缓存中的个性化的内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="98a16-168">但是，你可能想要缓存在浏览器缓存以提高性能的个性化的内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="98a16-169">如果缓存在浏览器中的内容，并且用户调用相同的控制器操作多次，然后可以从浏览器缓存中而不是服务器检索内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="98a16-170">列出 4 中的已修改的控制器缓存 GetName() 操作的输出。</span><span class="sxs-lookup"><span data-stu-id="98a16-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="98a16-171">但是，该内容又缓存仅在浏览器和不在服务器上。</span><span class="sxs-lookup"><span data-stu-id="98a16-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="98a16-172">这样，多个用户调用 GetName() 方法时，每个人员获取其自己的用户名称和不能是其他用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="98a16-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="98a16-173">**列出 4 – Controllers\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="98a16-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="98a16-174">请注意， &lt;OutputCache&gt;列出 4 中的属性包括一个设置为值 OutputCacheLocation.Client 的位置属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="98a16-175">&lt;OutputCache&gt;属性还包括 NoStore 属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="98a16-176">NoStore 属性用来通知代理服务器和浏览器，它们不应存储缓存的内容的永久副本。</span><span class="sxs-lookup"><span data-stu-id="98a16-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="98a16-177">不同的输出缓存</span><span class="sxs-lookup"><span data-stu-id="98a16-177">Varying the Output Cache</span></span>

<span data-ttu-id="98a16-178">在某些情况下，你可能想非常相同的内容的不同缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="98a16-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="98a16-179">例如，假设你要创建主/详细信息页。</span><span class="sxs-lookup"><span data-stu-id="98a16-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="98a16-180">主控页显示电影的标题的列表。</span><span class="sxs-lookup"><span data-stu-id="98a16-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="98a16-181">当你单击标题时，为所选的电影获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="98a16-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="98a16-182">如果缓存的详细信息页，然后将哪些影片无论您单击显示同一电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="98a16-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="98a16-183">第一个影片第一个用户选择将向所有将来的用户显示。</span><span class="sxs-lookup"><span data-stu-id="98a16-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="98a16-184">您可以通过利用的 VaryByParam 属性修复此问题&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="98a16-185">此属性使您能够创建不同的缓存的版本非常相同的内容时窗体参数或查询字符串参数而异。</span><span class="sxs-lookup"><span data-stu-id="98a16-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="98a16-186">例如，在列出 5 控制器公开名为 Master() 和 Details() 的两个操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="98a16-187">Master() 操作返回电影的标题的列表以及 Details() 操作返回的所选的影片详细信息。</span><span class="sxs-lookup"><span data-stu-id="98a16-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="98a16-188">**列出 5 – Controllers\MoviesController.vb**</span><span class="sxs-lookup"><span data-stu-id="98a16-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="98a16-189">Master() 操作包括 VaryByParam 属性的值"none"。</span><span class="sxs-lookup"><span data-stu-id="98a16-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="98a16-190">当调用操作，Master() 相同的缓存版本的主查看，则返回。</span><span class="sxs-lookup"><span data-stu-id="98a16-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="98a16-191">参数是任何形式的参数或查询字符串忽略 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="98a16-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="98a16-192">**图 2 – /Movies/Master 视图**</span><span class="sxs-lookup"><span data-stu-id="98a16-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="98a16-194">**图 3-/ 电影/详细信息视图**</span><span class="sxs-lookup"><span data-stu-id="98a16-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="98a16-196">Details() 操作包括具有"Id"的值的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="98a16-197">当不同的 Id 参数的值传递给控制器操作时，会生成不同的缓存的版本的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="98a16-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="98a16-198">它是一定要了解使用 VaryByParam 属性结果在多个缓存中，且不小于。</span><span class="sxs-lookup"><span data-stu-id="98a16-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="98a16-199">每个不同版本的 Id 参数创建的详细信息视图的不同缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="98a16-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="98a16-200">你可以将 VaryByParam 属性设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="98a16-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="98a16-201">\* = 如果窗体或查询字符串参数变化，可以创建不同的缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="98a16-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="98a16-202">none = Never 创建不同的缓存的版本</span><span class="sxs-lookup"><span data-stu-id="98a16-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="98a16-203">以分号的参数列表 = 创建不同的缓存的版本，当任何列表中的窗体或查询字符串参数变化时</span><span class="sxs-lookup"><span data-stu-id="98a16-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>


#### <a name="creating-a-cache-profile"></a><span data-ttu-id="98a16-204">创建缓存配置文件</span><span class="sxs-lookup"><span data-stu-id="98a16-204">Creating a Cache Profile</span></span>

<span data-ttu-id="98a16-205">作为配置输出缓存属性的修改的属性的替代方法&lt;OutputCache&gt;特性，你可以在 web 配置 (web.config) 文件中创建的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="98a16-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="98a16-206">在 web 配置文件中创建的缓存配置文件提供了几个重要优势。</span><span class="sxs-lookup"><span data-stu-id="98a16-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="98a16-207">首先，通过配置输出缓存中的 web 配置文件，可以控制如何控制器操作缓存在一个中心位置的内容。</span><span class="sxs-lookup"><span data-stu-id="98a16-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="98a16-208">你可以创建一个缓存配置文件，并将配置文件应用到多个控制器或控制器操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="98a16-209">其次，你可以修改 web 配置文件无需重新编译你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="98a16-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="98a16-210">如果你需要禁用缓存的应用程序已部署到生产，则可以只需修改 web 配置文件中定义的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="98a16-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="98a16-211">将自动检测并应用到的 web 配置文件的任何更改。</span><span class="sxs-lookup"><span data-stu-id="98a16-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="98a16-212">例如，&lt;缓存&gt;列表 6 中的 web 配置节定义名为 Cache1Hour 缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="98a16-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="98a16-213">&lt;缓存&gt;部分必须出现在&lt;system.web&gt; web 配置文件节。</span><span class="sxs-lookup"><span data-stu-id="98a16-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="98a16-214">**列出 6 – web.config 的 Caching 部分**</span><span class="sxs-lookup"><span data-stu-id="98a16-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="98a16-215">列出 7 中的控制器演示了如何将 Cache1Hour 配置文件应用到的控制器操作具有&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="98a16-216">**Listing 7 – Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="98a16-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="98a16-217">如果调用公开的列出 7 中的控制器的 index （） 操作则将以 1 小时为单位返回相同的时间。</span><span class="sxs-lookup"><span data-stu-id="98a16-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="98a16-218">总结</span><span class="sxs-lookup"><span data-stu-id="98a16-218">Summary</span></span>

<span data-ttu-id="98a16-219">输出缓存提供与极大地提高你的 ASP.NET MVC 应用程序的性能的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="98a16-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="98a16-220">在本教程中，您学习了如何使用&lt;OutputCache&gt;特性来缓存输出的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="98a16-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="98a16-221">你还了解了如何修改属性&lt;OutputCache&gt;如要修改如何获取缓存内容的持续时间和 VaryByParam 属性的属性。</span><span class="sxs-lookup"><span data-stu-id="98a16-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="98a16-222">最后，您学习了如何在 web 配置文件中定义缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="98a16-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98a16-223">[上一页](understanding-action-filters-vb.md)
> [下一页](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="98a16-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
