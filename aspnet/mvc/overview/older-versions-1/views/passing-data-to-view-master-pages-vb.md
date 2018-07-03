---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 将数据传递到视图母版页 (VB) |Microsoft Docs
author: microsoft
description: 本教程的目的是说明如何向视图母版页，从控制器传递数据。 探讨如何将数据传递到视图 m 的两种策略...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: e70f15d98101336dbef31b4f9d8b958632e46c01
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388511"
---
<a name="passing-data-to-view-master-pages-vb"></a><span data-ttu-id="56dc9-104">将数据传递到视图母版页 (VB)</span><span class="sxs-lookup"><span data-stu-id="56dc9-104">Passing Data to View Master Pages (VB)</span></span>
====================
<span data-ttu-id="56dc9-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="56dc9-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="56dc9-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="56dc9-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> <span data-ttu-id="56dc9-107">本教程的目的是说明如何向视图母版页，从控制器传递数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="56dc9-108">我们将介绍两种策略用于向视图母版页传递数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="56dc9-109">首先，我们将讨论导致难以维护的应用程序的简单解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="56dc9-110">接下来，我们检查需要稍有更多的初始工作，但更易于维护的应用程序中的结果的更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>


## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="56dc9-111">向视图母版页传递数据</span><span class="sxs-lookup"><span data-stu-id="56dc9-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="56dc9-112">本教程的目的是说明如何向视图母版页，从控制器传递数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="56dc9-113">我们将介绍两种策略用于向视图母版页传递数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="56dc9-114">首先，我们将讨论导致难以维护的应用程序的简单解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="56dc9-115">接下来，我们检查需要稍有更多的初始工作，但更易于维护的应用程序中的结果的更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="56dc9-116">问题</span><span class="sxs-lookup"><span data-stu-id="56dc9-116">The Problem</span></span>

<span data-ttu-id="56dc9-117">假设您要构建电影数据库应用程序，并且你想要在应用程序中每一页上显示电影类别列表 （见图 1）。</span><span class="sxs-lookup"><span data-stu-id="56dc9-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="56dc9-118">此外，假设电影类别的列表存储在数据库表中。</span><span class="sxs-lookup"><span data-stu-id="56dc9-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="56dc9-119">在这种情况下，最好从数据库检索类别和呈现的视图母版页中的电影类别列表。</span><span class="sxs-lookup"><span data-stu-id="56dc9-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>


<span data-ttu-id="56dc9-120">[![在视图母版页中显示电影类别](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="56dc9-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="56dc9-121">**图 01**： 在视图母版页中显示电影类别 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="56dc9-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image3.png))</span></span>


<span data-ttu-id="56dc9-122">下面是此问题。</span><span class="sxs-lookup"><span data-stu-id="56dc9-122">Here's the problem.</span></span> <span data-ttu-id="56dc9-123">如何检索在母版页中的电影类别的列表？</span><span class="sxs-lookup"><span data-stu-id="56dc9-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="56dc9-124">它很容易在母版页中直接调用模型类的方法。</span><span class="sxs-lookup"><span data-stu-id="56dc9-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="56dc9-125">换而言之，很容易就包括用于从数据库直接在主页面中检索数据的代码。</span><span class="sxs-lookup"><span data-stu-id="56dc9-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="56dc9-126">但是，绕过 MVC 控制器来访问数据库会违反是构建一个 MVC 应用程序的主要优点之一完全分离关注点。</span><span class="sxs-lookup"><span data-stu-id="56dc9-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="56dc9-127">在 MVC 应用程序，你想要由 MVC 控制器的 MVC 视图和 MVC 模型之间的所有交互。</span><span class="sxs-lookup"><span data-stu-id="56dc9-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="56dc9-128">此分离关注点会导致更易于维护、 可适应和可测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="56dc9-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="56dc9-129">MVC 应用程序中传递给视图 （包括视图母版页） 的所有数据应通过控制器操作都传递给视图。</span><span class="sxs-lookup"><span data-stu-id="56dc9-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="56dc9-130">此外，应通过利用查看数据的传递数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="56dc9-131">在本教程的其余部分，我将介绍两种方法向视图母版页传递视图的数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="56dc9-132">简单的解决方案</span><span class="sxs-lookup"><span data-stu-id="56dc9-132">The Simple Solution</span></span>

<span data-ttu-id="56dc9-133">让我们开始将视图数据从控制器传递到视图母版页的最简单解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="56dc9-134">最简单的解决方案是将每个控制器操作中传递的母版页的视图数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="56dc9-135">请考虑在列表 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="56dc9-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="56dc9-136">它公开两个名为的操作`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="56dc9-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="56dc9-137">`Index()`操作方法返回电影数据库表中的每一部电影。</span><span class="sxs-lookup"><span data-stu-id="56dc9-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="56dc9-138">`Details()`操作方法返回特定电影类别中的每一部电影。</span><span class="sxs-lookup"><span data-stu-id="56dc9-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="56dc9-139">**代码清单 1 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="56dc9-139">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

<span data-ttu-id="56dc9-140">请注意，同时`Index()`和`Details()`操作添加两个项以查看数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-140">Notice that both the `Index()` and the `Details()` actions add two items to view data.</span></span> <span data-ttu-id="56dc9-141">`Index()`操作将添加两个密钥： 类别和电影。</span><span class="sxs-lookup"><span data-stu-id="56dc9-141">The `Index()` action adds two keys: categories and movies.</span></span> <span data-ttu-id="56dc9-142">类别键代表电影类别视图主页所显示的列表。</span><span class="sxs-lookup"><span data-stu-id="56dc9-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="56dc9-143">电影键表示索引视图页所显示的影片的列表。</span><span class="sxs-lookup"><span data-stu-id="56dc9-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="56dc9-144">`Details()`操作还将添加名为类别和电影的两个密钥。</span><span class="sxs-lookup"><span data-stu-id="56dc9-144">The `Details()` action also adds two keys named categories and movies.</span></span> <span data-ttu-id="56dc9-145">类别键中，再次重申，表示电影类别视图主页所显示的列表。</span><span class="sxs-lookup"><span data-stu-id="56dc9-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="56dc9-146">电影键表示电影的详细信息视图页所显示的特定类别的列表 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="56dc9-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>


<span data-ttu-id="56dc9-147">[![详细信息视图](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="56dc9-147">[![The Details view](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="56dc9-148">**图 02**： 详细信息查看 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="56dc9-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image6.png))</span></span>


<span data-ttu-id="56dc9-149">索引视图包含在代码清单 2 中。</span><span class="sxs-lookup"><span data-stu-id="56dc9-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="56dc9-150">它只是循环访问列表中查看数据的电影项所表示的电影。</span><span class="sxs-lookup"><span data-stu-id="56dc9-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="56dc9-151">**代码清单 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="56dc9-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="56dc9-152">视图主页面都包含在清单 3。</span><span class="sxs-lookup"><span data-stu-id="56dc9-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="56dc9-153">视图母版页迭代并呈现所有由类别项中查看数据表示电影类别。</span><span class="sxs-lookup"><span data-stu-id="56dc9-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="56dc9-154">**代码清单 3 – `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="56dc9-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="56dc9-155">所有数据将都传递到的视图和视图母版页视图数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="56dc9-156">这是将数据传递给母版页的正确方法。</span><span class="sxs-lookup"><span data-stu-id="56dc9-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="56dc9-157">因此，为什么会这样使用此解决方案？</span><span class="sxs-lookup"><span data-stu-id="56dc9-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="56dc9-158">问题是此解决方案违反了 DRY （不要自我重复） 原则。</span><span class="sxs-lookup"><span data-stu-id="56dc9-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="56dc9-159">每个控制器操作必须添加电影类别以查看数据的完全相同的列表。</span><span class="sxs-lookup"><span data-stu-id="56dc9-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="56dc9-160">在应用程序中具有重复代码使你的应用程序更难以维护、 适应和修改。</span><span class="sxs-lookup"><span data-stu-id="56dc9-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="56dc9-161">很好的解决方案</span><span class="sxs-lookup"><span data-stu-id="56dc9-161">The Good Solution</span></span>

<span data-ttu-id="56dc9-162">在本部分中，我们检查将数据从控制器操作传递到视图母版页的替代，并更好，解决方案。</span><span class="sxs-lookup"><span data-stu-id="56dc9-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="56dc9-163">无需在每个控制器操作添加母版页的电影类别，我们添加电影类别查看数据一次。</span><span class="sxs-lookup"><span data-stu-id="56dc9-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="56dc9-164">应用程序控制器中添加了使用视图母版页的所有视图数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="56dc9-165">ApplicationController 类都包含在清单 4。</span><span class="sxs-lookup"><span data-stu-id="56dc9-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="56dc9-166">ApplicationController 类都包含在清单 4。</span><span class="sxs-lookup"><span data-stu-id="56dc9-166">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="56dc9-167">**列表 4 – `Controllers\ApplicationController.vb`**</span><span class="sxs-lookup"><span data-stu-id="56dc9-167">**Listing 4 – `Controllers\ApplicationController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

<span data-ttu-id="56dc9-168">有三个您应注意到了列表 4 中的应用程序控制器的操作。</span><span class="sxs-lookup"><span data-stu-id="56dc9-168">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="56dc9-169">首先，请注意，类继承自基 system.web.mvc.controller 中衍生类。</span><span class="sxs-lookup"><span data-stu-id="56dc9-169">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="56dc9-170">应用程序控制器是控制器类。</span><span class="sxs-lookup"><span data-stu-id="56dc9-170">The Application controller is a controller class.</span></span>

<span data-ttu-id="56dc9-171">其次，注意应用程序控制器类是一个 MustInherit 类。</span><span class="sxs-lookup"><span data-stu-id="56dc9-171">Second, notice that the Application controller class is a MustInherit class.</span></span> <span data-ttu-id="56dc9-172">MustInherit 类是具体类必须实现一个类。</span><span class="sxs-lookup"><span data-stu-id="56dc9-172">An MustInherit class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="56dc9-173">因为应用程序控制器是一个 MustInherit 类，您不能调用直接在类中定义任何方法。</span><span class="sxs-lookup"><span data-stu-id="56dc9-173">Because the Application controller is an MustInherit class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="56dc9-174">如果尝试直接调用应用程序类，然后将获取的找不到资源错误消息。</span><span class="sxs-lookup"><span data-stu-id="56dc9-174">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="56dc9-175">第三，请注意应用程序控制器包含将电影类别以查看数据的列表添加一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="56dc9-175">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="56dc9-176">每个控制器类都继承自应用程序控制器将自动调用应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="56dc9-176">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="56dc9-177">无论从应用程序控制器继承任何控制器上调用任何操作，电影类别是自动包含在视图数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-177">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="56dc9-178">列表 5 中的电影控制器继承自应用程序控制器。</span><span class="sxs-lookup"><span data-stu-id="56dc9-178">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="56dc9-179">**列表 5 – `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="56dc9-179">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

<span data-ttu-id="56dc9-180">电影控制器，就像在上一节中讨论的主页控制器一样公开名为的两个操作方法`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="56dc9-180">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="56dc9-181">请注意，电影类别视图主页所显示的列表并不添加到视图中的数据`Index()`或`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="56dc9-181">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="56dc9-182">电影控制器继承自应用程序控制器，因为电影类别列表中的添加自动查看数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-182">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="56dc9-183">请注意，将视图母版页的视图数据添加到此解决方案不违反 DRY （不要自我重复） 原则。</span><span class="sxs-lookup"><span data-stu-id="56dc9-183">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="56dc9-184">若要查看数据的电影类别的列表添加的代码包含只在一个位置： 应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="56dc9-184">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="56dc9-185">总结</span><span class="sxs-lookup"><span data-stu-id="56dc9-185">Summary</span></span>

<span data-ttu-id="56dc9-186">在本教程中，我们讨论了两种方法可以将视图数据从控制器传递到视图的母版页。</span><span class="sxs-lookup"><span data-stu-id="56dc9-186">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="56dc9-187">首先，我们探讨了一个简单，但难以维护的方法。</span><span class="sxs-lookup"><span data-stu-id="56dc9-187">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="56dc9-188">在第一个部分中，我们讨论了如何添加视图母版页的视图数据在每个每个控制器操作中应用程序中。</span><span class="sxs-lookup"><span data-stu-id="56dc9-188">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="56dc9-189">我们得出的结论是，这是错误的方法，因为它违反了 DRY （不要自我重复） 原则。</span><span class="sxs-lookup"><span data-stu-id="56dc9-189">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="56dc9-190">接下来，我们将探讨更理想的策略中添加数据视图母版页需查看数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-190">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="56dc9-191">无需在每个控制器操作添加的视图数据，我们添加了一次应用程序控制器中的视图数据。</span><span class="sxs-lookup"><span data-stu-id="56dc9-191">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="56dc9-192">这样一来，将数据传递到视图母版页中的 ASP.NET MVC 应用程序时，可以避免重复代码。</span><span class="sxs-lookup"><span data-stu-id="56dc9-192">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="56dc9-193">上一篇</span><span class="sxs-lookup"><span data-stu-id="56dc9-193">Previous</span></span>](creating-page-layouts-with-view-master-pages-vb.md)
