---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 4 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 74bd88408c4d60032a1275aa9f8540cf710dac36
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380903"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="21b0e-103">使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 4 部分</span><span class="sxs-lookup"><span data-stu-id="21b0e-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>
====================
<span data-ttu-id="21b0e-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="21b0e-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="21b0e-105">本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="21b0e-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="21b0e-106">将模板添加以进行编辑日期</span><span class="sxs-lookup"><span data-stu-id="21b0e-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="21b0e-107">在本部分将创建用于编辑 ASP.NET MVC 显示用于编辑模型属性标记的 UI 时要采用的日期的模板**日期**的枚举[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="21b0e-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attibute.</span></span> <span data-ttu-id="21b0e-108">该模板将呈现仅显示日期;将不显示时间。</span><span class="sxs-lookup"><span data-stu-id="21b0e-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="21b0e-109">在模板中将使用[jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/)弹出日历，以提供一种方法来编辑日期。</span><span class="sxs-lookup"><span data-stu-id="21b0e-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="21b0e-110">若要开始，请打开*Movie.cs*文件，并添加[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性**日期**枚举`ReleaseDate`属性，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="21b0e-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="21b0e-111">此代码会导致`ReleaseDate`没有在这种时间显示模板和编辑模板要显示的字段。</span><span class="sxs-lookup"><span data-stu-id="21b0e-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="21b0e-112">如果你的应用程序包含*date.cshtml*中的模板*Views\Shared\EditorTemplates*文件夹中或在*Views\Movies\EditorTemplates*文件夹中，该模板将用于呈现任何`DateTime`编辑时的属性。</span><span class="sxs-lookup"><span data-stu-id="21b0e-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="21b0e-113">否则内置的 ASP.NET 模板化系统将显示为日期属性。</span><span class="sxs-lookup"><span data-stu-id="21b0e-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="21b0e-114">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="21b0e-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="21b0e-115">选择要验证的发布日期输入的字段显示仅显示日期的编辑链接。</span><span class="sxs-lookup"><span data-stu-id="21b0e-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="21b0e-116">在中**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="21b0e-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="21b0e-117">单击**外**，然后单击**视图**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="21b0e-118">**添加视图**显示对话框。</span><span class="sxs-lookup"><span data-stu-id="21b0e-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="21b0e-119">在中**视图名称**框中，键入&quot;日期&quot;。</span><span class="sxs-lookup"><span data-stu-id="21b0e-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="21b0e-120">选择**创建为分部视图**复选框。</span><span class="sxs-lookup"><span data-stu-id="21b0e-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="21b0e-121">请确保**使用布局或母版页页**并**创建强类型化视图**不选中复选框。</span><span class="sxs-lookup"><span data-stu-id="21b0e-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="21b0e-122">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-122">Click **Add**.</span></span> <span data-ttu-id="21b0e-123">*Views\Shared\EditorTemplates\Date.cshtml*创建模板。</span><span class="sxs-lookup"><span data-stu-id="21b0e-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="21b0e-124">将以下代码添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="21b0e-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="21b0e-125">第一行代码声明的模型要`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="21b0e-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="21b0e-126">尽管不需要声明中编辑的模型类型和显示模板，但它是一种最佳做法，以便进行编译时检查传递给视图的模型。</span><span class="sxs-lookup"><span data-stu-id="21b0e-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="21b0e-127">（另一个好处是然后获取 IntelliSense，以在 Visual Studio 中的视图模型。）ASP.NET MVC 如果未声明的模型类型，将其视为[动态](https://msdn.microsoft.com/library/dd264741.aspx)类型，并且没有任何编译时类型检查。</span><span class="sxs-lookup"><span data-stu-id="21b0e-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="21b0e-128">如果声明的模型要`DateTime`类型，它将成为强类型化。</span><span class="sxs-lookup"><span data-stu-id="21b0e-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="21b0e-129">第二行是只需文本显示的 HTML 标记&quot;使用日期模板&quot;之前的日期字段。</span><span class="sxs-lookup"><span data-stu-id="21b0e-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="21b0e-130">你将暂时使用这行以验证正在使用此日期模板。</span><span class="sxs-lookup"><span data-stu-id="21b0e-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="21b0e-131">下一行是[Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)帮助器呈现`input`是文本框中的字段。</span><span class="sxs-lookup"><span data-stu-id="21b0e-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="21b0e-132">帮助程序的第三个参数使用匿名类型设置为文本框中的类`datefield`和类型设置为`date`。</span><span class="sxs-lookup"><span data-stu-id="21b0e-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="21b0e-133">(因为`class`是保留在 C# 中，您需要使用`@`字符来转义`class`C# 分析器中的属性。)</span><span class="sxs-lookup"><span data-stu-id="21b0e-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="21b0e-134">`date`类型为 HTML5 输入的类型，使识别 HTML5 的浏览器可以呈现的 HTML5 日历控件。</span><span class="sxs-lookup"><span data-stu-id="21b0e-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="21b0e-135">稍后将添加一些 JavaScript 以便挂接到 jQuery datepicker`Html.TextBox`元素使用`datefield`类。</span><span class="sxs-lookup"><span data-stu-id="21b0e-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="21b0e-136">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="21b0e-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="21b0e-137">你可以验证`ReleaseDate`编辑视图中的属性使用编辑模板，因为该模板将显示&quot;使用日期模板&quot;之前`ReleaseDate`文本输入框中，此图中所示：</span><span class="sxs-lookup"><span data-stu-id="21b0e-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="21b0e-138">在浏览器中查看页面的源代码。</span><span class="sxs-lookup"><span data-stu-id="21b0e-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="21b0e-139">(例如，右键单击页并选择**查看源**。)以下示例显示了一些页的标记演示`class`和`type`中呈现的 HTML 属性。</span><span class="sxs-lookup"><span data-stu-id="21b0e-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="21b0e-140">返回到*Views\Shared\EditorTemplates\Date.cshtml*模板和删除&quot;使用日期模板&quot;标记。</span><span class="sxs-lookup"><span data-stu-id="21b0e-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="21b0e-141">现在已完成的模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="21b0e-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="21b0e-142">添加 jQuery UI Datepicker 快捷日历使用 NuGet</span><span class="sxs-lookup"><span data-stu-id="21b0e-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="21b0e-143">在本部分中将添加[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出日历到日期编辑模板。</span><span class="sxs-lookup"><span data-stu-id="21b0e-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="21b0e-144">[JQuery UI](http://jqueryui.com/)库对于动画，高级效果和可自定义小组件提供支持。</span><span class="sxs-lookup"><span data-stu-id="21b0e-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="21b0e-145">因为它是基于 jQuery JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="21b0e-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="21b0e-146">Datepicker 快捷日历，就能轻松自然地输入而不输入字符串中使用的日历的日期。</span><span class="sxs-lookup"><span data-stu-id="21b0e-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="21b0e-147">弹出式日历还限制这些用户法律日期 — 普通文本输入的日期，您可以输入类似`2/33/1999`(年 2 月 33rd，1999年)，但[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出式日历不允许的。</span><span class="sxs-lookup"><span data-stu-id="21b0e-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="21b0e-148">首先，您必须安装 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="21b0e-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="21b0e-149">若要执行此操作，将使用 NuGet，这是 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中包含的程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="21b0e-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="21b0e-150">在 Visual Web Developer 中，从**工具**菜单中，选择**库程序包管理器**，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-150">In Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="21b0e-151">注意： 如果**工具**不会显示菜单**库程序包管理器**命令，你需要通过以下上的说明安装 NuGet[安装 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)页NuGet 网站。</span><span class="sxs-lookup"><span data-stu-id="21b0e-151">Note: If the **Tools** menu doesn't display the **Library Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="21b0e-152">如果使用 Visual Studio 而不是 Visual Web Developer 中，从**工具**菜单中，选择**库程序包管理器**，然后选择**添加库程序包引用**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="21b0e-153">在中**MVCMovie-管理 NuGet 包**对话框中，单击**联机**在左侧选项卡，然后输入&quot;jQuery.UI&quot;在搜索框中。</span><span class="sxs-lookup"><span data-stu-id="21b0e-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="21b0e-154">选择 j**查询 UI 小组件： Datepicker**，然后选择**安装**按钮。</span><span class="sxs-lookup"><span data-stu-id="21b0e-154">Select j **Query UI WIdgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="21b0e-155">NuGet 会将这些调试版本和缩小的版本的 jQuery UI 核心和 jQuery UI 日期选取器添加到你的项目：</span><span class="sxs-lookup"><span data-stu-id="21b0e-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="21b0e-156">*jquery.ui.core.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="21b0e-157">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="21b0e-158">*jquery.ui.datepicker.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="21b0e-159">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="21b0e-160">注意： 调试版本 (不包含的文件 *。 min.js*扩展) 可用于调试，但在生产站点中，应包括仅的缩减的版本。</span><span class="sxs-lookup"><span data-stu-id="21b0e-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="21b0e-161">若要实际使用 jQuery 日期选取器，您需要创建将挂接到编辑模板日历小组件的 jQuery 脚本。</span><span class="sxs-lookup"><span data-stu-id="21b0e-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="21b0e-162">在中**解决方案资源管理器**，右键单击*脚本*文件夹，然后选择**添加**，然后**新项**，，然后**JScript文件**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="21b0e-163">将文件命名*DatePickerReady.js*。</span><span class="sxs-lookup"><span data-stu-id="21b0e-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="21b0e-164">将以下代码添加到*DatePickerReady.js*文件：</span><span class="sxs-lookup"><span data-stu-id="21b0e-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="21b0e-165">如果您不熟悉 jQuery，下面提供了这一功能的简要说明： 第一行是&quot;jQuery 就绪&quot;函数，当已将加载一个页面中的所有 DOM 元素时调用。</span><span class="sxs-lookup"><span data-stu-id="21b0e-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="21b0e-166">第二行选择所有具有类名称的 DOM 元素`datefield`，然后调用`datepicker`为每个函数。</span><span class="sxs-lookup"><span data-stu-id="21b0e-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="21b0e-167">(请记住你添加`datefield`类来*Views\Shared\EditorTemplates\Date.cshtml*本教程前面部分的模板。)</span><span class="sxs-lookup"><span data-stu-id="21b0e-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="21b0e-168">接下来，打开*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="21b0e-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="21b0e-169">您需要添加对以下文件，以便可以使用日期选取器都是必需的引用：</span><span class="sxs-lookup"><span data-stu-id="21b0e-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="21b0e-170">*Content/themes/base/jquery.ui.core.css*</span><span class="sxs-lookup"><span data-stu-id="21b0e-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="21b0e-171">*Content/themes/base/jquery.ui.datepicker.css*</span><span class="sxs-lookup"><span data-stu-id="21b0e-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="21b0e-172">*Content/themes/base/jquery.ui.theme.css*</span><span class="sxs-lookup"><span data-stu-id="21b0e-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="21b0e-173">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="21b0e-174">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="21b0e-175">*DatePickerReady.js*</span><span class="sxs-lookup"><span data-stu-id="21b0e-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="21b0e-176">下面的示例演示的实际代码应将添加在底部`head`中的元素*Views\Shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="21b0e-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="21b0e-177">完整`head`部分如下所示：</span><span class="sxs-lookup"><span data-stu-id="21b0e-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="21b0e-178">[URL 内容帮助器](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法将资源路径转换为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="21b0e-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="21b0e-179">必须使用`@URL.Content`IIS 上运行应用程序时正确引用这些资源。</span><span class="sxs-lookup"><span data-stu-id="21b0e-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="21b0e-180">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="21b0e-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="21b0e-181">选择的编辑链接，然后将插入点定位到**ReleaseDate**字段。</span><span class="sxs-lookup"><span data-stu-id="21b0e-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="21b0e-182">显示的 jQuery UI 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="21b0e-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="21b0e-183">大多数 jQuery 控件，如 datepicker 可以广泛地自定义。</span><span class="sxs-lookup"><span data-stu-id="21b0e-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="21b0e-184">有关信息，请参阅[可视的自定义： 设计 jQuery UI 主题](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)上[jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/)站点。</span><span class="sxs-lookup"><span data-stu-id="21b0e-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="21b0e-185">支持 HTML5 日期输入的控件</span><span class="sxs-lookup"><span data-stu-id="21b0e-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="21b0e-186">因为更多浏览器支持 HTML5，您将想要使用本机 HTML5 输入，如`date`输入元素，并不使用 jQuery UI 日历。</span><span class="sxs-lookup"><span data-stu-id="21b0e-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="21b0e-187">可以将逻辑添加到应用程序以自动使用 HTML5 控件，如果浏览器支持它们。</span><span class="sxs-lookup"><span data-stu-id="21b0e-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="21b0e-188">若要执行此操作，替换的内容*DatePickerReady.js*具有以下文件：</span><span class="sxs-lookup"><span data-stu-id="21b0e-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="21b0e-189">此脚本的第一行使用 Modernizr 来验证支持 HTML5 日期输入。</span><span class="sxs-lookup"><span data-stu-id="21b0e-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="21b0e-190">如果不支持，jQuery UI 日期选取器已改为挂钩。</span><span class="sxs-lookup"><span data-stu-id="21b0e-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="21b0e-191">([Modernizr](http://www.modernizr.com/docs/)是开放源代码 JavaScript 库，检测到的本地实现 HTML5 和 CSS3 的可用性。</span><span class="sxs-lookup"><span data-stu-id="21b0e-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="21b0e-192">Modernizr 包含在您创建任何新 ASP.NET MVC 项目中。）</span><span class="sxs-lookup"><span data-stu-id="21b0e-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="21b0e-193">进行此更改之后，可以通过使用支持 HTML5，如 Opera 11 的浏览器对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="21b0e-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="21b0e-194">运行应用程序使用了 HTML5 兼容的浏览器并编辑电影条目。</span><span class="sxs-lookup"><span data-stu-id="21b0e-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="21b0e-195">HTML5 日期控件代替 jQuery UI 快捷日历：</span><span class="sxs-lookup"><span data-stu-id="21b0e-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="21b0e-196">由于浏览器的新版本以增量方式实现 HTML5，现在的一个好方法是将代码添加到你的网站可容纳各种各样的 HTML5 支持。</span><span class="sxs-lookup"><span data-stu-id="21b0e-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="21b0e-197">例如，更可靠*DatePickerReady.js*脚本如下所示，可仅部分支持 HTML5 日期控件的你站点的支持浏览器。</span><span class="sxs-lookup"><span data-stu-id="21b0e-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="21b0e-198">此脚本选择 HTML5`input`类型的元素`date`不完全支持 HTML5 日期控件。</span><span class="sxs-lookup"><span data-stu-id="21b0e-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="21b0e-199">对于这些元素，它挂接的 jQuery UI 快捷日历，然后改变`type`属性从`date`到`text`。</span><span class="sxs-lookup"><span data-stu-id="21b0e-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="21b0e-200">通过更改`type`属性从`date`到`text`，消除了 HTML5 日期的部分支持。</span><span class="sxs-lookup"><span data-stu-id="21b0e-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="21b0e-201">更加可靠*DatePickerReady.js*脚本，请参阅[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)。</span><span class="sxs-lookup"><span data-stu-id="21b0e-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="21b0e-202">将为 Null 的日期添加到模板</span><span class="sxs-lookup"><span data-stu-id="21b0e-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="21b0e-203">如果你使用其中一个现有的日期模板，并传递 null 的日期，您将收到运行时错误。</span><span class="sxs-lookup"><span data-stu-id="21b0e-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="21b0e-204">若要使日期模板更可靠，你将更改它们来处理 null 值。</span><span class="sxs-lookup"><span data-stu-id="21b0e-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="21b0e-205">若要支持为 null 的日期，更改中的代码*Views\Shared\DisplayTemplates\DateTime.cshtml*所示：</span><span class="sxs-lookup"><span data-stu-id="21b0e-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="21b0e-206">代码模型时也会返回空字符串**null**。</span><span class="sxs-lookup"><span data-stu-id="21b0e-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="21b0e-207">中的代码更改*Views\Shared\EditorTemplates\Date.cshtml*到以下文件：</span><span class="sxs-lookup"><span data-stu-id="21b0e-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="21b0e-208">当此代码运行时，如果模型不为 null，该模型的`DateTime`使用值。</span><span class="sxs-lookup"><span data-stu-id="21b0e-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="21b0e-209">如果模型为 null，则改为使用当前日期。</span><span class="sxs-lookup"><span data-stu-id="21b0e-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="21b0e-210">便捷</span><span class="sxs-lookup"><span data-stu-id="21b0e-210">Wrapup</span></span>

<span data-ttu-id="21b0e-211">本教程已介绍 ASP.NET 模板化帮助器的基础知识，并演示如何在 ASP.NET MVC 应用程序中使用 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="21b0e-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="21b0e-212">有关详细信息，请尝试以下资源：</span><span class="sxs-lookup"><span data-stu-id="21b0e-212">For more information, try these resources:</span></span>

- <span data-ttu-id="21b0e-213">本地化的信息，请参阅 Rajeesh 的博客[JQueryUI Datepicker 在 ASP.NET MVC 中](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。</span><span class="sxs-lookup"><span data-stu-id="21b0e-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="21b0e-214">有关的 jQuery UI 的信息，请参阅[jQuery UI](http://docs.jquery.com/UI)。</span><span class="sxs-lookup"><span data-stu-id="21b0e-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="21b0e-215">有关如何将本地化 datepicker 控件的信息，请参阅[UI/Datepicker/本地化](http://docs.jquery.com/UI/Datepicker/Localization)。</span><span class="sxs-lookup"><span data-stu-id="21b0e-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="21b0e-216">有关 ASP.NET MVC 模板的详细信息，请参阅 Brad Wilson 的博客系列上[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="21b0e-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="21b0e-217">序列针对 ASP.NET MVC 2 编写的尽管材料仍适用于 ASP.NET MVC 的当前版本。</span><span class="sxs-lookup"><span data-stu-id="21b0e-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="21b0e-218">上一篇</span><span class="sxs-lookup"><span data-stu-id="21b0e-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
