---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: 使用 CascadingDropDown (VB) 填充列表 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: edd6c330d21a7875b8f90fcf9bbde75978b6d08d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389594"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a>使用 CascadingDropDown (VB) 填充列表
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 （例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）若要解决的第一个挑战是实际填充下拉列表中使用此控件。


## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 （例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）若要解决的第一个挑战是实际填充下拉列表中使用此控件。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

然后，DropDownList 控件是必需的：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

对于此列表中，添加一个 CascadingDropDown 扩展程序。 它将发送的异步请求到 web 服务，这将返回的条目显示在列表中的列表。 为实现此目的，需要设置以下 CascadingDropDown 属性：

- `ServicePath`: Web 服务提供的列表项的 URL
- `ServiceMethod`: Web 方法提供的列表项
- `TargetControlID`: 下拉列表的 ID
- `Category`： 提交到 web 方法调用时类别信息
- `PromptText`： 以异步方式从服务器加载列表数据时显示的文本

下面是针对标记`CascadingDropDown`元素。 C# 和 VB 的唯一区别是关联的 web 服务的名称：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

来自的 JavaScript 代码`CascadingDropDown`扩展程序调用 web 服务方法具有以下签名：

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

因此重要的方面是该方法需要返回类型的数组`CascadingDropDownNameValue`（由 ASP.NET AJAX 控件工具包定义）。 在中`CascadingDropDownNameValue`构造函数，首先必须提供的列表项的文本，然后其值，就像`<option value="VALUE">NAME</option>`像在 HTML 中。 下面是一些示例数据：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

正在加载页在浏览器中的将触发要填充与三个供应商的列表。


[![列表已自动填充](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

自动填充列表 ([单击此项可查看原尺寸图像](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-auto-postback-with-cascadingdropdown-cs.md)
> [下一页](using-cascadingdropdown-with-a-database-vb.md)
