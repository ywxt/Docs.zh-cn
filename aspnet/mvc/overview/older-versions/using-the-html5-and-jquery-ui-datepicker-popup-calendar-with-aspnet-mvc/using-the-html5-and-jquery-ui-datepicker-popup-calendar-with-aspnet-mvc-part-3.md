---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 使用 ASP.NET MVC-第 3 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历 |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: fd1ae746f4f134b779c7eee50cf6c840bbb7068e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869460"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="da39c-103">使用 ASP.NET MVC-第 3 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历</span><span class="sxs-lookup"><span data-stu-id="da39c-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>
====================
<span data-ttu-id="da39c-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="da39c-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="da39c-105">本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MVC Web 应用程序中的基础知识。</span><span class="sxs-lookup"><span data-stu-id="da39c-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="working-with-complex-types"></a><span data-ttu-id="da39c-106">使用复杂类型</span><span class="sxs-lookup"><span data-stu-id="da39c-106">Working with Complex Types</span></span>

<span data-ttu-id="da39c-107">在本节中你将创建一个地址类，并了解如何创建模板，以显示它。</span><span class="sxs-lookup"><span data-stu-id="da39c-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="da39c-108">在*模型*文件夹中，创建名为的新类文件*Person.cs*将放置两种类型的位置：`Person`类和`Address`类。</span><span class="sxs-lookup"><span data-stu-id="da39c-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="da39c-109">`Person`类将包含一个属性，被类型化为`Address`。</span><span class="sxs-lookup"><span data-stu-id="da39c-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="da39c-110">`Address`类型是复杂类型，这意味着不内置类型，如之一`int`， `string`，或`double`。</span><span class="sxs-lookup"><span data-stu-id="da39c-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="da39c-111">相反，它具有多个属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-111">Instead, it has several properties.</span></span> <span data-ttu-id="da39c-112">新的类的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="da39c-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="da39c-113">在`Movie`控制器上，添加以下`PersonDetail`操作以显示 person 实例：</span><span class="sxs-lookup"><span data-stu-id="da39c-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="da39c-114">然后添加以下代码到`Movie`控制器来填充`Person`用一些示例数据模型：</span><span class="sxs-lookup"><span data-stu-id="da39c-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="da39c-115">打开*Views\Movies\PersonDetail.cshtml*文件并添加以下标记`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="da39c-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="da39c-116">按 Ctrl + F5 运行应用程序并导航到*电影/PersonDetail*。</span><span class="sxs-lookup"><span data-stu-id="da39c-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="da39c-117">`PersonDetail`视图不包含`Address`复杂类型，可以看出，在此屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="da39c-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="da39c-118">（不显示为任何地址。）</span><span class="sxs-lookup"><span data-stu-id="da39c-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="da39c-119">`Address`模型数据将不显示，因为它是一个复杂类型。</span><span class="sxs-lookup"><span data-stu-id="da39c-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="da39c-120">若要显示的地址信息，请打开*Views\Movies\PersonDetail.cshtml*再次文件并添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="da39c-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="da39c-121">完整标记`PersonDetail`现在视图如下所示：</span><span class="sxs-lookup"><span data-stu-id="da39c-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="da39c-122">运行一次，应用程序并显示`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="da39c-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="da39c-123">现在显示的地址信息：</span><span class="sxs-lookup"><span data-stu-id="da39c-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="da39c-124">创建用于复杂类型的模板</span><span class="sxs-lookup"><span data-stu-id="da39c-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="da39c-125">在本部分中，你将创建将用于呈现模板`Address`复杂类型。</span><span class="sxs-lookup"><span data-stu-id="da39c-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="da39c-126">当你创建的模板`Address`类型，ASP.NET MVC 可以自动使用它来设置应用程序中的任意位置的地址模型的格式。</span><span class="sxs-lookup"><span data-stu-id="da39c-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="da39c-127">这使你能够控制的呈现`Address`从一个地方即可应用程序中的类型。</span><span class="sxs-lookup"><span data-stu-id="da39c-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="da39c-128">在*Views\Shared\DisplayTemplates*文件夹中，创建名为强类型的分部视图**地址**:</span><span class="sxs-lookup"><span data-stu-id="da39c-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="da39c-129">单击**添加**，然后打开新*Views\Shared\DisplayTemplates\Address.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="da39c-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="da39c-130">新视图包含以下生成的标记：</span><span class="sxs-lookup"><span data-stu-id="da39c-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="da39c-131">运行应用程序并显示`PersonDetail`视图。</span><span class="sxs-lookup"><span data-stu-id="da39c-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="da39c-132">此时，`Address`刚创建的模板用于显示`Address`复杂类型，以便显示如下所示：</span><span class="sxs-lookup"><span data-stu-id="da39c-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="da39c-133">摘要： 方式可以指定的模型显示格式和模板</span><span class="sxs-lookup"><span data-stu-id="da39c-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="da39c-134">你已了解你可以通过使用以下方法指定的格式或模型属性的模板：</span><span class="sxs-lookup"><span data-stu-id="da39c-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="da39c-135">应用`DisplayFormat`属性设为模型中的属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="da39c-136">例如，下面的代码会导致没有时间的情况下显示的日期：</span><span class="sxs-lookup"><span data-stu-id="da39c-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="da39c-137">应用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性中的模型和指定的数据类型的属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="da39c-138">例如，下面的代码会导致没有时间的情况下显示的日期。</span><span class="sxs-lookup"><span data-stu-id="da39c-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="da39c-139">如果应用程序包含*date.cshtml*中的模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中，该模板将用于呈现`DateTime`属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="da39c-140">否则内置 ASP.NET 模板化系统将显示为日期属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="da39c-141">创建中的显示模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*其名称与你想要设置格式的数据类型相匹配的文件夹。</span><span class="sxs-lookup"><span data-stu-id="da39c-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="da39c-142">例如，您会看到*Views\Shared\DisplayTemplates\DateTime.cshtml*用于呈现`DateTime`模型，而无需添加到模型的属性，而无需任何标记添加到视图中的属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="da39c-143">使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)模型上要指定要显示的模型属性的模板的属性。</span><span class="sxs-lookup"><span data-stu-id="da39c-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="da39c-144">显式添加到的显示模板名称[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)调用在视图中。</span><span class="sxs-lookup"><span data-stu-id="da39c-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="da39c-145">你使用的方法取决于你需要在你的应用程序中执行操作。</span><span class="sxs-lookup"><span data-stu-id="da39c-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="da39c-146">并不少见混合使用这些方法以获取恰恰格式设置所需。</span><span class="sxs-lookup"><span data-stu-id="da39c-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="da39c-147">在下一步的部分中，你将切换项有点内容，将从自定义如何到自定义输入方式显示的数据移动。</span><span class="sxs-lookup"><span data-stu-id="da39c-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="da39c-148">您将挂钩到应用程序，以便提供指定日期的巧妙方法中的编辑视图 jQuery 包含 datepicker。</span><span class="sxs-lookup"><span data-stu-id="da39c-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="da39c-149">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="da39c-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
