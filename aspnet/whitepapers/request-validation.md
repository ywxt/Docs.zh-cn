---
uid: whitepapers/request-validation
title: 请求验证-阻止脚本攻击 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了请求验证功能的位置，默认情况下，应用程序无法处理未编码的 HTML 内容 submitt ASP.NET...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 0dfbfcae70792c57d530fc5e6fb73f8f96ec6e02
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809740"
---
<a name="request-validation---preventing-script-attacks"></a>请求验证-阻止脚本攻击
====================
> 本白皮书介绍其中，默认情况下，应用程序会阻止处理提交到服务器的未编码的 HTML 内容的 ASP.NET 请求验证功能。 当应用程序已被设计来安全地处理 HTML 数据时，可以禁用此请求验证功能。
> 
> 适用于 ASP.NET 1.1 和 ASP.NET 2.0。


请求验证的 ASP.NET 版本 1.1，一项功能可阻止服务器接受内容包含未编码 HTML。 此功能旨在帮助阻止某些脚本注入攻击，客户端脚本代码或 HTML 可以不知情的情况下提交到服务器、 存储，并随后呈现给其他用户。 我们仍强烈建议验证所有输入的数据和 HTML 对其在适当的时候进行编码。

例如，您创建一个网页，请求用户的电子邮件地址，然后选择电子邮件地址在数据库中的存储。 如果用户输入&lt;脚本&gt;警报 （"你好从脚本"）&lt;/script&gt;而不是一个有效的电子邮件地址，当提供该数据时，此脚本可执行如果内容未正确编码。 ASP.NET 请求验证功能可以避免这种情况发生。

## <a name="why-this-feature-is-useful"></a>为什么此功能很有用

许多站点并不知道它们是打开到简单的脚本注入攻击。 这些攻击的目的是通过显示 HTML，破坏站点还是用于可能执行客户端脚本以将用户重定向到黑客的站点，脚本注入攻击是 Web 开发人员必须应对的问题。

脚本注入攻击是需考虑的所有 web 开发人员，无论他们使用的 ASP.NET、 ASP 或其他 web 开发技术。

ASP.NET 请求验证功能主动防止这些攻击通过不允许未编码的 HTML 内容，除非开发人员决定以允许该内容由服务器进行处理。

## <a name="what-to-expect-error-page"></a>出现的情况: 错误页

下面的屏幕快照显示了一些示例 ASP.NET 代码：

![](request-validation/_static/image1.png)

运行此代码会生成一个简单的页面，您可以在文本框中输入一些文本中，单击按钮，并在标签控件中显示文本：

![](request-validation/_static/image2.png)

但是，如是 JavaScript，`<script>alert("hello!")</script>`输入并提交，则会得到了异常：

![](request-validation/_static/image3.png)

错误消息指出潜在的危险 Request.Form 的检测到值，并提供更多详细信息中并完全发生了什么以及如何更改行为的说明。 例如：

请求验证程序检测到潜在危险的客户端的输入的值，并在请求处理已中止。 此值可能表明攻击者尝试破坏应用程序，如跨站点脚本攻击的安全。 可以通过设置禁用请求验证`validateRequest=false`Page 指令中或在配置部分中。 但是，强烈建议，你的应用程序显式检查所有输入在这种情况下。

## <a name="disabling-request-validation-on-a-page"></a>禁用页面上的请求验证

若要禁用请求验证，必须设置的页面上`validateRequest`到 Page 指令属性`false`:

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 禁用请求验证后，可将内容提交到页;它是页面开发人员，以确保该内容的责任是正确编码或处理。

## <a name="disabling-request-validation-for-your-application"></a>禁用你的应用程序的请求验证

若要为应用程序禁用请求验证，必须修改或为应用程序创建 Web.config 文件并将设置的 validateRequest 特性`<pages />`部分`false`:

[!code-xml[Main](request-validation/samples/sample2.xml)]

如果你想要禁用请求验证的服务器上的所有应用程序，您可以执行此项修改 Machine.config 文件。

> [!CAUTION]
> 禁用请求验证后，可将内容提交到你的应用程序;它是应用程序开发人员，以确保该内容的责任是正确编码或处理。

下面的代码修改以关闭请求验证：

![](request-validation/_static/image4.png)

现在，如果以下 JavaScript 已输入到 textbox`<script>alert("hello!")</script>`结果将是：

![](request-validation/_static/image5.png)

若要防止这种情况发生，与处于关闭状态的请求验证，我们需要为 HTML 编码内容。

## <a name="how-to-html-encode-content"></a>如何为 HTML 编码内容

如果禁用了请求验证，所以最好对 HTML 编码的内容将存储以供将来使用。 HTML 编码将自动替换任何 '&lt;或&gt;（以及其他多个符号） 与相应的 HTML 编码表示形式。 例如，'&lt;替换为&amp;l t; 和&gt;将替换为&amp;g t;。 浏览器使用这些特殊的代码以显示&lt;或&gt;在浏览器中。

内容可以轻松地在服务器使用的编码 HTML `Server.HtmlEncode(string)` API。 内容也可以很容易 HTML 解码，也就是说，就会返回到标准 HTML 使用`Server.HtmlDecode(string)`方法。

![](request-validation/_static/image6.png)

生成中：

![](request-validation/_static/image7.png)
