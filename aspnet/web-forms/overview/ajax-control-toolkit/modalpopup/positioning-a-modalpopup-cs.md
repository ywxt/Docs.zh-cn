---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup (C#) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是该控件不提供...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: e767785f801b5110f0e9e915cd35c8a4425a9487
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834586"
---
<a name="positioning-a-modalpopup-c"></a>定位 ModalPopup (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是该控件不提供内置的功能，用于定位弹出窗口。


## <a name="overview"></a>概述

在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是该控件不提供内置的功能，用于定位弹出窗口。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`。 控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

接下来，添加一个面板作为模式弹出框。 一个按钮用于关闭弹出窗口：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

每当显示弹出窗口，它应定位在页中的某个特定位置中。 对于此任务中，创建客户端的 JavaScript 函数。 它首先尝试访问面板。 如果成功，将使用 CSS 和 JavaScript （更改将在弹出窗口的位置） 设置面板的位置。 但是，`ModalPopupExtender`还会控制尝试定位弹出窗口。 因此，JavaScript 代码重复定位弹出窗口中，每隔 10 秒。

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

正如您所看到的返回值的`setTimeout()`JavaScript 方法将保存在全局变量。 这样就可以停止重复的按需、 弹出窗口定位使用`clearTimeout()`方法：

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

现在剩下要做的是使浏览器调用这些函数在可能的情况。 `movePanel()`触发面板中单击该按钮时，必须调用 JavaScript 函数：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

并`stopMoving()`函数发挥作用时这可能关闭弹出窗口中触发`ModalPopupExtender`控件：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]


[![模式弹出框显示在指定的位置](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

模式弹出框显示在指定的位置 ([单击此项可查看原尺寸图像](positioning-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](handling-postbacks-from-a-modalpopup-cs.md)
> [下一页](launching-a-modal-popup-window-from-server-code-vb.md)
