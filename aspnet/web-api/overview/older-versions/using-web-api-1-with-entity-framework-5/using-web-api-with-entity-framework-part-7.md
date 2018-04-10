---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第 7 部分： 创建主页面 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: 2c378e68a1e6600daf655c19afbfe355e89496d4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="part-7-creating-the-main-page"></a><span data-ttu-id="177b5-102">第 7 部分： 创建主页面</span><span class="sxs-lookup"><span data-stu-id="177b5-102">Part 7: Creating the Main Page</span></span>
====================
<span data-ttu-id="177b5-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="177b5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="177b5-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="177b5-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="177b5-105">创建主页面</span><span class="sxs-lookup"><span data-stu-id="177b5-105">Creating the Main Page</span></span>

<span data-ttu-id="177b5-106">在本部分中，你将创建主应用程序页。</span><span class="sxs-lookup"><span data-stu-id="177b5-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="177b5-107">因此我们将方法处理它在几个步骤中，此页将会比管理员页中，更复杂。</span><span class="sxs-lookup"><span data-stu-id="177b5-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="177b5-108">与此同时，你将看到一些更高级的 Knockout.js 技术。</span><span class="sxs-lookup"><span data-stu-id="177b5-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="177b5-109">下面是基本页的布局：</span><span class="sxs-lookup"><span data-stu-id="177b5-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="177b5-110">"Products"包含产品的数组。</span><span class="sxs-lookup"><span data-stu-id="177b5-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="177b5-111">"购物车"包含的产品与数量的数组。</span><span class="sxs-lookup"><span data-stu-id="177b5-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="177b5-112">单击"添加放入购物车"更新购物车。</span><span class="sxs-lookup"><span data-stu-id="177b5-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="177b5-113">"Orders"包含订单 Id 的数组。</span><span class="sxs-lookup"><span data-stu-id="177b5-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="177b5-114">"详细信息"包含订单详细信息，这是项 （产品与数量） 的数组</span><span class="sxs-lookup"><span data-stu-id="177b5-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="177b5-115">我们将开始通过使用无数据绑定或脚本在 HTML 中，定义一些基本布局。</span><span class="sxs-lookup"><span data-stu-id="177b5-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="177b5-116">打开文件 Views/Home/Index.cshtml 并将替换为以下的所有内容：</span><span class="sxs-lookup"><span data-stu-id="177b5-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="177b5-117">接下来，添加一个脚本部分，并创建一个空的视图模型：</span><span class="sxs-lookup"><span data-stu-id="177b5-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="177b5-118">根据前面草的设计，我们视图模型需要可观察对象产品、 购物车、 订单和详细信息。</span><span class="sxs-lookup"><span data-stu-id="177b5-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="177b5-119">添加到以下变量`AppViewModel`对象：</span><span class="sxs-lookup"><span data-stu-id="177b5-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="177b5-120">用户可以从产品列表将项添加到购物车，和从购物车中删除项。</span><span class="sxs-lookup"><span data-stu-id="177b5-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="177b5-121">若要封装这些函数，我们将创建表示产品的另一个视图模型类。</span><span class="sxs-lookup"><span data-stu-id="177b5-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="177b5-122">将下列代码添加到 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="177b5-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="177b5-123">`ProductViewModel`类包含用于购物车之间转移产品的两个函数：`addItemToCart`将产品的一个单元添加到购物车，和`removeAllFromCart`中移除所有的产品数量。</span><span class="sxs-lookup"><span data-stu-id="177b5-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="177b5-124">用户可以选择一个现有的 order 并获取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="177b5-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="177b5-125">我们将封装到另一个视图模型此功能：</span><span class="sxs-lookup"><span data-stu-id="177b5-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="177b5-126">`OrderDetailsViewModel`初始化顺序，并且它通过向服务器发送 AJAX 请求提取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="177b5-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="177b5-127">另请注意`total`属性`OrderDetailsViewModel`。</span><span class="sxs-lookup"><span data-stu-id="177b5-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="177b5-128">此属性是一种特殊的可观测对象调用[计算可观测对象](http://knockoutjs.com/documentation/computedObservables.html)。</span><span class="sxs-lookup"><span data-stu-id="177b5-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="177b5-129">顾名思义，计算可观测对象允许你为计算值的数据绑定&#8212;在这种情况下，总体成本的顺序。</span><span class="sxs-lookup"><span data-stu-id="177b5-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="177b5-130">接下来，添加到这些函数`AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="177b5-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="177b5-131">`resetCart` 从购物车中移除所有项。</span><span class="sxs-lookup"><span data-stu-id="177b5-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="177b5-132">`getDetails` 获取为某一订单的详细信息 (由一个新的 p 通过`OrderDetailsViewModel`到`details`列表)。</span><span class="sxs-lookup"><span data-stu-id="177b5-132">`getDetails` gets the details for an order (by pusing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="177b5-133">`createOrder` 创建新订单并清空购物车。</span><span class="sxs-lookup"><span data-stu-id="177b5-133">`createOrder` creates a new order and empties the cart.</span></span>


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="177b5-134">最后，发出的产品和订单的 AJAX 请求初始化视图模型：</span><span class="sxs-lookup"><span data-stu-id="177b5-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="177b5-135">好了，这就是大量的代码，但我们构建分步，希望设计是清除。</span><span class="sxs-lookup"><span data-stu-id="177b5-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="177b5-136">现在我们可以将某些 Knockout.js 绑定添加到 HTML。</span><span class="sxs-lookup"><span data-stu-id="177b5-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="177b5-137">**产品**</span><span class="sxs-lookup"><span data-stu-id="177b5-137">**Products**</span></span>

<span data-ttu-id="177b5-138">以下是有关产品列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="177b5-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="177b5-139">这将循环访问产品数组并显示的名称和价格。</span><span class="sxs-lookup"><span data-stu-id="177b5-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="177b5-140">仅当用户登录时，"添加到订单"按钮可见。</span><span class="sxs-lookup"><span data-stu-id="177b5-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="177b5-141">在"添加到订单"按钮调用`addItemToCart`上`ProductViewModel`产品的实例。</span><span class="sxs-lookup"><span data-stu-id="177b5-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="177b5-142">此示例演示一个不错的功能的 Knockout.js： 当视图模型包含其他视图模型时，可以将绑定应用于内部的模型。</span><span class="sxs-lookup"><span data-stu-id="177b5-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="177b5-143">在此示例中，在绑定`foreach`应用于每个`ProductViewModel`实例。</span><span class="sxs-lookup"><span data-stu-id="177b5-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="177b5-144">这种方法是更清楚比的所有功能置于单个视图模型。</span><span class="sxs-lookup"><span data-stu-id="177b5-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="177b5-145">**Cart**</span><span class="sxs-lookup"><span data-stu-id="177b5-145">**Cart**</span></span>

<span data-ttu-id="177b5-146">下面是购物车的绑定：</span><span class="sxs-lookup"><span data-stu-id="177b5-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="177b5-147">这将循环访问购物车数组并显示名称、 价格和数量。</span><span class="sxs-lookup"><span data-stu-id="177b5-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="177b5-148">请注意，则会将"删除"链接和"创建订单"按钮绑定到视图模型函数。</span><span class="sxs-lookup"><span data-stu-id="177b5-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="177b5-149">**订单**</span><span class="sxs-lookup"><span data-stu-id="177b5-149">**Orders**</span></span>

<span data-ttu-id="177b5-150">以下是有关的订单列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="177b5-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="177b5-151">此循环访问订单，并显示订单 id。</span><span class="sxs-lookup"><span data-stu-id="177b5-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="177b5-152">Click 事件的链接绑定到`getDetails`函数。</span><span class="sxs-lookup"><span data-stu-id="177b5-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="177b5-153">**订单详细信息**</span><span class="sxs-lookup"><span data-stu-id="177b5-153">**Order Details**</span></span>

<span data-ttu-id="177b5-154">下面是显示订单详细信息的绑定：</span><span class="sxs-lookup"><span data-stu-id="177b5-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="177b5-155">这将循环访问的项的顺序，并显示产品、 价格和数量。</span><span class="sxs-lookup"><span data-stu-id="177b5-155">This iterates over the items in the order and displays the product, price, and quanity.</span></span> <span data-ttu-id="177b5-156">周围的 div 是详细信息数组包含一个或多个项时才可见。</span><span class="sxs-lookup"><span data-stu-id="177b5-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="177b5-157">结束语</span><span class="sxs-lookup"><span data-stu-id="177b5-157">Conclusion</span></span>

<span data-ttu-id="177b5-158">在本教程中，你创建的应用程序使用实体框架与数据库和 ASP.NET Web API，用于提供在数据层的顶部的面向公众的接口通信。</span><span class="sxs-lookup"><span data-stu-id="177b5-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="177b5-159">我们使用 ASP.NET MVC 4 来呈现的 HTML 页面，和 Knockout.js 加 jQuery，以提供动态交互，而无需重新加载页。</span><span class="sxs-lookup"><span data-stu-id="177b5-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="177b5-160">其他资源：</span><span class="sxs-lookup"><span data-stu-id="177b5-160">Additional resources:</span></span>

- [<span data-ttu-id="177b5-161">ASP.NET 数据访问内容映射</span><span class="sxs-lookup"><span data-stu-id="177b5-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="177b5-162">实体框架开发人员中心</span><span class="sxs-lookup"><span data-stu-id="177b5-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="177b5-163">上一篇</span><span class="sxs-lookup"><span data-stu-id="177b5-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
