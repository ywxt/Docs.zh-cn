---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第 10 部分： 导航和站点设计，结束语的最终更新 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 10 部分介绍了导航和 S.的最终更新...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f32509701dd112053aa4f31d6552601f961c7413
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825042"
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="3f853-104">第 10 部分： 导航和站点设计，结束语的最终更新</span><span class="sxs-lookup"><span data-stu-id="3f853-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>
====================
<span data-ttu-id="3f853-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="3f853-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3f853-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f853-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="3f853-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="3f853-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="3f853-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="3f853-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="3f853-109">第 10 部分介绍如何导航和站点设计，结束语的最终更新。</span><span class="sxs-lookup"><span data-stu-id="3f853-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>


<span data-ttu-id="3f853-110">我们已经为我们的站点，完成所有主要功能，但我们仍有一些功能，可添加到 site navigation — 站点导航、 主页页面和应用商店浏览页。</span><span class="sxs-lookup"><span data-stu-id="3f853-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="3f853-111">创建购物车摘要分部视图</span><span class="sxs-lookup"><span data-stu-id="3f853-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="3f853-112">我们想要跨整个站点中公开用户的购物车中的项目数。</span><span class="sxs-lookup"><span data-stu-id="3f853-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="3f853-113">我们可以轻松实现这通过创建分部视图添加到我们 Site.master。</span><span class="sxs-lookup"><span data-stu-id="3f853-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="3f853-114">如先前所示，购物车控制器包含 CartSummary 操作方法，它将返回分部视图：</span><span class="sxs-lookup"><span data-stu-id="3f853-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="3f853-115">若要创建 CartSummary 分部视图，右键单击视图/ShoppingCart 文件夹，然后选择添加视图。</span><span class="sxs-lookup"><span data-stu-id="3f853-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="3f853-116">视图 CartSummary 命名并选中"创建分部视图"复选框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3f853-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="3f853-117">CartSummary 分部视图是非常简单-只是一个链接到购物车索引视图显示购物车中的项的数目。</span><span class="sxs-lookup"><span data-stu-id="3f853-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="3f853-118">CartSummary.cshtml 的完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f853-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="3f853-119">我们可以通过使用 Html.RenderAction 方法包括站点主站点中的所有页面中包含分部视图。</span><span class="sxs-lookup"><span data-stu-id="3f853-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="3f853-120">RenderAction 需要我们指定的操作名称 ("CartSummary") 和控制器名称 ("ShoppingCart") 作为下面。</span><span class="sxs-lookup"><span data-stu-id="3f853-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="3f853-121">将此添加到站点布局之前, 我们还将创建流派菜单上以便我们可以将所有我们 Site.master 更新一次。</span><span class="sxs-lookup"><span data-stu-id="3f853-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="3f853-122">创建分部视图的流派菜单</span><span class="sxs-lookup"><span data-stu-id="3f853-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="3f853-123">我们可以使用户通过添加一个流派菜单，其中列出了所有流派可用在我们的存储中存储导航更容易。</span><span class="sxs-lookup"><span data-stu-id="3f853-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="3f853-124">我们将遵循相同的步骤还创建了 GenreMenu 分部视图，然后我们可以将这两个添加到站点 master。</span><span class="sxs-lookup"><span data-stu-id="3f853-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="3f853-125">首先，将以下 GenreMenu 控制器操作添加到 StoreController:</span><span class="sxs-lookup"><span data-stu-id="3f853-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="3f853-126">此操作会返回可以从我们将在下一步创建的分部视图将显示影片类型列表。</span><span class="sxs-lookup"><span data-stu-id="3f853-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="3f853-127">*注意： 我们添加了 [ChildActionOnly] 属性对该控制器操作，这表示我们只需要此操作以用于从分部视图。此属性将阻止执行通过浏览到 /Store/GenreMenu 的控制器操作。这不是必需的分部视图，但它是不错的做法，因为我们想要确保我们的控制器操作来按照我们的意图。我们还将返回 PartialView 而不是视图中，以便了解它不应为此视图中，使用布局的其他视图中包括的视图引擎。*</span><span class="sxs-lookup"><span data-stu-id="3f853-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="3f853-128">右键单击 GenreMenu 控制器操作并创建名为 GenreMenu 是强类型，如下所示使用流派视图数据类的分部视图。</span><span class="sxs-lookup"><span data-stu-id="3f853-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="3f853-129">更新要显示的项，如下所示使用未排序的列表的 GenreMenu 分部视图的视图代码。</span><span class="sxs-lookup"><span data-stu-id="3f853-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="3f853-130">更新站点布局，以显示我们的分部视图</span><span class="sxs-lookup"><span data-stu-id="3f853-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="3f853-131">我们可以将我们的分部视图添加到站点布局 (/视图/共享/\_Layout.cshtml) 通过调用 Html.RenderAction()。</span><span class="sxs-lookup"><span data-stu-id="3f853-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="3f853-132">我们将添加这两个在中，以及一些其他的标记来显示它们，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f853-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="3f853-133">现在当我们运行该应用程序，我们将看到左侧的导航区域中的流派和顶部车摘要。</span><span class="sxs-lookup"><span data-stu-id="3f853-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="3f853-134">更新到应用商店浏览页</span><span class="sxs-lookup"><span data-stu-id="3f853-134">Update to the Store Browse page</span></span>

<span data-ttu-id="3f853-135">存储浏览页正常运行，但不会看起来非常不错。</span><span class="sxs-lookup"><span data-stu-id="3f853-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="3f853-136">我们可以更新页后，可以更好的布局中显示唱片集，通过更新视图中的代码 （/Views/Store/Browse.cshtml），如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f853-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="3f853-137">此处我们将使用的 Url.Action 而不是 Html.ActionLink，以便我们可以将应用特殊格式设置为包含唱片集作品的链接。</span><span class="sxs-lookup"><span data-stu-id="3f853-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="3f853-138">*注意： 我们要显示这些唱片集的泛型唱片集封面。此信息存储在数据库中，通过存储管理器可编辑。你也可以添加您自己的作品。*</span><span class="sxs-lookup"><span data-stu-id="3f853-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="3f853-139">现在我们浏览到一种流派，我们将看到包含唱片集图片的网格中所示唱片集。</span><span class="sxs-lookup"><span data-stu-id="3f853-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="3f853-140">更新主页显示顶部销售相册</span><span class="sxs-lookup"><span data-stu-id="3f853-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="3f853-141">我们想要功能我们最畅销的唱片集在主页上，来提高销量。</span><span class="sxs-lookup"><span data-stu-id="3f853-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="3f853-142">我们将为我们处理此问题，并添加一些其他的图形中的 HomeController 进行一些更新。</span><span class="sxs-lookup"><span data-stu-id="3f853-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="3f853-143">首先，我们会将导航属性添加到我们唱片集的类，以便让 EntityFramework 知道它们关联。</span><span class="sxs-lookup"><span data-stu-id="3f853-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="3f853-144">最后几行我们**唱片集**类现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f853-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="3f853-145">*注意： 这将需要添加 using 语句，以便在 System.Collections.Generic 命名空间中。*</span><span class="sxs-lookup"><span data-stu-id="3f853-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="3f853-146">首先，我们将添加 storeDB 字段和 MvcMusicStore.Models using 语句，如我们其他控制器中所示。</span><span class="sxs-lookup"><span data-stu-id="3f853-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="3f853-147">接下来，我们将向它查询数据库以查找根据 OrderDetails 顶部销售相册 HomeController 中添加以下方法。</span><span class="sxs-lookup"><span data-stu-id="3f853-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="3f853-148">这是一个私有方法，因为我们不想将其作为控制器操作提供。</span><span class="sxs-lookup"><span data-stu-id="3f853-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="3f853-149">我们会将其包括在为简单起见，HomeController，但建议将您的业务逻辑移到相应的单独的服务类。</span><span class="sxs-lookup"><span data-stu-id="3f853-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="3f853-150">使用此操作后，我们可以更新索引控制器操作可以查询前 5 种销售唱片集并将其返回到视图。</span><span class="sxs-lookup"><span data-stu-id="3f853-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="3f853-151">更新 HomeController 的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="3f853-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="3f853-152">最后，我们将需要更新主页索引视图，以便它可以通过更新模型类型和唱片集列表添加到底部显示的唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="3f853-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="3f853-153">我们将利用此机会来还向页面添加标题和升级部分。</span><span class="sxs-lookup"><span data-stu-id="3f853-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="3f853-154">现在当我们运行该应用程序，我们会看到顶部销售 album 和我们的促销消息与我们更新后的主页。</span><span class="sxs-lookup"><span data-stu-id="3f853-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="3f853-155">结束语</span><span class="sxs-lookup"><span data-stu-id="3f853-155">Conclusion</span></span>

<span data-ttu-id="3f853-156">我们所见，ASP.NET MVC 可以轻松创建复杂的网站具有数据库访问，成员身份，AJAX，等等。</span><span class="sxs-lookup"><span data-stu-id="3f853-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="3f853-157">很快就会变。</span><span class="sxs-lookup"><span data-stu-id="3f853-157">pretty quickly.</span></span> <span data-ttu-id="3f853-158">希望本教程提供若要开始构建你自己的 ASP.NET MVC 应用程序所需的工具 ！</span><span class="sxs-lookup"><span data-stu-id="3f853-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>


> [!div class="step-by-step"]
> [<span data-ttu-id="3f853-159">上一篇</span><span class="sxs-lookup"><span data-stu-id="3f853-159">Previous</span></span>](mvc-music-store-part-9.md)
