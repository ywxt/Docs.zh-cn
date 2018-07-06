---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: 仅允许特定字符在文本框中 (VB) |Microsoft Docs
author: wenz
description: ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。 但是这仍然不会阻止用户根据键入的无效...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: e53d7282237c94b88c712e53bf607dcb94ccf1f2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830741"
---
<a name="allowing-only-certain-characters-in-a-text-box-vb"></a>仅允许特定字符在文本框中 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。 但是这仍然不会阻止用户键入无效的字符，并尝试提交窗体。


## <a name="overview"></a>概述

ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。 但是这仍然不会阻止用户键入无效的字符，并尝试提交窗体。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含`FilteredTextBox`控件扩展了文本框。 激活后，某些组的字符可能会输入到字段。

为实现此目的，我们首先需要像往常一样 ASP.NET AJAX`ScriptManager`这会加载哪些还由 ASP.NET AJAX 控件工具包的 JavaScript 库：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

然后，我们需要一个文本框：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

最后，`FilteredTextBoxExtender`控件负责限制允许用户键入的字符。 首先，设置`TargetControlID`归于`ID`的`TextBox`控件。 然后，选择一个可用`FilterType`值：

- `Custom` 默认设置;你必须提供一组有效字符为单位
- `LowercaseLetters` 仅小写字母
- `Numbers` 仅为数字
- `UppercaseLetters` 大写的字母

如果`Custom FilterType`使用时，`ValidChars`属性必须设置，并提供可能键入的字符的列表。 顺便提一下： 如果尝试将文本粘贴到文本框中，删除所有无效字符。

下面是针对标记`FilteredTextBoxExtender`仅允许数字的控件 (也是可能具有的某些内容`FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

运行页面，然后重试输入一个字母，如果启用 JavaScript，它不起作用;但是，数字显示在页上。 但是请注意，保护`FilteredTextBox`提供不是高防护： 如果 JavaScript 已启用，因此您必须使用其他验证方法，即 ASP 可能会在文本框中输入任何数据。NET 的验证控件。


[![可能输入仅数字](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

可能输入仅数字 ([单击此项可查看原尺寸图像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](allowing-only-certain-characters-in-a-text-box-cs.md)
