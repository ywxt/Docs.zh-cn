---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: 调整 DropShadow (C#) 的 Z-索引 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件中，已为冲突...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 5cee2acfac74c0790a7ad82bbfb503a8a16f6b47
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825643"
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a>调整 DropShadow (C#) 的 Z-索引
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。 当菜单项会弹出，随即出现之后投影。


## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。 当菜单项会弹出，随即出现之后投影。

## <a name="steps"></a>步骤

代码开始与面板本身，以便在面板包含足够多的效果是可见的文本包含足够多的文本：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

紧前面放置另一个面板`panelShadow`面板。 它包含一个具有水平方向，以便通过显示菜单项 (确切地说： 下)`dropShadow`面板):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

然后，将`DropShadowExtender`添加扩展`panelShadow`面板中的投影效果：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

最后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

当运行此脚本时，菜单项显示在面板的下方。 但是，菜单上使用的 CSS 类`panel`其中只需定义两件事要使元素显示在其他面板：

- 相对定位
- 正 z 索引

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

然后，`DropShadowExtender`控件不与菜单控件不再冲突。


[![之前: 菜单项不可见](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

之前: 菜单项不可见 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))


[![菜单项显示之后：](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

之后： 将显示菜单项 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))

> [!div class="step-by-step"]
> [下一篇](manipulating-dropshadow-properties-from-client-code-cs.md)
