---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 3 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: 11f9e0a8602e9ee1feda9d0e7d0d319add7c440c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400766"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="182a6-103">使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 3 部分</span><span class="sxs-lookup"><span data-stu-id="182a6-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>
====================
<span data-ttu-id="182a6-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="182a6-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="182a6-105">本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="182a6-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="working-with-complex-types"></a><span data-ttu-id="182a6-106">使用复杂类型</span><span class="sxs-lookup"><span data-stu-id="182a6-106">Working with Complex Types</span></span>

<span data-ttu-id="182a6-107">在本部分将创建 address 类，并了解如何创建模板，以显示它。</span><span class="sxs-lookup"><span data-stu-id="182a6-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="182a6-108">在中*模型*文件夹中，创建名为的新类文件*Person.cs*放置两种类型：`Person`类和一个`Address`类。</span><span class="sxs-lookup"><span data-stu-id="182a6-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="182a6-109">`Person`类将包含一个属性，它被类型化为`Address`。</span><span class="sxs-lookup"><span data-stu-id="182a6-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="182a6-110">`Address`类型是复杂类型，这意味着它不属于内置类型，如`int`， `string`，或`double`。</span><span class="sxs-lookup"><span data-stu-id="182a6-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="182a6-111">相反，它具有多个属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-111">Instead, it has several properties.</span></span> <span data-ttu-id="182a6-112">新的类的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="182a6-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="182a6-113">在中`Movie`控制器中，添加以下`PersonDetail`操作以显示 person 实例：</span><span class="sxs-lookup"><span data-stu-id="182a6-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="182a6-114">然后将以下代码添加到`Movie`控制器来填充`Person`具有一些示例数据的模型：</span><span class="sxs-lookup"><span data-stu-id="182a6-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="182a6-115">打开*Views\Movies\PersonDetail.cshtml*文件，并添加以下标记为`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="182a6-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="182a6-116">按 Ctrl + F5 运行应用程序并导航到*电影/PersonDetail*。</span><span class="sxs-lookup"><span data-stu-id="182a6-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="182a6-117">`PersonDetail`视图不包含`Address`复杂类型，可以看出，在此屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="182a6-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="182a6-118">（不显示为任何地址。）</span><span class="sxs-lookup"><span data-stu-id="182a6-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="182a6-119">`Address`因为它是一种复杂类型，不显示模型数据。</span><span class="sxs-lookup"><span data-stu-id="182a6-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="182a6-120">若要显示的地址信息，请打开*Views\Movies\PersonDetail.cshtml*再次文件，并添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="182a6-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="182a6-121">完整标记`PersonDetail`现在视图如下所示：</span><span class="sxs-lookup"><span data-stu-id="182a6-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="182a6-122">运行一次应用程序并显示`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="182a6-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="182a6-123">现在显示的地址信息：</span><span class="sxs-lookup"><span data-stu-id="182a6-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="182a6-124">为复杂类型创建模板</span><span class="sxs-lookup"><span data-stu-id="182a6-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="182a6-125">在本部分将创建将用于呈现模板`Address`复杂类型。</span><span class="sxs-lookup"><span data-stu-id="182a6-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="182a6-126">当你创建的模板`Address`类型，ASP.NET MVC 可自动使用它来设置应用程序中的任意位置的地址模型的格式。</span><span class="sxs-lookup"><span data-stu-id="182a6-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="182a6-127">这提供了一种方法来控制的呈现`Address`从一个地方即可在应用程序中的类型。</span><span class="sxs-lookup"><span data-stu-id="182a6-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="182a6-128">在中*Views\Shared\DisplayTemplates*文件夹中，创建名为的强类型化分部视图**地址**:</span><span class="sxs-lookup"><span data-stu-id="182a6-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="182a6-129">单击**外**，然后打开新*Views\Shared\DisplayTemplates\Address.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="182a6-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="182a6-130">新视图包含以下生成的标记：</span><span class="sxs-lookup"><span data-stu-id="182a6-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="182a6-131">运行应用程序并显示`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="182a6-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="182a6-132">这一次，`Address`刚创建的模板用于显示`Address`复杂类型，以便显示看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="182a6-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="182a6-133">指定的模型显示格式和模板摘要： 方法</span><span class="sxs-lookup"><span data-stu-id="182a6-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="182a6-134">您所见，您可以通过使用以下方法指定的格式或模型属性的模板：</span><span class="sxs-lookup"><span data-stu-id="182a6-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="182a6-135">将应用`DisplayFormat`属性为模型中的属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="182a6-136">例如，下面的代码会导致没有时间的情况下显示的日期：</span><span class="sxs-lookup"><span data-stu-id="182a6-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="182a6-137">将应用[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性中的模型和指定的数据类型的属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="182a6-138">例如，下面的代码会导致没有时间的情况下显示的日期。</span><span class="sxs-lookup"><span data-stu-id="182a6-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="182a6-139">如果应用程序包含*date.cshtml*中的模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中，该模板将用于呈现`DateTime`属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="182a6-140">否则内置的 ASP.NET 模板化系统将显示为日期属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="182a6-141">创建中的显示模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*其名称与你想要设置格式的数据类型相匹配的文件夹。</span><span class="sxs-lookup"><span data-stu-id="182a6-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="182a6-142">例如，您会看到*Views\Shared\DisplayTemplates\DateTime.cshtml*用于呈现`DateTime`模型，而无需添加到模型属性，而无需将任何标记添加到视图中的属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="182a6-143">使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)模型以指定要显示的模型属性的模板的属性。</span><span class="sxs-lookup"><span data-stu-id="182a6-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="182a6-144">显式添加到的显示模板名称[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)在视图中调用。</span><span class="sxs-lookup"><span data-stu-id="182a6-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="182a6-145">您使用的方法取决于您需要在你的应用程序中执行操作。</span><span class="sxs-lookup"><span data-stu-id="182a6-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="182a6-146">不少见混合使用这些方法以获取确切的类型的格式设置所需的。</span><span class="sxs-lookup"><span data-stu-id="182a6-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="182a6-147">在下一步部分中，将切换话题有点并从自定义如何向自定义输入的方式显示数据移动。</span><span class="sxs-lookup"><span data-stu-id="182a6-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="182a6-148">将挂接到应用程序，以便提供用于指定日期的巧妙方法中的编辑视图 jQuery datepicker。</span><span class="sxs-lookup"><span data-stu-id="182a6-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="182a6-149">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="182a6-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
