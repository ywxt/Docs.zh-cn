---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 选取列表 (VB) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c60d7cff7c841d23185fbdf07abf0e894b21cf5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831099"
---
<a name="picking-one-animation-out-of-a-list-vb"></a>选取列表 (VB) 的动画
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。 而不是一个常规的动画，`<Case>`发挥作用的元素。 对其 SelectScript 属性的值;返回值必须是数字。 具体取决于此编号，其中一个内子动画&lt;用例&gt;执行。 例如，如果 SelectScript 计算结果为 2，控件工具包运行中的第三个动画&lt;用例&gt;（从 0 开始计数）。

下面的标记定义三个子动画： 重设大小的宽度、 调整大小的高度和淡出。JavaScript 代码 (`Math.floor(3 * Math.random())`)，以便三个动画的之一运行，然后选择介于 0 到 2 之间的数字：

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


[![一个可能的三个动画: 面板中获取更宽](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

一个可能的三个动画: 面板中获取更广 ([单击此项可查看原尺寸图像](picking-one-animation-out-of-a-list-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](animation-depending-on-a-condition-vb.md)
> [下一页](animating-in-response-to-user-interaction-vb.md)
