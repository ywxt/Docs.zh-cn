---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: 启动模式弹出窗口通过服务器代码 (VB) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是，某些情况下需要该 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: ea5149e9dece5393bb4c431bfc440a745611496d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362834"
---
<a name="launching-a-modal-popup-window-from-server-code-vb"></a>启动模式弹出窗口通过服务器代码 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)

> 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是某些情况下需要打开模式弹出框在服务器端上触发。


## <a name="overview"></a>概述

在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是某些情况下需要打开模式弹出框在服务器端上触发。

## <a name="steps"></a>步骤

首先，需要一个 ASP.NET 按钮 web 控件来演示 ModalPopup 控件的工作原理。 添加此类中的某个按钮&lt;窗体&gt;新页上的元素：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

然后，您需要标记为你想要创建的弹出窗口。 其定义为`<asp:Panel>`控制并确保它包含一个按钮控件。 ModalPopup 控件可提供的功能，若要使此类按钮关闭弹出框;否则将无法轻松地使其消失。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

接下来向页面添加从 ASP.NET AJAX 工具包的 ModalPopup 控件。 设置加载控件的按钮，这样就会消失，按钮和实际弹出项的 ID 属性。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

与使用基于 ASP.NET AJAX; 的所有网页加载所需的 JavaScript 库获取不同的目标的浏览器所需脚本管理器：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

在浏览器中运行示例。 当单击按钮时，将显示模式弹出框。 若要实现使用服务器端代码相同的效果，一个新按钮，则需要：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

正如您所看到的按钮单击生成的回发，并执行`ServerButton_Click()`在服务器上的方法。 此方法中调用 JavaScript 函数`launchModal()`执行确切地，JavaScript 函数将执行加载页面后：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

作业的`launchModal()`是显示 ModalPopup。 `launchModal()`加载完整的 HTML 页后执行函数。 在该时间点，但是，ASP.NET AJAX 框架尚未完全加载。 因此，`launchModal()`函数只设置 ModalPopup 控件必须更高版本显示的变量：

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

`pageLoad()` JavaScript 函数是 ASP.NET AJAX 完全加载后执行的特殊函数。 因此我们将代码添加到此函数可显示 ModalPopup 控件，但是只有当`launchModal()`已调用之前：

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

`$find()`函数查找的页面上命名元素，并需要服务器端的 ID 作为参数。 因此，`$find("mpe")`返回的客户端表示形式 ModalPopup 控件; 它`show()`方法，可以显示的弹出窗口。


[![模式弹出框时出现的任一按钮单击](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

模式弹出框时出现的任一按钮单击 ([单击此项可查看原尺寸图像](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](positioning-a-modalpopup-cs.md)
> [下一页](using-modalpopup-with-a-repeater-control-vb.md)
