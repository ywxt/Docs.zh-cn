---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 修改动画从服务器端 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可以将动画...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 8954f025873ea553fde26c6e2330ce6e5be2b539
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804049"
---
<a name="modifying-animations-from-the-server-side-c"></a>修改动画从服务器端 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可能在服务器端发生更改动画


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可能在服务器端发生更改动画

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

代码的其余部分在服务器端上运行，并且不使用标记;相反，它使用代码来创建`AnimationExtender`控件：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

但是，该控件工具包当前不提供创建单个动画 API 访问权限。 不过，它是可以将设置`AnimationExtender`的动画属性设置为一个字符串，包含以声明方式分配动画时使用的 XML 标记。 若要创建的 XML 不能包含`<Animations>`元素可以使用.NET Framework 的 XML 支持，或在以下代码，只需提供的字符串：

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

最后，添加`AnimationExtender`控制转移到当前页上，在`<form runat="server">`元素，并确保动画包含并运行：

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]


[![使用服务器端 C# /VB 代码创建动画](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

使用服务器端 C# /VB 代码创建动画 ([单击此项可查看原尺寸图像](modifying-animations-from-the-server-side-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](triggering-an-animation-in-another-control-cs.md)
> [下一页](executing-animations-using-client-side-code-cs.md)
