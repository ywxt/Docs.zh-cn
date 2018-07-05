---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 数据绑定滑块控件 (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 就可以将绑定当前 positio...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cbb53309ccde9ed6be67a977a56cf2942bbe7f8c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400650"
---
<a name="databinding-the-slider-control-c"></a>数据绑定滑块控件 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)

> AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。


## <a name="overview"></a>概述

AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

接下来，添加两个`TextBox`到页面的控件。 一个将转换为图形滑块，和另一个将保存的滑块位置。

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

下一步已是最后一步。 `SliderExtender`从 ASP.NET AJAX 控件工具包控件使一个滑块，从第一个文本框和滑块位置更改时，会自动更新第二个文本框。 要使其工作，以便`SliderExtender`的`TargetControlID`属性必须设置为第一个文本框; ID`BoundControlID`属性必须设置为第二个文本框的 ID。

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

您可以看到在浏览器中，数据绑定的工作在两个方向： 在文本框中输入新值更新滑块的位置。 如果仅读取第二个文本框中，可以这样就更难用户手动更新中有值与文本字段添加较弱的保护。


[![滑块和文本框都保持同步](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)

滑块和文本框都是同步 ([单击此项可查看原尺寸图像](databinding-the-slider-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-the-slider-control-with-auto-postback-cs.md)
> [下一页](using-the-slider-control-with-auto-postback-vb.md)
