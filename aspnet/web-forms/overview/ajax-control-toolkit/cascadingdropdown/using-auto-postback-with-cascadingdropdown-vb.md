---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 通过 CascadingDropDown (VB) 使用自动回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 274189184b82734e89a30c9450079d7e07971f3c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378156"
---
<a name="using-auto-postback-with-cascadingdropdown-vb"></a>通过 CascadingDropDown (VB) 使用自动回发
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件自动回发功能不起作用，因为以异步方式将数据加载到列表生成本身 （不必要） 回发。 使用一些 JavaScript 代码，可以避免这种效果。


## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 （例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件自动回发功能不起作用，因为以异步方式将数据加载到列表生成本身 （不必要） 回发。 使用一些 JavaScript 代码，可以避免这种效果。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (之内&lt; `form` &gt;元素):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

然后，DropDownList 控件是必需的：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

对于此列表中，添加 CascadingDropDown 扩展程序以提供 web 服务 URL 和方法的信息：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

然后 CascadingDropDown 扩展程序以异步方式调用 web 服务使用以下方法签名：

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

该方法返回类型 CascadingDropDown 值的数组。 类型的构造函数要求第一次列表项的标题和值 (HTML`value`属性)。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

加载页面在浏览器中的将填充下拉列表中的与三个供应商，第二个被预先选定状态。 此外，ASP.NET 定义`__doPostBack()`JavaScript 方法。 页面加载后，此 JavaScript 调用添加到下拉列表中，但仅是否有元素中。 如果在列表中没有元素，控件工具包当前是否正在加载，因此 JavaScript 代码使用超时，并尝试再次在半秒。

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

这样一来，在列表中存在实际元素，并且用户选择一个条目时，回发才执行。


[![选择一个列表元素导致回发](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

选择一个列表元素导致回发 ([单击此项可查看原尺寸图像](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](presetting-list-entries-with-cascadingdropdown-vb.md)
