---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第 8 部分： 购物车与 Ajax 更新 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 8 部分介绍如何使用 Ajax 更新购物车。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 195c01ff0d71b2bfd0c00e71244d47a166330921
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871280"
---
<a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="79634-104">第 8 部分： 购物车与 Ajax 更新</span><span class="sxs-lookup"><span data-stu-id="79634-104">Part 8: Shopping Cart with Ajax Updates</span></span>
====================
<span data-ttu-id="79634-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="79634-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="79634-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="79634-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="79634-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="79634-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="79634-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="79634-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="79634-109">第 8 部分介绍如何使用 Ajax 更新购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>


<span data-ttu-id="79634-110">我们将允许用户将唱片集放在其购物车中，如果没有注册，但它们需要作为来宾要签出完成注册。</span><span class="sxs-lookup"><span data-stu-id="79634-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="79634-111">在购物和签出过程将分为两个控制器： 允许匿名将项添加到购物车，购物车控制器和签出控制器用于处理在结帐过程。</span><span class="sxs-lookup"><span data-stu-id="79634-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="79634-112">我们将使用在本部分中，购物车启动，然后生成下列部分中的在结帐过程。</span><span class="sxs-lookup"><span data-stu-id="79634-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="79634-113">添加车、 顺序和 OrderDetail 模型类</span><span class="sxs-lookup"><span data-stu-id="79634-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="79634-114">我们购物车和签出的过程将使用的某些新的类。</span><span class="sxs-lookup"><span data-stu-id="79634-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="79634-115">右键单击 Models 文件夹，然后添加车类 (Cart.cs) 替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="79634-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="79634-116">此类是非常类似于其他我们使用了目前为止，除了 RecordId 属性 [键] 属性。</span><span class="sxs-lookup"><span data-stu-id="79634-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="79634-117">我们车项将具有名为 CartID 以允许匿名购物的字符串标识符，但表包括名为 RecordId 整数主键。</span><span class="sxs-lookup"><span data-stu-id="79634-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="79634-118">按照约定，实体框架代码的第一个需要名为购物车的表的主键将 CartId 或 ID，但我们可以轻松地重写通过批注或代码如果我们想。</span><span class="sxs-lookup"><span data-stu-id="79634-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="79634-119">这是一个示例我们可以如何使用简单的约定的实体框架代码先进先时它们满足 us，但我们正在不受它们时它们不会。</span><span class="sxs-lookup"><span data-stu-id="79634-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="79634-120">接下来，添加 Order 类 (Order.cs) 替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="79634-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="79634-121">此类跟踪订单的摘要和传递信息。</span><span class="sxs-lookup"><span data-stu-id="79634-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="79634-122">**它不会尚未编译**，因为它具有一个 OrderDetails 的导航属性，具体取决于我们尚未创建的类。</span><span class="sxs-lookup"><span data-stu-id="79634-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="79634-123">让我们来修复现在通过添加一个名为 OrderDetail.cs，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="79634-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="79634-124">我们将使一个上次更新到我们 MusicStoreEntities 类，以包括 Dbset 该类将这些新的模型类，还包括 DbSet&lt;艺术家&gt;。</span><span class="sxs-lookup"><span data-stu-id="79634-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="79634-125">更新后的 MusicStoreEntities 类显示为下面。</span><span class="sxs-lookup"><span data-stu-id="79634-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="79634-126">管理购物车业务逻辑</span><span class="sxs-lookup"><span data-stu-id="79634-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="79634-127">接下来，我们将在模型文件夹中创建的购物车类。</span><span class="sxs-lookup"><span data-stu-id="79634-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="79634-128">购物车模型处理对车表的数据访问。</span><span class="sxs-lookup"><span data-stu-id="79634-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="79634-129">此外，它将处理到添加和从购物车中移除项的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="79634-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="79634-130">由于我们不希望要求用户注册的帐户，只是为了向其购物车中添加项，我们会将用户分配一个临时的唯一标识符 （使用 GUID 或全局唯一标识符） 时，他们访问购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="79634-131">我们将存储此 ID 使用 ASP.NET 会话类。</span><span class="sxs-lookup"><span data-stu-id="79634-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="79634-132">*注意： ASP.NET 会话是方便的位置来存储特定于用户的信息将过期后他们离开该站点。虽然不正确使用了会话状态都有较大的站点上的性能影响，我们轻度使用将适用于演示目的。*</span><span class="sxs-lookup"><span data-stu-id="79634-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="79634-133">购物车类公开以下方法：</span><span class="sxs-lookup"><span data-stu-id="79634-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="79634-134">**AddToCart**采用唱片集作为参数并将其添加到用户的购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="79634-135">由于车表跟踪每个唱片集的数量，它包括逻辑来创建一个新行，如果需要或只是递增数量，如果用户具有已排序的唱片集的一个副本。</span><span class="sxs-lookup"><span data-stu-id="79634-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="79634-136">**RemoveFromCart**使用唱片集 ID，并将其从用户的购物车中删除。</span><span class="sxs-lookup"><span data-stu-id="79634-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="79634-137">如果用户仅在其购物车具有唱片集的一个副本，删除行。</span><span class="sxs-lookup"><span data-stu-id="79634-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="79634-138">**EmptyCart**从用户的购物车中移除所有项。</span><span class="sxs-lookup"><span data-stu-id="79634-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="79634-139">**GetCartItems**检索进行显示或处理 CartItems 的列表。</span><span class="sxs-lookup"><span data-stu-id="79634-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="79634-140">**GetCount**检索唱片集用户具有在其购物车中的总次数。</span><span class="sxs-lookup"><span data-stu-id="79634-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="79634-141">**GetTotal**计算购物车中的所有项的总成本。</span><span class="sxs-lookup"><span data-stu-id="79634-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="79634-142">**CreateOrder**签出阶段将购物车转换为顺序。</span><span class="sxs-lookup"><span data-stu-id="79634-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="79634-143">**GetCart**是一种静态方法，这样我们控制器以获取车对象。</span><span class="sxs-lookup"><span data-stu-id="79634-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="79634-144">它使用**GetCartId**方法以处理 CartId 读取用户的会话。</span><span class="sxs-lookup"><span data-stu-id="79634-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="79634-145">GetCartId 方法需要 HttpContextBase，以便它可以从用户的会话中读取用户的 CartId。</span><span class="sxs-lookup"><span data-stu-id="79634-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="79634-146">下面是完整**购物车类**:</span><span class="sxs-lookup"><span data-stu-id="79634-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="79634-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="79634-147">ViewModels</span></span>

<span data-ttu-id="79634-148">我们购物车控制器需要进行一些复杂将信息传递给其视图不会完全映射到我们的模型对象。</span><span class="sxs-lookup"><span data-stu-id="79634-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="79634-149">我们不需要修改以满足我们的视图; 我们模型模型的类应表示我们的域，不是用户界面。</span><span class="sxs-lookup"><span data-stu-id="79634-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="79634-150">一种解决方案是将信息传递给使用 ViewBag 类中，我们使用存储管理器下拉列表中信息，但通过 ViewBag 传递的大量信息变得非常艰难来管理我们的视图。</span><span class="sxs-lookup"><span data-stu-id="79634-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="79634-151">到此解决方案是使用*ViewModel*模式。</span><span class="sxs-lookup"><span data-stu-id="79634-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="79634-152">使用此模式时我们将创建强类型的类对于我们的特定视图方案，进行优化的和其公开的动态值/所需内容由我们视图模板的属性。</span><span class="sxs-lookup"><span data-stu-id="79634-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="79634-153">然后，我们控制器类可以填充，并将这些视图优化类传递给我们要使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="79634-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="79634-154">这样，类型安全，编译时检查，和编辑器 IntelliSense 中查看模板。</span><span class="sxs-lookup"><span data-stu-id="79634-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="79634-155">我们将在购物车控制器中创建两个视图模型，以用于： ShoppingCartViewModel 将保留用户的购物车的内容和 ShoppingCartRemoveViewModel 将用于显示确认信息，当用户删除内容从购物车中。</span><span class="sxs-lookup"><span data-stu-id="79634-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="79634-156">让我们在我们要将组织的事物保存的项目的根目录中创建新的 Viewmodel 文件夹。</span><span class="sxs-lookup"><span data-stu-id="79634-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="79634-157">右键单击项目，选择添加 / 新文件夹。</span><span class="sxs-lookup"><span data-stu-id="79634-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="79634-158">该文件夹 Viewmodel 命名。</span><span class="sxs-lookup"><span data-stu-id="79634-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="79634-159">接下来，Viewmodel 文件夹中添加 ShoppingCartViewModel 类。</span><span class="sxs-lookup"><span data-stu-id="79634-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="79634-160">它具有两个属性： 车项，以及用于在购物车中保存的所有项的总价格的十进制值的列表。</span><span class="sxs-lookup"><span data-stu-id="79634-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="79634-161">现在将 ShoppingCartRemoveViewModel 添加到具有以下四个属性的 Viewmodel 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="79634-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="79634-162">购物车控制器</span><span class="sxs-lookup"><span data-stu-id="79634-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="79634-163">购物车控制器有三个主要用途： 将项添加到购物车、 从购物车，删除项和查看购物车的项目。</span><span class="sxs-lookup"><span data-stu-id="79634-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="79634-164">它将使的三个类使用我们刚刚创建： ShoppingCartViewModel、 ShoppingCartRemoveViewModel 和购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="79634-165">如下所示的 StoreController 和 StoreManagerController，我们将添加一个字段以保存 MusicStoreEntities 的实例。</span><span class="sxs-lookup"><span data-stu-id="79634-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="79634-166">使用空控制器模板向项目中添加一个新的购物车控制器。</span><span class="sxs-lookup"><span data-stu-id="79634-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="79634-167">下面是完成的购物车控制器。</span><span class="sxs-lookup"><span data-stu-id="79634-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="79634-168">索引和添加控制器操作应看上去很眼熟。</span><span class="sxs-lookup"><span data-stu-id="79634-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="79634-169">删除和 CartSummary 控制器操作处理两个的特殊情况下，我们将在下一节中讨论。</span><span class="sxs-lookup"><span data-stu-id="79634-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="79634-170">使用 jQuery 的 Ajax 更新</span><span class="sxs-lookup"><span data-stu-id="79634-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="79634-171">接下来，我们将创建强类型化为 ShoppingCartViewModel 并使用列表视图模板使用相同的方法为之前的购物车索引页。</span><span class="sxs-lookup"><span data-stu-id="79634-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="79634-172">但是，而不是使用次 Html.ActionLink 从购物车中删除项目，我们将使用 jQuery 来"连接"在此视图中的所有链接，其具有 HTML 类 RemoveLink 的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="79634-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="79634-173">而不是发布窗体，此 click 事件处理程序只需将 AJAX 回调我们 RemoveFromCart 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="79634-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="79634-174">RemoveFromCart 返回 JSON 序列化结果，其中我们 jQuery 回调然后分析并执行四个快速更新为使用 jQuery 的页：</span><span class="sxs-lookup"><span data-stu-id="79634-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="79634-175">从列表中移除已删除的唱片集</span><span class="sxs-lookup"><span data-stu-id="79634-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="79634-176">更新标头中的购物车计数</span><span class="sxs-lookup"><span data-stu-id="79634-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="79634-177">向用户显示一更新消息</span><span class="sxs-lookup"><span data-stu-id="79634-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="79634-178">更新购物车总价格</span><span class="sxs-lookup"><span data-stu-id="79634-178">Updates the cart total price</span></span>

<span data-ttu-id="79634-179">因为索引视图中的 Ajax 回调处理删除方案，我们不需要 RemoveFromCart 操作的其他视图。</span><span class="sxs-lookup"><span data-stu-id="79634-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="79634-180">下面是 /ShoppingCart/Index 视图的完整代码：</span><span class="sxs-lookup"><span data-stu-id="79634-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="79634-181">若要测试此项，我们需要能够将项目添加到我们的购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="79634-182">我们将更新我们**存储详细信息**视图包括"添加到购物车"按钮。</span><span class="sxs-lookup"><span data-stu-id="79634-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="79634-183">当我们解决一下时，我们可以包括一些我们已添加了唱片集其他信息由于我们上次更新此视图： 流派、 艺术家、 价格和唱片集画面。</span><span class="sxs-lookup"><span data-stu-id="79634-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="79634-184">此时将显示更新的存储详细信息查看代码，如下面所示。</span><span class="sxs-lookup"><span data-stu-id="79634-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="79634-185">现在我们可以单击通过应用商店和测试中添加和删除专辑与我们的购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="79634-186">运行应用程序，并浏览到存储索引。</span><span class="sxs-lookup"><span data-stu-id="79634-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="79634-187">接下来，单击一种风格，若要查看的唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="79634-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="79634-188">现在单击唱片集标题显示我们已更新的唱片集详细信息视图，包括"添加到购物车"按钮。</span><span class="sxs-lookup"><span data-stu-id="79634-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="79634-189">单击"添加到购物车"按钮显示我们购物车索引视图中的，购物车摘要列表。</span><span class="sxs-lookup"><span data-stu-id="79634-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="79634-190">在加载了您的购物车之后, 你可以单击删除购物车链接以查看您的购物车的 Ajax 更新。</span><span class="sxs-lookup"><span data-stu-id="79634-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="79634-191">我们已构建了一个有效的购物车这样未注册的用户将项添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="79634-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="79634-192">在以下部分中，我们将允许用户注册并完成结帐过程。</span><span class="sxs-lookup"><span data-stu-id="79634-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="79634-193">[上一页](mvc-music-store-part-7.md)
> [下一页](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="79634-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
