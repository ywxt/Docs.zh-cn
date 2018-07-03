---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 外部测试机器人 (C#) |Microsoft Docs
author: wenz
description: 自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。 在 ASP.NET AJAX Con NoBot 控件...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 41e8fda5138e4a94e7b8c4af0a5c2bd68e50e9e1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402715"
---
<a name="fighting-bots-c"></a>外部测试机器人 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。 ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。


## <a name="overview"></a>概述

自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。 ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。

## <a name="steps"></a>步骤

以击败智能机器人的一个常用方法是使用 CAPTCHAs 完全自动化的公共 Turing 测试来告诉计算机和人类相隔。 Turing 测试最初是一个测试，有人需要确定通信合作伙伴用户，也可以在计算机的位置。 在 web 中，验证码通常由一些失真字母都在其上的图像组成。 其思路是只有用户可以读取该图像，字母而 OCR 算法将会失败。

有几个优点和缺点，这种方法，但本主题的讨论不在本教程的范围。 但是没有 ASP.NET AJAX 控件工具包提供了类似的方法中的控件： `NoBot`。 它更容易克服比验证码，但非常易于使用和支付特别适合在其中它被视为成功完成，如果大多数垃圾邮件尝试博客等网站上的费用会大大降低，这`NoBot`控件可以执行操作。

`NoBot` 如果满足这些条件中至少一个则，截获当前 ASP.NET web 窗体的回发：

- 浏览器无法解决 JavaScript 难题 （例如当 JavaScript 停用）
- 用户提交窗体进行快速
- 客户端 IP 地址通常在一段时间中提交了表单。

若要检查这些条件，`NoBot`控件需要这些属性 （全部可选的）：

- `ResponseMinimumDelaySeconds` 最少的回发之间的秒数
- `CutoffWindowSeconds` 在其中一个 IP 发是度量值的时间间隔的时间长度
- `CutoffMaximumInstances` 每个时间间隔的秒的最大数量

以下标记要求至少两秒回发和之间，有超过五次回发或小于 30 秒间隔内：

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

然后照常请确保包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

因为大多数检查`NoBot`正在执行的操作发生在服务器端，您需要检查这些验证结果。 这可以通过调用`NoBot`的`IsValid()`方法。 它有一个参数 (作为`out`参数 /`ByRef`参数) 它属于类型`NoBotState`。 如果检查失败，其字符串表示形式包含的原因和`Valid`否则为。 以下代码将输出一条消息，根据`NoBot`的结果：

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

最后，你需要表单以提交和一个标签元素将其输出消息，并完成 ！

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

运行此脚本和停用 JavaScript 或在前两秒内提交窗体或在 30 秒内七次提交窗体时, 将收到一条错误消息。 但是恰当地使用此控件，因为只有大约 90 95%的用户可以使用 JavaScript 激活，因此 5-10%的用户将会失败`NoBot`的测试。


[![此错误消息可能被引起的智能机器人应用程序](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

此错误消息可能已由智能机器人应用程序 ([单击此项可查看原尺寸图像](fighting-bots-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一篇](fighting-bots-vb.md)
