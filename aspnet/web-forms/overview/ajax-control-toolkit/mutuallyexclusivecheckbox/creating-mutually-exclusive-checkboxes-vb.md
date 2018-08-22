---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 创建互斥复选框 (VB) |Microsoft Docs
author: wenz
description: 可以选择仅一组选项之一，通常用于单选按钮。 但还有一个缺点： 选择一个单选按钮组中的后，...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd338b622779b64dd59f9cf6f3e2365ef5cb3ffb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824731"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a>创建互斥复选框 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> 可以选择仅一组选项之一，通常用于单选按钮。 但还有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。 复选框可以在任何时候是未选中状态，但是不是互相排斥。 本教程提供了最佳的这两种方法： 是互斥的复选框。


## <a name="overview"></a>概述

可以选择仅一组选项之一，通常用于单选按钮。 但还有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。 复选框可以在任何时候是未选中状态，但是不是互相排斥。 本教程提供了最佳的这两种方法： 是互斥的复选框。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含 MutuallyExclusiveCheckBox 扩展器。 这使程序员可以分配给组名称的任何复选框 (`Key`属性)。 从同一组中的所有复选框，只有一个可能一次选择。

让我们开始新的 ASP.NET 页面上放置两个复选框。 可以有多个，但其中的两个已足够用于演示的原则：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

对于这两个复选框，必须将页上放 MutuallyExclusiveCheckBoxExtender 控件。 这两个键属性需要具有相同的值，就像 HTML 单选按钮元素的属性必须完全相同，表示一的组所属的值。 扩展器的 TargetControlID 属性指向复选框的 ID。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

最后，包括 ASP.NET AJAX`ScriptManager`所需 ASP.NET AJAX 控件工具包中的所有元素：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

保存并运行此页： 您可以选中和取消选中这两个复选框，但是在任何时间可以两个复选框进行检查。


[![可以一次选中一个复选框](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

可以一次选中一个复选框 ([单击此项可查看原尺寸图像](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](creating-mutually-exclusive-checkboxes-cs.md)
