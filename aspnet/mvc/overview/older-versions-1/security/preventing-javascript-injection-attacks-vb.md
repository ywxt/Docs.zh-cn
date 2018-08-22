---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: 阻止 JavaScript 注入攻击 (VB) |Microsoft Docs
author: StephenWalther
description: 阻止 JavaScript 注入攻击和跨站点脚本攻击发生给你。 在本教程中，Stephen Walther 解释了如何轻松地 de...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: c46b6e1ca13228feb764d9c660ad578576956970
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824462"
---
<a name="preventing-javascript-injection-attacks-vb"></a>阻止 JavaScript 注入攻击 (VB)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

[下载 PDF](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> 阻止 JavaScript 注入攻击和跨站点脚本攻击发生给你。 在本教程中，Stephen Walther 解释了如何轻松地抵御这些类型的 html 编码内容的攻击。


本教程的目的是说明如何在 ASP.NET MVC 应用程序中防止 JavaScript 注入攻击。 本教程讨论了两种方法可以保护你的网站对 JavaScript 注入攻击。 了解如何防止 JavaScript 注入攻击进行编码，显示的数据。 你还了解如何进行编码的数据，即表示你接受阻止 JavaScript 注入攻击。

## <a name="what-is-a-javascript-injection-attack"></a>什么是 JavaScript 注入攻击？

无论何时接受用户输入并重新显示用户输入，打开你的网站到 JavaScript 注入攻击。 让我们看一个具体的应用程序打开到 JavaScript 注入攻击的。

设想您创建了客户反馈网站 （参见图 1）。 客户可以访问的网站，并输入他们使用您的产品的体验反馈。 当客户提交其反馈时，反馈将重新显示反馈页面上。


[![客户反馈网站](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**图 01**： 客户反馈网站 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image3.png))


客户反馈网站使用`controller`列表 1 中。 这`controller`包含名为两个操作`Index()`和`Create()`。

**代码清单 1 – `HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

`Index()`方法将显示`Index`视图。 此方法将传递到以前的客户反馈的所有`Index`通过 （使用 LINQ to SQL 查询） 从数据库检索反馈的视图。

`Create()`方法创建新的反馈项并将其添加到数据库。 在窗体中输入客户的消息传递给`Create()`消息参数中的方法。 创建了一个反馈项并将消息分配给反馈项目`Message`属性。 反馈项目提交到与数据库`DataContext.SubmitChanges()`方法调用。 最后，访问者被重定向回`Index`视图的所有反馈的显示位置。

`Index`视图包含在代码清单 2。

**代码清单 2 – `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

`Index`视图具有两个部分。 顶端部分包含实际的客户反馈窗体。 下半部分包含一个 For...每个循环，循环遍历所有以前的客户反馈项并显示每个反馈项目的 EntryDate 和消息属性。

客户反馈网站是一个简单的网站。 遗憾的是，该网站已打开到 JavaScript 注入攻击。

假设在客户的反馈表单中输入以下文本：

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

此文本表示显示警告消息框的 JavaScript 脚本。 有人将此脚本提交到反馈后窗体中，消息<em>Boo ！</em>将显示时的任何人访问客户反馈网站将来 （请参见图 2）。


[![JavaScript 注入](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**图 02**: JavaScript 注入 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image6.png))


现在，对 JavaScript 注入攻击的初始响应可能才自傲。 您可能认为 JavaScript 注入攻击是只是一种*篡改*攻击。 你可能会认为，没有人可以任何操作真正邪恶通过提交 JavaScript 注入攻击。

遗憾的是，黑客可以执行一些真正，通过将 JavaScript 注入到网站的真正恶意操作。 JavaScript 注入攻击可用于执行跨站点脚本 (XSS) 攻击。 在跨站点脚本攻击中，您可以窃取用户机密信息并将信息发送到另一个网站。

例如，黑客可以使用 JavaScript 注入攻击来窃取其他用户的浏览器 cookie 的值。 如果在浏览器 cookie 中存储敏感信息，如密码、 信用卡号或社会安全号码 –，然后黑客可以使用 JavaScript 注入攻击来窃取此信息。 或者，如果用户在使用 JavaScript 攻击已遭到破坏的页中包含的窗体字段中输入的敏感信息，然后黑客可以使用注入的 JavaScript 来获取窗体数据并将其发送到另一个网站。

*请将被困难所吓倒*。 JavaScript 注入攻击非常重视和保护用户的机密信息。 在接下来的两部分中，我们将讨论您可以使用来保护 ASP.NET MVC 应用程序从 JavaScript 注入攻击的两种方法。

## <a name="approach-1-html-encode-in-the-view"></a>方法 #1： 在视图中 HTML 编码

一个阻止 JavaScript 注入攻击的简单方法是以 html 格式进行编码时重新显示在视图中的数据由网站的用户输入的任何数据。 已更新`Index`清单 3 中的视图遵循这种方法。

**代码清单 3 – `Index.aspx` (HTML 编码)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

请注意，值`feedback.Message`是 HTML 编码之前使用以下代码显示的值：

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

它以 html 格式的平均值对字符串进行编码？ HTML 编码字符串，危险字符如`<`并`>`替换为 HTML 实体引用，如`&lt;`和`&gt;`。 因此，在将字符串`<script>alert("Boo!")</script>`是 HTML 编码，它将转换为`&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。 作为 JavaScript 脚本时由浏览器进行解释，不再执行编码的字符串。 相反，图 3 中获得无害的页。


[![大大降低的 JavaScript 攻击](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**图 03**： 大大降低 JavaScript 攻击 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image9.png))


请注意，在`Index`查看清单 3 中的值`feedback.Message`进行编码。 值`feedback.EntryDate`不进行编码。 只需对用户输入的数据进行编码。 因为 EntryDate 的值在控制器中生成时，你不需要为 HTML 编码此值。

## <a name="approach-2-html-encode-in-the-controller"></a>方法 2： 在控制器中编码的 HTML

而不是 HTML 编码的数据在视图中显示数据时，你可以 HTML 提交到数据库的数据之前对数据进行编码。 此第二种方法执行的情况下`controller`列表 4 中。

**列表 4 – `HomeController.cs` (HTML 编码)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

请注意，消息的值是 HTML 编码，然后将值提交到该数据库在`Create()`操作。 当消息将重新显示在视图中时，消息是 HTML 编码，并且不执行消息中注入任何 JavaScript。

通常情况下，你应更倾向于通过此第二种方法在本教程中讨论的第一个方法。 此第二种方法的问题是，您最终得到的 HTML 编码的数据在数据库中。 换而言之，你数据库的数据是变脏的有趣的外观字符。

为什么这是错误的？ 如果您需要在 web 页面以外的内容中显示数据库数据，您将遇到问题。 例如，可以在 Windows 窗体应用程序中无法轻而易举地显示数据。

## <a name="summary"></a>总结

本教程的目的是被吓有关 JavaScript 注入攻击的潜在客户。 本教程中讨论过防御针对 JavaScript 注入攻击您的 ASP.NET MVC 应用程序的两种方法： 可以是 HTML 编码用户提交中的视图或你的数据可以 HTML 编码用户提交的控制器中的数据。

> [!div class="step-by-step"]
> [上一篇](authenticating-users-with-windows-authentication-vb.md)
