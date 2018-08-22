---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: 动态填充控件使用 JavaScript 代码 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到 t 上的目标控件...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d1c3b59896b8c509e9c62738ccd1b37c250a840
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825052"
---
<a name="dynamically-populating-a-control-using-javascript-code-vb"></a>动态填充控件使用 JavaScript 代码 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。 还有可能触发使用自定义客户端的 JavaScript 代码的填充。


## <a name="overview"></a>概述

`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。 还有可能触发使用自定义客户端的 JavaScript 代码的填充。

## <a name="steps"></a>步骤

首先，需要 ASP.NET Web 服务实现的方法调用的`DynamicPopulateExtender`控件。 Web 服务实现方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。 下面是代码 (文件`DynamicPopulate.vb.asmx`) 中检索当前日期中三种格式之一：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

在下一步中，创建一个新的 ASP.NET 站点并开始使用 ASP.NET AJAX ScriptManager 控件：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

然后，添加一个 label 控件 (例如使用具有相同名称的 HTML 控件或`<asp:Label />`web 控件) 的更高版本将显示 web 服务调用的结果。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

接下来，包括`DynamicPopulateExtender`控制并提供 web 服务信息、 目标控件，但不是这会触发这会在更高版本使用自定义 JavaScript 填充该控件的名称 ！

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

现在我们来的 JavaScript 部分。 `$find()`由 ASP.NET AJAX 库定义的函数返回对 ASP.NET AJAX 控件工具包的服务器端对象的引用如`DynamicPopulateExtender`。 在当前文件中，`$find("dpe")`返回到一个引用`DynamicPopulateExtender`页中的控件。 它公开一个名为方法`populate()`随即将会触发动态填充过程。 `populate()`方法需要一个参数： 参数作为上下文键`getDate()`web 方法。 因此，例如，`$find("dpe").populate("format1")`将填充与月-日-年格式的当前日期的标签。

为了让此示例更具灵活性，用户可能现在多个日期格式之间进行选择。 对于其中每项显示的单选按钮。 一次用户单击单选按钮，JavaScript 代码动态填充与所选的日期格式的标签。 下面是这些单选按钮：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

请注意，单选按钮，JavaScript 表达式的上下文中`this.value`当前按钮，它恰巧是完全相同的信息的值是指`getDate()`方法可以使用。


[![单击的按钮中指定的格式的服务器中检索日期](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

单击的按钮中指定的格式的服务器中检索日期 ([单击此项可查看原尺寸图像](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](dynamically-populating-a-control-vb.md)
> [下一页](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
