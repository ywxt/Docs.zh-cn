---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX 控件工具包控件和控件扩展程序 (C#) |Microsoft Docs
author: microsoft
description: 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页面。
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 2c978bec3780ef2e83aee32a084d1baf5066e0e2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817221"
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>使用 AJAX 控件工具包控件和控件扩展程序 (C#)
====================
by [Microsoft](https://github.com/microsoft)

> 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页面。


AJAX 控件工具包包含一组控件和控件扩展程序。 在本简短教程中，您将学习如何将控件和控件扩展程序添加到 ASP.NET 页面。

> [!NOTE] 
> 
> 有关安装 AJAX 控件工具包并将 AJAX 控件工具包添加到 Visual Studio/Visual Web Developer 工具箱中的说明，请参阅本教程[开始使用 AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-cs.md)。


## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX 控件工具包控件

AJAX 控件工具包控件的工作方式与普通的 ASP.NET 控件。 可以将控件从工具箱拖到 ASP.NET 页面。 可以将控件添加到设计视图或源视图中的页面。

使用 AJAX 控件工具包中的所有控件时一个特殊的要求。 页面必须包含一个 ScriptManager 控件。 ScriptManager 控件负责包括所有 AJAX 控件工具包控件所需的必要 JavaScript。

例如，AJAX 控件工具包选项卡包括名为编辑器控件的控件。 此控件显示丰富的 HTML 编辑器。 请按照下列步骤编辑器控件添加到页面：

1. 创建一个名为 ShowEditor.aspx 的新 ASP.NET 页
2. 选择工具箱中的 ScriptManager 控件从地板下面传来 AJAX 扩展选项卡并将控件拖到绘图页上。
3. 工具箱中选择从地板下面传来的 AJAX 控件工具包选项卡的编辑器控件并将控件拖到绘图页上 （请参阅图 1）。 在设计器应如图 2 所示。
4. 通过选择菜单选项来运行网站**调试、 启动调试**或按 F5 键。
5. 应看到图 3 中的页。


[![选择 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**图 01**： 选择 HTML 编辑器控件 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))


[![使用 ScriptManager 和编辑控件的 visual Studio 设计器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**图 02**： 使用 ScriptManager 和编辑控件的 Visual Studio 设计器 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))


[![DisplayEditor.aspx 页](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**图 03**: DisplayEditor.aspx 页 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控件工具包控件扩展器

AJAX 控件工具包还包含控件扩展程序。 顾名思义，扩展程序控件扩展了现有控件的功能。 例如，ConfirmButton 控件扩展程序扩展了标准 ASP.NET 按钮控件。 扩展器更改按钮控件的行为，使按钮将显示一个确认对话框时单击它。

控件扩展程序，就像 AJAX 控件工具包控件需要 ScriptManager 控件。 在开始使用的页中的控件扩展程序之前，必须向页面中添加 ScriptManager 控件。

请按照以下步骤使用 ConfirmButton 控件扩展程序操作：

1. 创建一个名为 ShowConfirmButton.aspx 的新 ASP.NET 页
2. 通过将控件拖到绘图页上从地板下面传来 AJAX 扩展选项卡添加到页面的 ScriptManager 控件。
3. 将标准的按钮控件添加到页中，通过将从地板下面传来标准选项卡按钮拖到设计器图面上的工具箱中。
4. 单击**添加扩展程序**任务选项 （请参阅图 4）。
5. 在选择扩展程序对话框中，选择 ConfirmButtonExtender （请参见图 5），然后单击确定按钮。
6. 在设计器中选择按钮控件和扩展的扩展程序，Button1\_ConfirmButtonExtender 节点在属性窗口中的 （请参阅图 6）。 将该值赋*真正？* ConfirmText 属性。
7. 通过选择菜单选项运行页**调试、 启动调试**或按 F5 键。


[![添加扩展器任务选项](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**图 04**: 添加扩展器任务选项 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))


[![选择 ConfirmButton 控件扩展程序](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**图 05**： 选择 ConfirmButton 控件扩展程序 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))


[![设置 ConfirmButton 属性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**图 06**： 设置 ConfirmButton 属性 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))


当页面打开时，会看到一个按钮。 单击按钮时，可以在图 7 中获取确认对话框。


[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**图 07**： 显示确认对话框 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))


请注意，您通常执行不将扩展程序控件拖到页。 相反，使用**添加扩展程序**任务选项可将扩展器添加到已添加到页面的控件。 此外，请注意，设置控件扩展程序属性通过打开要扩展的控件的属性表。

单个 ASP.NET 控件可以由多个控件扩展程序扩展。 要扩展的控件的属性表将列出所有与该控件关联的控件扩展程序。

> [!div class="step-by-step"]
> [上一页](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
