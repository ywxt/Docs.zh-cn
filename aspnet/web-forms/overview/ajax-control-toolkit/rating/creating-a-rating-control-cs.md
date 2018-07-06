---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 创建分级控件 (C#) |Microsoft Docs
author: wenz
description: 很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实有...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 67c66d2a28a247493a0b1ea67e15935c27af80ae
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830949"
---
<a name="creating-a-rating-control-c"></a>创建分级控件 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)

> 很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实为我们提供有控件工具包。


## <a name="overview"></a>概述

很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实为我们提供有控件工具包。

## <a name="steps"></a>步骤

首先，需要 （至少） 两种类型的映像： 一个用于已填充评级项和一个用于空评级项。 评级项通常是一个星号或笑脸。 对于此方案，作为本教程中的源的代码下载内容的一部分找到三个文件、 smiley.png 和 empty.png 和笑脸 done.png。

然后，创建一个新的 ASP.NET 文件并开始添加`ScriptManager`对它控制：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

然后，添加`Rating`ASP.NET AJAX 控件工具包中的控件。 以下属性需要为此示例设置：

- `CurrentRating` 若要使用初始分级
- `MaxRating` 最大评级
- `EmptyStarCssClass` 要使用的分级项 (star) 时的 CSS 类为空
- `FilledStarCssClass` 填写要使用的分级项 (star) 时的 CSS 类
- `StarCssClass` 要使用的可见状态的 CSS 类
- `WaitingStarCssClass` 要使用而星评级发送回发到服务器的 CSS 类

下面是用于创建具有五个评级控件的标记和其中无填充，最初的项 （表情符号）：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

三个引用的 CSS 类现在需要显示适当的图像文件，这是易于使用 CSS 来执行操作：

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

请确保提供的宽度和高度的三个映像，否则显示可能看起来有点 messed 向上。

最后，分级的结果应是向用户显示 （或至少保存在数据库中）。 因此，添加用于输出的回发到服务器分级窗体的文本消息和一个提交按钮的标签：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

在服务器端代码中，访问分级控件通过其`ID`，然后访问其`CurrentRating`属性的所选的评级项目，在我们的示例值介于 0 到 5 之间的数。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

保存页面，并将其加载到你的浏览器。 当将鼠标悬停 （最初为空） 分级项时，会发生 JavaScript 效果： 分级更改。 单击组星级，保留当前的分级。 最后，当用户提交窗体，服务器端代码将输出的所选的分级。


[![创建具有最少的代码的分级系统](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)

创建分级系统具有最少的代码 ([单击此项可查看原尺寸图像](creating-a-rating-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一篇](creating-a-rating-control-vb.md)
