---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第 7 部分： 创建主页面 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: bb4704e7f4f13fab04acdbdd642174884517e18a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834555"
---
<a name="part-7-creating-the-main-page"></a><span data-ttu-id="19402-102">第 7 部分： 创建主页面</span><span class="sxs-lookup"><span data-stu-id="19402-102">Part 7: Creating the Main Page</span></span>
====================
<span data-ttu-id="19402-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="19402-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="19402-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="19402-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="19402-105">创建主页面</span><span class="sxs-lookup"><span data-stu-id="19402-105">Creating the Main Page</span></span>

<span data-ttu-id="19402-106">在本部分中，将创建主应用程序页。</span><span class="sxs-lookup"><span data-stu-id="19402-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="19402-107">此页会比在管理页中，更复杂，因此我们将在几个步骤中处理它。</span><span class="sxs-lookup"><span data-stu-id="19402-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="19402-108">此过程中，你将看到一些更高级的 Knockout.js 技术。</span><span class="sxs-lookup"><span data-stu-id="19402-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="19402-109">下面是基本页的布局：</span><span class="sxs-lookup"><span data-stu-id="19402-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="19402-110">"产品"包含产品的数组。</span><span class="sxs-lookup"><span data-stu-id="19402-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="19402-111">"购物车"包含产品数量与的数组。</span><span class="sxs-lookup"><span data-stu-id="19402-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="19402-112">单击"添加添加到购物车"更新购物车。</span><span class="sxs-lookup"><span data-stu-id="19402-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="19402-113">"Orders"保留订单 Id 的数组。</span><span class="sxs-lookup"><span data-stu-id="19402-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="19402-114">"详细信息"包含订单详细信息，这是一个数组项 （产品数量）</span><span class="sxs-lookup"><span data-stu-id="19402-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="19402-115">我们将开始通过不带任何数据绑定或脚本在 HTML 中，定义一些基本布局。</span><span class="sxs-lookup"><span data-stu-id="19402-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="19402-116">打开文件 Views/Home/Index.cshtml 并使用以下内容替换中的所有内容：</span><span class="sxs-lookup"><span data-stu-id="19402-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="19402-117">接下来，添加脚本部分，并创建一个空的视图模型：</span><span class="sxs-lookup"><span data-stu-id="19402-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="19402-118">根据前面质地的设计，我们的视图模型需要的产品、 购物车、 订单和详细信息可观察量。</span><span class="sxs-lookup"><span data-stu-id="19402-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="19402-119">添加以下变量添加到`AppViewModel`对象：</span><span class="sxs-lookup"><span data-stu-id="19402-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="19402-120">用户可以将项从产品列表添加到购物车中，并从购物车中删除项目。</span><span class="sxs-lookup"><span data-stu-id="19402-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="19402-121">若要将这些功能封装，我们将创建表示产品的另一个视图模型类。</span><span class="sxs-lookup"><span data-stu-id="19402-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="19402-122">将下列代码添加到 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="19402-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="19402-123">`ProductViewModel`类包含用于向 / 从购物车移动产品的两个函数：`addItemToCart`将该产品的一个单元添加到购物车中，和`removeAllFromCart`中移除所有的产品数量。</span><span class="sxs-lookup"><span data-stu-id="19402-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="19402-124">用户可以选择现有订单，并获取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="19402-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="19402-125">我们将封装此功能加入到另一个视图模型：</span><span class="sxs-lookup"><span data-stu-id="19402-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="19402-126">`OrderDetailsViewModel`初始化采用的顺序，它通过向服务器发送 AJAX 请求提取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="19402-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="19402-127">另请注意`total`属性上的`OrderDetailsViewModel`。</span><span class="sxs-lookup"><span data-stu-id="19402-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="19402-128">此属性是一种特殊的可观察对象调用[计算可观察量](http://knockoutjs.com/documentation/computedObservables.html)。</span><span class="sxs-lookup"><span data-stu-id="19402-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="19402-129">如名称所示，计算可观察量可数据绑定到计算值&#8212;在这种情况下，总费用的顺序。</span><span class="sxs-lookup"><span data-stu-id="19402-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="19402-130">接下来，添加到这些函数`AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="19402-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="19402-131">`resetCart` 从购物车中移除所有项。</span><span class="sxs-lookup"><span data-stu-id="19402-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="19402-132">`getDetails` 获取订单的详细信息 (通过一个新的 p 通过`OrderDetailsViewModel`拖动到`details`列表)。</span><span class="sxs-lookup"><span data-stu-id="19402-132">`getDetails` gets the details for an order (by pusing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="19402-133">`createOrder` 创建新订单并清空该购物车。</span><span class="sxs-lookup"><span data-stu-id="19402-133">`createOrder` creates a new order and empties the cart.</span></span>


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="19402-134">最后，通过发出 AJAX 请求的产品和订单初始化视图模型：</span><span class="sxs-lookup"><span data-stu-id="19402-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="19402-135">好了，这是很多代码，但我们构建它向上逐步进行，因此希望设计已清除。</span><span class="sxs-lookup"><span data-stu-id="19402-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="19402-136">现在我们可以将某些 Knockout.js 绑定添加到 HTML。</span><span class="sxs-lookup"><span data-stu-id="19402-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="19402-137">**产品**</span><span class="sxs-lookup"><span data-stu-id="19402-137">**Products**</span></span>

<span data-ttu-id="19402-138">下面是产品列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="19402-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="19402-139">此循环访问产品数组并显示的名称和价格。</span><span class="sxs-lookup"><span data-stu-id="19402-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="19402-140">仅当用户登录时，则显示"添加到 Order"按钮。</span><span class="sxs-lookup"><span data-stu-id="19402-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="19402-141">"添加到 Order"按钮调用`addItemToCart`上`ProductViewModel`产品的实例。</span><span class="sxs-lookup"><span data-stu-id="19402-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="19402-142">此示例演示一个不错的功能的 Knockout.js： 当视图模型中包含其他视图模型时，可以应用这些绑定到的内部模型。</span><span class="sxs-lookup"><span data-stu-id="19402-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="19402-143">在此示例中，在绑定`foreach`应用于每个`ProductViewModel`实例。</span><span class="sxs-lookup"><span data-stu-id="19402-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="19402-144">这种方法是功能的将所有放到一个视图模型更加清晰。</span><span class="sxs-lookup"><span data-stu-id="19402-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="19402-145">**购物车**</span><span class="sxs-lookup"><span data-stu-id="19402-145">**Cart**</span></span>

<span data-ttu-id="19402-146">下面是在购物车的绑定：</span><span class="sxs-lookup"><span data-stu-id="19402-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="19402-147">此循环车数组并显示名称、 价格和数量。</span><span class="sxs-lookup"><span data-stu-id="19402-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="19402-148">请注意，"删除"链接和"创建订单"按钮绑定到视图模型的函数。</span><span class="sxs-lookup"><span data-stu-id="19402-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="19402-149">**订单**</span><span class="sxs-lookup"><span data-stu-id="19402-149">**Orders**</span></span>

<span data-ttu-id="19402-150">下面是有关订单列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="19402-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="19402-151">此循环访问订单和显示订单 id。</span><span class="sxs-lookup"><span data-stu-id="19402-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="19402-152">链接的 click 事件绑定到`getDetails`函数。</span><span class="sxs-lookup"><span data-stu-id="19402-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="19402-153">**订单详细信息**</span><span class="sxs-lookup"><span data-stu-id="19402-153">**Order Details**</span></span>

<span data-ttu-id="19402-154">下面是订单详细信息的绑定：</span><span class="sxs-lookup"><span data-stu-id="19402-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="19402-155">此循环按顺序的项并显示产品、 价格和数量。</span><span class="sxs-lookup"><span data-stu-id="19402-155">This iterates over the items in the order and displays the product, price, and quanity.</span></span> <span data-ttu-id="19402-156">周围的 div 是详细信息数组包含一个或多个项时才可见。</span><span class="sxs-lookup"><span data-stu-id="19402-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="19402-157">结束语</span><span class="sxs-lookup"><span data-stu-id="19402-157">Conclusion</span></span>

<span data-ttu-id="19402-158">在本教程中，您可以创建使用 Entity Framework 数据库和 ASP.NET Web API 提供面向公众的接口在数据层的顶部进行通信的应用程序。</span><span class="sxs-lookup"><span data-stu-id="19402-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="19402-159">我们使用 ASP.NET MVC 4 来呈现 HTML 页面和 Knockout.js 以及 jQuery，以提供动态交互，而无需重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="19402-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="19402-160">其他资源：</span><span class="sxs-lookup"><span data-stu-id="19402-160">Additional resources:</span></span>

- [<span data-ttu-id="19402-161">ASP.NET 数据访问内容映射</span><span class="sxs-lookup"><span data-stu-id="19402-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="19402-162">实体框架开发人员中心</span><span class="sxs-lookup"><span data-stu-id="19402-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="19402-163">上一篇</span><span class="sxs-lookup"><span data-stu-id="19402-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
