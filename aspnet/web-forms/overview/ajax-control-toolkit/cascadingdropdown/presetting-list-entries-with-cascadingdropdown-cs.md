---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: 预设置列表条目使用 CascadingDropDown (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 2599b5015f288b2e8d02577a0865252a862574a4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824741"
---
<a name="presetting-list-entries-with-cascadingdropdown-c"></a>预设置列表条目使用 CascadingDropDown (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 借助极少量的代码就可以动态加载数据后，预先选择一个列表元素。


## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 （例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）借助极少量的代码就可以动态加载数据后，预先选择一个列表元素。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

然后，DropDownList 控件是必需的：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

对于此列表中，添加 CascadingDropDown 扩展程序以提供 web 服务 URL 和方法的信息：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

然后 CascadingDropDown 扩展程序以异步方式调用 web 服务使用以下方法签名：

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

该方法返回类型 CascadingDropDown 值的数组。 类型的构造函数要求第一次列表项的标题和值 (HTML`value`属性)。 如果第三个参数设置为 true 时，列表中选择元素时自动在浏览器中。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

加载页面在浏览器中的将填充下拉列表中的与三个供应商，第二个被预先选定状态。


[![填充和预先自动选择列表](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)

填充和预先自动选择列表 ([单击此项可查看原尺寸图像](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-cascadingdropdown-with-a-database-cs.md)
> [下一页](using-auto-postback-with-cascadingdropdown-cs.md)
