---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[如何实现:]在包含 ASP.NET 的电子邮件中嵌入图像 |Microsoft Docs'
author: rick-anderson
description: Chris Pels 显示了如何使用 ASP.NET 在电子邮件中嵌入图像。 他创建 web 窗体 （带有字段的收件人、 发件人、 主题和正文），然后使用 AlternateView...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: d046c988c060580b856fb65c90521c3a2815e760
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824214"
---
<a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a><span data-ttu-id="50f24-104">[如何实现:]在包含 ASP.NET 的电子邮件中嵌入图像</span><span class="sxs-lookup"><span data-stu-id="50f24-104">[How Do I:] Embed an Image in an Email with ASP.NET</span></span>
====================
<span data-ttu-id="50f24-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="50f24-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="50f24-106">Chris Pels 显示了如何使用 ASP.NET 在电子邮件中嵌入图像。</span><span class="sxs-lookup"><span data-stu-id="50f24-106">Chris Pels shows how to embed an image in an email with ASP.NET.</span></span> <span data-ttu-id="50f24-107">他创建 web 窗体 （带有字段的收件人、 发件人、 主题和正文）、 AlternateView 类用于创建文本和 HTML 版本的一封电子邮件、 的 LinkedResource 类实例中存储图像，HTML AlternateView 将其嵌入。</span><span class="sxs-lookup"><span data-stu-id="50f24-107">He creates a web form (with fields for To, From, Subject, and Body), uses the AlternateView class to create text and HTML versions of an email, stores an image in a LinkedResource class instance, embeds it in the HTML AlternateView.</span></span> <span data-ttu-id="50f24-108">然后，他将这两个版本添加到 MailMessage 对象并将电子邮件发送两次，第一种使用 HTML 接收功能启用，然后作为纯文本。</span><span class="sxs-lookup"><span data-stu-id="50f24-108">He then adds both versions to the MailMessage object and sends the email twice, first with HTML-receiving capabilities enabled and then as text-only.</span></span> <span data-ttu-id="50f24-109">在 Outlook 中会显示这两个电子邮件消息。</span><span class="sxs-lookup"><span data-stu-id="50f24-109">Both email messages appear in Outlook.</span></span> <span data-ttu-id="50f24-110">该 HTML 版本显示嵌入的图像;文本版本却没有。</span><span class="sxs-lookup"><span data-stu-id="50f24-110">The HTML version shows the embedded image; the text version does not.</span></span>

[<span data-ttu-id="50f24-111">&#9654;观看视频 （19 分钟）</span><span class="sxs-lookup"><span data-stu-id="50f24-111">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)
