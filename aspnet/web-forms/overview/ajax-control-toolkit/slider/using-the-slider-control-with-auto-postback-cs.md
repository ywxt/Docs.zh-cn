---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 滑块控件中使用自动回发 (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 它是可以进行滑块自动过帐...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 8e855bebf557536b5f9e2b2730f828e54c63221e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366815"
---
<a name="using-the-slider-control-with-auto-postback-c"></a>滑块控件中使用自动回发 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 它是可以进行一次其值更改滑块自动回发。


## <a name="overview"></a>概述

AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 它是可以进行一次其值更改滑块自动回发。

## <a name="steps"></a>步骤

为了进行更改时自动回发的滑块，这两个文本框特性，因此需要`AutoPostBack="true"`： 文本框中，在将成为滑块本身，以及包含滑块的位置的文本框。 下面是为此，所需的标记：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

`SliderExtender`从 ASP.NET AJAX 控件工具包控件将滑块功能分配给两个文本框：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

更高版本将使用其他标签元素回发的用户通知：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

最后， `ScriptManager` ASP.NET ajax 控件将加载所需的 JavaScript 控件工具包，若要运行的：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

现在，滑块回发;在服务器端，可能会捕获和处理此事件：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


[![将滑块移动触发回发](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

将滑块移动触发回发 ([单击此项可查看原尺寸图像](using-the-slider-control-with-auto-postback-cs/_static/image3.png))


[![然后，此更改的日期写入标签中](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

然后，此更改的日期写入标签中 ([单击此项可查看原尺寸图像](using-the-slider-control-with-auto-postback-cs/_static/image6.png))

> [!div class="step-by-step"]
> [下一篇](databinding-the-slider-control-cs.md)
