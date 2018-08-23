---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 2 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 572185507016afc26fc2e06ede55361b2daed277
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832906"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="0a911-103">使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 2 部分</span><span class="sxs-lookup"><span data-stu-id="0a911-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>
====================
<span data-ttu-id="0a911-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="0a911-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="0a911-105">本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="0a911-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="0a911-106">添加自动的 DateTime 模板</span><span class="sxs-lookup"><span data-stu-id="0a911-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="0a911-107">在本教程的第一部分，您了解了如何将属性添加到模型以显式指定的格式设置，以及如何可以显式指定用于呈现模型的模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="0a911-108">例如， [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性在以下代码显式指定的格式设置`ReleaseDate`属性。</span><span class="sxs-lookup"><span data-stu-id="0a911-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicity specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="0a911-109">在以下示例中，[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性，使用`Date`枚举，指定应使用日期模板来呈现模型。</span><span class="sxs-lookup"><span data-stu-id="0a911-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="0a911-110">如果在项目中没有日期模板，则使用内置日期模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="0a911-111">但是，ASP。MVC 可以通过查找匹配的类型名称的模板来使用约定于配置的类型匹配。</span><span class="sxs-lookup"><span data-stu-id="0a911-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="0a911-112">这允许您创建的模板，会自动设置数据格式不使用任何属性或代码在所有情况下。</span><span class="sxs-lookup"><span data-stu-id="0a911-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="0a911-113">在本教程的此部分中，你将创建自动应用于类型的模型属性的模板[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0a911-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="0a911-114">无需使用一个属性或其他配置来指定应使用模板来呈现类型的所有模型属性[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0a911-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="0a911-115">您还将学习一种方法来自定义的单个属性或甚至是单个字段的显示。</span><span class="sxs-lookup"><span data-stu-id="0a911-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="0a911-116">若要开始，让我们删除现有的格式设置信息，并在应用程序中显示完整的日期。</span><span class="sxs-lookup"><span data-stu-id="0a911-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="0a911-117">打开*Movie.cs*文件并注释掉`DataType`特性，可以在`ReleaseDate`属性：</span><span class="sxs-lookup"><span data-stu-id="0a911-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="0a911-118">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="0a911-119">请注意，`ReleaseDate`属性现在将显示日期和时间，因为这是默认值时未不提供任何格式设置信息。</span><span class="sxs-lookup"><span data-stu-id="0a911-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="0a911-120">用于测试新的模板添加 CSS 样式</span><span class="sxs-lookup"><span data-stu-id="0a911-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="0a911-121">创建用于设置日期格式的模板之前，你将添加一些 CSS 样式规则可应用于新的模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="0a911-122">这些将帮助您验证在呈现的页面正在使用的新模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="0a911-123">打开*Content\Site.cs*s 文件，并将以下 CSS 规则添加到文件的底部：</span><span class="sxs-lookup"><span data-stu-id="0a911-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="0a911-124">添加日期时间的显示模板</span><span class="sxs-lookup"><span data-stu-id="0a911-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="0a911-125">现在可以创建新模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-125">Now you can create the new template.</span></span> <span data-ttu-id="0a911-126">在中*视图 \ 电影*文件夹中，创建*DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a911-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="0a911-127">在中*views/shared*文件夹中，创建*DisplayTemplates*文件夹和一个*EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a911-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="0a911-128">中的显示模板*Views\Shared\DisplayTemplates*文件夹将由所有控制器。</span><span class="sxs-lookup"><span data-stu-id="0a911-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="0a911-129">中的显示模板*Views\Movie\DisplayTemplates*将仅可由使用文件夹`Movie`控制器。</span><span class="sxs-lookup"><span data-stu-id="0a911-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="0a911-130">(如果具有相同名称的模板出现在这两个文件夹中的模板*Views\Movie\DisplayTemplates*文件夹 — 也就是说，更具体的模板-将优先于返回的视图的`Movie`控制器。)</span><span class="sxs-lookup"><span data-stu-id="0a911-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="0a911-131">在中**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a911-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="0a911-132">单击**外**，然后单击**视图**。</span><span class="sxs-lookup"><span data-stu-id="0a911-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="0a911-133">**添加视图**显示对话框。</span><span class="sxs-lookup"><span data-stu-id="0a911-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="0a911-134">在中**视图名称**框中，键入`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="0a911-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="0a911-135">（您必须使用此名称以匹配类型的名称。）</span><span class="sxs-lookup"><span data-stu-id="0a911-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="0a911-136">选择**创建为分部视图**复选框。</span><span class="sxs-lookup"><span data-stu-id="0a911-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="0a911-137">请确保**使用布局或母版页页**并**创建强类型化视图**不选中复选框。</span><span class="sxs-lookup"><span data-stu-id="0a911-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="0a911-138">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="0a911-138">Click **Add**.</span></span> <span data-ttu-id="0a911-139">一个*添加*在中创建模板*Views\Shared\DisplayTemplates*。</span><span class="sxs-lookup"><span data-stu-id="0a911-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="0a911-140">下图显示*视图*中的文件夹**解决方案资源管理器**后`DateTime`创建显示和编辑器的模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="0a911-141">打开*Views\Shared\DisplayTemplates\DateTime.cshtml*文件，并添加以下标记，使用[String.Format](https://msdn.microsoft.com/library/system.string.format.aspx)方法设置为不包括的时间日期的格式属性。</span><span class="sxs-lookup"><span data-stu-id="0a911-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="0a911-142">(`{0:d}`格式指定短日期格式。)</span><span class="sxs-lookup"><span data-stu-id="0a911-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="0a911-143">重复此步骤以创建`DateTime`中的模板*Views\Movie\DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a911-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="0a911-144">使用中的以下代码*Views\Movie\DisplayTemplates\DateTime.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0a911-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="0a911-145">`loud-1` CSS 类将导致日期显示为红色粗体文本。</span><span class="sxs-lookup"><span data-stu-id="0a911-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="0a911-146">您添加`loud-1`就像是暂时措施，以便你可以轻松查看此特定模板中使用时的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="0a911-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="0a911-147">所做的创建和自定义模板，ASP.NET 将用来显示日期。</span><span class="sxs-lookup"><span data-stu-id="0a911-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="0a911-148">更多常规模板 (在*Views\Shared\DisplayTemplates*文件夹) 显示简单的短日期。</span><span class="sxs-lookup"><span data-stu-id="0a911-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="0a911-149">专门用于模板`Movie`控制器 (在*Views\Movies\DisplayTemplates*文件夹) 也设置格式的短日期显示为红色粗体文本。</span><span class="sxs-lookup"><span data-stu-id="0a911-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="0a911-150">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="0a911-151">在浏览器呈现应用程序的索引视图。</span><span class="sxs-lookup"><span data-stu-id="0a911-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="0a911-152">`ReleaseDate`属性现在以红色粗体不包括的时间显示的日期。这可帮助你确认`DateTime`中的模板化帮助器*Views\Movies\DisplayTemplates*转移选择文件夹`DateTime`共享文件夹中的模板化帮助器 (*Views\Shared\DisplayTemplates*)。</span><span class="sxs-lookup"><span data-stu-id="0a911-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="0a911-153">现在重命名*Views\Movies\DisplayTemplates\DateTime.cshtml*的文件*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="0a911-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="0a911-154">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="0a911-155">这一次`ReleaseDate`属性将显示日期不包括的时间，而无需红色粗体日期。</span><span class="sxs-lookup"><span data-stu-id="0a911-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="0a911-156">这说明了数据的名称的模板类型 (在这种情况下`DateTime`) 会自动使用来显示该类型的所有模型属性。</span><span class="sxs-lookup"><span data-stu-id="0a911-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="0a911-157">重命名后*添加*文件为*LoudDateTime.cshtml*，ASP.NET 无法再找到中的模板*Views\Movies\DisplayTemplates*文件夹中，因此使用它*添加*模板从 * Views\Movies\Shared\*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a911-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the *Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="0a911-158">（模板匹配是不区分大小写，因此无法创建模板文件的名称与任何大小写。</span><span class="sxs-lookup"><span data-stu-id="0a911-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="0a911-159">例如， *DATETIME.chstml，添加*，并*添加*将所有匹配`DateTime`类型。)</span><span class="sxs-lookup"><span data-stu-id="0a911-159">For example, *DATETIME.chstml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="0a911-160">若要查看： 在此情况下，`ReleaseDate`正在使用显示字段*Views\Movies\DisplayTemplates\DateTime.cshtml*模板，其中使用短日期格式显示数据，但否则会添加任何特殊格式。</span><span class="sxs-lookup"><span data-stu-id="0a911-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="0a911-161">使用 UIHint 指定显示模板</span><span class="sxs-lookup"><span data-stu-id="0a911-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="0a911-162">如果 web 应用程序具有许多`DateTime`字段和默认情况下你想要仅限日期的格式显示全部或大部分它们*添加*模板是一个不错的方法。</span><span class="sxs-lookup"><span data-stu-id="0a911-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="0a911-163">但是，如果您有几个日期想要显示完整的日期和时间？</span><span class="sxs-lookup"><span data-stu-id="0a911-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="0a911-164">没问题。</span><span class="sxs-lookup"><span data-stu-id="0a911-164">No problem.</span></span> <span data-ttu-id="0a911-165">可以创建其他模板，并使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性指定的完整的日期和时间格式设置。</span><span class="sxs-lookup"><span data-stu-id="0a911-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="0a911-166">然后，您可以有选择地应用该模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-166">You can then selectively apply that template.</span></span> <span data-ttu-id="0a911-167">可以使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性在模型级别或您可以指定在视图内的模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="0a911-168">在本部分中，您将了解如何使用`UIHint`特性来有选择地更改某些情况下的日期时间字段的格式设置。</span><span class="sxs-lookup"><span data-stu-id="0a911-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="0a911-169">打开*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*文件和现有代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="0a911-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="0a911-170">这会导致要显示的完整的日期和时间，并将绿色和大型会使文本的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="0a911-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="0a911-171">打开*Movie.cs*文件，并添加[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)归于`ReleaseDate`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0a911-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="0a911-172">这将告知 ASP.NET MVC 的显示时`ReleaseDate`属性 (具体而言，并不只是任何`DateTime`对象)，它应使用*LoudDateTime.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="0a911-173">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="0a911-174">请注意，`ReleaseDate`属性现在显示的日期和时间，绿色字体大小。</span><span class="sxs-lookup"><span data-stu-id="0a911-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="0a911-175">返回到`UIHint`中的属性*Movie.cs*文件，并对它进行注释，因此*LoudDateTime.cshtml*不会使用模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="0a911-176">再次运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-176">Run the application again.</span></span> <span data-ttu-id="0a911-177">发布日期不会显示大型和绿色。</span><span class="sxs-lookup"><span data-stu-id="0a911-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="0a911-178">这将验证该*Views\Shared\DisplayTemplates\DateTime.cshtml* Index 和 Details 视图中使用模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="0a911-179">前面曾提到，您还可以应用在视图中，这样就可以将模板应用到某些数据的单个实例模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="0a911-180">打开*Views\Movies\Details.cshtml*视图。</span><span class="sxs-lookup"><span data-stu-id="0a911-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="0a911-181">添加`"LoudDateTime"`的第二个参数[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)寻求`ReleaseDate`字段。</span><span class="sxs-lookup"><span data-stu-id="0a911-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="0a911-182">完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="0a911-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="0a911-183">此步骤指定`LoudDateTime`模板应该用于显示模型属性，而不考虑哪些属性应用于模型。</span><span class="sxs-lookup"><span data-stu-id="0a911-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="0a911-184">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a911-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="0a911-185">验证是否正在使用影片索引页*Views\Shared\DisplayTemplates\DateTime.cshtml*模板 （红色粗体） 和*Movie\Details*网页使用的*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*模板 （大型和绿色）。</span><span class="sxs-lookup"><span data-stu-id="0a911-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="0a911-186">在下一部分中，将创建复杂类型的模板。</span><span class="sxs-lookup"><span data-stu-id="0a911-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a911-187">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="0a911-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
