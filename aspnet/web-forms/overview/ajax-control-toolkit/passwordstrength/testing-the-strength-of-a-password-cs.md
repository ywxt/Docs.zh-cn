---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 测试强度的密码 (C#) |Microsoft Docs
author: wenz
description: 密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。 在 ASP 中 PasswordStrength 控件。N...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: 2eec810a0e37347059d3e82a37b25d5663eab987
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839799"
---
<a name="testing-the-strength-of-a-password-c"></a>测试强度的密码 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> 密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。 ASP.NET AJAX 控件工具包中的 PasswordStrength 控件可以检查得再好密码。


## <a name="overview"></a>概述

密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。 `PasswordStrength` ASP.NET AJAX 控件工具包中的控件可以检查得再好密码的信息。

## <a name="steps"></a>步骤

`PasswordStrength`控件扩展的文本框中，并检查是否已经足够好中它的密码。 它提供了丰富的属性，则通过选项以下是只是其中一些：

- `MinimumNumericCharacters` 密码中所需的数字字符的最小数量
- `MinimumSymbolCharacters` 密码中所需的最小数量的符号字符 （不字母和数字）
- `PreferredPasswordLength` 最小密码长度
- `RequiresUpperAndLowerCaseCharacters` 是否需使用大写和小写字符的密码

`StrengthIndicatorType`提供的信息如何显示为文本的密码的强度 (值`"Text"`) 或作为一种类型的进度栏 (值`"BarIndicator"`)。 在`DisplayPosition`属性中，你将配置信息的显示位置。 下面是完整的示例，包括 ASP.NET AJAX`ScriptManager`控件，`PasswordStrength`控件和当然一个文本框，用户可能会在其中输入密码。 为了演示目的后, 一种形式字段是普通文本字段并不是密码字段，以便您可以看到在开发过程中您键入的内容。

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

运行该页并立即键入： 仅输入小写字母、 大写字母、 数字和符号后，密码被视为为不可换行。


[![现在，密码是 （很） 高](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

现在，密码是 （非常） 很好 ([单击此项可查看原尺寸图像](testing-the-strength-of-a-password-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一篇](testing-the-strength-of-a-password-vb.md)
