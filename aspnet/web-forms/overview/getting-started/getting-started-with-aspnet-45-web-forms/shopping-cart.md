---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 购物车 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 00fd00778477bea21add76c799dbfe24dfdec1dc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816997"
---
<a name="shopping-cart"></a><span data-ttu-id="7cea9-103">购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-103">Shopping Cart</span></span>
====================
<span data-ttu-id="7cea9-104">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="7cea9-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="7cea9-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="7cea9-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="7cea9-106">此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="7cea9-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="7cea9-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。</span><span class="sxs-lookup"><span data-stu-id="7cea9-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="7cea9-108">本教程介绍将购物车添加到 Wingtip Toys 示例 ASP.NET Web 窗体应用程序所需的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="7cea9-108">This tutorial describes the business logic required to add a shopping cart to the Wingtip Toys sample ASP.NET Web Forms application.</span></span> <span data-ttu-id="7cea9-109">本教程基于上一教程"显示数据的项和详细信息"，而是 Wingtip Toy 存储教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="7cea9-109">This tutorial builds on the previous tutorial "Display Data Items and Details" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="7cea9-110">完成本教程后，对示例应用的用户将能够添加、 删除和修改在其购物车中的产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-110">When you've completed this tutorial, the users of your sample app will be able to add, remove, and modify the products in their shopping cart.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7cea9-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="7cea9-111">What you'll learn:</span></span>

1. <span data-ttu-id="7cea9-112">如何创建 web 应用程序的购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-112">How to create a shopping cart for the web application.</span></span>
2. <span data-ttu-id="7cea9-113">如何使用户能够将项添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-113">How to enable users to add items to the shopping cart.</span></span>
3. <span data-ttu-id="7cea9-114">How to add [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控件来显示购物车详细信息。</span><span class="sxs-lookup"><span data-stu-id="7cea9-114">How to add a [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) control to display shopping cart details.</span></span>
4. <span data-ttu-id="7cea9-115">如何计算和显示订单总计。</span><span class="sxs-lookup"><span data-stu-id="7cea9-115">How to calculate and display the order total.</span></span>
5. <span data-ttu-id="7cea9-116">如何删除和更新购物车中的项目。</span><span class="sxs-lookup"><span data-stu-id="7cea9-116">How to remove and update items in the shopping cart.</span></span>
6. <span data-ttu-id="7cea9-117">如何包括购物车计数器。</span><span class="sxs-lookup"><span data-stu-id="7cea9-117">How to include a shopping cart counter.</span></span>

## <a name="code-features-in-this-tutorial"></a><span data-ttu-id="7cea9-118">在本教程中的代码功能：</span><span class="sxs-lookup"><span data-stu-id="7cea9-118">Code features in this tutorial:</span></span>

1. <span data-ttu-id="7cea9-119">实体框架代码优先</span><span class="sxs-lookup"><span data-stu-id="7cea9-119">Entity Framework Code First</span></span>
2. <span data-ttu-id="7cea9-120">数据注释</span><span class="sxs-lookup"><span data-stu-id="7cea9-120">Data Annotations</span></span>
3. <span data-ttu-id="7cea9-121">强类型数据控件</span><span class="sxs-lookup"><span data-stu-id="7cea9-121">Strongly typed data controls</span></span>
4. <span data-ttu-id="7cea9-122">模型绑定</span><span class="sxs-lookup"><span data-stu-id="7cea9-122">Model binding</span></span>

## <a name="creating-a-shopping-cart"></a><span data-ttu-id="7cea9-123">创建购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-123">Creating a Shopping Cart</span></span>

<span data-ttu-id="7cea9-124">前面在本系列教程，您可以添加页面和代码，以查看数据库中的产品数据。</span><span class="sxs-lookup"><span data-stu-id="7cea9-124">Earlier in this tutorial series, you added pages and code to view product data from a database.</span></span> <span data-ttu-id="7cea9-125">在本教程中，你将创建购物车管理产品的用户有兴趣购买。</span><span class="sxs-lookup"><span data-stu-id="7cea9-125">In this tutorial, you'll create a shopping cart to manage the products that users are interested in buying.</span></span> <span data-ttu-id="7cea9-126">用户将能够浏览并将项添加到购物车，即使它们未注册或登录。</span><span class="sxs-lookup"><span data-stu-id="7cea9-126">Users will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="7cea9-127">若要管理购物车访问，你会将用户分配一个唯一`ID`首次使用全局唯一标识符 (GUID)，当用户访问购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-127">To manage shopping cart access, you will assign users a unique `ID` using a globally unique identifier (GUID) when the user accesses the shopping cart for the first time.</span></span> <span data-ttu-id="7cea9-128">将存储此`ID`使用 ASP.NET 会话状态。</span><span class="sxs-lookup"><span data-stu-id="7cea9-128">You'll store this `ID` using the ASP.NET Session state.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7cea9-129">ASP.NET 会话状态是很方便地存储在用户离开站点将到期的特定于用户的信息。</span><span class="sxs-lookup"><span data-stu-id="7cea9-129">The ASP.NET Session state is a convenient place to store user-specific information which will expire after the user leaves the site.</span></span> <span data-ttu-id="7cea9-130">虽然不恰当使用会话状态的可能较大的站点上会影响性能，打造出色会话状态适用于演示目的的使用。</span><span class="sxs-lookup"><span data-stu-id="7cea9-130">While misuse of session state can have performance implications on larger sites, light use of session state works well for demonstration purposes.</span></span> <span data-ttu-id="7cea9-131">Wingtip Toys 示例项目演示如何使用会话状态而无需外部提供程序，其中会话状态是存储的进程内托管站点的 web 服务器上。</span><span class="sxs-lookup"><span data-stu-id="7cea9-131">The Wingtip Toys sample project shows how to use session state without an external provider, where session state is stored in-process on the web server hosting the site.</span></span> <span data-ttu-id="7cea9-132">提供应用程序的多个实例的大型站点或不同服务器运行的应用程序的多个实例的站点，请考虑使用**Windows Azure 缓存服务**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-132">For larger sites that provide multiple instances of an application or for sites that run multiple instances of an application on different servers, consider using **Windows Azure Cache Service**.</span></span> <span data-ttu-id="7cea9-133">此缓存服务提供的分布式缓存服务的外部 web 站点且解决了使用进程内会话状态的问题。</span><span class="sxs-lookup"><span data-stu-id="7cea9-133">This Cache Service provides a distributed caching service that is external to the web site and solves the problem of using in-process session state.</span></span> <span data-ttu-id="7cea9-134">有关详细信息，请参阅[如何将 ASP.NET 会话状态与 Windows Azure Web Sites](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。</span><span class="sxs-lookup"><span data-stu-id="7cea9-134">For more information see, [How to Use ASP.NET Session State with Windows Azure Web Sites](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider).</span></span>


### <a name="add-cartitem-as-a-model-class"></a><span data-ttu-id="7cea9-135">将 CartItem 添加为 Model 类</span><span class="sxs-lookup"><span data-stu-id="7cea9-135">Add CartItem as a Model Class</span></span>

<span data-ttu-id="7cea9-136">通过创建在本系列教程的前面定义的类别和产品数据的架构`Category`并`Product`中的类*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cea9-136">Earlier in this tutorial series, you defined the schema for the category and product data by creating the `Category` and `Product` classes in the *Models* folder.</span></span> <span data-ttu-id="7cea9-137">现在，添加了新类来定义购物车的架构。</span><span class="sxs-lookup"><span data-stu-id="7cea9-137">Now, add a new class to define the schema for the shopping cart.</span></span> <span data-ttu-id="7cea9-138">稍后在本教程中，你将添加用于处理对数据访问类`CartItem`表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-138">Later in this tutorial, you will add a class to handle data access to the `CartItem` table.</span></span> <span data-ttu-id="7cea9-139">此类将提供用于添加、 删除和更新购物车中的项目的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="7cea9-139">This class will provide the business logic to add, remove, and update items in the shopping cart.</span></span>

1. <span data-ttu-id="7cea9-140">右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-140">Right-click the *Models* folder and select **Add** -&gt; **New Item**.</span></span> 

    ![购物车-新项](shopping-cart/_static/image1.png)
2. <span data-ttu-id="7cea9-142">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="7cea9-142">The **Add New Item** dialog box is displayed.</span></span> <span data-ttu-id="7cea9-143">选择**代码**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-143">Select **Code**, and then select **Class**.</span></span> 

    ![购物车中的添加新项对话框](shopping-cart/_static/image2.png)
3. <span data-ttu-id="7cea9-145">此新类命名*CartItem.cs*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-145">Name this new class *CartItem.cs*.</span></span>
4. <span data-ttu-id="7cea9-146">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-146">Click **Add**.</span></span>  
   <span data-ttu-id="7cea9-147">在编辑器中显示新类文件中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-147">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="7cea9-148">默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7cea9-148">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

<span data-ttu-id="7cea9-149">`CartItem`类包含将定义每个用户添加到购物车产品的架构。</span><span class="sxs-lookup"><span data-stu-id="7cea9-149">The `CartItem` class contains the schema that will define each product a user adds to the shopping cart.</span></span> <span data-ttu-id="7cea9-150">此类是类似于您在本系列教程前面创建的其他架构类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-150">This class is similar to the other schema classes you created earlier in this tutorial series.</span></span> <span data-ttu-id="7cea9-151">按照约定，Entity Framework Code First 期望的主键`CartItem`表将`CartItemId`或`ID`。</span><span class="sxs-lookup"><span data-stu-id="7cea9-151">By convention, Entity Framework Code First expects that the primary key for the `CartItem` table will be either `CartItemId` or `ID`.</span></span> <span data-ttu-id="7cea9-152">但是，代码将使用数据批注覆盖默认行为`[Key]`属性。</span><span class="sxs-lookup"><span data-stu-id="7cea9-152">However, the code overrides the default behavior by using the data annotation `[Key]` attribute.</span></span> <span data-ttu-id="7cea9-153">`Key` ItemId 属性特性指定`ItemID`属性是主键。</span><span class="sxs-lookup"><span data-stu-id="7cea9-153">The `Key` attribute of the ItemId property specifies that the `ItemID` property is the primary key.</span></span>

<span data-ttu-id="7cea9-154">`CartId`属性指定`ID`与要购买的项相关联的用户。</span><span class="sxs-lookup"><span data-stu-id="7cea9-154">The `CartId` property specifies the `ID` of the user that is associated with the item to purchase.</span></span> <span data-ttu-id="7cea9-155">将添加代码以创建此用户`ID`当用户访问购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-155">You'll add code to create this user `ID` when the user accesses the shopping cart.</span></span> <span data-ttu-id="7cea9-156">这`ID`也将存储为 ASP.NET 会话变量。</span><span class="sxs-lookup"><span data-stu-id="7cea9-156">This `ID` will also be stored as an ASP.NET Session variable.</span></span>

### <a name="update-the-product-context"></a><span data-ttu-id="7cea9-157">更新产品上下文</span><span class="sxs-lookup"><span data-stu-id="7cea9-157">Update the Product Context</span></span>

<span data-ttu-id="7cea9-158">除了添加`CartItem`类，您将需要更新数据库上下文类，管理的实体类并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="7cea9-158">In addition to adding the `CartItem` class, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="7cea9-159">若要执行此操作，您将添加新创建`CartItem`模型类到`ProductContext`类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-159">To do this, you will add the newly created `CartItem` model class to the `ProductContext` class.</span></span>

1. <span data-ttu-id="7cea9-160">在中**解决方案资源管理器**，找到并打开*ProductContext.cs*文件中*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cea9-160">In **Solution Explorer**, find and open the *ProductContext.cs* file in the *Models* folder.</span></span>
2. <span data-ttu-id="7cea9-161">添加到突出显示的代码*ProductContext.cs*文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7cea9-161">Add the highlighted code to the *ProductContext.cs* file as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

<span data-ttu-id="7cea9-162">如以前在此教程系列中的代码中所述*ProductContext.cs*文件将添加`System.Data.Entity`命名空间，以便有权访问的实体框架的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="7cea9-162">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="7cea9-163">此功能包括查询、 插入、 更新和删除通过使用强类型化对象数据的功能。</span><span class="sxs-lookup"><span data-stu-id="7cea9-163">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="7cea9-164">`ProductContext`类将访问权限添加到新添加`CartItem`的模型。</span><span class="sxs-lookup"><span data-stu-id="7cea9-164">The `ProductContext` class adds access to the newly added `CartItem` model class.</span></span>

### <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="7cea9-165">管理购物车业务逻辑</span><span class="sxs-lookup"><span data-stu-id="7cea9-165">Managing the Shopping Cart Business Logic</span></span>

<span data-ttu-id="7cea9-166">接下来，将创建`ShoppingCart`中的新类*逻辑*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cea9-166">Next, you'll create the `ShoppingCart` class in a new *Logic* folder.</span></span> <span data-ttu-id="7cea9-167">`ShoppingCart`类处理的数据访问`CartItem`表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-167">The `ShoppingCart` class handles data access to the `CartItem` table.</span></span> <span data-ttu-id="7cea9-168">类还将包括业务逻辑，可添加、 删除和更新购物车中的项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-168">The class will also include the business logic to add, remove, and update items in the shopping cart.</span></span>

<span data-ttu-id="7cea9-169">您将添加的购物车逻辑将包含的功能来管理以下操作：</span><span class="sxs-lookup"><span data-stu-id="7cea9-169">The shopping cart logic that you will add will contain the functionality to manage the following actions:</span></span>

1. <span data-ttu-id="7cea9-170">将项添加到购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-170">Adding items to the shopping cart</span></span>
2. <span data-ttu-id="7cea9-171">从购物车中删除项</span><span class="sxs-lookup"><span data-stu-id="7cea9-171">Removing items from the shopping cart</span></span>
3. <span data-ttu-id="7cea9-172">获取购物车 ID</span><span class="sxs-lookup"><span data-stu-id="7cea9-172">Getting the shopping cart ID</span></span>
4. <span data-ttu-id="7cea9-173">正在从购物车检索项目</span><span class="sxs-lookup"><span data-stu-id="7cea9-173">Retrieving items from the shopping cart</span></span>
5. <span data-ttu-id="7cea9-174">合计购物车商品的量</span><span class="sxs-lookup"><span data-stu-id="7cea9-174">Totaling the amount of all the shopping cart items</span></span>
6. <span data-ttu-id="7cea9-175">正在更新购物车数据</span><span class="sxs-lookup"><span data-stu-id="7cea9-175">Updating the shopping cart data</span></span>

<span data-ttu-id="7cea9-176">购物车页 (*ShoppingCart.aspx*) 并且将一起使用的购物车类来访问购物车数据。</span><span class="sxs-lookup"><span data-stu-id="7cea9-176">A shopping cart page (*ShoppingCart.aspx*) and the shopping cart class will be used together to access shopping cart data.</span></span> <span data-ttu-id="7cea9-177">购物车页将显示用户将添加到购物车的所有项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-177">The shopping cart page will display all the items the user adds to the shopping cart.</span></span> <span data-ttu-id="7cea9-178">除了购物车页和类，你将创建一个页 (*AddToCart.aspx*) 若要将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-178">Besides the shopping cart page and class, you'll create a page (*AddToCart.aspx*) to add products to the shopping cart.</span></span> <span data-ttu-id="7cea9-179">您还将添加到代码*ProductList.aspx*页和*ProductDetails.aspx*将提供一个指向页*AddToCart.aspx*页上，以便用户可以添加放入购物车产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-179">You will also add code to the *ProductList.aspx* page and the *ProductDetails.aspx* page that will provide a link to the *AddToCart.aspx* page, so that the user can add products to the shopping cart.</span></span>

<span data-ttu-id="7cea9-180">下图显示了当用户将产品添加到购物车时出现的基本过程。</span><span class="sxs-lookup"><span data-stu-id="7cea9-180">The following diagram shows the basic process that occurs when the user adds a product to the shopping cart.</span></span>

![购物车-将添加到购物车](shopping-cart/_static/image3.png)

<span data-ttu-id="7cea9-182">当用户单击**添加到购物车**任一链接*ProductList.aspx*页或*ProductDetails.aspx*页上，应用程序将导航到*AddToCart.aspx*页，然后自动向*ShoppingCart.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-182">When the user clicks the **Add To Cart** link on either the *ProductList.aspx* page or the *ProductDetails.aspx* page, the application will navigate to the *AddToCart.aspx* page and then automatically to the *ShoppingCart.aspx* page.</span></span> <span data-ttu-id="7cea9-183">*AddToCart.aspx*页将购物车类中调用方法来向购物车添加选择产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-183">The *AddToCart.aspx* page will add the select product to the shopping cart by calling a method in the ShoppingCart class.</span></span> <span data-ttu-id="7cea9-184">*ShoppingCart.aspx*页将显示已添加到购物车的产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-184">The *ShoppingCart.aspx* page will display the products that have been added to the shopping cart.</span></span>

#### <a name="creating-the-shopping-cart-class"></a><span data-ttu-id="7cea9-185">创建购物车类</span><span class="sxs-lookup"><span data-stu-id="7cea9-185">Creating the Shopping Cart Class</span></span>

<span data-ttu-id="7cea9-186">`ShoppingCart`类将添加到应用程序中单独的文件夹，以便将模型 （模型文件夹）、 页面 （根文件夹） 和逻辑 （逻辑文件夹） 之间的明显区别。</span><span class="sxs-lookup"><span data-stu-id="7cea9-186">The `ShoppingCart` class will be added to a separate folder in the application so that there will be a clear distinction between the model (Models folder), the pages (root folder) and the logic (Logic folder).</span></span>

1. <span data-ttu-id="7cea9-187">在中**解决方案资源管理器**，右键单击**WingtipToys**项目，然后选择**添加**-&gt;**新文件夹**.</span><span class="sxs-lookup"><span data-stu-id="7cea9-187">In **Solution Explorer**, right-click the **WingtipToys**project and select **Add**-&gt;**New Folder**.</span></span> <span data-ttu-id="7cea9-188">将新文件夹命名*逻辑*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-188">Name the new folder *Logic*.</span></span>
2. <span data-ttu-id="7cea9-189">右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-189">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>
3. <span data-ttu-id="7cea9-190">添加名为的新类文件*ShoppingCartActions.cs*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-190">Add a new class file named *ShoppingCartActions.cs*.</span></span>
4. <span data-ttu-id="7cea9-191">默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7cea9-191">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

<span data-ttu-id="7cea9-192">`AddToCart`方法使单个产品要基于的产品在购物车包含`ID`。</span><span class="sxs-lookup"><span data-stu-id="7cea9-192">The `AddToCart` method enables individual products to be included in the shopping cart based on the product `ID`.</span></span> <span data-ttu-id="7cea9-193">产品添加到购物车中，或如果购物车已包含该产品的项，递增数量。</span><span class="sxs-lookup"><span data-stu-id="7cea9-193">The product is added to the cart, or if the cart already contains an item for that product, the quantity is incremented.</span></span>

<span data-ttu-id="7cea9-194">`GetCartId`方法返回在购物车`ID`用户。</span><span class="sxs-lookup"><span data-stu-id="7cea9-194">The `GetCartId` method returns the cart `ID` for the user.</span></span> <span data-ttu-id="7cea9-195">购物车`ID`用于跟踪用户已在其购物车中的项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-195">The cart `ID` is used to track the items that a user has in their shopping cart.</span></span> <span data-ttu-id="7cea9-196">如果用户不具有现有购物车`ID`，新车`ID`为其创建。</span><span class="sxs-lookup"><span data-stu-id="7cea9-196">If the user does not have an existing cart `ID`, a new cart `ID` is created for them.</span></span> <span data-ttu-id="7cea9-197">如果用户作为已注册用户，在购物车登录`ID`设置为其用户名称。</span><span class="sxs-lookup"><span data-stu-id="7cea9-197">If the user is signed in as a registered user, the cart `ID` is set to their user name.</span></span> <span data-ttu-id="7cea9-198">但是，如果用户未登录，在购物车`ID`设置为唯一值 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="7cea9-198">However, if the user is not signed in, the cart `ID` is set to a unique value (a GUID).</span></span> <span data-ttu-id="7cea9-199">GUID 可确保为每个用户，基于在会话上创建该只有一个购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-199">A GUID ensures that only one cart is created for each user, based on session.</span></span>

<span data-ttu-id="7cea9-200">`GetCartItems`方法返回的购物车商品的用户列表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-200">The `GetCartItems` method returns a list of shopping cart items for the user.</span></span> <span data-ttu-id="7cea9-201">稍后在本教程中，你将看到模型绑定用于显示购物车使用中的购物车项`GetCartItems`方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-201">Later in this tutorial, you will see that model binding is used to display the cart items in the shopping cart using the `GetCartItems` method.</span></span>

### <a name="creating-the-add-to-cart-functionality"></a><span data-ttu-id="7cea9-202">创建到车添加功能</span><span class="sxs-lookup"><span data-stu-id="7cea9-202">Creating the Add-To-Cart Functionality</span></span>

<span data-ttu-id="7cea9-203">前面曾提到，您将创建一个名为处理页*AddToCart.aspx*将用于将新产品添加到用户的购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-203">As mentioned earlier, you will create a processing page named *AddToCart.aspx* that will be used to add new products to the shopping cart of the user.</span></span> <span data-ttu-id="7cea9-204">此页将调用`AddToCart`中的方法`ShoppingCart`刚创建的类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-204">This page will call the `AddToCart` method in the `ShoppingCart` class that you just created.</span></span> <span data-ttu-id="7cea9-205">*AddToCart.aspx*页将期望的产品`ID`传递给它。</span><span class="sxs-lookup"><span data-stu-id="7cea9-205">The *AddToCart.aspx* page will expect that a product `ID` is passed to it.</span></span> <span data-ttu-id="7cea9-206">此产品`ID`调用时将使用`AddToCart`中的方法`ShoppingCart`类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-206">This product `ID` will be used when calling the `AddToCart` method in the `ShoppingCart` class.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7cea9-207">您将修改代码隐藏 (*AddToCart.aspx.cs*) 的此页上，不是在页面 UI (*AddToCart.aspx*)。</span><span class="sxs-lookup"><span data-stu-id="7cea9-207">You will be modifying the code-behind (*AddToCart.aspx.cs*) for this page, not the page UI (*AddToCart.aspx*).</span></span>


#### <a name="to-create-the-add-to-cart-functionality"></a><span data-ttu-id="7cea9-208">若要创建添加车功能：</span><span class="sxs-lookup"><span data-stu-id="7cea9-208">To create the Add-To-Cart functionality:</span></span>

1. <span data-ttu-id="7cea9-209">在中**解决方案资源管理器**，右键单击**WingtipToys**项目，然后单击**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-209">In **Solution Explorer**, right-click the **WingtipToys**project, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="7cea9-210">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="7cea9-210">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="7cea9-211">将标准的新页 （Web 窗体） 添加到名为应用程序*AddToCart.aspx*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-211">Add a standard new page (Web Form) to the application named *AddToCart.aspx*.</span></span> 

    ![购物车-添加 Web 窗体](shopping-cart/_static/image4.png)
3. <span data-ttu-id="7cea9-213">在中**解决方案资源管理器**，右键单击*AddToCart.aspx*页，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-213">In **Solution Explorer**, right-click the *AddToCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="7cea9-214">*AddToCart.aspx.cs*在编辑器中打开代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="7cea9-214">The *AddToCart.aspx.cs* code-behind file is opened in the editor.</span></span>
4. <span data-ttu-id="7cea9-215">中的现有代码替换*AddToCart.aspx.cs*以下的代码隐藏：</span><span class="sxs-lookup"><span data-stu-id="7cea9-215">Replace the existing code in the *AddToCart.aspx.cs* code-behind with the following:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

<span data-ttu-id="7cea9-216">当*AddToCart.aspx*加载页面时，该产品`ID`检索查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-216">When the *AddToCart.aspx* page is loaded, the product `ID` is retrieved from the query string.</span></span> <span data-ttu-id="7cea9-217">接下来，创建购物车类的实例并用于调用`AddToCart`在本教程前面部分添加的方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-217">Next, an instance of the shopping cart class is created and used to call the `AddToCart` method that you added earlier in this tutorial.</span></span> <span data-ttu-id="7cea9-218">`AddToCart`中包含的方法*ShoppingCartActions.cs*文件中，包括逻辑，用于将所选的产品添加到购物车或递增的所选产品的产品数量。</span><span class="sxs-lookup"><span data-stu-id="7cea9-218">The `AddToCart` method, contained in the *ShoppingCartActions.cs* file, includes the logic to add the selected product to the shopping cart or increment the product quantity of the selected product.</span></span> <span data-ttu-id="7cea9-219">如果尚未添加到购物车产品，产品添加到`CartItem`数据库表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-219">If the product hasn't been added to the shopping cart, the product is added to the `CartItem` table of the database.</span></span> <span data-ttu-id="7cea9-220">如果已添加到购物车产品，用户将添加同一产品的其他项中递增的产品数量`CartItem`表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-220">If the product has already been added to the shopping cart and the user adds an additional item of the same product, the product quantity is incremented in the `CartItem` table.</span></span> <span data-ttu-id="7cea9-221">最后，页面将重定向回到*ShoppingCart.aspx*将添加下一步，其中用户会看到在购物车中的项的更新的列表中的页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-221">Finally, the page redirects back to the *ShoppingCart.aspx* page that you'll add in the next step, where the user sees an updated list of items in the cart.</span></span>

<span data-ttu-id="7cea9-222">如前面所述，用户`ID`用于标识与特定用户关联的产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-222">As previously mentioned, a user `ID` is used to identify the products that are associated with a specific user.</span></span> <span data-ttu-id="7cea9-223">这`ID`添加到中的行`CartItem`表每次用户将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-223">This `ID` is added to a row in the `CartItem` table each time the user adds a product to the shopping cart.</span></span>

### <a name="creating-the-shopping-cart-ui"></a><span data-ttu-id="7cea9-224">创建购物车 UI</span><span class="sxs-lookup"><span data-stu-id="7cea9-224">Creating the Shopping Cart UI</span></span>

<span data-ttu-id="7cea9-225">*ShoppingCart.aspx*页将显示用户添加到购物车的产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-225">The *ShoppingCart.aspx* page will display the products that the user has added to their shopping cart.</span></span> <span data-ttu-id="7cea9-226">它还将提供添加、 删除和更新购物车中的项的功能。</span><span class="sxs-lookup"><span data-stu-id="7cea9-226">It will also provide the ability to add, remove and update items in the shopping cart.</span></span>

1. <span data-ttu-id="7cea9-227">在中**解决方案资源管理器**，右键单击**WingtipToys**，单击**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-227">In **Solution Explorer**, right-click **WingtipToys**, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="7cea9-228">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="7cea9-228">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="7cea9-229">添加新页面 （Web 窗体），通过选择包含一个母版页**使用母版页的 Web 窗体**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-229">Add a new page (Web Form) that includes a master page by selecting **Web Form using Master Page**.</span></span> <span data-ttu-id="7cea9-230">命名新页面*ShoppingCart.aspx*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-230">Name the new page *ShoppingCart.aspx*.</span></span>
3. <span data-ttu-id="7cea9-231">选择**Site.Master**附加到新创建的母版页 *.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-231">Select **Site.Master** to attach the master page to the newly created *.aspx* page.</span></span>
4. <span data-ttu-id="7cea9-232">在中*ShoppingCart.aspx*页上，将现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="7cea9-232">In the *ShoppingCart.aspx* page, replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

<span data-ttu-id="7cea9-233">*ShoppingCart.aspx*页包含**GridView**控件命名为`CartList`。</span><span class="sxs-lookup"><span data-stu-id="7cea9-233">The *ShoppingCart.aspx* page includes a **GridView** control named `CartList`.</span></span> <span data-ttu-id="7cea9-234">此控件使用模型绑定将购物车数据绑定到数据库中**GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="7cea9-234">This control uses model binding to bind the shopping cart data from the database to the **GridView** control.</span></span> <span data-ttu-id="7cea9-235">当您将设置`ItemType`的属性**GridView**控件，数据绑定表达式`Item`现已推出将成为强类型化的控件和控件的标记。</span><span class="sxs-lookup"><span data-stu-id="7cea9-235">When you set the `ItemType` property of the **GridView** control, the data-binding expression `Item` is available in the markup of the control and the control becomes strongly typed.</span></span> <span data-ttu-id="7cea9-236">如本系列教程前面所述，可以选择的详细信息`Item`对象使用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="7cea9-236">As mentioned earlier in this tutorial series, you can select details of the `Item` object using IntelliSense.</span></span> <span data-ttu-id="7cea9-237">若要配置数据控件，以使用模型绑定选择数据，请设置`SelectMethod`控件的属性。</span><span class="sxs-lookup"><span data-stu-id="7cea9-237">To configure a data control to use model binding to select data, you set the `SelectMethod` property of the control.</span></span> <span data-ttu-id="7cea9-238">在上面的标记中，您设置`SelectMethod`若要使用 GetShoppingCartItems 方法可返回一系列`CartItem`对象。</span><span class="sxs-lookup"><span data-stu-id="7cea9-238">In the markup above, you set the `SelectMethod` to use the GetShoppingCartItems method which returns a list of `CartItem` objects.</span></span> <span data-ttu-id="7cea9-239">**GridView**数据控件在页生命周期中的适当时间调用方法，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="7cea9-239">The **GridView** data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="7cea9-240">`GetShoppingCartItems`仍将添加的方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-240">The `GetShoppingCartItems` method must still be added.</span></span>

#### <a name="retrieving-the-shopping-cart-items"></a><span data-ttu-id="7cea9-241">检索购物车商品</span><span class="sxs-lookup"><span data-stu-id="7cea9-241">Retrieving the Shopping Cart Items</span></span>

<span data-ttu-id="7cea9-242">接下来，您将代码添加到*ShoppingCart.aspx.cs*隐藏代码检索并填充购物车 UI。</span><span class="sxs-lookup"><span data-stu-id="7cea9-242">Next, you add code to the *ShoppingCart.aspx.cs* code-behind to retrieve and populate the Shopping Cart UI.</span></span>

1. <span data-ttu-id="7cea9-243">在中**解决方案资源管理器**，右键单击*ShoppingCart.aspx*页，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-243">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="7cea9-244">*ShoppingCart.aspx.cs*在编辑器中打开代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="7cea9-244">The *ShoppingCart.aspx.cs* code-behind file is opened in the editor.</span></span>
2. <span data-ttu-id="7cea9-245">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7cea9-245">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

<span data-ttu-id="7cea9-246">如前面所述`GridView`数据控件调用`GetShoppingCartItems`方法在适当的时间在页生命周期并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="7cea9-246">As mentioned above, the `GridView` data control calls the `GetShoppingCartItems` method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="7cea9-247">`GetShoppingCartItems`方法创建的一个实例`ShoppingCartActions`对象。</span><span class="sxs-lookup"><span data-stu-id="7cea9-247">The `GetShoppingCartItems` method creates an instance of the `ShoppingCartActions` object.</span></span> <span data-ttu-id="7cea9-248">然后，代码使用该实例在购物车中返回的项，通过调用`GetCartItems`方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-248">Then, the code uses that instance to return the items in the cart by calling the `GetCartItems` method.</span></span>

### <a name="adding-products-to-the-shopping-cart"></a><span data-ttu-id="7cea9-249">将产品添加到购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-249">Adding Products to the Shopping Cart</span></span>

<span data-ttu-id="7cea9-250">当任一*ProductList.aspx*或*ProductDetails.aspx*显示页面，用户将能够将产品添加到购物车使用的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-250">When either the *ProductList.aspx* or the *ProductDetails.aspx* page is displayed, the user will be able to add the product to the shopping cart using a link.</span></span> <span data-ttu-id="7cea9-251">当他们单击链接时，该应用程序导航到名为处理页面*AddToCart.aspx*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-251">When they click the link, the application navigates to the processing page named *AddToCart.aspx*.</span></span> <span data-ttu-id="7cea9-252">*AddToCart.aspx*页将调用`AddToCart`中的方法`ShoppingCart`在本教程前面部分添加的类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-252">The *AddToCart.aspx* page will call the `AddToCart` method in the `ShoppingCart` class that you added earlier in this tutorial.</span></span>

<span data-ttu-id="7cea9-253">现在，您将添加**添加到购物车**指向同时*ProductList.aspx*页并*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-253">Now, you'll add an **Add to Cart** link to both the *ProductList.aspx* page and the *ProductDetails.aspx* page.</span></span> <span data-ttu-id="7cea9-254">此链接将包括该产品`ID`从数据库中检索的。</span><span class="sxs-lookup"><span data-stu-id="7cea9-254">This link will include the product `ID` that is retrieved from the database.</span></span>

1. <span data-ttu-id="7cea9-255">在中**解决方案资源管理器**，找到并打开名为的页*ProductList.aspx*。</span><span class="sxs-lookup"><span data-stu-id="7cea9-255">In **Solution Explorer**, find and open the page named *ProductList.aspx*.</span></span>
2. <span data-ttu-id="7cea9-256">添加到的黄色突出显示的标记*ProductList.aspx*页上，以便整个页面显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7cea9-256">Add the markup highlighted in yellow to the *ProductList.aspx* page so that the entire page appears as follows:</span></span>  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a><span data-ttu-id="7cea9-257">测试购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-257">Testing the Shopping Cart</span></span>

<span data-ttu-id="7cea9-258">运行应用程序，请参阅如何将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-258">Run the application to see how you add products to the shopping cart.</span></span>

1. <span data-ttu-id="7cea9-259">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cea9-259">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="7cea9-260">项目重新创建数据库后，浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-260">After the project recreates the database, the browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="7cea9-261">选择**汽车**类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-261">Select **Cars** from the category navigation menu.</span></span>  
 <span data-ttu-id="7cea9-262">*ProductList.aspx*显示仅"Cars"类别中包含的产品显示页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-262">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> 

    ![购物车的汽车](shopping-cart/_static/image5.png)
3. <span data-ttu-id="7cea9-264">单击**添加到购物车**链接旁边的第一个产品列出 (转换 car)。</span><span class="sxs-lookup"><span data-stu-id="7cea9-264">Click the **Add to Cart** link next to the first product listed (the convertible car).</span></span>   
 <span data-ttu-id="7cea9-265">*ShoppingCart.aspx*显示页面时，在您的购物车中显示所选内容。</span><span class="sxs-lookup"><span data-stu-id="7cea9-265">The *ShoppingCart.aspx* page is displayed, showing the selection in your shopping cart.</span></span> 

    ![购物车的购物车](shopping-cart/_static/image6.png)
4. <span data-ttu-id="7cea9-267">选择查看其他产品**平面**类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-267">View additional products by selecting **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="7cea9-268">单击**添加到购物车**旁边列出的第一个产品的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-268">Click the **Add to Cart** link next to the first product listed.</span></span>  
 <span data-ttu-id="7cea9-269">*ShoppingCart.aspx*页显示与其他项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-269">The *ShoppingCart.aspx* page is displayed with the additional item.</span></span>
6. <span data-ttu-id="7cea9-270">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="7cea9-270">Close the browser.</span></span>

### <a name="calculating-and-displaying-the-order-total"></a><span data-ttu-id="7cea9-271">计算和显示订单总计</span><span class="sxs-lookup"><span data-stu-id="7cea9-271">Calculating and Displaying the Order Total</span></span>

<span data-ttu-id="7cea9-272">除了将产品添加到购物车中，您将添加`GetTotal`方法`ShoppingCart`类，并在购物车页中显示订单总金额。</span><span class="sxs-lookup"><span data-stu-id="7cea9-272">In addition to adding products to the shopping cart, you will add a `GetTotal` method to the `ShoppingCart` class and display the total order amount in the shopping cart page.</span></span>

1. <span data-ttu-id="7cea9-273">在中**解决方案资源管理器**，打开*ShoppingCartActions.cs*文件中*逻辑*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cea9-273">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="7cea9-274">添加以下`GetTotal`方法用到的黄色突出显示`ShoppingCart`类，以便此类显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7cea9-274">Add the following `GetTotal` method highlighted in yellow to the `ShoppingCart` class, so that the class appears as follows:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

<span data-ttu-id="7cea9-275">首先，`GetTotal`方法获取用户的购物车中的 ID。</span><span class="sxs-lookup"><span data-stu-id="7cea9-275">First, the `GetTotal` method gets the ID of the shopping cart for the user.</span></span> <span data-ttu-id="7cea9-276">然后该方法获取购物车总数乘以每个产品在购物车中列出的产品数量的产品价格。</span><span class="sxs-lookup"><span data-stu-id="7cea9-276">Then the method gets the cart total by multiplying the product price by the product quantity for each product listed in the cart.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7cea9-277">上面的代码中使用可以为 null 的类型"`int?`"。</span><span class="sxs-lookup"><span data-stu-id="7cea9-277">The above code uses the nullable type "`int?`".</span></span> <span data-ttu-id="7cea9-278">可以为 null 的类型可以表示为基础类型的也以 null 值的所有值。</span><span class="sxs-lookup"><span data-stu-id="7cea9-278">Nullable types can represent all the values of an underlying type, and also as a null value.</span></span> <span data-ttu-id="7cea9-279">有关详细信息，请参阅[使用可以为 Null 的类型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="7cea9-279">For more information see, [Using Nullable Types](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx).</span></span>


### <a name="modify-the-shopping-cart-display"></a><span data-ttu-id="7cea9-280">修改购物车显示</span><span class="sxs-lookup"><span data-stu-id="7cea9-280">Modify the Shopping Cart Display</span></span>

<span data-ttu-id="7cea9-281">接下来将修改的代码*ShoppingCart.aspx*页面以调`GetTotal`方法，并显示总*ShoppingCart.aspx*页上加载页面时。</span><span class="sxs-lookup"><span data-stu-id="7cea9-281">Next you'll modify the code for the *ShoppingCart.aspx* page to call the `GetTotal` method and display that total on the *ShoppingCart.aspx* page when the page loads.</span></span>

1. <span data-ttu-id="7cea9-282">在中**解决方案资源管理器**，右键单击*ShoppingCart.aspx*页，然后选择**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-282">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and select **View Code**.</span></span>
2. <span data-ttu-id="7cea9-283">在中*ShoppingCart.aspx.cs*文件中，更新`Page_Load`通过添加以下代码以黄色突出显示的处理程序：</span><span class="sxs-lookup"><span data-stu-id="7cea9-283">In the *ShoppingCart.aspx.cs* file, update the `Page_Load` handler by adding the following code highlighted in yellow:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

<span data-ttu-id="7cea9-284">当*ShoppingCart.aspx*加载页面，它将加载购物车对象，然后通过调用中检索的购物车总额`GetTotal`方法的`ShoppingCart`类。</span><span class="sxs-lookup"><span data-stu-id="7cea9-284">When the *ShoppingCart.aspx* page loads, it loads the shopping cart object and then retrieves the shopping cart total by calling the `GetTotal` method of the `ShoppingCart` class.</span></span> <span data-ttu-id="7cea9-285">购物车是否为空，该结果被显示消息。</span><span class="sxs-lookup"><span data-stu-id="7cea9-285">If the shopping cart is empty, a message to that effect is displayed.</span></span>

### <a name="testing-the-shopping-cart-total"></a><span data-ttu-id="7cea9-286">测试的购物车总额</span><span class="sxs-lookup"><span data-stu-id="7cea9-286">Testing the Shopping Cart Total</span></span>

<span data-ttu-id="7cea9-287">运行应用程序现在，请参阅如何您可以不只将产品加入购物车，但您可以看到购物车总额。</span><span class="sxs-lookup"><span data-stu-id="7cea9-287">Run the application now to see how you can not only add a product to the shopping cart, but you can see the shopping cart total.</span></span>

1. <span data-ttu-id="7cea9-288">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cea9-288">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="7cea9-289">在浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-289">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="7cea9-290">选择**汽车**类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-290">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="7cea9-291">单击**添加到购物车**旁边的第一个产品的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-291">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="7cea9-292">*ShoppingCart.aspx*页中显示订单总计。</span><span class="sxs-lookup"><span data-stu-id="7cea9-292">The *ShoppingCart.aspx* page is displayed with the order total.</span></span> 

    ![购物车的购物车总计](shopping-cart/_static/image7.png)
4. <span data-ttu-id="7cea9-294">将一些其他产品 （例如，平面） 添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="7cea9-294">Add some other products (for example, a plane) to the cart.</span></span>
5. <span data-ttu-id="7cea9-295">*ShoppingCart.aspx*页中显示已添加的所有产品更新的总数。</span><span class="sxs-lookup"><span data-stu-id="7cea9-295">The *ShoppingCart.aspx* page is displayed with an updated total for all the products you've added.</span></span> 

    ![购物车的多个产品](shopping-cart/_static/image8.png)
6. <span data-ttu-id="7cea9-297">通过关闭浏览器窗口中停止正在运行的应用。</span><span class="sxs-lookup"><span data-stu-id="7cea9-297">Stop the running app by closing the browser window.</span></span>

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a><span data-ttu-id="7cea9-298">将更新和签出按钮添加到购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-298">Adding Update and Checkout Buttons to the Shopping Cart</span></span>

<span data-ttu-id="7cea9-299">若要允许用户修改购物车，你将添加**更新**按钮和一个**签出**购物车页的按钮。</span><span class="sxs-lookup"><span data-stu-id="7cea9-299">To allow the users to modify the shopping cart, you'll add an **Update** button and a **Checkout** button to the shopping cart page.</span></span> <span data-ttu-id="7cea9-300">**签出**直到更高版本中本系列教程不使用按钮。</span><span class="sxs-lookup"><span data-stu-id="7cea9-300">The **Checkout** button is not used until later in this tutorial series.</span></span>

1. <span data-ttu-id="7cea9-301">在中**解决方案资源管理器**，打开*ShoppingCart.aspx* web 应用程序项目的根目录中的页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-301">In **Solution Explorer**, open the *ShoppingCart.aspx* page in the root of the web application project.</span></span>
2. <span data-ttu-id="7cea9-302">若要添加**更新**按钮并**签出**按钮*ShoppingCart.aspx*页上，添加到的现有标记的黄色突出显示的标记，如中所示以下代码：</span><span class="sxs-lookup"><span data-stu-id="7cea9-302">To add the **Update** button and the **Checkout** button to the *ShoppingCart.aspx* page, add the markup highlighted in yellow to the existing markup, as shown in the following code:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

<span data-ttu-id="7cea9-303">当用户单击**更新**按钮，`UpdateBtn_Click`将调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7cea9-303">When the user clicks the **Update** button, the `UpdateBtn_Click` event handler will be called.</span></span> <span data-ttu-id="7cea9-304">此事件处理程序将调用将在下一步添加的代码。</span><span class="sxs-lookup"><span data-stu-id="7cea9-304">This event handler will call the code that you'll add in the next step.</span></span>

<span data-ttu-id="7cea9-305">接下来，你可以更新中包含的代码*ShoppingCart.aspx.cs*文件，以遍历车商品并调用`RemoveItem`和`UpdateItem`方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-305">Next, you can update the code contained in the *ShoppingCart.aspx.cs* file to loop through the cart items and call the `RemoveItem` and `UpdateItem` methods.</span></span>

1. <span data-ttu-id="7cea9-306">在中**解决方案资源管理器**，打开*ShoppingCart.aspx.cs* web 应用程序项目的根目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="7cea9-306">In **Solution Explorer**, open the *ShoppingCart.aspx.cs* file in the root of the web application project.</span></span>
2. <span data-ttu-id="7cea9-307">添加以下代码部分用到的黄色突出显示*ShoppingCart.aspx.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="7cea9-307">Add the following code sections highlighted in yellow to the *ShoppingCart.aspx.cs* file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

<span data-ttu-id="7cea9-308">当用户单击**更新**按钮*ShoppingCart.aspx*页上，调用 UpdateCartItems 方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-308">When the user clicks the **Update** button on the *ShoppingCart.aspx* page, the UpdateCartItems method is called.</span></span> <span data-ttu-id="7cea9-309">UpdateCartItems 方法获取在购物车中的每个项的更新的值。</span><span class="sxs-lookup"><span data-stu-id="7cea9-309">The UpdateCartItems method gets the updated values for each item in the shopping cart.</span></span> <span data-ttu-id="7cea9-310">然后，UpdateCartItems 方法调用`UpdateShoppingCartDatabase`方法 （添加和下一步中所述） 以添加或从购物车中删除项目。</span><span class="sxs-lookup"><span data-stu-id="7cea9-310">Then, the UpdateCartItems method calls the `UpdateShoppingCartDatabase` method (added and explained in the next step) to either add or remove items from the shopping cart.</span></span> <span data-ttu-id="7cea9-311">更新数据库以反映放入购物车中，更新后**GridView**购物车页上通过调用更新控件`DataBind`方法**GridView**。</span><span class="sxs-lookup"><span data-stu-id="7cea9-311">Once the database has been updated to reflect the updates to the shopping cart, the **GridView** control is updated on the shopping cart page by calling the `DataBind` method for the **GridView**.</span></span> <span data-ttu-id="7cea9-312">此外，订单总金额购物车页上的将更新以反映更新的项列表。</span><span class="sxs-lookup"><span data-stu-id="7cea9-312">Also, the total order amount on the shopping cart page is updated to reflect the updated list of items.</span></span>

### <a name="updating-and-removing-shopping-cart-items"></a><span data-ttu-id="7cea9-313">更新和删除购物车商品</span><span class="sxs-lookup"><span data-stu-id="7cea9-313">Updating and Removing Shopping Cart Items</span></span>

<span data-ttu-id="7cea9-314">上*ShoppingCart.aspx*页中，可以看到已添加控件更新项的数量和删除项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-314">On the *ShoppingCart.aspx* page, you can see controls have been added for updating the quantity of an item and removing an item.</span></span> <span data-ttu-id="7cea9-315">现在，添加将使处理这些控件的代码。</span><span class="sxs-lookup"><span data-stu-id="7cea9-315">Now, add the code that will make these controls work.</span></span>

1. <span data-ttu-id="7cea9-316">在中**解决方案资源管理器**，打开*ShoppingCartActions.cs*文件中*逻辑*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cea9-316">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="7cea9-317">添加以下代码以到黄色突出显示*ShoppingCartActions.cs*类文件：</span><span class="sxs-lookup"><span data-stu-id="7cea9-317">Add the following code highlighted in yellow to the *ShoppingCartActions.cs* class file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

<span data-ttu-id="7cea9-318">`UpdateShoppingCartDatabase`方法，从调用`UpdateCartItems`方法*ShoppingCart.aspx.cs*页上，包含用于更新或从购物车中删除项目的逻辑。</span><span class="sxs-lookup"><span data-stu-id="7cea9-318">The `UpdateShoppingCartDatabase` method, called from the `UpdateCartItems` method on the *ShoppingCart.aspx.cs* page, contains the logic to either update or remove items from the shopping cart.</span></span> <span data-ttu-id="7cea9-319">`UpdateShoppingCartDatabase`方法循环访问购物车列表中的所有行。</span><span class="sxs-lookup"><span data-stu-id="7cea9-319">The `UpdateShoppingCartDatabase` method iterates through all the rows within the shopping cart list.</span></span> <span data-ttu-id="7cea9-320">如果已标记的购物车项被删除，或者数量为小于 1，`RemoveItem`调用方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-320">If a shopping cart item has been marked to be removed, or the quantity is less than one, the `RemoveItem` method is called.</span></span> <span data-ttu-id="7cea9-321">否则，购物车项检查的更新时`UpdateItem`调用方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-321">Otherwise, the shopping cart item is checked for updates when the `UpdateItem` method is called.</span></span> <span data-ttu-id="7cea9-322">已删除或更新购物车项后，在保存数据库更改。</span><span class="sxs-lookup"><span data-stu-id="7cea9-322">After the shopping cart item has been removed or updated, the database changes are saved.</span></span>

<span data-ttu-id="7cea9-323">`ShoppingCartUpdates`结构用来保存所有购物车商品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-323">The `ShoppingCartUpdates` structure is used to hold all the shopping cart items.</span></span> <span data-ttu-id="7cea9-324">`UpdateShoppingCartDatabase`方法使用`ShoppingCartUpdates`结构，以确定任何一项需要更新或删除。</span><span class="sxs-lookup"><span data-stu-id="7cea9-324">The `UpdateShoppingCartDatabase` method uses the `ShoppingCartUpdates` structure to determine if any of the items need to be updated or removed.</span></span>

<span data-ttu-id="7cea9-325">在下一步的教程中，您将使用`EmptyCart`方法清除购物车后购买产品。</span><span class="sxs-lookup"><span data-stu-id="7cea9-325">In the next tutorial, you will use the `EmptyCart` method to clear the shopping cart after purchasing products.</span></span> <span data-ttu-id="7cea9-326">但现在，您将使用`GetCount`刚添加到方法*ShoppingCartActions.cs*文件以确定购物车中有多少项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-326">But for now, you will use the `GetCount` method that you just added to the *ShoppingCartActions.cs* file to determine how many items are in the shopping cart.</span></span>

### <a name="adding-a-shopping-cart-counter"></a><span data-ttu-id="7cea9-327">添加购物车计数器</span><span class="sxs-lookup"><span data-stu-id="7cea9-327">Adding a Shopping Cart Counter</span></span>

<span data-ttu-id="7cea9-328">若要允许用户查看购物车中的项总数，您将添加到计数器*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-328">To allow the user to view the total number of items in the shopping cart, you will add a counter to the *Site.Master* page.</span></span> <span data-ttu-id="7cea9-329">此计数器也将作为放入购物车的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-329">This counter will also act as a link to the shopping cart.</span></span>

1. <span data-ttu-id="7cea9-330">在中**解决方案资源管理器**，打开*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-330">In **Solution Explorer**, open the *Site.Master* page.</span></span>
2. <span data-ttu-id="7cea9-331">通过添加购物车计数器链接，因此，它按如下所示显示黄色再到导航部分中所示修改标记：</span><span class="sxs-lookup"><span data-stu-id="7cea9-331">Modify the markup by adding the shopping cart counter link as shown in yellow to the navigation section so it appears as follows:</span></span>  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. <span data-ttu-id="7cea9-332">接下来，更新的代码隐藏*Site.Master.cs*文件添加，如下所示以黄色突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="7cea9-332">Next, update the code-behind of the *Site.Master.cs* file by adding the code highlighted in yellow as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

<span data-ttu-id="7cea9-333">页面呈现为 HTML 之前,`Page_PreRender`引发事件。</span><span class="sxs-lookup"><span data-stu-id="7cea9-333">Before the page is rendered as HTML, the `Page_PreRender` event is raised.</span></span> <span data-ttu-id="7cea9-334">在中`Page_PreRender`处理程序，购物车的总计数由调用`GetCount`方法。</span><span class="sxs-lookup"><span data-stu-id="7cea9-334">In the `Page_PreRender` handler, the total count of the shopping cart is determined by calling the `GetCount` method.</span></span> <span data-ttu-id="7cea9-335">返回的值添加到`cartCount`的标记中包含的跨度*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-335">The returned value is added to the `cartCount` span included in the markup of the *Site.Master* page.</span></span> <span data-ttu-id="7cea9-336">`<span>`标记使要正确呈现的内部元素。</span><span class="sxs-lookup"><span data-stu-id="7cea9-336">The `<span>` tags enables the inner elements to be properly rendered.</span></span> <span data-ttu-id="7cea9-337">该站点的任何页显示时，将显示购物车总额。</span><span class="sxs-lookup"><span data-stu-id="7cea9-337">When any page of the site is displayed, the shopping cart total will be displayed.</span></span> <span data-ttu-id="7cea9-338">用户还可以单击以显示购物车的购物车总额。</span><span class="sxs-lookup"><span data-stu-id="7cea9-338">The user can also click the shopping cart total to display the shopping cart.</span></span>

## <a name="testing-the-completed-shopping-cart"></a><span data-ttu-id="7cea9-339">测试已完成的购物车</span><span class="sxs-lookup"><span data-stu-id="7cea9-339">Testing the Completed Shopping Cart</span></span>

<span data-ttu-id="7cea9-340">可以在购物车中运行应用程序现在以查看如何添加、 删除和更新的项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-340">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="7cea9-341">购物车总额将反映在购物车中的所有项的总成本。</span><span class="sxs-lookup"><span data-stu-id="7cea9-341">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="7cea9-342">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cea9-342">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="7cea9-343">在浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="7cea9-343">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="7cea9-344">选择**汽车**类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-344">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="7cea9-345">单击**添加到购物车**旁边的第一个产品的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-345">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="7cea9-346">*ShoppingCart.aspx*页中显示订单总计。</span><span class="sxs-lookup"><span data-stu-id="7cea9-346">The *ShoppingCart.aspx* page is displayed with the order total.</span></span>
4. <span data-ttu-id="7cea9-347">选择**平面**类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="7cea9-347">Select **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="7cea9-348">单击**添加到购物车**旁边的第一个产品的链接。</span><span class="sxs-lookup"><span data-stu-id="7cea9-348">Click the **Add To Cart** link next to the first product.</span></span>
6. <span data-ttu-id="7cea9-349">第一项的数量设置为 3 的购物车中并选择**删除项**第二个项的复选框。<a id="a"></a></span><span class="sxs-lookup"><span data-stu-id="7cea9-349">Set the quantity of the first item in the shopping cart to 3 and select the **Remove Item** check box of the second item.<a id="a"></a></span></span>
7. <span data-ttu-id="7cea9-350">单击**更新**按钮来更新购物车页并显示新的订单总计。</span><span class="sxs-lookup"><span data-stu-id="7cea9-350">Click the **Update** button to update the shopping cart page and display the new order total.</span></span> 

    ![购物车的购物车更新](shopping-cart/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="7cea9-352">总结</span><span class="sxs-lookup"><span data-stu-id="7cea9-352">Summary</span></span>

<span data-ttu-id="7cea9-353">在本教程中，您创建了购物车的 Wingtip Toys Web 窗体示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cea9-353">In this tutorial, you have created a shopping cart for the Wingtip Toys Web Forms sample application.</span></span> <span data-ttu-id="7cea9-354">在本教程期间你已使用 Entity Framework Code First、 数据批注、 强类型的数据控件和模型绑定。</span><span class="sxs-lookup"><span data-stu-id="7cea9-354">During this tutorial you have used Entity Framework Code First, data annotations, strongly typed data controls, and model binding.</span></span>

<span data-ttu-id="7cea9-355">购物车支持添加、 删除和更新用户已经选择购买的项。</span><span class="sxs-lookup"><span data-stu-id="7cea9-355">The shopping cart supports adding, deleting, and updating items that the user has selected for purchase.</span></span> <span data-ttu-id="7cea9-356">除了实现购物车功能，已了解如何显示在购物车商品**GridView**控制并计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="7cea9-356">In addition to implementing the shopping cart functionality, you have learned how to display shopping cart items in a **GridView** control and calculate the order total.</span></span>

## <a name="addition-information"></a><span data-ttu-id="7cea9-357">其他信息</span><span class="sxs-lookup"><span data-stu-id="7cea9-357">Addition Information</span></span>

[<span data-ttu-id="7cea9-358">ASP.NET 会话状态概述</span><span class="sxs-lookup"><span data-stu-id="7cea9-358">ASP.NET Session State Overview</span></span>](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> <span data-ttu-id="7cea9-359">[上一页](display_data_items_and_details.md)
> [下一页](checkout-and-payment-with-paypal.md)</span><span class="sxs-lookup"><span data-stu-id="7cea9-359">[Previous](display_data_items_and_details.md)
[Next](checkout-and-payment-with-paypal.md)</span></span>
