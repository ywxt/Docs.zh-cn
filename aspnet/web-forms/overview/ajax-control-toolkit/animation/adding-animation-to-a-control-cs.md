---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 将动画添加到控件 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 本教程演示如何...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: aa977883af931bb74b791104cf4ee3212079e43a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831677"
---
<a name="adding-animation-to-a-control-c"></a>将动画添加到控件 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 本教程演示如何设置此类动画。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 本教程演示如何设置此类动画。

## <a name="steps"></a>步骤

第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

在此方案中的动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

面板关联的 CSS 类定义的背景颜色和宽度：

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

接下来，我们需要`AnimationExtender`。 提供后`ID`和常用`runat="server"`，则`TargetControlID`属性必须设置为该控件，要进行动画处理，在本例中，面板：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

使用 XML 语法，遗憾的是当前不完全支持 Visual Studio 的 IntelliSense 以声明方式，应用整个动画。 根节点是`<Animations>;`在此节点中，这将决定当 animation(s) take(s) 位置允许多个事件：

- `OnClick` （鼠标单击）
- `OnHoverOut` （当鼠标离开控件）
- `OnHoverOver` (当鼠标悬停在控件上，停止`OnHoverOut`动画)
- `OnLoad` （如果已加载页）
- `OnMouseOut` （当鼠标离开控件）
- `OnMouseOver` (当鼠标悬停在控件上，不会停止`OnMouseOut`动画)

Framework 附带了动画，每个由其自己的 XML 元素表示一组。 下面是所选内容：

- `<Color>` （更改一种颜色）
- `<FadeIn>` （淡入淡出）
- `<FadeOut>` （淡出）
- `<Property>` （更改控件的属性）
- `<Pulse>` (pulsating)
- `<Resize>` （更改大小）
- `<Scale>` （按比例更改大小）

在此示例中，面板应淡出。该动画应需要 1.5 秒钟的时间 (`Duration`属性)，显示每秒 24 帧 （动画步骤） (`Fps` attributs)。 下面是完整标记`AnimationExtender`控件：

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

当运行此脚本时，面板会显示，并在一个半秒内淡出。


[![在面板淡出](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)

在面板淡出 ([单击此项可查看原尺寸图像](adding-animation-to-a-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一篇](executing-several-animations-at-the-same-time-cs.md)
