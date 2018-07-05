---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: 通过用户控件和 JavaScript (C#) 使用 DynamicPopulate |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到 t 上的目标控件...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: cba1647e69cbaebf0accb745278590e357d8c2c1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370414"
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a>通过用户控件和 JavaScript (C#) 使用 DynamicPopulate
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)

> ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。 还有可能触发使用自定义客户端的 JavaScript 代码的填充。 但是特别留意具有扩展器驻留在用户控件时要执行。


## <a name="overview"></a>概述

`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。 还有可能触发使用自定义客户端的 JavaScript 代码的填充。 但是特别留意具有扩展器驻留在用户控件时要执行。

## <a name="steps"></a>步骤

首先，需要 ASP.NET Web 服务实现的方法调用的`DynamicPopulateExtender`控件。 Web 服务实现方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。 下面是代码 (文件`DynamicPopulate.cs.asmx`) 中检索当前日期中三种格式之一：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

在下一步中创建新的用户控件 (`.ascx`文件)，表示由其第一行中的以下声明：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

一个&lt; `label` &gt;元素将用于显示来自服务器的数据。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

此外在用户控件文件中，我们将使用三个单选按钮，每个表示一个 web 服务支持的三个可能的日期格式。 当用户单击一个单选按钮上时，浏览器将执行 JavaScript 代码如下所示：

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

此代码访问`DynamicPopulateExtender`（不用再担心如何奇怪 ID 尚不，这将稍后介绍），并触发数据动态填充。 中的当前单选按钮，上下文`this.value`其值即是指`format1`，`format2`或`format3`完全什么 web 方法的要求。

唯一尚未缺少用户控件中是`DynamicPopulateExtender`可链接到 web 服务的单选按钮控件。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

再一次可能会注意该控件中使用的奇怪 ID:`mcd1$myDate`而不是`myDate`。 以前，使用的 JavaScript 代码`mcd1_dpe1`访问`DynamicPopulateExtender`而不是`dpe1`。此命名策略是一个特殊的要求时使用`DynamicPopulateExtender`用户控件内。 此外，您必须将用户控件嵌入特定的方式，以使其工作。 创建一个新的 ASP.NET 页面并注册你只需实现的用户控件标记前缀：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

然后，包括 ASP.NET AJAX`ScriptManager`新页上的控件：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

最后，将用户控件添加到页面。 只需设置其`ID`属性 (和`runat="server"`，当然)，但您还必须将其设置为一个特定的名称：`mcd1`由于这是用户控件内用于使用 JavaScript 访问它的前缀。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

就是这么简单！ 页面行为是否符合预期： 用户单击其中一个单选按钮，该工具包中的控件调用 web 服务，并以所需的格式显示当前日期。


[![单选按钮位于用户控件](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)

单选按钮位于用户控件 ([单击此项可查看原尺寸图像](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](dynamically-populating-a-control-using-javascript-code-cs.md)
> [下一页](dynamically-populating-a-control-vb.md)
