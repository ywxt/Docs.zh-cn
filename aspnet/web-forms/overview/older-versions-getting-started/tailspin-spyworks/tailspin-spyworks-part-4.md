---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第 4 部分： 列出了所有产品 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 4 部分介绍的产品列表与 GridView contr....
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 69b26344e6dcdbf27e94da90ad5d6cd79f27ccd3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30881059"
---
<a name="part-4-listing-products"></a><span data-ttu-id="c3d9f-104">第 4 部分： 列表产品</span><span class="sxs-lookup"><span data-stu-id="c3d9f-104">Part 4: Listing Products</span></span>
====================
<span data-ttu-id="c3d9f-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c3d9f-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c3d9f-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c3d9f-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c3d9f-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c3d9f-109">第 4 部分介绍的产品列表与 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-109">Part 4 covers listing products with the GridView control.</span></span>


## <a id="_Toc260221670"></a>  <span data-ttu-id="c3d9f-110">列出的产品与 GridView 控件</span><span class="sxs-lookup"><span data-stu-id="c3d9f-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="c3d9f-111">让我们在我们的解决方案并选择"添加"和"新项"开始通过"右键单击"实现我们 ProductsList.aspx 页面。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="c3d9f-112">选择"Web 窗体使用母版页"并输入 ProductsList.aspx 一个页名称"。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="c3d9f-113">单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="c3d9f-114">接下来选择我们放置 Site.Master 页的"样式"文件夹，并从"文件夹的内容"窗口中选择它。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="c3d9f-115">单击"确定"以创建页。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="c3d9f-116">我们的数据库填充产品数据，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="c3d9f-117">我们的页面因过期而我们再次将使用实体数据源来访问该产品的数据，但我们需要此实例中选择产品实体，我们需要限制返回到只有是所选类别的项。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="c3d9f-118">若要实现此目的，我们将告诉到自动生成 EntityDataSource WHERE 子句，并且我们将指定 WhereParameter。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="c3d9f-119">你将还记得，当我们在我们"产品类别菜单"中创建菜单项我们动态生成的链接通过将 CatagoryID 添加到每个链接查询字符串。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CatagoryID to the QueryString for each link.</span></span> <span data-ttu-id="c3d9f-120">我们将告诉要从该查询字符串参数派生的位置参数的实体数据源。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="c3d9f-121">接下来，我们将配置要显示的产品列表的 ListView 控件。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="c3d9f-122">若要创建最佳购物体验我们将为我们 ListVew 中显示每种产品压缩几种简洁的功能。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="c3d9f-123">产品名称将是该产品的详细信息视图的链接。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="c3d9f-124">将显示产品的价格。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="c3d9f-125">将显示产品的映像，并且我们将动态选择的映像从目录映像目录在我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="c3d9f-126">我们将包含一个用于立即将特定的产品添加到购物车链接。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="c3d9f-127">下面是我们 ListView 控件实例的标记。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="c3d9f-128">我们动态生成每个显示的产品的多个的链接。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="c3d9f-129">此外，我们测试自己的新页之前我们需要创建目录结构的产品目录映像，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="c3d9f-130">访问我们的产品图像后，我们可以测试我们的产品列表页面。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="c3d9f-131">从网站的主页上，单击其中一个类别列表链接。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="c3d9f-132">现在，我们需要实现 ProductDetials.apsx 页和 AddToCart 功能。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-132">Now we need to implement the ProductDetials.apsx page and the AddToCart functionality.</span></span>

<span data-ttu-id="c3d9f-133">使用文件-&gt;新建以创建页名称 ProductDetails.aspx 我们像以前一样使用母版页的站点。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="c3d9f-134">我们将再次使用 EntityDataSource 控件来访问数据库中的特定产品记录和我们将使用 ASP.NET FormView 控件来显示产品数据，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="c3d9f-135">如果格式一个看起来有点有趣，给你，请不要担心。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="c3d9f-136">上面的标记留出空间显示布局中为多个我们将更高版本实现的功能。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="c3d9f-137">购物车将表示在我们的应用程序更复杂的逻辑。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="c3d9f-138">若要开始，使用文件-&gt;新建创建调用 MyShoppingCart.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="c3d9f-139">请注意，我们不选择 ShoppingCart.aspx 的名称。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="c3d9f-140">我们的数据库包含名为"ShoppingCart"的表。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="c3d9f-141">我们生成实体数据模型时已为数据库中每个表创建一个类。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="c3d9f-142">因此，实体数据模型生成名为"ShoppingCart"实体类。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="c3d9f-143">我们无法编辑该模型，以便我们无法将该名称用于我们购物车实现或扩展针对我们的需求，但我们将选择而是只需选择将避免冲突的名称。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply slect a name that will avoid the conflict.</span></span>

<span data-ttu-id="c3d9f-144">它也是值得注意的，我们将创建简单的购物车和具有购物车显示嵌入的购物车逻辑。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="c3d9f-145">我们还可以选择在完全独立的业务层中实现我们购物车。</span><span class="sxs-lookup"><span data-stu-id="c3d9f-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3d9f-146">[上一页](tailspin-spyworks-part-3.md)
> [下一页](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="c3d9f-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
