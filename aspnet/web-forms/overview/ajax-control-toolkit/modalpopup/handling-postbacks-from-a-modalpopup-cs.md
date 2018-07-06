---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: 处理回发 ModalPopup (C#) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 Pos 时，必须格外谨慎处理...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 0f27d28b9851f8e26c207a6bc495e98ad70577a2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838117"
---
<a name="handling-postbacks-from-a-modalpopup-c"></a>处理回发 ModalPopup (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 从弹出窗口中创建一个回发时，必须格外小心。


## <a name="overview"></a>概述

在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 从弹出窗口中创建一个回发时，必须格外小心。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

接下来，添加一个面板作为模式弹出框。 存在，用户可以输入一个名称和电子邮件地址。 一个按钮用于关闭弹出窗口和保存的信息。 请注意，`OnClick`属性设置，以便在回发发生时单击此按钮：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

页面本身包含两个标签，以便完全相同的信息： 名称和电子邮件地址。 一个按钮用于触发模式弹出框：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

为了使显示的弹出窗口，添加`ModalPopupExtender`控件。 设置`PopupControlID`属性为面板的 ID 和`TargetControlID`到按钮的 ID:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

现在只要`Save`模式弹出框内单击时，服务器端`SaveData()`执行方法。 您可以在数据存储中保存输入的数据。 为简单起见，只需标签中输出的新数据：

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

此外，应使用当前名称和电子邮件填充模式弹出框中的文本框控件。 但是这是仅有必要不回发发生时。 如果回发，ASP.NET 视图状态功能便会自动填充的文本框使用适当的值。

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]


[![模式弹出框会导致回发](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

模式弹出框会导致回发 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-modalpopup-with-a-repeater-control-cs.md)
> [下一页](positioning-a-modalpopup-cs.md)
