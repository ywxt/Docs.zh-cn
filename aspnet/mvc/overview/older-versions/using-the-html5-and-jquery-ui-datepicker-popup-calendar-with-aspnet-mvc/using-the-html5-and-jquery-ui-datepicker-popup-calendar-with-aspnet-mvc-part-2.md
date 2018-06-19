---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 使用 ASP.NET MVC-第 2 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历 |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 84112316a9ace732cb7d75d7cbaeb071c72de822
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875443"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="6cf19-103">使用 ASP.NET MVC-第 2 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历</span><span class="sxs-lookup"><span data-stu-id="6cf19-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>
====================
<span data-ttu-id="6cf19-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="6cf19-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="6cf19-105">本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MVC Web 应用程序中的基础知识。</span><span class="sxs-lookup"><span data-stu-id="6cf19-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="6cf19-106">添加自动的 DateTime 模板</span><span class="sxs-lookup"><span data-stu-id="6cf19-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="6cf19-107">在本教程的第一部分，您将了解如何将属性添加到模型后，若要显式指定格式设置，以及如何显式指定用于对模型进行渲染的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="6cf19-108">例如， [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)中下面的代码显式属性指定的格式设置`ReleaseDate`属性。</span><span class="sxs-lookup"><span data-stu-id="6cf19-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicity specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="6cf19-109">在下面的示例中， [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性，使用`Date`枚举，指定日期模板应该用于对模型进行渲染。</span><span class="sxs-lookup"><span data-stu-id="6cf19-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="6cf19-110">如果你的项目中没有日期的模板，则使用内置日期模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="6cf19-111">但是，ASP。MVC，可以执行类型匹配通过查找与一种类型的名称匹配的模板来使用约定转移配置。</span><span class="sxs-lookup"><span data-stu-id="6cf19-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="6cf19-112">这允许您创建的模板，自动设置数据格式不使用任何属性或代码在所有情况下。</span><span class="sxs-lookup"><span data-stu-id="6cf19-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="6cf19-113">对于本教程的此部分，你将创建的模板，将自动应用于类型的模型属性[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6cf19-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="6cf19-114">无需使用属性或其他配置来指定应使用的模板来呈现的类型的所有模型属性[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6cf19-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="6cf19-115">你还将了解了如何自定义单独的属性或甚至是单个字段的显示。</span><span class="sxs-lookup"><span data-stu-id="6cf19-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="6cf19-116">若要开始，让我们删除现有的格式设置信息，并在应用程序中显示完整的日期。</span><span class="sxs-lookup"><span data-stu-id="6cf19-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="6cf19-117">打开*Movie.cs*文件，并注释掉`DataType`属性`ReleaseDate`属性：</span><span class="sxs-lookup"><span data-stu-id="6cf19-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="6cf19-118">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="6cf19-119">请注意，`ReleaseDate`属性现在显示的日期和时间，因为这是默认值时未不提供任何格式设置信息。</span><span class="sxs-lookup"><span data-stu-id="6cf19-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="6cf19-120">为测试新模板添加 CSS 样式</span><span class="sxs-lookup"><span data-stu-id="6cf19-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="6cf19-121">在创建用于设置日期格式的模板之前，你将添加一些 CSS 样式规则可应用于新的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="6cf19-122">这些将帮助您验证在呈现的页面使用的新模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="6cf19-123">打开*Content\Site.cs*s 文件并将以下 CSS 规则添加到文件的底部：</span><span class="sxs-lookup"><span data-stu-id="6cf19-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="6cf19-124">添加日期时间的显示模板</span><span class="sxs-lookup"><span data-stu-id="6cf19-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="6cf19-125">现在你可以创建新的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-125">Now you can create the new template.</span></span> <span data-ttu-id="6cf19-126">在*Views\Movies*文件夹中，创建*DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="6cf19-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="6cf19-127">在*views/shared*文件夹中，创建*DisplayTemplates*文件夹和*EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="6cf19-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="6cf19-128">中的显示模板*Views\Shared\DisplayTemplates*文件夹将由所有控制器。</span><span class="sxs-lookup"><span data-stu-id="6cf19-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="6cf19-129">中的显示模板*Views\Movie\DisplayTemplates*将仅可由使用文件夹`Movie`控制器。</span><span class="sxs-lookup"><span data-stu-id="6cf19-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="6cf19-130">(如果具有相同名称的模板出现在这两个文件夹中中的模板*Views\Movie\DisplayTemplates*文件夹 — 也就是说，更具体的模板-优先视图返回的`Movie`控制器。)</span><span class="sxs-lookup"><span data-stu-id="6cf19-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="6cf19-131">在**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="6cf19-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="6cf19-132">单击**添加**，然后单击**视图**。</span><span class="sxs-lookup"><span data-stu-id="6cf19-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="6cf19-133">**添加视图**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="6cf19-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="6cf19-134">在**视图名称**框中，键入`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="6cf19-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="6cf19-135">（你必须使用此名称以便匹配类型的名称。）</span><span class="sxs-lookup"><span data-stu-id="6cf19-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="6cf19-136">选择**创建为分部视图**复选框。</span><span class="sxs-lookup"><span data-stu-id="6cf19-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="6cf19-137">请确保**使用的布局或 master 页面**和**创建强类型化视图**不选中的复选框。</span><span class="sxs-lookup"><span data-stu-id="6cf19-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="6cf19-138">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="6cf19-138">Click **Add**.</span></span> <span data-ttu-id="6cf19-139">A *DateTime.cshtml*中创建模板*Views\Shared\DisplayTemplates*。</span><span class="sxs-lookup"><span data-stu-id="6cf19-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="6cf19-140">下图显示*视图*文件夹中的**解决方案资源管理器**后`DateTime`创建显示和编辑器模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="6cf19-141">打开*Views\Shared\DisplayTemplates\DateTime.cshtml*文件并添加以下标记，使用[String.Format](https://msdn.microsoft.com/library/system.string.format.aspx)方法来设置该属性为无时间日期格式。</span><span class="sxs-lookup"><span data-stu-id="6cf19-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="6cf19-142">(`{0:d}`格式指定短日期格式。)</span><span class="sxs-lookup"><span data-stu-id="6cf19-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="6cf19-143">重复此步骤以创建`DateTime`中的模板*Views\Movie\DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="6cf19-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="6cf19-144">使用下面的代码*Views\Movie\DisplayTemplates\DateTime.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="6cf19-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="6cf19-145">`loud-1` CSS 类将导致为红色粗体文本显示的日期。</span><span class="sxs-lookup"><span data-stu-id="6cf19-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="6cf19-146">你添加`loud-1`一样临时度量值，以便你可以轻松地查看此特定模板中使用时的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="6cf19-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="6cf19-147">已执行哪些操作将创建并自定义 ASP.NET 将用来显示日期的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="6cf19-148">更多常规模板 (在*Views\Shared\DisplayTemplates*文件夹) 显示简单的短日期。</span><span class="sxs-lookup"><span data-stu-id="6cf19-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="6cf19-149">专用于模板`Movie`控制器 (在*Views\Movies\DisplayTemplates*文件夹) 将也格式化短日期显示为红色粗体文本。</span><span class="sxs-lookup"><span data-stu-id="6cf19-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="6cf19-150">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="6cf19-151">浏览器呈现应用程序的索引视图。</span><span class="sxs-lookup"><span data-stu-id="6cf19-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="6cf19-152">`ReleaseDate`属性现在以红色粗体无时间中显示的日期。这可帮助你确认`DateTime`中的模板化帮助器*Views\Movies\DisplayTemplates*文件夹所选的转移`DateTime`共享文件夹中的模板化帮助器 (*Views\Shared\DisplayTemplates*)。</span><span class="sxs-lookup"><span data-stu-id="6cf19-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="6cf19-153">现在重命名*Views\Movies\DisplayTemplates\DateTime.cshtml*文件为*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="6cf19-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="6cf19-154">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="6cf19-155">这一次`ReleaseDate`属性显示日期时间而不以粗体显示的红色字体。</span><span class="sxs-lookup"><span data-stu-id="6cf19-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="6cf19-156">这表明，具有的数据的名称的模板类型 (在这种情况下`DateTime`) 会自动使用来显示该类型的所有模型属性。</span><span class="sxs-lookup"><span data-stu-id="6cf19-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="6cf19-157">重命名检查完*DateTime.cshtml*文件为*LoudDateTime.cshtml*，找不到 ASP.NET 中的模板*Views\Movies\DisplayTemplates*文件夹，所以只有在使用*DateTime.cshtml*从模板 * Views\Movies\Shared\*文件夹。</span><span class="sxs-lookup"><span data-stu-id="6cf19-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the *Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="6cf19-158">（模板匹配是区分大小写，因此你可以使用任何大小写创建模板文件的名称。</span><span class="sxs-lookup"><span data-stu-id="6cf19-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="6cf19-159">例如， *DATETIME.chstml、 datetime.cshtml*，和*DaTeTiMe.cshtml*将所有匹配`DateTime`类型。)</span><span class="sxs-lookup"><span data-stu-id="6cf19-159">For example, *DATETIME.chstml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="6cf19-160">若要查看： 此时，`ReleaseDate`字段显示的是使用*Views\Movies\DisplayTemplates\DateTime.cshtml*模板，但显示的数据使用短日期格式，否则将添加没有特殊格式。</span><span class="sxs-lookup"><span data-stu-id="6cf19-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="6cf19-161">使用 UIHint 若要指定显示模板</span><span class="sxs-lookup"><span data-stu-id="6cf19-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="6cf19-162">如果 web 应用程序的许多`DateTime`字段并且默认情况下你想要仅日期格式显示全部或大部分它们*DateTime.cshtml*模板是一种好方法。</span><span class="sxs-lookup"><span data-stu-id="6cf19-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="6cf19-163">但是，如果您有几个日期想要显示的完整的日期和时间？</span><span class="sxs-lookup"><span data-stu-id="6cf19-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="6cf19-164">没问题。</span><span class="sxs-lookup"><span data-stu-id="6cf19-164">No problem.</span></span> <span data-ttu-id="6cf19-165">你可以创建其他模板，并使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)特性以指定完整的日期和时间格式设置。</span><span class="sxs-lookup"><span data-stu-id="6cf19-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="6cf19-166">然后，你可以有选择地应用该模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-166">You can then selectively apply that template.</span></span> <span data-ttu-id="6cf19-167">你可以使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)在模型级别或你的特性可以指定视图内的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="6cf19-168">在此部分中，你将了解如何使用`UIHint`特性有选择地更改某些情况下的日期时间字段的格式。</span><span class="sxs-lookup"><span data-stu-id="6cf19-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="6cf19-169">打开*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*文件并将现有代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="6cf19-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="6cf19-170">这会导致要显示的完整的日期和时间，并将添加 CSS 类，使该文本，绿色和大型。</span><span class="sxs-lookup"><span data-stu-id="6cf19-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="6cf19-171">打开*Movie.cs*文件并添加[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性设为`ReleaseDate`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="6cf19-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="6cf19-172">这将告知 ASP.NET MVC，在显示时`ReleaseDate`属性 (具体而言，并不只是任何`DateTime`对象)，它应使用*LoudDateTime.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="6cf19-173">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="6cf19-174">请注意，`ReleaseDate`属性现在显示的日期和时间，大的绿色字体。</span><span class="sxs-lookup"><span data-stu-id="6cf19-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="6cf19-175">返回到`UIHint`属性中*Movie.cs*文件，并注释掉因此*LoudDateTime.cshtml*不会使用模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="6cf19-176">再次运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-176">Run the application again.</span></span> <span data-ttu-id="6cf19-177">发布日期不会显示大型和绿色。</span><span class="sxs-lookup"><span data-stu-id="6cf19-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="6cf19-178">此验证*Views\Shared\DisplayTemplates\DateTime.cshtml*索引和详细信息视图中使用模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="6cf19-179">如前所述，你还可以应用在视图中，这样就可以将模板应用到一个单独的实例的某些数据模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="6cf19-180">打开*Views\Movies\Details.cshtml*视图。</span><span class="sxs-lookup"><span data-stu-id="6cf19-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="6cf19-181">添加`"LoudDateTime"`的第二个参数[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)寻求`ReleaseDate`字段。</span><span class="sxs-lookup"><span data-stu-id="6cf19-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="6cf19-182">完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="6cf19-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="6cf19-183">此步骤指定`LoudDateTime`应使用模板来显示模型属性，而不考虑哪些属性应用于模型。</span><span class="sxs-lookup"><span data-stu-id="6cf19-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="6cf19-184">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="6cf19-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="6cf19-185">验证是否正在使用影片索引页*Views\Shared\DisplayTemplates\DateTime.cshtml*模板 （红色粗体） 和*Movie\Details*网页使用的*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*模板 （大型和绿色）。</span><span class="sxs-lookup"><span data-stu-id="6cf19-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="6cf19-186">在下一步的部分中，你将创建用于复杂类型的模板。</span><span class="sxs-lookup"><span data-stu-id="6cf19-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6cf19-187">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="6cf19-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
