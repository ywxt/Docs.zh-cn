---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: 通过 ReorderList (VB) 使用回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供了可以由用户通过拖放重新排序的列表。 只要列表重新排序，采购订单...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 1e2124327a36c94db8bafbdf91f767068ac7e834
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834966"
---
<a name="using-postbacks-with-reorderlist-vb"></a>通过 ReorderList (VB) 使用回发
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> AJAX 控件工具包中的 ReorderList 控件提供了可以由用户通过拖放重新排序的列表。 只要列表重新排序，回发应通知更改的服务器。


## <a name="overview"></a>概述

`ReorderList` AJAX 控件工具包中的控件提供了可以由用户通过拖放重新排序的列表。 只要列表重新排序，回发应通知更改的服务器。

## <a name="steps"></a>步骤

有多个可能的数据来源的`ReorderList`控件。 一种是使用`XmlDataSource`控件：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

若要将绑定到此 XML`ReorderList`必须设置控制和启用回发，以下属性：

- `DataSourceID`： 数据源的 ID
- `SortOrderField`： 要作为排序依据的属性
- `AllowReorder`： 是否允许用户重新排列列表元素
- `PostBackOnReorder`： 是否创建一个回发时重新排列列表

下面是控件的相应标记：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

内`ReorderList`可能会使用绑定控件，数据源中的特定数据`Eval()`方法：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

在任意位置的页上，标签将在实际应用的最后一个重新排序发生时保存的信息：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

此标签填入处理回发的服务器端代码中的文本：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

最后，若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须置于页面：

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![每个重新排序触发回发](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

每个重新排序触发回发 ([单击此项可查看原尺寸图像](using-postbacks-with-reorderlist-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](drag-and-drop-via-reorderlist-cs.md)
> [下一页](drag-and-drop-via-reorderlist-vb.md)
