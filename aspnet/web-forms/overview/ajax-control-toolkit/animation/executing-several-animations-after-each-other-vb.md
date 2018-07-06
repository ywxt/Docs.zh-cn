---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 多个动画逐一执行 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它允许运行跌落造成的严重...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 3d94619ca40d288f8a5a391ef02103902bd2550c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835950"
---
<a name="executing-several-animations-after-each-other-vb"></a>多个动画逐一执行 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它允许在它们运行多个动画一个。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它允许在它们运行多个动画一个。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。 通常情况下，`<OnLoad>`只接受一个动画。 此动画框架允许你联接为一个，并使用多个动画`<Sequence>`元素。 中的所有动画`<Sequence>`是执行一个接一个。 下面是有关可能的标记`AnimationExtender`控件，首先进行更广泛的面板和增大或减小其高度：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

当您运行此脚本，面板第一次获得更宽且然后较小。


[![第一次增加宽度](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

第一次增加宽度 ([单击此项可查看原尺寸图像](executing-several-animations-after-each-other-vb/_static/image3.png))


[![再减少高度](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

然后减小高度 ([单击此项可查看原尺寸图像](executing-several-animations-after-each-other-vb/_static/image6.png))

> [!div class="step-by-step"]
> [上一页](executing-several-animations-at-the-same-time-vb.md)
> [下一页](animation-depending-on-a-condition-vb.md)
