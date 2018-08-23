---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 发送电子邮件从 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本章介绍如何从网站发送自动的电子邮件。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 4429b9df0a6bc689eb3549c13aee598353c438af
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832505"
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>从 ASP.NET Web Pages (Razor) 站点发送电子邮件
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 此文章介绍了如何使用 ASP.NET Web Pages (Razor) 时，从网站发送电子邮件。
> 
> 你将学习：
> 
> - 如何从你的网站发送一封电子邮件。
> - 如何将文件附加到电子邮件。
> 
> 这是引入一文中的 ASP.NET 功能：
> 
> - `WebMail`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>从你的网站发送电子邮件

有各种类型的原因，用户可能需要从你的网站发送电子邮件。 可能会将确认消息发送到用户，或你可能会向自己发送通知 （例如情况下，新的用户已注册的。）`WebMail`帮助程序可以轻松为你发送电子邮件。

若要使用`WebMail`帮助器，您必须有权访问 SMTP 服务器。 (代表 SMTP*简单邮件传输协议*。)SMTP 服务器是只将消息转发到收件人的服务器的电子邮件服务器&#8212;它是电子邮件的出站端。 如果为你的网站使用宿主提供程序，它们可能将你设置电子邮件和他们可以告诉您 SMTP 服务器名称是什么。 如果使用的企业网络内部，管理员或 IT 部门可以通常向您提供有关可以使用的 SMTP 服务器的信息。 如果在在家工作，甚至可能能够测试使用普通的电子邮件提供程序，可以告诉您他们 SMTP 服务器的名称。 您通常需要：

- SMTP 服务器的名称。
- 端口号。 这几乎总是为 25。 但是，您的 ISP 可能需要使用端口 587。 如果使用安全套接字层 (SSL) 的电子邮件，可能需要不同的端口。 请与你的电子邮件提供商。
- 凭据 （用户名、 密码）。

在此过程中，将创建两个页面。 第一页具有允许用户输入说明，就像它们在技术支持窗体中填满一个窗体。 第一页提交到第二页其信息。 在第二个页中，代码中提取用户的信息并发送一封电子邮件。 它还显示一条消息，确认已收到问题报告。

![[image]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 为了简化此示例中，代码将初始化`WebMail`帮助器直接在页，使用它。 但是，对于真实网站，很好地了解此类的初始化代码放在全局文件中，以便您初始化`WebMail`你的网站中的所有文件的帮助器。 有关详细信息，请参阅[自定义网站的行为为 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。


1. 创建新的网站。
2. 添加一个名为的新页*EmailRequest.cshtml*并添加以下标记： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    请注意，`action`窗体元素的属性已设置为*ProcessRequest.cshtml*。 这意味着窗体，将提交到该页面而不是在当前页面。
3. 添加一个名为的新页*ProcessRequest.cshtml*到网站并添加以下代码和标记：   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    在代码中，你将获取已提交到页面的窗体字段的值。 然后，调用`WebMail`帮助者`Send`方法来创建和发送电子邮件。 在这种情况下，要使用的值是组成窗体中已提交的值串联的文本。

    此页的代码位于`try/catch`块。 如果出于任何原因将发送一封电子邮件不起作用 （例如，设置不正确） 中的代码`catch`块在运行，并设置`errorMessage`已发生的错误的变量。 (有关详细信息`try/catch`块或`<text>`标记中，请参阅[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)。)

    页上，在正文中如果`errorMessage`变量为空 （默认值），用户会看到一条消息，已发送电子邮件消息。 如果`errorMessage`变量设置为 true，用户将看到一条消息已发送消息的问题。

    请注意，在显示一条错误消息的页面的部分，没有其他测试： `if(debuggingFlag)`。 这是一个变量，可以设置为 true，如果您遇到问题，发送电子邮件。 当`debuggingFlag`为 true，和如果发送电子邮件问题，一条错误消息显示，显示 ASP.NET 尝试发送电子邮件时已报告任何内容。 公平警告，尽管： 当它不能发送电子邮件时，ASP.NET 报告的错误消息可以是泛型。 例如，如果 ASP.NET 无法联系 SMTP 服务器 （例如，因为在服务器名称中，所做错误），错误为`Failure sending mail`。

    > [!NOTE] 
    > 
    > **重要**当从异常对象中获取一条错误消息 (`ex`代码中)，不要*不*定期将通过该消息传递给用户。 异常对象通常包括，用户应不会看到，这甚至可能存在安全漏洞的信息。 这就是为什么此代码包含在变量`debuggingFlag`，用作为开关来显示错误消息和为什么默认情况下该变量设置为 false。 应设置该变量为 true （并因此显示的错误消息）*仅*如果遇到问题发送电子邮件，并且需要进行调试。 已修复任何问题之后, 设置`debuggingFlag`回 false。

    修改以下电子邮件在代码中的相关的设置：

   - 设置`your-SMTP-host`到有权访问 SMTP 服务器的名称。
   - 设置`your-user-name-here`到 SMTP 服务器帐户的用户名。
   - 设置`your-account-password`为 SMTP 服务器帐户的密码。
   - 设置`your-email-address-here`到电子邮件地址。 这是从发送消息的电子邮件地址。 (某些电子邮件提供程序不会允许您指定其他`From`地址，并且将你的用户名称作为`From`地址。)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>配置电子邮件设置
     > 
     > 它可以是一个挑战，有些是为了确保您具有正确设置的 SMTP 服务器、 端口号，依次类推。 下面是一些提示：
     > 
     > - SMTP 服务器名称通常是类似于`smtp.provider.com`或`smtp.provider.net`。 但是，如果将站点发布到宿主提供程序，将 SMTP 服务器名此时可能`localhost`。 这是因为电子邮件服务器发布和提供程序的服务器上运行你的站点之后，可能在本地从你的应用程序的角度来看。 此服务器名称中的更改可能意味着您必须在发布过程中更改 SMTP 服务器名称。
     > - 端口号通常为 25。 但是，某些提供程序需要使用端口 587 或某些其他端口。
     > - 请确保使用正确的凭据。 如果你已将站点发布到宿主提供程序，使用提供程序专门指示用于电子邮件的凭据。 这些可能是不同于你使用发布的凭据。
     > - 有时您根本不需要凭据。 如果要发送电子邮件使用您个人的 ISP，电子邮件提供商可能已经知道你的凭据。 发布后，你可能需要使用比测试本地计算机上的其他凭据。
     > - 如果你的电子邮件提供商使用加密，则必须设置`WebMail.EnableSsl`到`true`。
4. 运行*EmailRequest.cshtml*页在浏览器中。 (请确保的页中选择**文件**工作区之前运行它。)
5. 输入您的姓名和问题说明，并单击**提交**按钮。 将重定向到*ProcessRequest.cshtml*页上，这可确认您的消息并向你发送一封电子邮件。 

    ![[image]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>发送使用电子邮件的文件

此外可以发送与附加到电子邮件的文件。 在此过程中，创建一个文本文件和两个 HTML 页面。 将文本文件作为电子邮件附件。

1. 在网站中，添加新的文本文件并将其命名*MyFile.txt*。
2. 复制以下文本并将其粘贴在文件中： 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. 创建一个名为页*SendFile.cshtml*并添加以下标记： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. 创建一个名为页*ProcessFile.cshtml*并添加以下标记： 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 修改以下电子邮件中的代码示例中的相关的设置：

    - 设置`your-SMTP-host`到有权访问 SMTP 服务器的名称。
    - 设置`your-user-name-here`到 SMTP 服务器帐户的用户名。
    - 设置`your-email-address-here`到电子邮件地址。 这是从发送消息的电子邮件地址。
    - 设置`your-account-password`为 SMTP 服务器帐户的密码。
    - 设置`target-email-address-here`到电子邮件地址。 （如之前，您通常情况下将发送一封电子邮件给其他人，但对于测试，您可以将其发送给自己。）
6. 运行*SendFile.cshtml*页在浏览器中。
7. 输入您的姓名、 主题行和要附加的文本文件的名称 (*MyFile.txt*)。
8. 单击 `Submit` 按钮。 如前面一样，将重定向到*ProcessFile.cshtml*页上，这可确认您的消息和其向你发送一封电子邮件与附加的文件。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


- [ASP.NET 网页 (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)
- [简单邮件传输协议](https://msdn.microsoft.com/library/aa480435.aspx)
- [为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
