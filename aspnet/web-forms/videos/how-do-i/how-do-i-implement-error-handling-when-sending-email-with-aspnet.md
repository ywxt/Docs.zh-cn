---
uid: web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
title: '[如何实现:]使用 ASP.NET 发送电子邮件时实现错误处理 |Microsoft Docs'
author: rick-anderson
description: Chris Pels 演示如何实现 ASP.NET 电子邮件时的错误处理。 他创建 ASP.NET 网页发送电子邮件，显示了如何配置和 lt....
ms.author: aspnetcontent
ms.date: 11/06/2008
ms.assetid: c02ffd50-aa19-4cdc-b1bf-760989979a61
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
msc.type: video
ms.openlocfilehash: ebe6f451cad2ba4a9311b5882337b637de7f381e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814722"
---
<a name="how-do-i-implement-error-handling-when-sending-email-with-aspnet"></a><span data-ttu-id="6fe3c-104">[如何实现:]使用 ASP.NET 发送电子邮件时实现错误处理</span><span class="sxs-lookup"><span data-stu-id="6fe3c-104">[How Do I:] Implement Error Handling when Sending Email with ASP.NET</span></span>
====================
<span data-ttu-id="6fe3c-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="6fe3c-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="6fe3c-106">Chris Pels 演示如何实现 ASP.NET 电子邮件时的错误处理。</span><span class="sxs-lookup"><span data-stu-id="6fe3c-106">Chris Pels shows how to implement error handling when sending an email with ASP.NET.</span></span> <span data-ttu-id="6fe3c-107">他创建 ASP.NET 网页发送电子邮件，说明了如何配置&lt;mailSettings&gt;在 web.config 文件中，介绍了 System.Net.Mail 类以及如何它用于创建和发送电子邮件消息。</span><span class="sxs-lookup"><span data-stu-id="6fe3c-107">He creates an ASP.NET web page to send email, shows how to configure &lt;mailSettings&gt; in the web.config file, describes the System.Net.Mail class and how it's used to create and send email messages.</span></span> <span data-ttu-id="6fe3c-108">然后，他添加使用 System.Net.Mail 异常类，它们提供有关时发送电子邮件，可能发生的错误的信息和评审 SmtpStatusCode 枚举，它提供了一系列可能的结果发送的电子邮件时的错误处理SmtpClient。</span><span class="sxs-lookup"><span data-stu-id="6fe3c-108">He then adds error handling using System.Net.Mail exception classes, which provide information about errors that can occur when sending email, and reviews the SmtpStatusCode enumeration, which provides a list of possible outcomes when sending an email with the SmtpClient.</span></span> <span data-ttu-id="6fe3c-109">最后，他将发送测试电子邮件的引发异常，并检查错误处理 Visual Studio 调试器中的信息。</span><span class="sxs-lookup"><span data-stu-id="6fe3c-109">Finally, he sends a test email that raises an exception and reviews the error handling information in the Visual Studio debugger.</span></span>

[<span data-ttu-id="6fe3c-110">&#9654;观看视频 （24 分钟）</span><span class="sxs-lookup"><span data-stu-id="6fe3c-110">&#9654; Watch video (24 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-error-handling-when-sending-email-with-aspnet)
