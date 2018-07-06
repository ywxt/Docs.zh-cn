---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 使用多个弹出控件 (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 还有可能要使用 m...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a2be36ecf17a95d53e5e912ba0a90113f70f2fb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807630"
---
<a name="using-multiple-popup-controls-vb"></a>使用多个弹出控件 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 还有可能要使用在同一页上的多个弹出控件。


## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 还有可能要使用在同一页上的多个弹出控件。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

接下来，添加一个面板作为弹出窗口。 在当前的方案中，面板包含`Calendar`控件。 为了避免引起的日历的回发页面刷新，面板都会放到`UpdatePanel`控件：

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

该页还包含两个文本框。 对于每个文本框，文本框中激活后，应显示日历弹出框。

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

现在扩展使用的两个文本框的每个`PopupControlExtender`。 `TargetControlID`属性提供绑定到扩展器控件的 ID。 `PopupControlID`属性包含的弹出面板的 ID。 在这种情况下，这两个扩展程序显示相同的面板中，但也是可能的不同的面板。

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

现在只要您在文本字段内单击，日历显示字段的下方，您可以选择一个日期。 （所选的日期取回到文本框中将介绍在不同的教程。）


[![当用户单击文本框中，将显示日历](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](using-multiple-popup-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [下一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
