---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 发送电子邮件从 ASP.NET Web 页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本章介绍如何从网站发送自动的电子邮件。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 9be242d238c627a9557fe7ff7e596974e5b7d1c8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="36640-103">从 ASP.NET Web 页 (Razor) 站点发送电子邮件</span><span class="sxs-lookup"><span data-stu-id="36640-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="36640-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="36640-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="36640-105">此文章介绍了如何使用 ASP.NET Web 页 (Razor) 时，从网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="36640-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="36640-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="36640-107">如何从您的网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="36640-108">如何将文件附加到电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="36640-109">这是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="36640-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="36640-110">`WebMail`帮助器。</span><span class="sxs-lookup"><span data-stu-id="36640-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="36640-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="36640-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="36640-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="36640-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="36640-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="36640-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="36640-114">从你的网站发送电子邮件消息</span><span class="sxs-lookup"><span data-stu-id="36640-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="36640-115">有各种原因为什么你可能需要从你的网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="36640-116">可能将确认消息发送给用户，或你可能向自己发送通知 （例如情况下，新的用户已注册。）`WebMail`帮助程序轻松用于发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="36640-117">若要使用`WebMail`帮助器，你必须有权访问 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="36640-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="36640-118">(代表 SMTP*简单邮件传输协议*。)SMTP 服务器是仅将消息转发给接收方的服务器的电子邮件服务器&#8212;它是电子邮件的出站端。</span><span class="sxs-lookup"><span data-stu-id="36640-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="36640-119">如果为你的网站使用托管提供商，它们可能你使用设置电子邮件，它们可以告诉你你 SMTP 服务器名称是什么。</span><span class="sxs-lookup"><span data-stu-id="36640-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="36640-120">如果你正在公司网络内部，管理员或 IT 部门可通常提供有关你可以使用的 SMTP 服务器的信息。</span><span class="sxs-lookup"><span data-stu-id="36640-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="36640-121">如果你在在家工作，即使可能能够使用你普通的电子邮件提供商联系，可以告诉他们 SMTP 服务器的名称进行测试。</span><span class="sxs-lookup"><span data-stu-id="36640-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="36640-122">你通常需要：</span><span class="sxs-lookup"><span data-stu-id="36640-122">You typically need:</span></span>

- <span data-ttu-id="36640-123">SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="36640-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="36640-124">端口号。</span><span class="sxs-lookup"><span data-stu-id="36640-124">The port number.</span></span> <span data-ttu-id="36640-125">这几乎始终为 25。</span><span class="sxs-lookup"><span data-stu-id="36640-125">This is almost always 25.</span></span> <span data-ttu-id="36640-126">但是，你的 ISP 可能要求你为使用端口 587。</span><span class="sxs-lookup"><span data-stu-id="36640-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="36640-127">如果将安全套接字层 (SSL) 用于电子邮件，你可能需要不同的端口。</span><span class="sxs-lookup"><span data-stu-id="36640-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="36640-128">咨询你的电子邮件提供商。</span><span class="sxs-lookup"><span data-stu-id="36640-128">Check with your email provider.</span></span>
- <span data-ttu-id="36640-129">凭据 （用户名、 密码）。</span><span class="sxs-lookup"><span data-stu-id="36640-129">Credentials (user name, password).</span></span>

<span data-ttu-id="36640-130">在此过程中，你将创建两个页。</span><span class="sxs-lookup"><span data-stu-id="36640-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="36640-131">第一页具有一个窗体，可让用户输入的描述，就像它们已填写技术支持窗体。</span><span class="sxs-lookup"><span data-stu-id="36640-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="36640-132">第一页提交到第二页其信息。</span><span class="sxs-lookup"><span data-stu-id="36640-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="36640-133">在第二个页中，代码中提取用户的信息，并发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="36640-134">它还显示确认已接收的问题报告的消息。</span><span class="sxs-lookup"><span data-stu-id="36640-134">It also displays a message confirming that the problem report has been received.</span></span>

![[image]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="36640-136">为了简化本示例，此代码初始化`WebMail`帮助器直接在其中使用的页。</span><span class="sxs-lookup"><span data-stu-id="36640-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="36640-137">但是，对于实际网站，很好地了解如下的初始化代码放在全局文件中，以便你初始化`WebMail`中你的网站的所有文件的帮助器。</span><span class="sxs-lookup"><span data-stu-id="36640-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="36640-138">有关详细信息，请参阅[自定义站点范围的行为的 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。</span><span class="sxs-lookup"><span data-stu-id="36640-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>


1. <span data-ttu-id="36640-139">创建新网站。</span><span class="sxs-lookup"><span data-stu-id="36640-139">Create a new website.</span></span>
2. <span data-ttu-id="36640-140">添加一个名为的新页*EmailRequest.cshtml*并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="36640-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="36640-141">请注意， `action` form 元素的属性已设置为*ProcessRequest.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="36640-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="36640-142">这意味着窗体，将提交到该页面而不是返回当前页。</span><span class="sxs-lookup"><span data-stu-id="36640-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="36640-143">添加一个名为的新页*ProcessRequest.cshtml*到网站并添加下面的代码和标记：</span><span class="sxs-lookup"><span data-stu-id="36640-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="36640-144">在代码中，你将获取已提交到该页的窗体字段的值。</span><span class="sxs-lookup"><span data-stu-id="36640-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="36640-145">然后，你调用`WebMail`帮助器的`Send`方法创建并发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="36640-146">在这种情况下，要使用的值组成的串联从窗体提交的值的文本。</span><span class="sxs-lookup"><span data-stu-id="36640-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="36640-147">此页的代码位于`try/catch`块。</span><span class="sxs-lookup"><span data-stu-id="36640-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="36640-148">如果出于任何原因将发送一封电子邮件不起作用 （例如，设置不正确） 中的代码`catch`块运行并设置`errorMessage`变量已发生的错误。</span><span class="sxs-lookup"><span data-stu-id="36640-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="36640-149">(有关详细信息`try/catch`块或`<text>`标记中，请参阅[ASP.NET 网页编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)。)</span><span class="sxs-lookup"><span data-stu-id="36640-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="36640-150">在正文中页上，如果`errorMessage`变量为空 （默认值），则用户将看到一条消息，发送电子邮件消息。</span><span class="sxs-lookup"><span data-stu-id="36640-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="36640-151">如果`errorMessage`变量设置为 true，用户所见一条消息已发送消息的问题。</span><span class="sxs-lookup"><span data-stu-id="36640-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="36640-152">请注意，在显示一条错误消息的页的部分，没有其他的测试： `if(debuggingFlag)`。</span><span class="sxs-lookup"><span data-stu-id="36640-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="36640-153">这是一个变量，可以设置为 true，如果你无法发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="36640-154">当`debuggingFlag`为 true，并且如果发送电子邮件问题，一条错误消息将显示表明 ASP.NET 尝试发送电子邮件时已报告任何内容。</span><span class="sxs-lookup"><span data-stu-id="36640-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="36640-155">公平警告，但： 它不能发送电子邮件时，ASP.NET 将报告错误消息可以是泛型。</span><span class="sxs-lookup"><span data-stu-id="36640-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="36640-156">例如，如果 ASP.NET 无法联系 SMTP 服务器 （例如，因为你的服务器名称中所做错误），错误为`Failure sending mail`。</span><span class="sxs-lookup"><span data-stu-id="36640-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="36640-157">**重要**当从异常对象中获取一条错误消息 (`ex`在代码中)，请执行*不*定期将该消息通过传递给用户。</span><span class="sxs-lookup"><span data-stu-id="36640-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="36640-158">异常对象通常包含的信息的用户看不到，这甚至可能出现安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="36640-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="36640-159">这就是为什么此代码包含具有变量`debuggingFlag`，使用作为开关以显示错误消息和为什么默认情况下的变量设置为 false。</span><span class="sxs-lookup"><span data-stu-id="36640-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="36640-160">应设置为 true （，因此显示错误消息） 该变量*仅*如果遇到问题发送电子邮件，并且需要进行调试。</span><span class="sxs-lookup"><span data-stu-id="36640-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="36640-161">已修复任何问题之后, 设置`debuggingFlag`回 false。</span><span class="sxs-lookup"><span data-stu-id="36640-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="36640-162">修改以下电子邮件的代码中的相关的设置：</span><span class="sxs-lookup"><span data-stu-id="36640-162">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="36640-163">设置`your-SMTP-host`到可以访问 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="36640-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="36640-164">设置`your-user-name-here`到您的 SMTP 服务器帐户的用户名。</span><span class="sxs-lookup"><span data-stu-id="36640-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="36640-165">设置`your-account-password`到您的 SMTP 服务器帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="36640-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="36640-166">设置`your-email-address-here`为您自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36640-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="36640-167">这是从发送消息的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36640-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="36640-168">(某些电子邮件提供商不允许你指定一个不同`From`地址，并将使用你的用户名称作为`From`地址。)</span><span class="sxs-lookup"><span data-stu-id="36640-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a><span data-ttu-id="36640-169">配置电子邮件设置</span><span class="sxs-lookup"><span data-stu-id="36640-169">Configuring Email Settings</span></span>
     > 
     > <span data-ttu-id="36640-170">它可以是一个难题，有时以确保具有正确的 SMTP 服务器端口号和等的设置。</span><span class="sxs-lookup"><span data-stu-id="36640-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="36640-171">下面是一些提示：</span><span class="sxs-lookup"><span data-stu-id="36640-171">Here are a few tips:</span></span>
     > 
     > - <span data-ttu-id="36640-172">SMTP 服务器名称通常是类似`smtp.provider.com`或`smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="36640-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="36640-173">但是，如果你将你的站点发布到托管提供商，SMTP 服务器名称在该点可能是`localhost`。</span><span class="sxs-lookup"><span data-stu-id="36640-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="36640-174">这是因为已发布和提供程序的服务器上运行你的站点后，电子邮件服务器可能还会从你的应用程序的角度本地。</span><span class="sxs-lookup"><span data-stu-id="36640-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="36640-175">这一更改服务器名称可能意味着你必须更改发布过程的一部分的 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="36640-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
     > - <span data-ttu-id="36640-176">端口号通常为 25。</span><span class="sxs-lookup"><span data-stu-id="36640-176">The port number is usually 25.</span></span> <span data-ttu-id="36640-177">但是，某些访问接口要求你为使用端口 587 或某些其他端口。</span><span class="sxs-lookup"><span data-stu-id="36640-177">However, some providers require you to use port 587 or some other port.</span></span>
     > - <span data-ttu-id="36640-178">请确保使用正确的凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="36640-179">如果你已将站点发布到宿主提供程序，使用提供程序专门指示适用于电子邮件的凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="36640-180">这些可能不同于用来发布的凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-180">These might be different from the credentials you use to publish.</span></span>
     > - <span data-ttu-id="36640-181">有时则根本不需要凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="36640-182">如果您要发送电子邮件使用您的个人 ISP，电子邮件提供商可能已经知道你的凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="36640-183">在发布后，你可能需要使用比测试本地计算机上的不同凭据。</span><span class="sxs-lookup"><span data-stu-id="36640-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
     > - <span data-ttu-id="36640-184">如果你的电子邮件提供商使用加密，则必须设置`WebMail.EnableSsl`到`true`。</span><span class="sxs-lookup"><span data-stu-id="36640-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="36640-185">运行*EmailRequest.cshtml*在浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="36640-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="36640-186">(请确保页中选择**文件**工作区之前运行它。)</span><span class="sxs-lookup"><span data-stu-id="36640-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="36640-187">输入您的姓名和问题的说明中，，然后单击**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="36640-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="36640-188">要重定向到*ProcessRequest.cshtml*页，其中确认你的消息并向你发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36640-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[image]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="36640-190">使用电子邮件的文件发送</span><span class="sxs-lookup"><span data-stu-id="36640-190">Sending a File Using Email</span></span>

<span data-ttu-id="36640-191">你还可以发送附加到电子邮件的文件。</span><span class="sxs-lookup"><span data-stu-id="36640-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="36640-192">在此过程中，你可以创建文本文件和两个 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="36640-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="36640-193">你将使用电子邮件附件的文本文件。</span><span class="sxs-lookup"><span data-stu-id="36640-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="36640-194">在网站中，添加新的文本文件并将其命名*MyFile.txt*。</span><span class="sxs-lookup"><span data-stu-id="36640-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="36640-195">复制以下文本并将其粘贴在文件中：</span><span class="sxs-lookup"><span data-stu-id="36640-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="36640-196">创建一个名为页*SendFile.cshtml*并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="36640-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="36640-197">创建一个名为页*ProcessFile.cshtml*并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="36640-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="36640-198">修改以下电子邮件的示例中的代码中的相关的设置：</span><span class="sxs-lookup"><span data-stu-id="36640-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="36640-199">设置`your-SMTP-host`到可以访问 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="36640-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="36640-200">设置`your-user-name-here`到您的 SMTP 服务器帐户的用户名。</span><span class="sxs-lookup"><span data-stu-id="36640-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="36640-201">设置`your-email-address-here`为您自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36640-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="36640-202">这是从发送消息的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36640-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="36640-203">设置`your-account-password`到您的 SMTP 服务器帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="36640-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="36640-204">设置`target-email-address-here`为您自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36640-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="36640-205">（如之前，你通常会发送一封电子邮件给其他人，但对于测试，你可以将其发送给自己。）</span><span class="sxs-lookup"><span data-stu-id="36640-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="36640-206">运行*SendFile.cshtml*在浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="36640-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="36640-207">输入你的名称、 的主题行中，和要附加的文本文件的名称 (*MyFile.txt*)。</span><span class="sxs-lookup"><span data-stu-id="36640-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="36640-208">单击 `Submit` 按钮。</span><span class="sxs-lookup"><span data-stu-id="36640-208">Click the `Submit` button.</span></span> <span data-ttu-id="36640-209">如之前，要重定向到*ProcessFile.cshtml*页上，其中确认你的消息和其向你发送电子邮件与附加的文件。</span><span class="sxs-lookup"><span data-stu-id="36640-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="36640-210">其他资源</span><span class="sxs-lookup"><span data-stu-id="36640-210">Additional Resources</span></span>


- [<span data-ttu-id="36640-211">ASP.NET 网页 (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="36640-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="36640-212">简单邮件传输协议</span><span class="sxs-lookup"><span data-stu-id="36640-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="36640-213">为 ASP.NET 网页自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="36640-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
