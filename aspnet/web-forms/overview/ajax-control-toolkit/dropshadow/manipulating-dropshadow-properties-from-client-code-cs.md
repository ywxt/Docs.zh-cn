---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 操作 Dropshadow 从客户端代码 (C#) |Microsoft Docs
author: wenz
description: 自定义 DataList 的编辑界面
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: e3166b9da97a0f4097566b62ba52b6d672eab78f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377280"
---
<a name="manipulating-dropshadow-properties-from-client-code-c"></a>操作 Dropshadow 从客户端代码 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScript 代码更改此扩展器的属性。


## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScript 代码更改此扩展器的属性。

## <a name="steps"></a>步骤

代码开头包含几行文本的面板：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

关联的 CSS 类为面板提供了一种很好的背景色：

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

`DropShadowExtender`添加进来以扩展面板中的投影效果，设置为 50%的不透明度：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

然后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

另一个面板包含用于设置投影的不透明度的两个 JavaScript 链接： 减号链接会降低阴影的不透明度，加上链接会增加它。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。 ASP.NET AJAX 定义`$find()`完全该任务的方法。 然后，将`get_Opacity()`方法检索当前不透明度，`set_Opacity()`方法将其设置。 JavaScript 代码然后将当前的不透明度值放入`<label>`元素：

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

在客户端上更改不透明度 ([单击此项可查看原尺寸图像](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [下一页](adjusting-the-z-index-of-a-dropshadow-vb.md)
