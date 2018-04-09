---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 使用 ASP.NET MVC-第 4 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历 |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: c6df727107b0a045341badefbf99eec773cd4eff
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="61876-103">使用 ASP.NET MVC-第 4 部分中使用 HTML5 和 jQuery UI Datepicker 弹出日历</span><span class="sxs-lookup"><span data-stu-id="61876-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>
====================
<span data-ttu-id="61876-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="61876-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="61876-105">本教程将教您如何使用编辑器模板、 显示模板和 jQuery UI datepicker 弹出日历，ASP.NET MVC Web 应用程序中的基础知识。</span><span class="sxs-lookup"><span data-stu-id="61876-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="61876-106">用于编辑日期添加模板</span><span class="sxs-lookup"><span data-stu-id="61876-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="61876-107">在本部分中，你将创建用于编辑日期的 ASP.NET MVC UI 显示用于编辑标记有的模型属性时将应用的模板**日期**的枚举[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="61876-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attibute.</span></span> <span data-ttu-id="61876-108">该模板将呈现仅显示日期;不会显示时间。</span><span class="sxs-lookup"><span data-stu-id="61876-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="61876-109">在模板中，你将使用[jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/)弹出日历，以提供一种方法编辑日期。</span><span class="sxs-lookup"><span data-stu-id="61876-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="61876-110">若要开始，打开*Movie.cs*文件并添加[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性与**日期**枚举`ReleaseDate`属性，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="61876-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="61876-111">此代码会导致`ReleaseDate`中的时间显示模板和编辑模板没有要显示的字段。</span><span class="sxs-lookup"><span data-stu-id="61876-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="61876-112">如果你的应用程序包含*date.cshtml*中的模板*Views\Shared\EditorTemplates*文件夹中或在*Views\Movies\EditorTemplates*文件夹中，该模板将用于呈现任何`DateTime`编辑时的属性。</span><span class="sxs-lookup"><span data-stu-id="61876-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="61876-113">否则内置 ASP.NET 模板化系统将显示为日期属性。</span><span class="sxs-lookup"><span data-stu-id="61876-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="61876-114">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="61876-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="61876-115">选择的编辑链接，以验证发布日期的输入的字段的显示仅显示日期。</span><span class="sxs-lookup"><span data-stu-id="61876-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="61876-116">在**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="61876-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="61876-117">单击**添加**，然后单击**视图**。</span><span class="sxs-lookup"><span data-stu-id="61876-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="61876-118">**添加视图**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="61876-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="61876-119">在**视图名称**框中，键入&quot;日期&quot;。</span><span class="sxs-lookup"><span data-stu-id="61876-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="61876-120">选择**创建为分部视图**复选框。</span><span class="sxs-lookup"><span data-stu-id="61876-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="61876-121">请确保**使用的布局或 master 页面**和**创建强类型化视图**不选中的复选框。</span><span class="sxs-lookup"><span data-stu-id="61876-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="61876-122">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="61876-122">Click **Add**.</span></span> <span data-ttu-id="61876-123">*Views\Shared\EditorTemplates\Date.cshtml*创建模板。</span><span class="sxs-lookup"><span data-stu-id="61876-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="61876-124">以下代码添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="61876-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="61876-125">第一行声明模型要`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="61876-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="61876-126">尽管你不需要声明中编辑的模型类型和显示模板，但它是一种最佳做法，以便你可以获得编译时检查传递给视图的模型。</span><span class="sxs-lookup"><span data-stu-id="61876-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="61876-127">（另一个好处是您会收到 IntelliSense 对于 Visual Studio 中的视图中的模型。）ASP.NET MVC 如果未声明的模型类型，将其视为[动态](https://msdn.microsoft.com/library/dd264741.aspx)键入并且没有任何编译时类型检查。</span><span class="sxs-lookup"><span data-stu-id="61876-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="61876-128">如果你声明模型要`DateTime`类型，它将成为强类型。</span><span class="sxs-lookup"><span data-stu-id="61876-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="61876-129">第二行是仅文本显示的 HTML 标记&quot;使用日期模板&quot;之前的日期字段。</span><span class="sxs-lookup"><span data-stu-id="61876-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="61876-130">你将暂时使用此行以验证正在使用此日期模板。</span><span class="sxs-lookup"><span data-stu-id="61876-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="61876-131">下一行是[Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)呈现的帮助器`input`字段的文本框。</span><span class="sxs-lookup"><span data-stu-id="61876-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="61876-132">帮助器的第三个参数使用一个匿名类型设置的文本设置为的类`datefield`和类型设置为`date`。</span><span class="sxs-lookup"><span data-stu-id="61876-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="61876-133">(因为`class`是保留在 C# 中，你需要使用`@`字符进行转义`class`C# 分析器中的属性。)</span><span class="sxs-lookup"><span data-stu-id="61876-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="61876-134">`date`类型是一个 HTML5 输入的类型，使感知 HTML5 浏览器呈现 HTML5 日历控件。</span><span class="sxs-lookup"><span data-stu-id="61876-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="61876-135">稍后你将添加一些 JavaScript 挂接到 jQuery datepicker`Html.TextBox`元素使用`datefield`类。</span><span class="sxs-lookup"><span data-stu-id="61876-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="61876-136">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="61876-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="61876-137">你可以验证`ReleaseDate`编辑视图中的属性使用编辑模板，因为该模板显示&quot;使用日期模板&quot;之前`ReleaseDate`文本输入框中，此图中所示：</span><span class="sxs-lookup"><span data-stu-id="61876-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="61876-138">在浏览器中，查看的页面的源。</span><span class="sxs-lookup"><span data-stu-id="61876-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="61876-139">(例如，右击该页并选择**查看源**。)以下示例显示了一些页中，标记来说明`class`和`type`呈现的 HTML 中的属性。</span><span class="sxs-lookup"><span data-stu-id="61876-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="61876-140">返回到*Views\Shared\EditorTemplates\Date.cshtml*模板和删除&quot;使用日期模板&quot;标记。</span><span class="sxs-lookup"><span data-stu-id="61876-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="61876-141">现在已完成的模板类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="61876-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="61876-142">添加 jQuery UI Datepicker 弹出日历使用 NuGet</span><span class="sxs-lookup"><span data-stu-id="61876-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="61876-143">在本部分将添加[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出日历，日期编辑模板。</span><span class="sxs-lookup"><span data-stu-id="61876-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="61876-144">[JQuery UI](http://jqueryui.com/)库为动画，高级效果，以及可自定义小组件提供了支持。</span><span class="sxs-lookup"><span data-stu-id="61876-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="61876-145">它是基础的 jQuery JavaScript 库生成的。</span><span class="sxs-lookup"><span data-stu-id="61876-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="61876-146">包含 datepicker 弹出日历可以简单而自然以输入日期而不输入字符串中使用的日历。</span><span class="sxs-lookup"><span data-stu-id="61876-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="61876-147">弹出日历还限制到合法日期的用户-针对日期的普通文本条目会让你输入类似`2/33/1999`(年 2 月 33rd、 1999年)，但[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出日历不允许的。</span><span class="sxs-lookup"><span data-stu-id="61876-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="61876-148">首先，你必须安装 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="61876-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="61876-149">若要这样做，将使用 NuGet，是的 Visual Studio 2010 和 Visual Web Developer 的 SP1 版本中包括的包管理器。</span><span class="sxs-lookup"><span data-stu-id="61876-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="61876-150">在 Visual Web Developer 中，从**工具**菜单上，选择**库程序包管理器**，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="61876-150">In Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="61876-151">注意： 如果**工具**菜单中未显示**库程序包管理器**命令时，你需要按照的说明安装 NuGet[安装 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)页NuGet 网站。</span><span class="sxs-lookup"><span data-stu-id="61876-151">Note: If the **Tools** menu doesn't display the **Library Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="61876-152">如果你使用 Visual Studio 而不是 Visual Web Developer 中，从**工具**菜单上，选择**库程序包管理器**，然后选择**添加库程序包引用**。</span><span class="sxs-lookup"><span data-stu-id="61876-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="61876-153">在**MVCMovie-管理 NuGet 包**对话框中，单击**联机**在左侧选项卡，然后输入&quot;jQuery.UI&quot;的搜索框中。</span><span class="sxs-lookup"><span data-stu-id="61876-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="61876-154">选择 j**查询 UI 小组件： Datepicker**，然后选择**安装**按钮。</span><span class="sxs-lookup"><span data-stu-id="61876-154">Select j **Query UI WIdgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="61876-155">NuGet 将这些调试版本和缩减的版本的 jQuery UI 核心和 jQuery UI 日期选取器添加到你的项目中：</span><span class="sxs-lookup"><span data-stu-id="61876-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="61876-156">*jquery.ui.core.js*</span><span class="sxs-lookup"><span data-stu-id="61876-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="61876-157">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="61876-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="61876-158">*jquery.ui.datepicker.js*</span><span class="sxs-lookup"><span data-stu-id="61876-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="61876-159">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="61876-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="61876-160">注意： 的调试版本 (不包含的文件*。 min.js*扩展) 可用于调试，但在生产站点，你会包括仅缩减的版本。</span><span class="sxs-lookup"><span data-stu-id="61876-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="61876-161">若要实际使用 jQuery 日期选取器，你需要创建将挂钩到编辑模板日历小组件的 jQuery 脚本。</span><span class="sxs-lookup"><span data-stu-id="61876-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="61876-162">在**解决方案资源管理器**，右键单击*脚本*文件夹，然后选择**添加**，然后**新项**，，然后**JScript文件**。</span><span class="sxs-lookup"><span data-stu-id="61876-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="61876-163">命名该文件*DatePickerReady.js*。</span><span class="sxs-lookup"><span data-stu-id="61876-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="61876-164">以下代码添加到*DatePickerReady.js*文件：</span><span class="sxs-lookup"><span data-stu-id="61876-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="61876-165">如果你不熟悉 jQuery，下面是这一功能的简要说明： 第一行是&quot;jQuery 准备&quot;函数，它在已加载页面中的所有 DOM 元素时调用。</span><span class="sxs-lookup"><span data-stu-id="61876-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="61876-166">第二行选择具有的类名称的所有 DOM 元素`datefield`，然后调用`datepicker`为每个函数。</span><span class="sxs-lookup"><span data-stu-id="61876-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="61876-167">(请记住你添加`datefield`类到*Views\Shared\EditorTemplates\Date.cshtml*在本教程前面的模板。)</span><span class="sxs-lookup"><span data-stu-id="61876-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="61876-168">接下来，打开*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="61876-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="61876-169">你需要添加对以下文件，以便你可以使用日期选取器将所有所需的引用：</span><span class="sxs-lookup"><span data-stu-id="61876-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="61876-170">*Content/themes/base/jquery.ui.core.css*</span><span class="sxs-lookup"><span data-stu-id="61876-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="61876-171">*Content/themes/base/jquery.ui.datepicker.css*</span><span class="sxs-lookup"><span data-stu-id="61876-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="61876-172">*Content/themes/base/jquery.ui.theme.css*</span><span class="sxs-lookup"><span data-stu-id="61876-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="61876-173">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="61876-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="61876-174">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="61876-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="61876-175">*DatePickerReady.js*</span><span class="sxs-lookup"><span data-stu-id="61876-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="61876-176">下面的示例演示实际代码，你应添加在底部`head`中的元素*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="61876-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="61876-177">完整`head`部分如下所示：</span><span class="sxs-lookup"><span data-stu-id="61876-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="61876-178">[URL 内容帮助器](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法将资源路径转换为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="61876-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="61876-179">必须使用`@URL.Content`正确引用这些资源，在 IIS 上运行应用程序时。</span><span class="sxs-lookup"><span data-stu-id="61876-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="61876-180">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="61876-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="61876-181">选择的编辑链接，则将放到插入点**ReleaseDate**字段。</span><span class="sxs-lookup"><span data-stu-id="61876-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="61876-182">将显示 jQuery UI 弹出日历。</span><span class="sxs-lookup"><span data-stu-id="61876-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="61876-183">大多数 jQuery 控件，如 datepicker 可以广泛地自定义。</span><span class="sxs-lookup"><span data-stu-id="61876-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="61876-184">有关信息，请参阅[Visual 自定义项： 设计 jQuery UI 主题](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)上[jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/)站点。</span><span class="sxs-lookup"><span data-stu-id="61876-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="61876-185">支持 HTML5 日期输入的控件</span><span class="sxs-lookup"><span data-stu-id="61876-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="61876-186">因为多个浏览器支持 HTML5，你将想要使用输入的信息，如本机 HTML5`date`输入元素，并使用 jQuery UI 日历。</span><span class="sxs-lookup"><span data-stu-id="61876-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="61876-187">可以将逻辑添加到你的应用程序，如果浏览器支持它们自动使用 HTML5 控件。</span><span class="sxs-lookup"><span data-stu-id="61876-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="61876-188">若要执行此操作，将内容*DatePickerReady.js*替换为以下文件：</span><span class="sxs-lookup"><span data-stu-id="61876-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="61876-189">此脚本的第一行使用 Modernizr 检验支持 HTML5 日期输入。</span><span class="sxs-lookup"><span data-stu-id="61876-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="61876-190">如果不支持，jQuery UI 日期选取器已改为挂钩。</span><span class="sxs-lookup"><span data-stu-id="61876-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="61876-191">([Modernizr](http://www.modernizr.com/docs/)是检测到的可用性的 HTML5 和 CSS3 的本机实现一个开放源代码 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="61876-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="61876-192">Modernizr 中包括你创建的任何新的 ASP.NET MVC 项目。）</span><span class="sxs-lookup"><span data-stu-id="61876-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="61876-193">已进行此更改后，可以通过使用支持 HTML5，如 Opera 11 的浏览器对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="61876-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="61876-194">运行使用 HTML5 兼容浏览器的应用程序和编辑电影条目。</span><span class="sxs-lookup"><span data-stu-id="61876-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="61876-195">HTML5 日期控件代替 jQuery UI 弹出日历：</span><span class="sxs-lookup"><span data-stu-id="61876-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="61876-196">因为的浏览器的新版本以增量方式实现 HTML5，现在一个好方法是将代码添加到你还包含许多丰富的 HTML5 支持的网站。</span><span class="sxs-lookup"><span data-stu-id="61876-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="61876-197">例如，更可靠*DatePickerReady.js*脚本如下所示，从而使你站点支持的浏览器仅部分支持 HTML5 日期控件。</span><span class="sxs-lookup"><span data-stu-id="61876-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="61876-198">此脚本选择 HTML5`input`类型的元素`date`不完全支持 HTML5 日期控件。</span><span class="sxs-lookup"><span data-stu-id="61876-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="61876-199">对于这些元素，它挂钩 jQuery UI 弹出日历，然后更改`type`属性从`date`到`text`。</span><span class="sxs-lookup"><span data-stu-id="61876-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="61876-200">通过更改`type`属性从`date`到`text`，消除部分 HTML5 日期支持。</span><span class="sxs-lookup"><span data-stu-id="61876-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="61876-201">甚至更可靠*DatePickerReady.js*处找不到脚本[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)。</span><span class="sxs-lookup"><span data-stu-id="61876-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="61876-202">将为 Null 的日期添加到模板</span><span class="sxs-lookup"><span data-stu-id="61876-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="61876-203">如果你使用其中一个现有的日期模板并将传递 null 日期时，你将获得运行时错误。</span><span class="sxs-lookup"><span data-stu-id="61876-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="61876-204">若要使日期模板更可靠，你将更改它们以处理 null 值。</span><span class="sxs-lookup"><span data-stu-id="61876-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="61876-205">若要支持可以为 null 的日期，更改中的代码*Views\Shared\DisplayTemplates\DateTime.cshtml*所示：</span><span class="sxs-lookup"><span data-stu-id="61876-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="61876-206">代码模型时也会返回空字符串**null**。</span><span class="sxs-lookup"><span data-stu-id="61876-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="61876-207">更改中的代码*Views\Shared\EditorTemplates\Date.cshtml*到以下文件：</span><span class="sxs-lookup"><span data-stu-id="61876-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="61876-208">当此代码运行时，如果模型不为 null，该模型的`DateTime`使用值。</span><span class="sxs-lookup"><span data-stu-id="61876-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="61876-209">如果模型为 null，则改用当前的日期。</span><span class="sxs-lookup"><span data-stu-id="61876-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="61876-210">便捷</span><span class="sxs-lookup"><span data-stu-id="61876-210">Wrapup</span></span>

<span data-ttu-id="61876-211">本教程已覆盖 ASP.NET 模板化帮助器的基础知识，并向你显示如何在 ASP.NET MVC 应用程序中使用 jQuery UI datepicker 弹出日历。</span><span class="sxs-lookup"><span data-stu-id="61876-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="61876-212">有关详细信息，请尝试这些资源：</span><span class="sxs-lookup"><span data-stu-id="61876-212">For more information, try these resources:</span></span>

- <span data-ttu-id="61876-213">本地化的信息，请参阅 Rajeesh 的博客[ASP.NET mvc JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。</span><span class="sxs-lookup"><span data-stu-id="61876-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="61876-214">有关 jQuery UI 的信息，请参阅[jQuery UI](http://docs.jquery.com/UI)。</span><span class="sxs-lookup"><span data-stu-id="61876-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="61876-215">有关如何本地化 datepicker 控件的信息，请参阅[UI/Datepicker/本地化](http://docs.jquery.com/UI/Datepicker/Localization)。</span><span class="sxs-lookup"><span data-stu-id="61876-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="61876-216">有关 ASP.NET MVC 模板的详细信息，请参阅 Brad wilson 制作的博客连载文章上[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="61876-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="61876-217">序列为 ASP.NET MVC 2 编写的虽然材料将仍适用于当前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="61876-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="61876-218">上一篇</span><span class="sxs-lookup"><span data-stu-id="61876-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
