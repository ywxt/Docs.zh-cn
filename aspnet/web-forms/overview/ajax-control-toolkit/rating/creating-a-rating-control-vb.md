---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 创建分级控件 (VB) |Microsoft Docs
author: wenz
description: 很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实有...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 501859b833eb18147e483b0d7a7359133d790d8b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368843"
---
<a name="creating-a-rating-control-vb"></a>创建分级控件 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> 很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实为我们提供有控件工具包。


## <a name="overview"></a>概述

很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实为我们提供有控件工具包。

## <a name="steps"></a>步骤

首先，需要 （至少） 两种类型的映像： 一个用于已填充评级项和一个用于空评级项。 评级项通常是一个星号或笑脸。 对于此方案，作为本教程中的源的代码下载内容的一部分找到三个文件、 smiley.png 和 empty.png 和笑脸 done.png。

然后，创建一个新的 ASP.NET 文件并开始添加`ScriptManager`对它控制：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

然后，添加`Rating`ASP.NET AJAX 控件工具包中的控件。 以下属性需要为此示例设置：

- `CurrentRating` 若要使用初始分级
- `MaxRating` 最大评级
- `EmptyStarCssClass` 要使用的分级项 (star) 时的 CSS 类为空
- `FilledStarCssClass` 填写要使用的分级项 (star) 时的 CSS 类
- `StarCssClass` 要使用的可见状态的 CSS 类
- `WaitingStarCssClass` 要使用而星评级发送回发到服务器的 CSS 类

下面是用于创建具有五个评级控件的标记和其中无填充，最初的项 （表情符号）：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

三个引用的 CSS 类现在需要显示适当的图像文件，这是易于使用 CSS 来执行操作：

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

请确保提供的宽度和高度的三个映像，否则显示可能看起来有点 messed 向上。

最后，分级的结果应是向用户显示 （或至少保存在数据库中）。 因此，添加用于输出的回发到服务器分级窗体的文本消息和一个提交按钮的标签：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

在服务器端代码中，访问分级控件通过其`ID`，然后访问其`CurrentRating`属性的所选的评级项目，在我们的示例值介于 0 到 5 之间的数。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

保存页面，并将其加载到你的浏览器。 当将鼠标悬停 （最初为空） 分级项时，会发生 JavaScript 效果： 分级更改。 单击组星级，保留当前的分级。 最后，当用户提交窗体，服务器端代码将输出的所选的分级。


[![创建具有最少的代码的分级系统](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

创建分级系统具有最少的代码 ([单击此项可查看原尺寸图像](creating-a-rating-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](creating-a-rating-control-cs.md)
