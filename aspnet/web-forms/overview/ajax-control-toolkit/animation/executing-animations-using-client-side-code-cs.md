---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: 执行动画使用客户端代码 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画执行中...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b58579a2a3b4849a69337600492e2b1a69175513
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389119"
---
<a name="executing-animations-using-client-side-code-c"></a>使用客户端代码 (C#) 执行动画
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可能使用自定义客户端的 JavaScript 代码会触发动画执行。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可能使用自定义客户端的 JavaScript 代码会触发动画执行。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

内`<Animations>`节点，请使用`<OnClick>`运行动画一次用户单击的面板。 添加两个动画 parallelly 执行：

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

为了演示目的，此动画 （和使用控件工具包创建的任何其他动画） 执行该页面运行后，使用 JavaScript 代码。 我们首先需要访问`AnimationExtender`控件。 ASP.NET AJAX 库提供了`$find()`此任务的函数：

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

`AnimationExtender`控件公开一个丰富的 API，包括名称与在 XML 标记中使用的事件处理程序方法： `OnClick()`， `OnLoad()`，依次类推。 例如，调用`OnClick()`方法将执行内的动画`<OnClick>`元素的`AnimationExtender`控件：

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

下面是模拟的面板中单击了页面完全加载后的完整客户端的 JavaScript 代码，请注意，`pageLoad()`都包括的 JavaScript 库一直和函数名称使用它在由调用 ASP.NET AJAX 一次页面加载。

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


[![动画立即运行而无需单击鼠标](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

动画立即运行不带鼠标单击 ([单击此项可查看原尺寸图像](executing-animations-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](modifying-animations-from-the-server-side-cs.md)
> [下一页](changing-an-animation-using-client-side-code-cs.md)
