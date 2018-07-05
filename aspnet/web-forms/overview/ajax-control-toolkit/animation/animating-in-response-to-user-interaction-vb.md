---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 以响应用户交互 (VB) 进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画可以星型...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 4b774a058e715e4a98e767daf92886f24e627822
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815520"
---
<a name="animating-in-response-to-user-interaction-vb"></a>以响应用户交互 (VB) 进行动画处理
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

内`<Animations>`节点中，有五种方法来启动通过用户交互动画 (缺少的元素是`<OnLoad>`整个页面完全加载后执行):

- `<OnClick>` （在控件上的鼠标单击）
- `<OnHoverOut>` （鼠标离开控件）
- `<OnHoverOver>` (鼠标悬停在控件，停止`<OnHoverOut>`动画)
- `<OnMouseOut>` （鼠标离开控件）
- `<OnMouseOver>` (鼠标悬停在控件，不会停止`<OnMouseOut>`动画)

在此方案中，`<OnClick>`使用。 当用户单击的面板中时，它将调整大小并同时淡出。

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


[![鼠标单击启动动画](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

鼠标单击启动动画 ([单击此项可查看原尺寸图像](animating-in-response-to-user-interaction-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](picking-one-animation-out-of-a-list-vb.md)
> [下一页](disabling-actions-during-animation-vb.md)
