---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 选取列表 (C#) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 7ef2c5d37c32150d17b798e22290f33b5619a14c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834667"
---
<a name="picking-one-animation-out-of-a-list-c"></a>选取列表 (C#) 的动画
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。 而不是一个常规的动画，`<Case>`发挥作用的元素。 对其 SelectScript 属性的值;返回值必须是数字。 具体取决于此编号，其中一个内子动画&lt;用例&gt;执行。 例如，如果 SelectScript 计算结果为 2，控件工具包运行中的第三个动画&lt;用例&gt;（从 0 开始计数）。

下面的标记定义三个子动画： 重设大小的宽度、 调整大小的高度和淡出。JavaScript 代码 (`Math.floor(3 * Math.random())`)，以便三个动画的之一运行，然后选择介于 0 到 2 之间的数字：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


[![一个可能的三个动画: 面板中获取更宽](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

一个可能的三个动画: 面板中获取更广 ([单击此项可查看原尺寸图像](picking-one-animation-out-of-a-list-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](animation-depending-on-a-condition-cs.md)
> [下一页](animating-in-response-to-user-interaction-cs.md)
