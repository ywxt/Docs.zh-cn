---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 从服务器端 (VB) 修改动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可以将动画...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: d39a40f2776d5b87bf82d1a6c6282ce920f4a907
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401949"
---
<a name="modifying-animations-from-the-server-side-vb"></a>从服务器端 (VB) 修改动画
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可能在服务器端发生更改动画


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可能在服务器端发生更改动画

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

代码的其余部分在服务器端上运行，并且不使用标记;相反，它使用代码来创建`AnimationExtender`控件：

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

但是，该控件工具包当前不提供创建单个动画 API 访问权限。 不过，它是可以将设置`AnimationExtender`的动画属性设置为一个字符串，包含以声明方式分配动画时使用的 XML 标记。 若要创建的 XML 不能包含`<Animations>`元素可以使用.NET Framework 的 XML 支持，或在以下代码，只需提供的字符串：

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

最后，添加`AnimationExtender`控制转移到当前页上，在`<form runat="server">`元素，并确保动画包含并运行：

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


[![使用服务器端 C# /VB 代码创建动画](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

使用服务器端 C# /VB 代码创建动画 ([单击此项可查看原尺寸图像](modifying-animations-from-the-server-side-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](triggering-an-animation-in-another-control-vb.md)
> [下一页](executing-animations-using-client-side-code-vb.md)
