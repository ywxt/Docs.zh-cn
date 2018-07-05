---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 调整 DropShadow (VB) 的 Z-索引 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件中，已为冲突...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 78697f51a09dfaad315255efa23120d4c456bfea
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829539"
---
<a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>调整 DropShadow (VB) 的 Z-索引
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。 当菜单项会弹出，随即出现之后投影。


## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。 当菜单项会弹出，随即出现之后投影。

## <a name="steps"></a>步骤

代码开始与面板本身，以便在面板包含足够多的效果是可见的文本包含足够多的文本：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

紧前面放置另一个面板`panelShadow`面板。 它包含一个具有水平方向，以便通过显示菜单项 (确切地说： 下)`dropShadow`面板):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

然后，将`DropShadowExtender`添加扩展`panelShadow`面板中的投影效果：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

最后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

当运行此脚本时，菜单项显示在面板的下方。 但是，菜单上使用的 CSS 类`panel`其中只需定义两件事要使元素显示在其他面板：

- 相对定位
- 正 z 索引

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

然后，`DropShadowExtender`控件不与菜单控件不再冲突。


[![之前: 菜单项不可见](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

之前: 菜单项不可见 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))


[![菜单项显示之后：](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

之后： 将显示菜单项 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))

> [!div class="step-by-step"]
> [上一页](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一页](manipulating-dropshadow-properties-from-client-code-vb.md)
