---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第 5 部分： 使用 Knockout.js 创建动态 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: 7d8bd4732ecf73c14251ceebfd667310f6e197b4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37801688"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="37c7e-102">第 5 部分： 使用 Knockout.js 创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="37c7e-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>
====================
<span data-ttu-id="37c7e-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="37c7e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="37c7e-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="37c7e-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="37c7e-105">使用 Knockout.js 创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="37c7e-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="37c7e-106">在本部分中，我们将使用 Knockout.js 将功能添加到管理员视图。</span><span class="sxs-lookup"><span data-stu-id="37c7e-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="37c7e-107">[Knockout.js](http://knockoutjs.com/)是一个 Javascript 库，它可以更轻松地将 HTML 控件绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="37c7e-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="37c7e-108">Knockout.js 使用模型-视图-视图模型 (MVVM) 模式。</span><span class="sxs-lookup"><span data-stu-id="37c7e-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="37c7e-109">*模型*（在我们的用例、 产品和订单） 的业务域中的数据的服务器端表示形式。</span><span class="sxs-lookup"><span data-stu-id="37c7e-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="37c7e-110">*视图*是表示层 (HTML)。</span><span class="sxs-lookup"><span data-stu-id="37c7e-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="37c7e-111">*视图模型*是 Javascript 对象，用于保存模型数据。</span><span class="sxs-lookup"><span data-stu-id="37c7e-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="37c7e-112">视图模型是在 ui 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="37c7e-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="37c7e-113">它并不知道 HTML 表示形式。</span><span class="sxs-lookup"><span data-stu-id="37c7e-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="37c7e-114">相反，它表示抽象视图，例如"的项列表"的功能。</span><span class="sxs-lookup"><span data-stu-id="37c7e-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="37c7e-115">该视图是数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="37c7e-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="37c7e-116">向视图模型的更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="37c7e-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="37c7e-117">视图模型还获取从视图中，如按钮单击事件，并对该模型，例如，创建订单执行操作。</span><span class="sxs-lookup"><span data-stu-id="37c7e-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="37c7e-118">首先，我们将定义视图模型。</span><span class="sxs-lookup"><span data-stu-id="37c7e-118">First we'll define the view-model.</span></span> <span data-ttu-id="37c7e-119">之后，我们将向视图模型绑定的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="37c7e-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="37c7e-120">将以下 Razor 部分添加到 Admin.cshtml:</span><span class="sxs-lookup"><span data-stu-id="37c7e-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="37c7e-121">可以在文件中的任意位置添加此部分。</span><span class="sxs-lookup"><span data-stu-id="37c7e-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="37c7e-122">呈现视图时，在 HTML 页的底部会出现的部分是否在关闭前右键&lt;/b o d&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="37c7e-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="37c7e-123">所有的此页的脚本将放入注释所指示的脚本标记：</span><span class="sxs-lookup"><span data-stu-id="37c7e-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="37c7e-124">首先，定义一个视图模型类：</span><span class="sxs-lookup"><span data-stu-id="37c7e-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="37c7e-125">**ko.observableArray**是一种特殊的 Knockout，调用中的对象*可观察量*。</span><span class="sxs-lookup"><span data-stu-id="37c7e-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="37c7e-126">从[Knockout.js 文档](http://knockoutjs.com/documentation/observables.html)： 可观察量是"JavaScript 对象，它可以通知有关更改的订阅服务器。"</span><span class="sxs-lookup"><span data-stu-id="37c7e-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="37c7e-127">当一个可观测对象的内容更改时，视图将自动更新以匹配。</span><span class="sxs-lookup"><span data-stu-id="37c7e-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="37c7e-128">若要填充`products`数组中向 web API 发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="37c7e-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="37c7e-129">还记得我们存储的基 URI 的视图包中的 API (请参阅[第 4 部分](using-web-api-with-entity-framework-part-4.md)本教程的)。</span><span class="sxs-lookup"><span data-stu-id="37c7e-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="37c7e-130">接下来，将函数添加到视图模型来创建、 更新和删除产品。</span><span class="sxs-lookup"><span data-stu-id="37c7e-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="37c7e-131">这些函数将提交到 web API 的 AJAX 调用，并使用结果更新视图模型。</span><span class="sxs-lookup"><span data-stu-id="37c7e-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="37c7e-132">现在最重要的部分： DOM 时是 fulled 加载，调用**ko.applyBindings**函数并传递中的新实例`ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="37c7e-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="37c7e-133">**Ko.applyBindings**方法激活 Knockout，并将视图模型连接到视图。</span><span class="sxs-lookup"><span data-stu-id="37c7e-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="37c7e-134">现在，我们有一个视图模型，我们可以创建绑定。</span><span class="sxs-lookup"><span data-stu-id="37c7e-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="37c7e-135">Knockout.js，在您执行此操作通过添加`data-bind`属性到 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="37c7e-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="37c7e-136">例如，若要将 HTML 列表绑定到一个数组，使用`foreach`绑定：</span><span class="sxs-lookup"><span data-stu-id="37c7e-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="37c7e-137">`foreach`绑定循环访问数组和数组中创建子元素的每个对象。</span><span class="sxs-lookup"><span data-stu-id="37c7e-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="37c7e-138">数组对象的属性可以引用上的子元素的绑定。</span><span class="sxs-lookup"><span data-stu-id="37c7e-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="37c7e-139">将以下绑定添加到"产品更新"列表：</span><span class="sxs-lookup"><span data-stu-id="37c7e-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="37c7e-140">`<li>`元素的作用域中出现**foreach**绑定。</span><span class="sxs-lookup"><span data-stu-id="37c7e-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="37c7e-141">表示 Knockout 将呈现一次的每个产品中的元素`products`数组。</span><span class="sxs-lookup"><span data-stu-id="37c7e-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="37c7e-142">所有内绑定`<li>`元素引用该产品实例。</span><span class="sxs-lookup"><span data-stu-id="37c7e-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="37c7e-143">例如，`$data.Name`是指`Name`产品上的属性。</span><span class="sxs-lookup"><span data-stu-id="37c7e-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="37c7e-144">若要设置的文本输入的值，使用`value`绑定。</span><span class="sxs-lookup"><span data-stu-id="37c7e-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="37c7e-145">按钮绑定到函数上的模型-视图，使用`click`绑定。</span><span class="sxs-lookup"><span data-stu-id="37c7e-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="37c7e-146">Product 实例作为参数传递给每个函数。</span><span class="sxs-lookup"><span data-stu-id="37c7e-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="37c7e-147">有关详细信息[Knockout.js 文档](http://knockoutjs.com/documentation/observables.html)具有很好的各种绑定的说明。</span><span class="sxs-lookup"><span data-stu-id="37c7e-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="37c7e-148">接下来，添加的绑定**提交**添加产品窗体上的事件：</span><span class="sxs-lookup"><span data-stu-id="37c7e-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="37c7e-149">此绑定调用`create`视图模型来创建一个新的产品上的函数。</span><span class="sxs-lookup"><span data-stu-id="37c7e-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="37c7e-150">下面是管理员视图的完整代码：</span><span class="sxs-lookup"><span data-stu-id="37c7e-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="37c7e-151">运行应用程序、 管理员帐户，登录并单击"管理员"链接。</span><span class="sxs-lookup"><span data-stu-id="37c7e-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="37c7e-152">应看到的产品列表，并能够创建、 更新或删除产品。</span><span class="sxs-lookup"><span data-stu-id="37c7e-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37c7e-153">[上一页](using-web-api-with-entity-framework-part-4.md)
> [下一页](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="37c7e-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
