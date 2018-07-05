---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用 ColorPicker 控件扩展程序 (VB) |Microsoft Docs
author: microsoft
description: 颜色选取器是客户端的颜色选择功能提供用户界面中的弹出控件的 ASP.NET AJAX 扩展程序。 可以将它附加到任何 ASP.NET...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: cad012dd1ce93714ecb127bf3543d5c65803aba9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374174"
---
<a name="using-the-colorpicker-control-extender-vb"></a>使用 ColorPicker 控件扩展程序 (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 颜色选取器是客户端的颜色选择功能提供用户界面中的弹出控件的 ASP.NET AJAX 扩展程序。 可以将它附加到任何 ASP.NET TextBox 控件。 它。


本教程的目的是说明如何使用 AJAX 控件工具包 ColorPicker 控件扩展程序。 ColorPicker 控件扩展程序显示弹出对话框中，可用于选择一种颜色。 只要您想要提供一个直观的用户界面，供用户选择一种颜色，颜色选取器非常有用。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>扩展具有 ColorPicker 控件扩展程序的文本框控件

例如，假设你想要创建可使访问者可以创建自定义的业务卡的网站。 访问者可以为业务卡中输入的文本并选取的颜色。 列表 1 中的 ASP.NET 页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。 当用户提交窗体时，显示所选的值 （请参阅图 1）。


[![用于创建名片的简单窗体](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**图 01**： 用于创建名片的简单窗体 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image2.png))


**代码清单 1-CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

在列表 1 中的工作原理，但窗体不提供出色的用户体验。 用户必须键入到文本框的一种颜色。 如果用户想要的专用的颜色-例如，只是正确的峰值绿色-则为用户阴影必须弄清楚的 HTML 颜色代码而无需任何帮助。

ColorPicker 控件扩展程序可用于创建更好的用户体验。 颜色选取器时将焦点移到 TextBox 控件显示颜色对话框 （请参见图 2）。


[![ColorPicker 控件扩展程序](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**图 02**: ColorPicker 控件扩展程序 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image4.png))


需要完成 ColorPicker 控件扩展程序中使用的窗体列表 1 中的两个步骤：

1. 向页面添加一个 ScriptManager 控件
2. ColorPicker 控件扩展程序添加到页面

可以使用颜色选取器之前，你必须将 ScriptManager 添加到您的页面。 添加 ScriptManager 的好时机是在打开服务器端下方&lt;窗体&gt;标记。 您可以将 ScriptManager 到绘图页上从工具箱 （ScriptManager 位于 AJAX 扩展选项卡下）。 或者，可以在服务器端窗体标记下打开到源视图键入以下标记：

&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;

ColorPicker 控件扩展程序添加到页面的最简单方法是在设计视图中。 如果将鼠标悬停 txtCardColor 文本框中，智能任务选项会显示，用于启用你添加扩展器 （请参见图 3）。 如果选择此选项，则将显示扩展器向导 （请参阅图 4）。


[![添加扩展器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**图 03**： 添加扩展器 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image6.png))


[![选择扩展程序控件扩展程序向导](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**图 04**： 选择使用扩展器向导扩展程序控件 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image8.png))


可以选择要扩展 txtCardColor 文本框使用颜色选取器扩展器的颜色选取器扩展程序。 单击确定以关闭该对话框。

进行这些更改后，页面的源如下所示代码清单 2。

**代码清单 2-CreateCard.aspx （使用颜色选取器）**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

请注意到该页面现在包含出现正下方的 txtCardColor TextBox 控件的 ColorPickerExtender 控件。 ColorPickerExtender 控件扩展 txtCardColor 控件，以便显示颜色选取器对话框。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>使用一个按钮以启动颜色选取器对话框

颜色选取器扩展器支持以下属性：

- PopupButtonId-显示颜色选取器对话框的页上的按钮的 ID。
- PopupPosition-的位置，相对于目标控件，颜色选取器对话框。 可能的值为 Absolute、 Center、 BottomLeft、 BottomRight、 左边框、 TopRight，向右、 和左侧 （默认值为 BottomLeft）。
- SampleControlId-显示所选的颜色的控件的 ID。
- SelectedColor-选定颜色选取器的初始颜色。

这些属性可用于自定义颜色选取器对话框的显示方式和所选的颜色的显示方式。 列表 3 中的页说明了如何使用多个这些属性。

**代码清单 3-CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

列表 3 中的页包括选取颜色按钮 （请参见图 5）。 单击此按钮时，颜色选取器对话框将出现在文本框上方。 如果从对话框中选择一种颜色的所选的颜色显示为 lblSample 标签控件的背景色。

ColorPicker PopupButtonID 属性用于将选择颜色按钮与颜色选取器扩展程序相关联。 提供 PopupButtonID 属性的值，颜色选取器对话框不会再出现在目标控件有焦点。 您必须单击按钮以显示对话框。

SampleControlID 属性用于将显示颜色选取器与所选的颜色的控件相关联。 颜色选取器将此控件的背景色更改为当前选定的颜色。


[![显示具有一个按钮的颜色选取器对话框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**图 05**： 显示颜色选取器对话框使用一个按钮 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image10.png))


## <a name="summary"></a>总结

在本教程中，您学习了如何使用 ColorPicker 控件扩展程序显示弹出颜色选取器对话框。 首先，我们探讨了如何显示对话框时焦点移动到 TextBox 控件。 接下来，您学习了如何创建显示颜色选取器对话框，单击该按钮的按钮。

> [!div class="step-by-step"]
> [上一篇](using-the-colorpicker-control-extender-cs.md)
