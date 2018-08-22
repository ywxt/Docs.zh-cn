---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 动态添加 Accordion 窗格 (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明 w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 16cefadb7086a658b20558526757f9229a43fcc9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830467"
---
<a name="dynamically-adding-an-accordion-pane-c"></a>动态添加 Accordion 窗格 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明内页面本身，但可以使用服务器端代码来实现相同的结果。


## <a name="overview"></a>概述

AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明内页面本身，但可以使用服务器端代码来实现相同的结果。

## <a name="steps"></a>步骤

可折叠面板控件公开服务器端代码的所有重要属性。 除此之外，`Panes`属性授予访问权限的窗格组成可折叠面板集合。 每个窗格中的类型没有`AccordionPane`。 因此，轻松地创建此类的窗格为：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`HeaderContainer`的属性`AccordionPane`提供访问的窗格; 标头部分中的 ASP.NET 控件`ContentContainer`属性的`AccordionPane`窗格的内容部分对执行相同操作。 这使得 ASP.NET 代码，可以将内容添加到窗格：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

最后，必须将窗格添加到`Panes`可折叠面板的集合：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

下面是将两个窗格添加到 Accordion 控件的完整服务器端代码：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

唯一缺少元素是可折叠面板本身，具体取决于是否存在 ASP.NET`ScriptManager`控件：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

若要完成该示例，两个可折叠面板控件中引用的 CSS 类提供浏览器的样式信息：

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


[![服务器端代码动态添加 accordion 中的数据](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

服务器端代码动态添加 accordion 中的数据 ([单击此项可查看原尺寸图像](dynamically-adding-an-accordion-pane-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](databinding-to-an-accordion-cs.md)
> [下一页](databinding-to-an-accordion-vb.md)
