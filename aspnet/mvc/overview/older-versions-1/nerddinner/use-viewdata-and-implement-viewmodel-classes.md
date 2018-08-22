---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 和实现 ViewModel 类 |Microsoft Docs
author: microsoft
description: 步骤 6 显示了如何启用对更丰富的窗体编辑方案中，支持，并还讨论了可用于将数据从控制器传递到视图的两种方法:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 8df1ca30f8c0415b68d29eeaa0f7d83a606989ff
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830475"
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="84b27-103">使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="84b27-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="84b27-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="84b27-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="84b27-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="84b27-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="84b27-106">这是一种免费的第 6 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="84b27-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="84b27-107">步骤 6 显示了如何启用对更丰富的窗体编辑方案中，支持，并还讨论了可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="84b27-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="84b27-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="84b27-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="84b27-109">NerdDinner 步骤 6: ViewData 和 ViewModel</span><span class="sxs-lookup"><span data-stu-id="84b27-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="84b27-110">我们已涵盖了多个窗体发布方案，并讨论了如何实现创建、 更新和删除 (CRUD) 支持。</span><span class="sxs-lookup"><span data-stu-id="84b27-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="84b27-111">现在，我们将采取进一步的我们 DinnersController 的实现，并启用对更丰富的窗体编辑方案的支持。</span><span class="sxs-lookup"><span data-stu-id="84b27-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="84b27-112">在此期间，我们将讨论可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="84b27-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="84b27-113">将数据从控制器传递到视图模板</span><span class="sxs-lookup"><span data-stu-id="84b27-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="84b27-114">MVC 模式的定义特征之一是严格"关注点分离"它可帮助应用程序的不同组件之间强制实施。</span><span class="sxs-lookup"><span data-stu-id="84b27-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="84b27-115">模型、 控制器和视图每个良好定义的角色和责任，并且它们彼此之间相互进行通信以定义完善的方式。</span><span class="sxs-lookup"><span data-stu-id="84b27-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="84b27-116">这有助于提升可测试性和代码重用。</span><span class="sxs-lookup"><span data-stu-id="84b27-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="84b27-117">当控制器类决定呈现 HTML 响应返回给客户端时，它负责显式传递到视图模板的所有数据所需呈现响应。</span><span class="sxs-lookup"><span data-stu-id="84b27-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="84b27-118">视图模板应永远不会执行任何数据检索或应用程序逻辑，并应改为其本身限制为只包含从控制器传递给它的模型/数据驱动的呈现代码。</span><span class="sxs-lookup"><span data-stu-id="84b27-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="84b27-119">稍后再试模型数据按我们 DinnersController 传递到我们的视图模板的类很简单，简单 – index （），对于 Dinner 对象的列表，以及单个 Dinner 对象在 Details()、 edit （）、 create （） 和 delete （） 的情况下。</span><span class="sxs-lookup"><span data-stu-id="84b27-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="84b27-120">因为我们将更多的 UI 功能添加到我们的应用程序时，我们通常要需要传递多个只是呈现 HTML 响应我们视图模板中的此数据。</span><span class="sxs-lookup"><span data-stu-id="84b27-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="84b27-121">例如，我们可能想要修改我们编辑中的"国家/地区"字段，从而成为一个 HTML 文本框，到 dropdownlist 创建视图。</span><span class="sxs-lookup"><span data-stu-id="84b27-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="84b27-122">而不是硬编码的视图模板中的国家/地区名称的下拉列表，我们可能想要生成基于的受支持的国家/地区，我们动态填充的列表。</span><span class="sxs-lookup"><span data-stu-id="84b27-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="84b27-123">我们将需要一种方法将 Dinner 对象传递*和*支持国家/地区列表从控制器到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="84b27-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="84b27-124">让我们看看我们可以实现此目的的两种方法。</span><span class="sxs-lookup"><span data-stu-id="84b27-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="84b27-125">使用 ViewData 字典</span><span class="sxs-lookup"><span data-stu-id="84b27-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="84b27-126">控制器基类公开可用于将其他数据项从控制器传递给视图的"ViewData"字典属性。</span><span class="sxs-lookup"><span data-stu-id="84b27-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="84b27-127">例如，若要支持我们想要从正在 dropdownlist 到一个 HTML 文本框，更改"国家/地区"文本框中的，我们编辑视图中的方案，我们可以更新将可用作 m SelectList 对象传递 （除了一个 Dinner 对象） 我们 edit （） 操作方法国家/地区 dropdownlist odel。</span><span class="sxs-lookup"><span data-stu-id="84b27-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="84b27-128">上述 SelectList 的构造函数接受县来填充，下拉 downlist，以及当前所选的值的列表。</span><span class="sxs-lookup"><span data-stu-id="84b27-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="84b27-129">然后，我们可以更新我们 Edit.aspx 视图模板，而不是我们使用了以前的 Html.TextBox() 帮助器方法使用 Html.DropDownList() 帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="84b27-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="84b27-130">上面的 Html.DropDownList() 帮助程序方法采用两个参数。</span><span class="sxs-lookup"><span data-stu-id="84b27-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="84b27-131">第一个是要输出的 HTML 窗体元素的名称。</span><span class="sxs-lookup"><span data-stu-id="84b27-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="84b27-132">第二个是我们通过 ViewData 字典传递"SelectList"模型。</span><span class="sxs-lookup"><span data-stu-id="84b27-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="84b27-133">我们使用 C#"作为"关键字将强制转换为 SelectList 字典中的类型。</span><span class="sxs-lookup"><span data-stu-id="84b27-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="84b27-134">现在，当我们运行我们的应用程序和访问权限和 */Dinners/Edit/1* URL 在浏览器中我们将看到我们编辑 UI 更新以显示 dropdownlist 的国家/地区而不是一个文本框：</span><span class="sxs-lookup"><span data-stu-id="84b27-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="84b27-135">因为我们还呈现中 （在方案中发生错误时） 的 HTTP POST 编辑方法的编辑视图模板，我们将需要确保我们还更新此方法将 SelectList 添加到 ViewData，在错误情况中呈现的视图模板时：</span><span class="sxs-lookup"><span data-stu-id="84b27-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="84b27-136">并且我们 DinnersController 的编辑方案现在支持 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="84b27-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="84b27-137">使用视图模型的模式</span><span class="sxs-lookup"><span data-stu-id="84b27-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="84b27-138">ViewData 字典方法具有优势是相当快速且轻松地实现。</span><span class="sxs-lookup"><span data-stu-id="84b27-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="84b27-139">一些开发人员不喜欢使用基于字符串的字典，不过，由于拼写错误可能会导致将不会在编译时捕获的错误。</span><span class="sxs-lookup"><span data-stu-id="84b27-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="84b27-140">非类型化的 ViewData 字典还需要使用"为"运算符或强制转换时使用 C# 等视图模板中的强类型化语言。</span><span class="sxs-lookup"><span data-stu-id="84b27-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="84b27-141">我们可以使用另一种方法是一个通常称为"视图模型的"模式。</span><span class="sxs-lookup"><span data-stu-id="84b27-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="84b27-142">使用此模式时我们将创建强类型化的类，针对我们特定视图的方案，进行了优化和其公开动态值/内容所需的视图模板的属性。</span><span class="sxs-lookup"><span data-stu-id="84b27-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="84b27-143">我们的控制器类可以填充，然后将这些视图优化类传递给我们要使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="84b27-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="84b27-144">这样，类型安全性、 编译时检查，以及在视图模板中的编辑器 intellisense。</span><span class="sxs-lookup"><span data-stu-id="84b27-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="84b27-145">例如，若要启用 dinner 窗体类似如下的编辑方案，我们可以创建"DinnerFormViewModel"类公开两个强类型属性： 一个 Dinner 对象和所需填充国家/地区 dropdownlist 的 SelectList 模型：</span><span class="sxs-lookup"><span data-stu-id="84b27-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="84b27-146">我们可以然后更新要创建使用从存储库中，我们检索的 Dinner 对象 DinnerFormViewModel 我们 edit （） 操作方法，并将其传递给视图模板：</span><span class="sxs-lookup"><span data-stu-id="84b27-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="84b27-147">然后我们视图模板，因此它需要"DinnerFormViewModel"而不是"Dinner"对象通过更改 edit.aspx 页面顶部的"继承"特性的更新如下所示，我们将：</span><span class="sxs-lookup"><span data-stu-id="84b27-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="84b27-148">我们执行此操作，我们视图模板中的"模型"属性的 intellisense 将更新以反映我们传递给它的 DinnerFormViewModel 类型的对象模型：</span><span class="sxs-lookup"><span data-stu-id="84b27-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="84b27-149">我们然后可以更新其工作我们查看代码。</span><span class="sxs-lookup"><span data-stu-id="84b27-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="84b27-150">请注意，我们未更改的输入元素的名称如何我们正在创建 （窗体元素将仍被命名为"Title"，"国家/地区"） – 但我们正在更新的 HTML 帮助器方法来检索使用 DinnerFormViewModel 类的值：</span><span class="sxs-lookup"><span data-stu-id="84b27-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="84b27-151">我们还会更新我们编辑 post 方法以呈现错误时所使用的 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="84b27-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="84b27-152">我们还可以更新我们的 create （） 操作方法，以重复使用的完全相同*DinnerFormViewModel*类来启用的国家/地区 DropDownList 中那些也。</span><span class="sxs-lookup"><span data-stu-id="84b27-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="84b27-153">下面是 HTTP GET 实现：</span><span class="sxs-lookup"><span data-stu-id="84b27-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="84b27-154">下面是创建 HTTP POST 方法的实现：</span><span class="sxs-lookup"><span data-stu-id="84b27-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="84b27-155">并且我们编辑和创建屏幕现在支持方法是下拉列表选择国家/地区。</span><span class="sxs-lookup"><span data-stu-id="84b27-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="84b27-156">自定义形状 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="84b27-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="84b27-157">在上述方案中，我们 DinnerFormViewModel 类直接将 Dinner 模型对象公开为属性，以及支持 SelectList 模型属性。</span><span class="sxs-lookup"><span data-stu-id="84b27-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="84b27-158">这种方法，我们要创建我们视图模板中的 HTML UI 方法相对较接近于我们的域模型对象的方案中工作正常。</span><span class="sxs-lookup"><span data-stu-id="84b27-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="84b27-159">这并不适合的情况下，可以使用的一种选择是创建一个自定义形状的 ViewModel 类的对象模型更适用于使用由视图 – 和可能看起来完全不同的基础的域模型对象。</span><span class="sxs-lookup"><span data-stu-id="84b27-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="84b27-160">例如，它可能会公开不同的属性名和/或从多个模型对象收集的聚合属性。</span><span class="sxs-lookup"><span data-stu-id="84b27-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="84b27-161">自定义形状 ViewModel 类可用于同时将数据从控制器传递到要呈现，以及用于帮助处理回发到控制器的操作方法的窗体数据的视图。</span><span class="sxs-lookup"><span data-stu-id="84b27-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="84b27-162">对于此更高版本的情况下，可能必须使用窗体发布数据中，更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际域模型对象的操作方法。</span><span class="sxs-lookup"><span data-stu-id="84b27-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="84b27-163">自定义形状 ViewModel 类可以提供了很大的灵活性，并需要调查任何时间在您开始太过于复杂的操作方法中的视图模板或窗体发布代码中找到的呈现代码。</span><span class="sxs-lookup"><span data-stu-id="84b27-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="84b27-164">这通常是登录域模型不完全对应于要生成的 UI 和中间形自定义 ViewModel 类可帮助。</span><span class="sxs-lookup"><span data-stu-id="84b27-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="84b27-165">下一步</span><span class="sxs-lookup"><span data-stu-id="84b27-165">Next Step</span></span>

<span data-ttu-id="84b27-166">让我们现在看一下如何使用分区和母版页的重复使用并在我们的应用程序之间共享 UI。</span><span class="sxs-lookup"><span data-stu-id="84b27-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84b27-167">[上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="84b27-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
