---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第 10 部分： 导航和站点设计，结束的最终更新 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 10 部分介绍对导航和 s。 最后更新...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: b40d194c4d08f3564da59bacde4b5d3d7663373a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878589"
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="6957b-104">第 10 部分： 导航和站点设计，结束的最终更新</span><span class="sxs-lookup"><span data-stu-id="6957b-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>
====================
<span data-ttu-id="6957b-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="6957b-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="6957b-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="6957b-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="6957b-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="6957b-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="6957b-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="6957b-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="6957b-109">第 10 部分介绍如何对导航和站点设计，结束的最终更新。</span><span class="sxs-lookup"><span data-stu-id="6957b-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>


<span data-ttu-id="6957b-110">对于我们的站点，完成所有的主要功能，但我们仍有一些功能添加到站点导航、 主页上，和应用商店浏览页。</span><span class="sxs-lookup"><span data-stu-id="6957b-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="6957b-111">创建摘要部分购物车视图</span><span class="sxs-lookup"><span data-stu-id="6957b-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="6957b-112">我们想要公开整个站点内的用户的购物车中的项的数目。</span><span class="sxs-lookup"><span data-stu-id="6957b-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="6957b-113">我们可以轻松地实现这通过创建其添加到我们 Site.master 了分部视图。</span><span class="sxs-lookup"><span data-stu-id="6957b-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="6957b-114">如前面所示，购物车控制器包括返回了分部视图的 CartSummary 操作方法：</span><span class="sxs-lookup"><span data-stu-id="6957b-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="6957b-115">若要创建 CartSummary 分部视图，右键单击视图/ShoppingCart 文件夹，然后选择添加视图。</span><span class="sxs-lookup"><span data-stu-id="6957b-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="6957b-116">将视图 CartSummary 命名并检查"创建了分部视图"复选框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6957b-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="6957b-117">CartSummary 分部视图的过程非常简单-只需购物车中的显示项的数目的购物车索引视图的链接。</span><span class="sxs-lookup"><span data-stu-id="6957b-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="6957b-118">CartSummary.cshtml 的完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="6957b-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="6957b-119">我们可以在站点上，使用 Html.RenderAction 方法包括站点母版上，任何页中包含了分部视图。</span><span class="sxs-lookup"><span data-stu-id="6957b-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="6957b-120">RenderAction 要求我们指定操作名称 ("CartSummary") 和控制器名称 ("ShoppingCart") 作为下面。</span><span class="sxs-lookup"><span data-stu-id="6957b-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="6957b-121">之前将此添加到站点布局，我们还将创建流派菜单以便我们可以将所有我们 Site.master 更新一次。</span><span class="sxs-lookup"><span data-stu-id="6957b-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="6957b-122">创建流派菜单分部视图</span><span class="sxs-lookup"><span data-stu-id="6957b-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="6957b-123">我们可以让它为我们的用户通过添加一个流派菜单，其中列出了所有风格可用在我们的存储中存储导航容易得多。</span><span class="sxs-lookup"><span data-stu-id="6957b-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="6957b-124">我们将遵循相同的步骤还创建了 GenreMenu 分部视图，然后我们可以将这两个添加到站点 master。</span><span class="sxs-lookup"><span data-stu-id="6957b-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="6957b-125">首先，将以下 GenreMenu 控制器操作添加到 StoreController:</span><span class="sxs-lookup"><span data-stu-id="6957b-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="6957b-126">此操作返回的列表将显示的部分视图中，我们将在下一步创建的风格。</span><span class="sxs-lookup"><span data-stu-id="6957b-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="6957b-127">*注意： 我们具有 [ChildActionOnly] 特性添加到此控制器操作，这表示我们只想要从分部视图使用此操作。此属性将阻止从正在执行通过浏览到 /Store/GenreMenu 的控制器操作。这不是必需的分部视图，但它是很好的做法，由于我们想要确保按我们期望的那样使用我们的控制器操作。我们还会返回 PartialView 而不是视图中，这样就知道，它不应为此视图中，使用布局，因为它正在包括在其他视图的视图引擎。*</span><span class="sxs-lookup"><span data-stu-id="6957b-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="6957b-128">右键单击 GenreMenu 控制器操作，然后创建名为强类型使用流派视图数据类，如下所示的 GenreMenu 了分部视图。</span><span class="sxs-lookup"><span data-stu-id="6957b-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="6957b-129">更新 GenreMenu 分部视图以显示，如下所示使用未经排序的列表项的视图代码。</span><span class="sxs-lookup"><span data-stu-id="6957b-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="6957b-130">更新站点布局，以显示我们分部视图</span><span class="sxs-lookup"><span data-stu-id="6957b-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="6957b-131">我们可以将我们分部视图添加到站点布局 (/视图/共享/\_Layout.cshtml) 通过调用 Html.RenderAction()。</span><span class="sxs-lookup"><span data-stu-id="6957b-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="6957b-132">我们将添加这两个在中，以及一些其他的标记来显示它们，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6957b-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="6957b-133">现在当我们运行应用程序，我们将看到在左侧的导航区域中 Genre 和顶部购物车摘要。</span><span class="sxs-lookup"><span data-stu-id="6957b-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="6957b-134">更新到应用商店浏览页</span><span class="sxs-lookup"><span data-stu-id="6957b-134">Update to the Store Browse page</span></span>

<span data-ttu-id="6957b-135">应用商店浏览页上正常运行，但看上去很好。</span><span class="sxs-lookup"><span data-stu-id="6957b-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="6957b-136">我们可以更新页后，可以更好的布局中显示专辑，通过更新的视图代码 （/Views/Store/Browse.cshtml 中找到），如下所示：</span><span class="sxs-lookup"><span data-stu-id="6957b-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="6957b-137">此处我们正在使用的 Url.Action 而不是次 Html.ActionLink，以便我们可以应用到该链接可以包括唱片集图稿特殊格式设置。</span><span class="sxs-lookup"><span data-stu-id="6957b-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="6957b-138">*注意： 我们均会显示这些专辑泛型唱片集封面。此信息存储在数据库，并通过存储管理器可编辑。你是欢迎添加你自己的图片。*</span><span class="sxs-lookup"><span data-stu-id="6957b-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="6957b-139">现在当我们浏览到一种风格，我们将看到与唱片集图稿网格中所示唱片集。</span><span class="sxs-lookup"><span data-stu-id="6957b-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="6957b-140">更新主页上显示顶部销售专辑</span><span class="sxs-lookup"><span data-stu-id="6957b-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="6957b-141">我们想要功能我们最畅销的专辑在主页上，来提高销量。</span><span class="sxs-lookup"><span data-stu-id="6957b-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="6957b-142">对我们 HomeController 来处理，并添加一些其他的图形中，我们将进行一些更新。</span><span class="sxs-lookup"><span data-stu-id="6957b-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="6957b-143">首先，我们将添加一个导航属性到唱片集类，以便 EntityFramework 知道它们相关联。</span><span class="sxs-lookup"><span data-stu-id="6957b-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="6957b-144">最后几行我们**唱片集**类现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="6957b-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="6957b-145">*注意： 这将需要添加 using 语句，以便为 System.Collections.Generic 命名空间中。*</span><span class="sxs-lookup"><span data-stu-id="6957b-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="6957b-146">首先，我们将添加 storeDB 字段和 MvcMusicStore.Models using 语句，如下所示我们其他控制器。</span><span class="sxs-lookup"><span data-stu-id="6957b-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="6957b-147">接下来，我们将向它查询我们的数据库以查找根据 OrderDetails 顶部销售专辑 HomeController 中添加以下方法。</span><span class="sxs-lookup"><span data-stu-id="6957b-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="6957b-148">这是一个私有方法，因为我们不想将其提供为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="6957b-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="6957b-149">我们会将其包括在为简单起见，HomeController 但建议将你的业务逻辑移到适当的单独的服务类。</span><span class="sxs-lookup"><span data-stu-id="6957b-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="6957b-150">完成此操作后，我们可以更新要查询前 5 销售唱片集并将它们返回到视图的索引控制器操作。</span><span class="sxs-lookup"><span data-stu-id="6957b-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="6957b-151">更新 HomeController 的完整代码所示。</span><span class="sxs-lookup"><span data-stu-id="6957b-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="6957b-152">最后，我们将需要更新我们主页索引视图，以便它可以通过更新模型类型，并将唱片集列表添加到底部显示的唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="6957b-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="6957b-153">我们将利用此机会来还向页面添加一个标题和促销部分。</span><span class="sxs-lookup"><span data-stu-id="6957b-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="6957b-154">现在我们运行应用程序时，我们将看到使用顶部销售专辑和我们的促销消息我们更新的主页。</span><span class="sxs-lookup"><span data-stu-id="6957b-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="6957b-155">结束语</span><span class="sxs-lookup"><span data-stu-id="6957b-155">Conclusion</span></span>

<span data-ttu-id="6957b-156">我们已了解，ASP.NET MVC 便于对来创建复杂的网站和数据库访问，成员身份，AJAX 等。</span><span class="sxs-lookup"><span data-stu-id="6957b-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="6957b-157">非常快速。</span><span class="sxs-lookup"><span data-stu-id="6957b-157">pretty quickly.</span></span> <span data-ttu-id="6957b-158">希望本教程已授予所需若要开始构建您自己的 ASP.NET MVC 应用程序工具 ！</span><span class="sxs-lookup"><span data-stu-id="6957b-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>


> [!div class="step-by-step"]
> [<span data-ttu-id="6957b-159">上一篇</span><span class="sxs-lookup"><span data-stu-id="6957b-159">Previous</span></span>](mvc-music-store-part-9.md)
