---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第 5 部分： 使用 Knockout.js 创建动态 UI |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: b63446d076fbb1143641dead788042967b996bf8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873805"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="a6573-102">第 5 部分： 使用 Knockout.js 创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="a6573-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>
====================
<span data-ttu-id="a6573-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a6573-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a6573-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="a6573-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="a6573-105">使用 Knockout.js 创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="a6573-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="a6573-106">在此部分中，我们将使用 Knockout.js 将功能添加到管理视图。</span><span class="sxs-lookup"><span data-stu-id="a6573-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="a6573-107">[Knockout.js](http://knockoutjs.com/)是一个 Javascript 库，可以轻松地将 HTML 控件绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="a6573-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="a6573-108">Knockout.js 使用模型-视图-视图模型 (MVVM) 模式。</span><span class="sxs-lookup"><span data-stu-id="a6573-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="a6573-109">*模型*是服务器端表示形式 （在我们用例、 产品和 orders） 对业务领域中的数据。</span><span class="sxs-lookup"><span data-stu-id="a6573-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="a6573-110">*视图*是表示层 (HTML)。</span><span class="sxs-lookup"><span data-stu-id="a6573-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="a6573-111">*视图模型*是保存模型数据的 Javascript 对象。</span><span class="sxs-lookup"><span data-stu-id="a6573-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="a6573-112">视图模型是 UI 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="a6573-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="a6573-113">它具有的 HTML 表示不知道。</span><span class="sxs-lookup"><span data-stu-id="a6573-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="a6573-114">相反，它表示抽象视图，如"的项的列表"的功能。</span><span class="sxs-lookup"><span data-stu-id="a6573-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="a6573-115">该视图被数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="a6573-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="a6573-116">对视图模型更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="a6573-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="a6573-117">视图模型还从视图中，例如按钮单击、 获取事件，并对模型，如创建顺序执行操作。</span><span class="sxs-lookup"><span data-stu-id="a6573-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="a6573-118">首先我们将定义视图模型。</span><span class="sxs-lookup"><span data-stu-id="a6573-118">First we'll define the view-model.</span></span> <span data-ttu-id="a6573-119">之后，我们将到视图模型绑定的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="a6573-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="a6573-120">将以下 Razor 部分添加到 Admin.cshtml:</span><span class="sxs-lookup"><span data-stu-id="a6573-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="a6573-121">可以在文件中的任意位置添加此部分。</span><span class="sxs-lookup"><span data-stu-id="a6573-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="a6573-122">该视图呈现时，部分会出现在 HTML 页中，底部右键在关闭前&lt;/b o&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="a6573-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="a6573-123">所有此页的脚本将放入注释所指示的脚本标记：</span><span class="sxs-lookup"><span data-stu-id="a6573-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="a6573-124">首先，定义一个视图模型类：</span><span class="sxs-lookup"><span data-stu-id="a6573-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="a6573-125">**ko.observableArray**是中 Knockout，调用对象的特殊*可观测对象*。</span><span class="sxs-lookup"><span data-stu-id="a6573-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="a6573-126">从[Knockout.js 文档](http://knockoutjs.com/documentation/observables.html): 可观测对象是一个"JavaScript 对象，可以通知有关更改的订阅服务器。"</span><span class="sxs-lookup"><span data-stu-id="a6573-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="a6573-127">当可观测对象的内容更改时，视图将自动更新以匹配。</span><span class="sxs-lookup"><span data-stu-id="a6573-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="a6573-128">若要填充`products`数组，对 web API 进行 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="a6573-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="a6573-129">回想一下我们在视图包 API 为存储的基 URI (请参阅[第 4 部分](using-web-api-with-entity-framework-part-4.md)本教程的)。</span><span class="sxs-lookup"><span data-stu-id="a6573-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="a6573-130">接下来，将函数添加到视图模型来创建、 更新和删除产品。</span><span class="sxs-lookup"><span data-stu-id="a6573-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="a6573-131">这些函数将提交到 web API 的 AJAX 调用，并使用的结果来更新视图模型。</span><span class="sxs-lookup"><span data-stu-id="a6573-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="a6573-132">现在的最重要的部分： 当 DOM 是 fulled 加载，调用**ko.applyBindings**函数并传入的新实例`ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="a6573-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="a6573-133">**Ko.applyBindings**方法激活 Knockout 和到视图连线视图模型。</span><span class="sxs-lookup"><span data-stu-id="a6573-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="a6573-134">现在，我们已视图模型，我们可以创建绑定。</span><span class="sxs-lookup"><span data-stu-id="a6573-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="a6573-135">在 Knockout.js，你执行此操作通过添加`data-bind`于 HTML 元素属性。</span><span class="sxs-lookup"><span data-stu-id="a6573-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="a6573-136">例如，若要将一个 HTML 列表绑定到一个数组，请使用`foreach`绑定：</span><span class="sxs-lookup"><span data-stu-id="a6573-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="a6573-137">`foreach`绑定循环访问数组和数组中创建子元素的每个对象。</span><span class="sxs-lookup"><span data-stu-id="a6573-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="a6573-138">上的子元素的绑定可以指数组对象上的属性。</span><span class="sxs-lookup"><span data-stu-id="a6573-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="a6573-139">将以下绑定添加到"更新产品"列表中：</span><span class="sxs-lookup"><span data-stu-id="a6573-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="a6573-140">`<li>`元素出现在范围内**foreach**绑定。</span><span class="sxs-lookup"><span data-stu-id="a6573-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="a6573-141">表示 Knockout 将呈现一次为每个产品中的元素`products`数组。</span><span class="sxs-lookup"><span data-stu-id="a6573-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="a6573-142">中的绑定的所有`<li>`元素引用该产品实例。</span><span class="sxs-lookup"><span data-stu-id="a6573-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="a6573-143">例如，`$data.Name`指`Name`产品上的属性。</span><span class="sxs-lookup"><span data-stu-id="a6573-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="a6573-144">若要设置的文本输入的值，使用`value`绑定。</span><span class="sxs-lookup"><span data-stu-id="a6573-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="a6573-145">按钮上模型-视图中，绑定到函数使用`click`绑定。</span><span class="sxs-lookup"><span data-stu-id="a6573-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="a6573-146">产品实例作为参数传递给每个函数。</span><span class="sxs-lookup"><span data-stu-id="a6573-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="a6573-147">有关详细信息， [Knockout.js 文档](http://knockoutjs.com/documentation/observables.html)具有良好的各种绑定的说明。</span><span class="sxs-lookup"><span data-stu-id="a6573-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="a6573-148">接下来，添加的绑定**提交**添加产品窗体上的事件：</span><span class="sxs-lookup"><span data-stu-id="a6573-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="a6573-149">此绑定调用`create`视图模型来创建新产品上的函数。</span><span class="sxs-lookup"><span data-stu-id="a6573-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="a6573-150">下面是管理视图的完整代码：</span><span class="sxs-lookup"><span data-stu-id="a6573-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="a6573-151">运行应用程序的管理员帐户，登录，单击"Admin"链接。</span><span class="sxs-lookup"><span data-stu-id="a6573-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="a6573-152">你应查看的产品的列表，并能够创建、 更新或删除产品。</span><span class="sxs-lookup"><span data-stu-id="a6573-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6573-153">[上一页](using-web-api-with-entity-framework-part-4.md)
> [下一页](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="a6573-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
