---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 通过 (VB) 的客户端代码操作 Dropshadow |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScrip 更改此扩展器的属性...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: d8b8330174f6f49e96c42a0e15eeaf934bf24f87
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830079"
---
<a name="manipulating-dropshadow-properties-from-client-code-vb"></a>通过 (VB) 的客户端代码操作 Dropshadow
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScript 代码更改此扩展器的属性。


## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScript 代码更改此扩展器的属性。

## <a name="steps"></a>步骤

代码开头包含几行文本的面板：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

关联的 CSS 类为面板提供了一种很好的背景色：

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

`DropShadowExtender`添加进来以扩展面板中的投影效果，设置为 50%的不透明度：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

然后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

另一个面板包含用于设置投影的不透明度的两个 JavaScript 链接： 减号链接会降低阴影的不透明度，加上链接会增加它。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。 ASP.NET AJAX 定义`$find()`完全该任务的方法。 然后，将`get_Opacity()`方法检索当前不透明度，`set_Opacity()`方法将其设置。 JavaScript 代码然后将当前的不透明度值放入`<label>`元素：

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

在客户端上更改不透明度 ([单击此项可查看原尺寸图像](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](adjusting-the-z-index-of-a-dropshadow-vb.md)
