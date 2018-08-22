---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[如何实现:]以异步方式使用 ASP.NET 发送电子邮件 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris Pels 演示如何在 ASP.NET 中使用 System.Net.Mail 类发送异步电子邮件。 首先，请参阅如何配置 web si...
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: fc6d1d9b36eec042d1aec22e0e125e8807460a90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824454"
---
<a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="8ed55-104">[如何实现:]以异步方式使用 ASP.NET 发送电子邮件</span><span class="sxs-lookup"><span data-stu-id="8ed55-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>
====================
<span data-ttu-id="8ed55-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="8ed55-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="8ed55-106">在此视频中，Chris Pels 演示如何在 ASP.NET 中使用 System.Net.Mail 类发送异步电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8ed55-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="8ed55-107">首先，请参阅如何配置网站以使用电子邮件发送&lt;mailSettings&gt; web.config 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="8ed55-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="8ed55-108">接下来，创建简单的用户界面，用于输入电子邮件信息。</span><span class="sxs-lookup"><span data-stu-id="8ed55-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="8ed55-109">然后了解如何创建使用 MailMessage 类在代码隐藏页中创建一封电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8ed55-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="8ed55-110">该过程的一部分创建的事件处理程序遵循的电子邮件发送的异步回调。</span><span class="sxs-lookup"><span data-stu-id="8ed55-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="8ed55-111">在事件处理程序请参阅如何使用可提供有关发送过程的电子邮件信息 AsynchCompletedEventArgs 类的实例。</span><span class="sxs-lookup"><span data-stu-id="8ed55-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="8ed55-112">最后，在调试模式下，执行步骤以异步方式发送测试电子邮件并查看从进程收到的实际电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8ed55-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="8ed55-113">&#9654;观看视频 （18 分钟）</span><span class="sxs-lookup"><span data-stu-id="8ed55-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
