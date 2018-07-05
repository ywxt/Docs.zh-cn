---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 创建自定义 HTML 帮助程序 (VB) |Microsoft Docs
author: microsoft
description: 本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。 通过利用 HTML 帮助器...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 0b1f4a6afc62eb23d4591d515e973298da4630f9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396593"
---
<a name="creating-custom-html-helpers-vb"></a>创建自定义 HTML 帮助程序 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> 本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。 通过利用 HTML 帮助程序，可以减少量，你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置枯燥乏味。


本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。 通过利用 HTML 帮助程序，可以减少量，你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置枯燥乏味。

在本教程的第一个部分中，我介绍了一些现有 ASP.NET MVC framework 附带的 HTML 帮助程序。 接下来，我将介绍创建自定义 HTML 帮助程序的两个方法： 我说明了如何创建自定义 HTML 帮助程序，通过创建的共享的方法，并创建扩展方法。

## <a name="understanding-html-helpers"></a>了解 HTML 帮助程序

HTML 帮助器就是返回一个字符串的方法。 该字符串可表示任何类型的所需的内容。 例如，使用 HTML 帮助器来呈现标准 HTML 标记与 HTML 一样`<input>`和`<img>`标记。 此外可以使用 HTML 帮助器来呈现选项卡条带或 HTML 表的数据库数据等更复杂的内容。

ASP.NET MVC 框架包括以下一组标准的 HTML 帮助程序 （这不是完整的列表）：

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

例如，考虑列表 1 中的窗体。 呈现此窗体所使用的两个标准 HTML 帮助程序 （请参阅图 1） 的帮助。 使用此窗体`Html.BeginForm()`和`Html.TextBox()`帮助器方法。


[![与 HTML 帮助器呈现页](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**图 01**： 与 HTML 帮助器呈现的页 ([单击以查看实际尺寸的图像](creating-custom-html-helpers-vb/_static/image3.png))


**代码清单 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()`帮助器方法用于创建开始和结束 HTML`<form>`标记。 请注意，`Html.BeginForm()`方法调用中的 using 语句。 使用语句将确保`<form>`标记获取使用的结尾处结束块。

如果您愿意，而不是创建一个 using 块中，您可以调用 Html.EndForm() 帮助器方法来关闭`<form>`标记。 使用任何方法来创建一个打开和关闭`<form>`似乎是最直观的标记。

`Html.TextBox()`帮助器方法用于在列表 1 中呈现 HTML`<input>`标记。 如果你看到代码清单 2 中的 HTML 源，然后在浏览器中选择查看源。 请注意源包含标准的 HTML 标记。

> [!IMPORTANT]
> 请注意，`Html.TextBox()`帮助器呈现 HTML`<%= %>`标记而不是`<% %>`标记。 如果不包含等号，然后执行任何操作获取浏览器中呈现。

ASP.NET MVC 框架包含一小组帮助程序。 很可能需要扩展 MVC 框架使用自定义 HTML 帮助程序。 在本教程的其余部分，了解创建自定义 HTML 帮助程序的两个方法。

**代码清单 2 – `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>使用共享方法创建 HTML 帮助程序

若要创建新的 HTML 帮助器的最简单方法是创建返回的字符串的共享的方法。 例如，假设你决定创建新的 HTML 帮助程序呈现 HTML`<label>`标记。 可以使用在代码清单 2 中的类来呈现`<label>`。

**代码清单 2 – `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

没有什么特别之处代码清单 2 中的类。 `Label()`方法只返回一个字符串。

列表 3 中已修改的索引视图使用`LabelHelper`呈现 HTML`<label>`标记。 请注意，该视图包含`<%@ imports %>`导入 Application1.Helpers 命名空间的指令。

**代码清单 2 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>使用扩展方法创建 HTML 帮助程序

如果你想要创建的 HTML 帮助程序就类似于标准的 HTML 帮助程序，它们包含在 ASP.NET MVC framework，则需要创建扩展方法。 扩展方法，可向现有类中添加新的方法。 在创建时的 HTML 帮助器方法，添加到新方法`HtmlHelper`表示视图的 Html 属性的类。

列表 3 中的 Visual Basic 模块添加名为扩展方法`Label()`到`HtmlHelper`类。 有一些您会注意到有关此模块的内容。 首先，请注意，该模块用修饰`<Extension()>`属性。 若要使用此属性，必须导入`System.Runtime.CompilerServices`命名空间

其次，注意的第一个参数`Label()`方法表示`HtmlHelper`类。 扩展方法的第一个参数指示的扩展方法扩展的类。

**代码清单 3 – `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

创建一个扩展方法，并已成功生成应用程序后，扩展方法将出现在 Visual Studio Intellisense 等所有其他方法的类 （请参见图 2）。 唯一的区别是该扩展方法显示一个特殊符号旁边 （向下箭头的图标）。


[![使用 Html.Label() 扩展方法](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**图 02**： 使用 Html.Label() 扩展方法 ([单击以查看实际尺寸的图像](creating-custom-html-helpers-vb/_static/image6.png))


列表 4 中经过修改的索引视图使用 Html.Label() 扩展方法呈现的所有其&lt;标签&gt;标记。

**列表 4 – `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>总结

在本教程中，您学习了创建自定义 HTML 帮助程序的两个方法。 首先，您学习了如何创建自定义`Label()`通过创建的共享的方法的 HTML 帮助器返回的字符串。 接下来，您学习了如何创建自定义`Label()`上创建扩展方法的 HTML 帮助器方法`HtmlHelper`类。

在本教程中，我专注于构建一个非常简单的 HTML 帮助器方法。 请注意，HTML 帮助器可以是你想的那么复杂。 您可以构建丰富的内容，如树视图、 菜单或表的数据库数据呈现的 HTML 帮助程序。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-views-overview-vb.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
