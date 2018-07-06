---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第 4 部分： 列出了所有产品 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 4 部分介绍了列出产品使用 GridView contr....
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: ec349a2564a63fd950ca5f6a171e6ffd1199c28a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813068"
---
<a name="part-4-listing-products"></a><span data-ttu-id="b8d25-104">第 4 部分： 列出产品</span><span class="sxs-lookup"><span data-stu-id="b8d25-104">Part 4: Listing Products</span></span>
====================
<span data-ttu-id="b8d25-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="b8d25-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="b8d25-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="b8d25-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="b8d25-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="b8d25-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="b8d25-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="b8d25-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="b8d25-109">第 4 部分介绍如何列出产品使用 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="b8d25-109">Part 4 covers listing products with the GridView control.</span></span>


## <a id="_Toc260221670"></a>  <span data-ttu-id="b8d25-110">列出了所有产品使用 GridView 控件</span><span class="sxs-lookup"><span data-stu-id="b8d25-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="b8d25-111">让我们开始在我们的解决方案，并选择"添加"和"新建项"通过"右键单击"实现我们 ProductsList.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="b8d25-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="b8d25-112">选择"Web 窗体使用母版页"并输入页名称为 ProductsList.aspx"。</span><span class="sxs-lookup"><span data-stu-id="b8d25-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="b8d25-113">单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="b8d25-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="b8d25-114">接下来选择其中我们放置 Site.Master 页的"样式"文件夹并从"文件夹的内容"窗口中选择它。</span><span class="sxs-lookup"><span data-stu-id="b8d25-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="b8d25-115">单击"确定"以创建页。</span><span class="sxs-lookup"><span data-stu-id="b8d25-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="b8d25-116">我们的数据库填充产品数据，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b8d25-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="b8d25-117">创建我们的页面后我们将再次使用实体数据源来访问该产品数据，但我们需要在此实例中选择的产品实体，我们需要限制为仅所选类别返回的项。</span><span class="sxs-lookup"><span data-stu-id="b8d25-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="b8d25-118">若要完成此我们将告诉 EntityDataSource 到自动生成 WHERE 子句，并且我们将指定 WhereParameter。</span><span class="sxs-lookup"><span data-stu-id="b8d25-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="b8d25-119">您会记得，我们在我们"产品类别菜单"中创建菜单项时我们动态生成链接通过将 CatagoryID 添加到每个链接在查询字符串。</span><span class="sxs-lookup"><span data-stu-id="b8d25-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CatagoryID to the QueryString for each link.</span></span> <span data-ttu-id="b8d25-120">我们将告诉实体数据源为位置参数派生的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="b8d25-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="b8d25-121">接下来，我们将配置 ListView 控件来显示产品列表。</span><span class="sxs-lookup"><span data-stu-id="b8d25-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="b8d25-122">若要创建最佳购物体验，我们将压缩到我们 ListVew 中显示的每个产品的几种简洁的功能。</span><span class="sxs-lookup"><span data-stu-id="b8d25-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="b8d25-123">产品名称将是该产品的详细信息视图的链接。</span><span class="sxs-lookup"><span data-stu-id="b8d25-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="b8d25-124">将显示产品的价格。</span><span class="sxs-lookup"><span data-stu-id="b8d25-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="b8d25-125">将显示产品的图像，我们将动态选择的图像目录 images 目录从我们的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="b8d25-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="b8d25-126">我们将包含一个链接，立即将特定的产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="b8d25-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="b8d25-127">下面是我们 ListView 控件实例的标记。</span><span class="sxs-lookup"><span data-stu-id="b8d25-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="b8d25-128">我们正在动态创建每个显示的产品的多个的链接。</span><span class="sxs-lookup"><span data-stu-id="b8d25-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="b8d25-129">此外，我们测试自己的新页面之前我们需要创建目录结构的产品目录映像，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b8d25-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="b8d25-130">访问我们产品的映像后我们可以测试我们的产品列表页面。</span><span class="sxs-lookup"><span data-stu-id="b8d25-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="b8d25-131">在站点的主页上，单击其中一个类别列表链接。</span><span class="sxs-lookup"><span data-stu-id="b8d25-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="b8d25-132">现在，我们需要实现 ProductDetials.apsx 页和 AddToCart 功能。</span><span class="sxs-lookup"><span data-stu-id="b8d25-132">Now we need to implement the ProductDetials.apsx page and the AddToCart functionality.</span></span>

<span data-ttu-id="b8d25-133">使用文件-&gt;新建以创建页名称 ProductDetails.aspx 我们像以前一样使用站点的母版页。</span><span class="sxs-lookup"><span data-stu-id="b8d25-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="b8d25-134">我们将再次使用 EntityDataSource 控件来访问数据库中的特定产品记录，我们将运用 ASP.NET FormView 控件来显示产品数据，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b8d25-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="b8d25-135">如果格式设置一个看起来有点很好笑，您不必担心。</span><span class="sxs-lookup"><span data-stu-id="b8d25-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="b8d25-136">上面的标记留出空间显示布局中的几个更高版本，我们将实现的功能。</span><span class="sxs-lookup"><span data-stu-id="b8d25-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="b8d25-137">购物车将表示在应用程序中更复杂的逻辑。</span><span class="sxs-lookup"><span data-stu-id="b8d25-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="b8d25-138">若要开始，使用文件-&gt;新建以创建名为 MyShoppingCart.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="b8d25-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="b8d25-139">请注意，我们不会选择 ShoppingCart.aspx 的名称。</span><span class="sxs-lookup"><span data-stu-id="b8d25-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="b8d25-140">我们的数据库包含名为"ShoppingCart"的表。</span><span class="sxs-lookup"><span data-stu-id="b8d25-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="b8d25-141">我们生成实体数据模型时为数据库中每个表已创建的类。</span><span class="sxs-lookup"><span data-stu-id="b8d25-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="b8d25-142">因此，实体数据模型生成一个名为"ShoppingCart"的实体类。</span><span class="sxs-lookup"><span data-stu-id="b8d25-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="b8d25-143">我们无法编辑该模型，以便我们可以使用我们的购物车实现该名称或将其扩展为我们的需求，但我们将避免发生冲突的名称只需选择在前面为改为选择。</span><span class="sxs-lookup"><span data-stu-id="b8d25-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply slect a name that will avoid the conflict.</span></span>

<span data-ttu-id="b8d25-144">它也是值得注意的，我们将创建简单购物车和购物车显示嵌入的购物车逻辑。</span><span class="sxs-lookup"><span data-stu-id="b8d25-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="b8d25-145">我们还可以选择在完全独立的业务层中实现我们的购物车。</span><span class="sxs-lookup"><span data-stu-id="b8d25-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b8d25-146">[上一页](tailspin-spyworks-part-3.md)
> [下一页](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="b8d25-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
