---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 和实现 ViewModel 类 |Microsoft 文档
author: microsoft
description: 步骤 6 显示如何启用对更丰富的形式编辑方案中的支持还介绍了可以用于将数据从控制器传递到视图的两种方法:...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 9ba8758bd6524f3e300f3fd91ef68cfe8a3587a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879421"
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="43311-103">使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="43311-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="43311-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="43311-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="43311-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="43311-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="43311-106">这是一个免费的第 6 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="43311-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="43311-107">步骤 6 显示如何启用对更丰富的形式编辑方案中的支持还介绍了可以用于将数据从控制器传递到视图的两种方法： ViewData 和视图模型。</span><span class="sxs-lookup"><span data-stu-id="43311-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="43311-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="43311-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="43311-109">NerdDinner 步骤 6: ViewData 和视图模型</span><span class="sxs-lookup"><span data-stu-id="43311-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="43311-110">我们已介绍大量的窗体 post 方案，并讨论了如何实现创建、 更新和删除 (CRUD) 支持。</span><span class="sxs-lookup"><span data-stu-id="43311-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="43311-111">现在，我们将进一步采用我们 DinnersController 实现，并启用对更丰富的形式编辑方案的支持。</span><span class="sxs-lookup"><span data-stu-id="43311-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="43311-112">在完成此任务中，我们将讨论这两种方法可以用于将数据从控制器传递到视图： ViewData 和视图模型。</span><span class="sxs-lookup"><span data-stu-id="43311-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="43311-113">将从控制器的数据传递给视图模板</span><span class="sxs-lookup"><span data-stu-id="43311-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="43311-114">MVC 模式的定义特征之一是指严格"隔离的问题"它有助于强制应用程序在不同组件之间。</span><span class="sxs-lookup"><span data-stu-id="43311-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="43311-115">模型、 控制器和视图每个很好地定义角色和职责，并且它们之间相互进行通信以定义完善的方式。</span><span class="sxs-lookup"><span data-stu-id="43311-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="43311-116">这有助于提升可测试性和代码重用。</span><span class="sxs-lookup"><span data-stu-id="43311-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="43311-117">当控制器类决定呈现 HTML 响应回客户端时，它负责显式将传递到的所有数据所需呈现响应查看模板。</span><span class="sxs-lookup"><span data-stu-id="43311-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="43311-118">查看模板应永远不会执行任何数据检索或应用程序逻辑 –，并应改为将其本身为只包含从传递给它由控制器模型/数据驱动的呈现代码限制。</span><span class="sxs-lookup"><span data-stu-id="43311-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="43311-119">稍后再试模型数据按我们 DinnersController 传递到我们查看模板的类很简单，直截了当的 – 的 index （），对于 Dinner 对象的列表和单个 Dinner 对象对于 Details()、 edit （）、 create （） 和 delete （）。</span><span class="sxs-lookup"><span data-stu-id="43311-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="43311-120">我们将更多的用户界面功能添加到我们的应用程序时，我们通常将需要传递多个仅呈现在我们的视图模板中的 HTML 响应此数据。</span><span class="sxs-lookup"><span data-stu-id="43311-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="43311-121">例如，我们可能想要修改我们编辑中的"国家/地区"字段，从而防止到 dropdownlist HTML 文本框中创建视图。</span><span class="sxs-lookup"><span data-stu-id="43311-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="43311-122">而不是硬编码的视图模板中的国家/地区名称的下拉列表，我们可能想要生成从我们动态填充的受支持国家/地区的列表。</span><span class="sxs-lookup"><span data-stu-id="43311-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="43311-123">我们将需要一种方法将 Dinner 对象传递*和*支持国家/地区从我们控制器到我们查看模板的列表。</span><span class="sxs-lookup"><span data-stu-id="43311-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="43311-124">让我们看一下我们可以实现此目的的两种方法。</span><span class="sxs-lookup"><span data-stu-id="43311-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="43311-125">使用 ViewData 字典</span><span class="sxs-lookup"><span data-stu-id="43311-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="43311-126">控制器基该类会公开一个"ViewData"字典属性，可以用于将从控制器的其他数据项传递到视图。</span><span class="sxs-lookup"><span data-stu-id="43311-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="43311-127">例如，若要支持的方案，我们想要从正在到 dropdownlist HTML 文本框中更改"国家/地区"文本框中，我们编辑视图中的，我们可以更新我们 edit （） 的操作方法中将可以用作 m 此时对象传递 （除了一个 Dinner 对象）国家/地区 dropdownlist odel。</span><span class="sxs-lookup"><span data-stu-id="43311-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="43311-128">上述此时的构造函数将接受所在国家/地区来填充，放 downlist，以及当前选择的值的列表。</span><span class="sxs-lookup"><span data-stu-id="43311-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="43311-129">然后，我们可以更新我们 Edit.aspx 视图模板，而不是我们以前使用的 Html.TextBox() 帮助器方法使用 Html.DropDownList() 帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="43311-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="43311-130">上面的 Html.DropDownList() 帮助程序方法采用两个参数。</span><span class="sxs-lookup"><span data-stu-id="43311-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="43311-131">第一个是要输出的 HTML 窗体元素的名称。</span><span class="sxs-lookup"><span data-stu-id="43311-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="43311-132">第二个是我们通过 ViewData 字典传递"此时"模型。</span><span class="sxs-lookup"><span data-stu-id="43311-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="43311-133">我们将使用 C#"as"关键字来强制转换为此时字典中的类型。</span><span class="sxs-lookup"><span data-stu-id="43311-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="43311-134">现在当我们运行我们的应用程序和访问时和 */Dinners/Edit/1* URL 我们浏览器中我们将看到我们编辑 UI 更新以显示国家/地区，而不是文本框中的说明：</span><span class="sxs-lookup"><span data-stu-id="43311-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="43311-135">因为我们也呈现编辑视图模板从 HTTP POST 编辑方法 （在方案中发生错误时），我们将需要确保我们还更新此方法可添加到 ViewData 此时，在错误情况中呈现的视图模板时：</span><span class="sxs-lookup"><span data-stu-id="43311-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="43311-136">并且，我们 DinnersController 的编辑方案现在支持 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="43311-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="43311-137">使用 ViewModel 模式</span><span class="sxs-lookup"><span data-stu-id="43311-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="43311-138">ViewData 字典方法具有一个优势是相当快速且轻松地实现。</span><span class="sxs-lookup"><span data-stu-id="43311-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="43311-139">一些开发人员不喜欢使用基于字符串的字典，不过，由于拼写错误可能导致在编译时将不会捕获的错误。</span><span class="sxs-lookup"><span data-stu-id="43311-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="43311-140">非类型化的 ViewData 字典还需要使用"为"运算符或强制转换时使用 C# 之类视图模板中的强类型语言。</span><span class="sxs-lookup"><span data-stu-id="43311-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="43311-141">我们可以使用一种方法是一个通常称为"ViewModel"模式。</span><span class="sxs-lookup"><span data-stu-id="43311-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="43311-142">使用此模式时我们将创建强类型的类对于我们的特定视图方案，进行优化的和其公开的动态值/所需内容由我们视图模板的属性。</span><span class="sxs-lookup"><span data-stu-id="43311-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="43311-143">然后，我们控制器类可以填充，并将这些视图优化类传递给我们要使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="43311-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="43311-144">这样，类型安全，编译时检查，和编辑器 intellisense 中查看模板。</span><span class="sxs-lookup"><span data-stu-id="43311-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="43311-145">例如，若要启用 dinner 窗体类似下面的编辑方案我们可以创建"DinnerFormViewModel"类公开两个强类型属性： Dinner 对象和所需填充国家/地区的 dropdownlist 此时模型：</span><span class="sxs-lookup"><span data-stu-id="43311-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="43311-146">我们可以然后更新要创建使用从我们的存储库，我们检索 Dinner 对象 DinnerFormViewModel 我们 edit （） 操作方法，并将其传递给我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="43311-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="43311-147">我们将然后更新我们视图模板，因此它需要"DinnerFormViewModel"而不是"Dinner"对象通过更改 edit.aspx 页顶部的"继承"属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="43311-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="43311-148">一旦我们执行此操作，我们视图模板中的"模型"属性的 intellisense 将更新以反映我们传递的 DinnerFormViewModel 类型的对象模型：</span><span class="sxs-lookup"><span data-stu-id="43311-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="43311-149">然后，我们可以更新我们查看代码，以便关闭它。</span><span class="sxs-lookup"><span data-stu-id="43311-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="43311-150">请注意如何我们未更改的输入元素的名称下面，我们将创建 （窗体元素将仍被命名为"标题"、"国家/地区"） – 但我们正在更新的 HTML 帮助器方法来检索使用 DinnerFormViewModel 类的值：</span><span class="sxs-lookup"><span data-stu-id="43311-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="43311-151">我们将更新时要使用 DinnerFormViewModel 类的呈现错误我们编辑 post 方法：</span><span class="sxs-lookup"><span data-stu-id="43311-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="43311-152">我们还可以更新我们的 create （） 的操作方法以重复使用的确切相同*DinnerFormViewModel*类启用的国家/地区的 DropDownList 中那些以及。</span><span class="sxs-lookup"><span data-stu-id="43311-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="43311-153">下面是 HTTP GET 实现：</span><span class="sxs-lookup"><span data-stu-id="43311-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="43311-154">下面是创建 HTTP POST 方法的实现：</span><span class="sxs-lookup"><span data-stu-id="43311-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="43311-155">和我们编辑和创建屏幕现在支持针对选取国家/地区的方法是下拉列表。</span><span class="sxs-lookup"><span data-stu-id="43311-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="43311-156">自定义形状 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="43311-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="43311-157">在上述方案中，我们 DinnerFormViewModel 类直接作为属性，以及支持此时模型属性公开 Dinner 模型对象。</span><span class="sxs-lookup"><span data-stu-id="43311-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="43311-158">此方法很好地适用于其中我们要在我们的视图模板创建的 HTML UI 方法相对较接近于我们域模型对象的方案。</span><span class="sxs-lookup"><span data-stu-id="43311-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="43311-159">对于方案这不是这种情况，你可以使用的一个选项是创建一个自定义形状的 ViewModel 类更视图 – 将其对象模型优化为消耗和可能看起来完全不同于基础的域模型对象。</span><span class="sxs-lookup"><span data-stu-id="43311-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="43311-160">例如，它可能无法公开不同的属性名称和/或从多个模型对象收集的聚合属性。</span><span class="sxs-lookup"><span data-stu-id="43311-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="43311-161">可以自定义形状 ViewModel 类用于同时将数据从控制器传递到呈现，以及以帮助处理回发到控制器的操作方法的窗体数据的视图。</span><span class="sxs-lookup"><span data-stu-id="43311-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="43311-162">对于此更高版本的情况下，你可能必须使用窗体发送数据，更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际域模型对象的操作方法。</span><span class="sxs-lookup"><span data-stu-id="43311-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="43311-163">自定义形状 ViewModel 类可以提供极大的灵活性，并需要调查任何时间在你开始获取过于复杂的操作方法中的视图模板或窗体发布代码中查找呈现代码。</span><span class="sxs-lookup"><span data-stu-id="43311-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="43311-164">这通常是注册你的域模型不完全对应于你要生成的 UI 和中间的自定义形状 ViewModel 类可帮助。</span><span class="sxs-lookup"><span data-stu-id="43311-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="43311-165">下一步</span><span class="sxs-lookup"><span data-stu-id="43311-165">Next Step</span></span>

<span data-ttu-id="43311-166">让我们现在看一下我们可以如何使用它们和主控页重复使用并在我们的应用程序之间共享 UI。</span><span class="sxs-lookup"><span data-stu-id="43311-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="43311-167">[上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="43311-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
