---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 动画 (VB) 过程中禁用操作 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它还支持操作...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 811e1d75f79885f3f4c561d9211fec625fcf1807
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823563"
---
<a name="disabling-actions-during-animation-vb"></a>动画 (VB) 过程中禁用操作
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它还支持的操作，例如鼠标点击操作。 但是时鼠标单击启动动画，最好在动画期间禁用鼠标单击。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它还支持的操作，例如鼠标点击操作。 但是时鼠标单击启动动画，最好在动画期间禁用鼠标单击。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

动画将应用于如下的 HTML 按钮：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

请注意，由于我们不希望按钮以创建一个回发; 而不是 Web 控件使用 HTML 控件它应只需启动为我们的客户端的动画。

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

内`<Animations>`节点，`<OnClick>`是正确的元素，用于处理鼠标单击。 但是，在动画期间，可以单击该按钮。 `<EnableAction>`元素可以考虑到这一点。 设置`Enabled="false"`动画的一部分禁用的按钮。 因为我们要使用多个单独的动画 （禁用按钮和实际的动画）`<Parallel>`元素必须为粘合连接成一个单一的动画。 下面是完整标记`AnimationExtender`:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

它还可以在列表的末尾使用下面的 XML 元素的动画结束后重新启用到按钮：

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

但是在给定方案这将是没有用自按钮淡出，并且不在动画结束时可见。


[![动画运行时，将禁用的按钮](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

动画运行时，将禁用的按钮 ([单击此项可查看原尺寸图像](disabling-actions-during-animation-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](animating-in-response-to-user-interaction-vb.md)
> [下一页](triggering-an-animation-in-another-control-vb.md)
