---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 对 UpdatePanel 控件 (C#) 进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 内容的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 9907af3349cd1d3c8a4e3dbdf7a96960982a2e5d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395235"
---
<a name="animating-an-updatepanel-control-c"></a>对 UpdatePanel 控件 (C#) 进行动画处理
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 UpdatePanel 的内容，一个特殊的扩展程序存在的严重依赖于此动画框架： UpdatePanelAnimation。 本教程演示如何为 UpdatePanel 设置此类动画。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 有关的内容`UpdatePanel`，一个特殊的扩展程序存在的严重依赖于此动画框架： `UpdatePanelAnimation`。 本教程演示如何设置此类动画，以`UpdatePanel`。

## <a name="steps"></a>步骤

第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

在此方案中的动画将应用于 ASP.NET`Wizard`驻留在 web 控件`UpdatePanel`。 （任意） 的三个步骤提供足够的选项来触发回发：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

所需的标记`UpdatePanelAnimationExtender`控件是非常类似于用于标记`AnimationExtender`。 在`TargetControlID`我们提供的特性`ID`的`UpdatePanel`进行动画处理; 内`UpdatePanelAnimationExtender`控件，`<Animations>`元素保留的 XML 标记。 但是还有一个区别： 事件和事件处理程序的数量是有限与`AnimationExtender`。 有关`UpdatePanels`，只有两个其中存在：

- `<OnUpdated>` UpdatePanel 更新时
- `<OnUpdating>` 当 UpdatePanel 启动更新

在此方案中，新的内容`UpdatePanel`（之后在回发） 应淡入。 这是为此，时必需的标记：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

现在每次回发的 UpdatePanel 中发生时，新的面板内容淡入顺利。


[![淡入淡出下一步的向导步骤](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

淡入淡出下一步的向导步骤 ([单击此项可查看原尺寸图像](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](changing-an-animation-using-client-side-code-cs.md)
> [下一页](dynamically-controlling-updatepanel-animations-cs.md)
