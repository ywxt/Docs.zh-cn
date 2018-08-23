---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 使用客户端代码 (VB) 更改动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可以在动画...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: bfce413cd45daab62a247d596d9b51cb82cc7f97
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832504"
---
<a name="changing-an-animation-using-client-side-code-vb"></a>使用客户端代码 (VB) 更改动画
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可以使用自定义客户端的 JavaScript 代码更改动画。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可以使用自定义客户端的 JavaScript 代码更改动画。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

通过 HTML 按钮会启动实际的动画：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

请注意，没有任何`<Animations>`中的节点`AnimationExtender`控件。 自定义 JavaScript 代码用于提供与控件一起使用的动画。

与使用服务器 API 的`AnimationExtender`，没有无法轻松地将动画尚未分配给该扩展器。 但是扩展器确实公开了几种方法来读取和写入动画注册的各种事件 (`OnClick`， `OnLoad`，依此类推)。 下面是一些可能的恶意活动：

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

返回值的格式`get_*()`函数和变量的格式`set_*()`函数是一个 JSON 字符串，提供的对象表示形式的 XML 标记是什么。 目前，没有方法来传递一个对象，但可以读取某个对象从给定的动画 (`get_OnXXXBehavior()`方法)。

下面是一个 JSON 字符串 (不带分隔引号和格式可以很好地) 表示动画触发的按钮，但调整其大小时和淡出在同一时间对面板进行动画处理：

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

以下 JavaScript 代码将分配到此 JSON descripting`OnClick`动画的当前扩展程序并运行它：

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]


[![动画立即运行而无需单击鼠标 （和使用很少标记）](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

动画立即运行不带鼠标单击 （和使用很少标记） ([单击此项可查看原尺寸图像](changing-an-animation-using-client-side-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](executing-animations-using-client-side-code-vb.md)
> [下一页](animating-an-updatepanel-control-vb.md)
