---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 提高性能与输出缓存 (VB) |Microsoft Docs
author: microsoft
description: 在本教程中，您学习如何你可以显著提升性能的 ASP.NET MVC web 应用程序通过利用的输出缓存。 您...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 9402d7e053ef11eeefa92d112b05ec255d5ec6f7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832263"
---
<a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="17a61-104">使用输出缓存 (VB) 提高性能</span><span class="sxs-lookup"><span data-stu-id="17a61-104">Improving Performance with Output Caching (VB)</span></span>
====================
<span data-ttu-id="17a61-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="17a61-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="17a61-106">在本教程中，您学习如何你可以显著提升性能的 ASP.NET MVC web 应用程序通过利用的输出缓存。</span><span class="sxs-lookup"><span data-stu-id="17a61-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="17a61-107">了解如何缓存，以便相同的内容不需要创建新用户调用该操作的每个时间的控制器操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="17a61-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>


<span data-ttu-id="17a61-108">本教程的目的是说明如何可以极大地改善性能 ASP.NET MVC 应用程序通过利用输出缓存。</span><span class="sxs-lookup"><span data-stu-id="17a61-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="17a61-109">输出缓存可以缓存由控制器操作返回的内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="17a61-110">这样一来，相同的内容不需要为其生成每个调用相同的控制器操作的时间。</span><span class="sxs-lookup"><span data-stu-id="17a61-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="17a61-111">例如，假设您的 ASP.NET MVC 应用程序在名为索引视图中显示的数据库记录列表。</span><span class="sxs-lookup"><span data-stu-id="17a61-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="17a61-112">通常情况下，每个用户调用返回索引视图的控制器操作的时间的数据库记录集必须是从数据库中检索通过执行数据库查询。</span><span class="sxs-lookup"><span data-stu-id="17a61-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="17a61-113">如果您手动，充分利用输出缓存则可以避免每次任何用户调用相同的控制器操作时执行数据库查询。</span><span class="sxs-lookup"><span data-stu-id="17a61-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="17a61-114">该视图可以检索从而不是从控制器操作正在重新生成缓存。</span><span class="sxs-lookup"><span data-stu-id="17a61-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="17a61-115">你可以避免执行冗余缓存启用在服务器上工作。</span><span class="sxs-lookup"><span data-stu-id="17a61-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="17a61-116">启用输出缓存</span><span class="sxs-lookup"><span data-stu-id="17a61-116">Enabling Output Caching</span></span>

<span data-ttu-id="17a61-117">启用输出缓存通过添加&lt;OutputCache&gt;属性为单独的控制器操作或整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="17a61-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="17a61-118">例如，在列表 1 中的控制器将公开名为 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="17a61-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="17a61-119">Index （） 操作的输出缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="17a61-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="17a61-120">**代码清单 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="17a61-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


<span data-ttu-id="17a61-121">在 ASP.NET MVC 的 Beta 版本中，输出缓存不适合的 URL，如[ http://www.MySite.com/ ](http://www.mysite.com/)。</span><span class="sxs-lookup"><span data-stu-id="17a61-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="17a61-122">相反，您必须输入的 URL，如[ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)。</span><span class="sxs-lookup"><span data-stu-id="17a61-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>


<span data-ttu-id="17a61-123">在列表 1 中，index （） 操作的输出缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="17a61-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="17a61-124">如果您愿意，可以指定更长的时间的缓存持续时间。</span><span class="sxs-lookup"><span data-stu-id="17a61-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="17a61-125">例如，如果你想要缓存的一天的控制器操作输出则可以指定缓存持续时间为 86400 秒 (60 秒\*60 分钟\*24 小时)。</span><span class="sxs-lookup"><span data-stu-id="17a61-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="17a61-126">没有内容不能保证将你指定的时间量内缓存。</span><span class="sxs-lookup"><span data-stu-id="17a61-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="17a61-127">当内存资源变得较低时，缓存会自动启动正在收回的内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="17a61-128">列表 1 中的主页控制器返回代码清单 2 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="17a61-129">并没有什么特别有关此视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-129">There is nothing special about this view.</span></span> <span data-ttu-id="17a61-130">索引视图仅显示当前时间 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="17a61-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="17a61-131">**代码清单 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="17a61-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="17a61-132">**图 1 – 缓存索引视图**</span><span class="sxs-lookup"><span data-stu-id="17a61-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="17a61-134">如果通过在你的浏览器的地址栏中输入 URL /Home/索引调用 index （） 操作多个时间和重复达到你的浏览器中的刷新/重新加载按钮，然后显示索引视图的时间不会更改为 10 秒。</span><span class="sxs-lookup"><span data-stu-id="17a61-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="17a61-135">显示在同一时间，因为缓存视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="17a61-136">请务必了解，为每个用户访问你的应用程序缓存相同的视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="17a61-137">调用 index （） 操作的任何人将获得相同的缓存的版本的索引视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="17a61-138">这意味着大幅减少 web 服务器提供的索引视图时必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="17a61-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="17a61-139">代码清单 2 中的视图发生要做的一些非常简单。</span><span class="sxs-lookup"><span data-stu-id="17a61-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="17a61-140">该视图只显示当前时间。</span><span class="sxs-lookup"><span data-stu-id="17a61-140">The view just displays the current time.</span></span> <span data-ttu-id="17a61-141">但是，你可以同样轻松地缓存一个视图，显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="17a61-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="17a61-142">在这种情况下，组数据库记录不需要每次调用返回的视图的控制器操作时从数据库检索。</span><span class="sxs-lookup"><span data-stu-id="17a61-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="17a61-143">缓存可以减少您的 web 服务器和数据库服务器必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="17a61-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="17a61-144">不使用的页面&lt;%@ OutputCache %&gt;指令在 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="17a61-145">此指令窜的 Web 窗体世界，并且不应使用 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="17a61-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="17a61-146">在其中缓存内容</span><span class="sxs-lookup"><span data-stu-id="17a61-146">Where Content is Cached</span></span>

<span data-ttu-id="17a61-147">默认情况下，当您使用&lt;OutputCache&gt;属性，内容缓存在三个位置中： web 服务器、 任何代理服务器和 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="17a61-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="17a61-148">您可以控制完全在其中缓存内容通过修改的 Location 属性&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="17a61-149">可以将位置属性设置为以下值之一：</span><span class="sxs-lookup"><span data-stu-id="17a61-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="17a61-150">·任何</span><span class="sxs-lookup"><span data-stu-id="17a61-150">· Any</span></span>
> 
> <span data-ttu-id="17a61-151">·客户端</span><span class="sxs-lookup"><span data-stu-id="17a61-151">· Client</span></span>
> 
> <span data-ttu-id="17a61-152">·下游</span><span class="sxs-lookup"><span data-stu-id="17a61-152">· Downstream</span></span>
> 
> <span data-ttu-id="17a61-153">·服务器</span><span class="sxs-lookup"><span data-stu-id="17a61-153">· Server</span></span>
> 
> <span data-ttu-id="17a61-154">·无</span><span class="sxs-lookup"><span data-stu-id="17a61-154">· None</span></span>
> 
> <span data-ttu-id="17a61-155">·ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="17a61-155">· ServerAndClient</span></span>


<span data-ttu-id="17a61-156">默认情况下，位置属性具有值 Any。</span><span class="sxs-lookup"><span data-stu-id="17a61-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="17a61-157">但是，有些情况下在其中可能要缓存仅在浏览器上或只能在服务器上。</span><span class="sxs-lookup"><span data-stu-id="17a61-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="17a61-158">例如，如果缓存的每个用户进行个性化设置的信息然后不应缓存在服务器上的信息。</span><span class="sxs-lookup"><span data-stu-id="17a61-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="17a61-159">如果您要为不同的用户显示不同的信息，则应缓存仅在客户端上的信息。</span><span class="sxs-lookup"><span data-stu-id="17a61-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="17a61-160">例如，清单 3 中的控制器将公开名为 GetName() 返回当前用户名称的操作。</span><span class="sxs-lookup"><span data-stu-id="17a61-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="17a61-161">如果 Jack 登录到该网站并调用 GetName() 操作然后操作返回的字符串"Hi Jack"。</span><span class="sxs-lookup"><span data-stu-id="17a61-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="17a61-162">如果以后，Jill 要登录到该网站并调用 GetName() 操作然后她还将获取字符串"Hi Jack"。</span><span class="sxs-lookup"><span data-stu-id="17a61-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="17a61-163">Jack 最初调用控制器操作后，该字符串缓存的所有用户在 web 服务器上。</span><span class="sxs-lookup"><span data-stu-id="17a61-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="17a61-164">**代码清单 3 – Controllers\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="17a61-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="17a61-165">很可能在列表 3 中的控制器不适所需的方式。</span><span class="sxs-lookup"><span data-stu-id="17a61-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="17a61-166">您不希望向 Jill 显示消息"Hi Jack"。</span><span class="sxs-lookup"><span data-stu-id="17a61-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="17a61-167">你应该永远不会缓存服务器缓存中的个性化的内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="17a61-168">但是，你可能想要将个性化的内容缓存在浏览器缓存以提高性能。</span><span class="sxs-lookup"><span data-stu-id="17a61-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="17a61-169">如果缓存在浏览器中的内容，并且用户可以多次调用相同的控制器操作，然后可从浏览器缓存中而不是服务器检索内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="17a61-170">列表 4 中的已修改的控制器缓存 GetName() 操作的输出。</span><span class="sxs-lookup"><span data-stu-id="17a61-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="17a61-171">但是，仅在浏览器上并不是服务器上缓存内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="17a61-172">这样一来，当多个用户调用 GetName() 方法时，每个人员获取其自己的用户名称并不是另一个用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="17a61-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="17a61-173">**列表 4 – Controllers\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="17a61-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="17a61-174">请注意， &lt;OutputCache&gt;列表 4 中的属性包括位置属性设置为值 OutputCacheLocation.Client。</span><span class="sxs-lookup"><span data-stu-id="17a61-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="17a61-175">&lt;OutputCache&gt;属性还包括 NoStore 属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="17a61-176">NoStore 属性用于通知代理服务器和浏览器，它们不应存储在缓存内容的永久副本。</span><span class="sxs-lookup"><span data-stu-id="17a61-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="17a61-177">不同的输出缓存</span><span class="sxs-lookup"><span data-stu-id="17a61-177">Varying the Output Cache</span></span>

<span data-ttu-id="17a61-178">在某些情况下，您可能希望完全相同的内容的不同缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="17a61-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="17a61-179">例如，假设要创建母版/详细信息页。</span><span class="sxs-lookup"><span data-stu-id="17a61-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="17a61-180">主页面显示电影标题的列表。</span><span class="sxs-lookup"><span data-stu-id="17a61-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="17a61-181">单击标题时，可以为所选电影获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="17a61-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="17a61-182">如果缓存的详细信息页，然后将哪些电影无论您单击显示同一电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="17a61-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="17a61-183">将向所有将来的用户显示第一个用户所选的第一个影片。</span><span class="sxs-lookup"><span data-stu-id="17a61-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="17a61-184">可以通过利用的 VaryByParam 属性解决此问题&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="17a61-185">此属性，可创建不同的缓存的版本的完全相同的内容时窗体参数或查询字符串参数而异。</span><span class="sxs-lookup"><span data-stu-id="17a61-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="17a61-186">例如，在列表 5 中的控制器将公开名为 Master() 和 Details() 的两个操作。</span><span class="sxs-lookup"><span data-stu-id="17a61-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="17a61-187">Master() 操作返回的电影标题列表和 Details() 操作返回所选电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="17a61-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="17a61-188">**列表 5 – Controllers\MoviesController.vb**</span><span class="sxs-lookup"><span data-stu-id="17a61-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="17a61-189">Master() 操作包括 VaryByParam 属性具有值"none"。</span><span class="sxs-lookup"><span data-stu-id="17a61-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="17a61-190">当查看的 Master() 调用操作，主节点的相同的缓存版本，则返回。</span><span class="sxs-lookup"><span data-stu-id="17a61-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="17a61-191">任何窗体参数或查询字符串参数被忽略 （见图 2）。</span><span class="sxs-lookup"><span data-stu-id="17a61-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="17a61-192">**图 2 – /Movies/Master 视图**</span><span class="sxs-lookup"><span data-stu-id="17a61-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="17a61-194">**图 3-/ Movies/详细信息视图**</span><span class="sxs-lookup"><span data-stu-id="17a61-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="17a61-196">Details() 操作包括具有值"Id"的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="17a61-197">如果不同的 Id 参数的值传递到控制器操作，生成不同的缓存的版本的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="17a61-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="17a61-198">它是必须了解使用 VaryByParam 属性结果在多个缓存的和不是失望。</span><span class="sxs-lookup"><span data-stu-id="17a61-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="17a61-199">每个不同版本的 Id 参数创建的详细信息视图的不同缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="17a61-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="17a61-200">您可以将 VaryByParam 属性设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="17a61-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="17a61-201">\* = 创建不同的缓存的版本，只要窗体或查询字符串参数而异。</span><span class="sxs-lookup"><span data-stu-id="17a61-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="17a61-202">none = 从不创建不同的缓存的版本</span><span class="sxs-lookup"><span data-stu-id="17a61-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="17a61-203">以分号的参数列表 = 创建不同的缓存的版本，只要任何窗体或查询字符串参数列表中各不相同</span><span class="sxs-lookup"><span data-stu-id="17a61-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>


#### <a name="creating-a-cache-profile"></a><span data-ttu-id="17a61-204">创建缓存配置文件</span><span class="sxs-lookup"><span data-stu-id="17a61-204">Creating a Cache Profile</span></span>

<span data-ttu-id="17a61-205">作为配置输出缓存属性的修改的属性的替代方法&lt;OutputCache&gt;属性，您可以在 web 配置 (web.config) 文件中创建的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="17a61-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="17a61-206">在 web 配置文件中创建的缓存配置文件提供了几个重要优势。</span><span class="sxs-lookup"><span data-stu-id="17a61-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="17a61-207">首先，通过配置输出缓存的 web 配置文件中，可以控制如何控制器操作缓存在一个中心位置的内容。</span><span class="sxs-lookup"><span data-stu-id="17a61-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="17a61-208">可以创建一个缓存配置文件，并将该配置文件应用于多个控制器或控制器操作。</span><span class="sxs-lookup"><span data-stu-id="17a61-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="17a61-209">其次，您可以修改 web 配置文件无需重新编译你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="17a61-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="17a61-210">如果你需要禁用缓存的应用程序已部署到生产环境，则可以只需修改 web 配置文件中定义的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="17a61-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="17a61-211">将自动检测到并应用到 web 配置文件的任何更改。</span><span class="sxs-lookup"><span data-stu-id="17a61-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="17a61-212">例如，&lt;缓存&gt;列表 6 中的 web 配置节定义名为 Cache1Hour 的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="17a61-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="17a61-213">&lt;缓存&gt;部分必须出现在&lt;system.web&gt; web 配置文件的部分。</span><span class="sxs-lookup"><span data-stu-id="17a61-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="17a61-214">**代码清单 6 – 缓存部分中的 web.config**</span><span class="sxs-lookup"><span data-stu-id="17a61-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="17a61-215">列表 7 中的控制器演示了如何将 Cache1Hour 配置文件应用到的控制器操作具有&lt;OutputCache&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="17a61-216">**列表 7 – Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="17a61-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="17a61-217">如果调用公开的清单 7 中的控制器的 index （） 操作然后将 1 个小时返回相同的时间。</span><span class="sxs-lookup"><span data-stu-id="17a61-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="17a61-218">总结</span><span class="sxs-lookup"><span data-stu-id="17a61-218">Summary</span></span>

<span data-ttu-id="17a61-219">输出缓存提供的极大改善了 ASP.NET MVC 应用程序的性能非常简单的方法。</span><span class="sxs-lookup"><span data-stu-id="17a61-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="17a61-220">在本教程中，您学习了如何使用&lt;OutputCache&gt;要缓存的控制器操作的输出属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="17a61-221">您还学习了如何修改的属性&lt;OutputCache&gt;如要修改内容获取缓存的持续时间和 VaryByParam 属性的属性。</span><span class="sxs-lookup"><span data-stu-id="17a61-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="17a61-222">最后，您学习了如何在 web 配置文件中定义缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="17a61-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="17a61-223">[上一页](understanding-action-filters-vb.md)
> [下一页](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="17a61-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
