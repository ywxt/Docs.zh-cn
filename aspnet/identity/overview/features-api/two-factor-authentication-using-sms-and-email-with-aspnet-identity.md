---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: 具有 ASP.NET 标识使用 SMS 和电子邮件的双因素身份验证 |Microsoft 文档
author: HaoK
description: 本教程将演示如何设置双因素身份验证 (2FA) 使用 SMS 和电子邮件。 由 Rick Anderson 撰写本文时 ( @RickAndMSFT )、 Pr....
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/15/2015
ms.topic: article
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: c8f628d177004a8569dde2651469ed591e48591e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876132"
---
<a name="two-factor-authentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="bfd06-104">具有 ASP.NET 标识使用 SMS 和电子邮件的双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="bfd06-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>
====================
<span data-ttu-id="bfd06-105">通过[Hao 永远](https://github.com/HaoK)， [Pranav Rastogi](https://github.com/rustd)， [Rick Anderson](https://github.com/Rick-Anderson)， [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="bfd06-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="bfd06-106">本教程将演示如何设置双因素身份验证 (2FA) 使用 SMS 和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="bfd06-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="bfd06-107">由 Rick Anderson 撰写本文时 ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT))，Pranav Rastogi ([@rustd](https://twitter.com/rustd))，Hao 永远和 Suhas Joshi。</span><span class="sxs-lookup"><span data-stu-id="bfd06-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="bfd06-108">NuGet 示例主要由 Hao 永远编写。</span><span class="sxs-lookup"><span data-stu-id="bfd06-108">The NuGet sample was written primarily by Hao Kung.</span></span>


<span data-ttu-id="bfd06-109">本主题涵盖以下方面：</span><span class="sxs-lookup"><span data-stu-id="bfd06-109">This topic covers the following:</span></span>

- [<span data-ttu-id="bfd06-110">生成标识示例</span><span class="sxs-lookup"><span data-stu-id="bfd06-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="bfd06-111">设置 SMS 进行双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="bfd06-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="bfd06-112">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="bfd06-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="bfd06-113">如何注册双因素身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="bfd06-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="bfd06-114">合并社交和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="bfd06-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="bfd06-115">帐户锁定免受暴力攻击</span><span class="sxs-lookup"><span data-stu-id="bfd06-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="bfd06-116">生成标识示例</span><span class="sxs-lookup"><span data-stu-id="bfd06-116">Building the Identity sample</span></span>

<span data-ttu-id="bfd06-117">在本部分中，你将使用 NuGet 下载我们会使用的示例。</span><span class="sxs-lookup"><span data-stu-id="bfd06-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="bfd06-118">首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="bfd06-119">安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="bfd06-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="bfd06-120">警告： 你必须安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)来完成本教程。</span><span class="sxs-lookup"><span data-stu-id="bfd06-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>


1. <span data-ttu-id="bfd06-121">创建一个新***空***ASP.NET Web 项目。</span><span class="sxs-lookup"><span data-stu-id="bfd06-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="bfd06-122">在程序包管理器控制台中，输入以下以下命令：</span><span class="sxs-lookup"><span data-stu-id="bfd06-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="bfd06-123">在本教程中，我们将使用[SendGrid](http://sendgrid.com/)发送电子邮件和[Twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)有关 sms texting。</span><span class="sxs-lookup"><span data-stu-id="bfd06-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="bfd06-124">`Identity.Samples`程序包将安装我们将使用的代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="bfd06-125">设置[项目以使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="bfd06-126">*可选*： 按照中的说明我[电子邮件确认教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)以挂钩 SendGrid 然后运行应用并注册电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="bfd06-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="bfd06-127">* 可选: * 的示例删除演示电子邮件链接确认代码 (`ViewBag.Link`帐户控制器中的代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-127">*Optional: *Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="bfd06-128">请参阅`DisplayEmail`和`ForgotPasswordConfirmation`操作方法和 razor 视图)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="bfd06-129"><em>可选: * 删除`ViewBag.Status`代码从管理和帐户控制器和 *Views\Account\VerifyCode.cshtml</em>和<em>Views\Manage\VerifyPhoneNumber.cshtml</em> razor 视图。</span><span class="sxs-lookup"><span data-stu-id="bfd06-129"><em>Optional: *Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml</em> and <em>Views\Manage\VerifyPhoneNumber.cshtml</em> razor views.</span></span> <span data-ttu-id="bfd06-130">或者，你仍可以保留`ViewBag.Status`显示效果以测试本地而无需挂钩和发送电子邮件和短信的此应用程序工作原理。</span><span class="sxs-lookup"><span data-stu-id="bfd06-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="bfd06-131">警告： 如果你更改任何在此示例中的安全设置，生产应用将需要经过显式调出所做的更改的安全审核。</span><span class="sxs-lookup"><span data-stu-id="bfd06-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>


<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="bfd06-132">设置 SMS 进行双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="bfd06-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="bfd06-133">本教程提供有关使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="bfd06-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="bfd06-134">**使用 SMS 提供程序创建的用户帐户**</span><span class="sxs-lookup"><span data-stu-id="bfd06-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="bfd06-135">创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。</span><span class="sxs-lookup"><span data-stu-id="bfd06-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="bfd06-136">**安装其他包或添加服务引用**</span><span class="sxs-lookup"><span data-stu-id="bfd06-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="bfd06-137">Twilio:</span><span class="sxs-lookup"><span data-stu-id="bfd06-137">Twilio:</span></span>  
   <span data-ttu-id="bfd06-138">在程序包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="bfd06-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="bfd06-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="bfd06-139">ASPSMS:</span></span>  
   <span data-ttu-id="bfd06-140">下面的服务引用需要添加：</span><span class="sxs-lookup"><span data-stu-id="bfd06-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="bfd06-141">地址:</span><span class="sxs-lookup"><span data-stu-id="bfd06-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="bfd06-142">命名空间:</span><span class="sxs-lookup"><span data-stu-id="bfd06-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="bfd06-143">**了解 SMS 提供程序用户凭据**</span><span class="sxs-lookup"><span data-stu-id="bfd06-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="bfd06-144">Twilio:</span><span class="sxs-lookup"><span data-stu-id="bfd06-144">Twilio:</span></span>  
   <span data-ttu-id="bfd06-145">从**仪表板**选项卡上的 Twilio 帐户，复制**帐户 SID**和**身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="bfd06-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="bfd06-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="bfd06-146">ASPSMS:</span></span>  
   <span data-ttu-id="bfd06-147">从你的帐户设置，导航到**用户密钥**并将其复制以及你自定义**密码**。</span><span class="sxs-lookup"><span data-stu-id="bfd06-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="bfd06-148">我们将更高版本将这些值存储在变量中`SMSAccountIdentification`和`SMSAccountPassword`。</span><span class="sxs-lookup"><span data-stu-id="bfd06-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="bfd06-149">**指定 SenderID / 发起方**</span><span class="sxs-lookup"><span data-stu-id="bfd06-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="bfd06-150">Twilio:</span><span class="sxs-lookup"><span data-stu-id="bfd06-150">Twilio:</span></span>  
   <span data-ttu-id="bfd06-151">从**数字**选项卡上，复制你的 Twilio 电话号码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="bfd06-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="bfd06-152">ASPSMS:</span></span>  
   <span data-ttu-id="bfd06-153">在**解锁原始发件人**菜单上，解锁一个或多个发送方或选择 （不支持的所有网络） 的字母数字发起方。</span><span class="sxs-lookup"><span data-stu-id="bfd06-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="bfd06-154">我们将更高版本将此值存储在变量`SMSAccountFrom`。</span><span class="sxs-lookup"><span data-stu-id="bfd06-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="bfd06-155">**将 SMS 提供程序凭据传输到应用程序**</span><span class="sxs-lookup"><span data-stu-id="bfd06-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="bfd06-156">提供的凭据和发件人的电话号码向应用程序：</span><span class="sxs-lookup"><span data-stu-id="bfd06-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="bfd06-157">安全-永远不会存储在源代码中敏感数据。</span><span class="sxs-lookup"><span data-stu-id="bfd06-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="bfd06-158">帐户和凭据添加到上面为了让示例比较简单的代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="bfd06-159">请参阅 Jon 输入[ASP.NET MVC： 保留源控件的专用设置扩展](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="bfd06-160">**数据传输到 SMS 提供程序的实现**</span><span class="sxs-lookup"><span data-stu-id="bfd06-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="bfd06-161">配置`SmsService`类*应用\_Start\IdentityConfig.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="bfd06-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="bfd06-162">具体取决于使用 SMS 提供程序激活或者**Twilio**或**ASPSMS**部分：</span><span class="sxs-lookup"><span data-stu-id="bfd06-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="bfd06-163">运行应用程序和你之前注册的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="bfd06-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="bfd06-164">单击你的用户 ID，将激活`Index`中的操作方法`Manage`控制器。</span><span class="sxs-lookup"><span data-stu-id="bfd06-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="bfd06-165">单击添加。</span><span class="sxs-lookup"><span data-stu-id="bfd06-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="bfd06-166">几秒钟后你将获取验证码短信。</span><span class="sxs-lookup"><span data-stu-id="bfd06-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="bfd06-167">输入它，然后按**提交**。</span><span class="sxs-lookup"><span data-stu-id="bfd06-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="bfd06-168">管理视图显示已添加你的电话号码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="bfd06-169">检查代码</span><span class="sxs-lookup"><span data-stu-id="bfd06-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="bfd06-170">`Index`中的操作方法`Manage`控制器设置基于上一个操作的状态消息，并提供更改您的本地密码或添加一个本地帐户的链接。</span><span class="sxs-lookup"><span data-stu-id="bfd06-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="bfd06-171">`Index`方法还会显示状态或你 2FA 电话版本号、 外部登录名、 2FA 启用，并请记住 （稍后进行说明） 此浏览器的 2FA 方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="bfd06-172">单击你的标题栏中的用户 ID （电子邮件） 不会将消息传递。</span><span class="sxs-lookup"><span data-stu-id="bfd06-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="bfd06-173">单击**电话号码： 删除**链接传递`Message=RemovePhoneSuccess`作为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bfd06-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="bfd06-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="bfd06-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="bfd06-175">`AddPhoneNumber`操作方法会显示一个对话框，输入电话号码可以接收 SMS 消息。</span><span class="sxs-lookup"><span data-stu-id="bfd06-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="bfd06-176">单击**发送验证码**按钮发送到 HTTP POST 的电话号码`AddPhoneNumber`操作方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="bfd06-177">`GenerateChangePhoneNumberTokenAsync`方法生成将在 SMS 消息中设置的安全令牌。</span><span class="sxs-lookup"><span data-stu-id="bfd06-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="bfd06-178">如果已配置 SMS 服务，会在字符串令牌发送&quot;你的安全代码是&lt;令牌&gt;&quot;。</span><span class="sxs-lookup"><span data-stu-id="bfd06-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="bfd06-179">`SmsService.SendAsync`以异步方式调用方法，则应用将重定向到`VerifyPhoneNumber`操作方法 （其中显示以下对话框），你可以在其中输入验证代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="bfd06-180">一旦你输入代码，然后单击提交，将代码发布到 HTTP POST`VerifyPhoneNumber`操作方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="bfd06-181">`ChangePhoneNumberAsync`方法检查已发布的安全代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="bfd06-182">如果代码正确无误，电话号码将添加到`PhoneNumber`字段`AspNetUsers`表。</span><span class="sxs-lookup"><span data-stu-id="bfd06-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="bfd06-183">如果该调用成功，`SignInAsync`调用方法：</span><span class="sxs-lookup"><span data-stu-id="bfd06-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="bfd06-184">`isPersistent`参数设置是否跨多个请求身份验证会话保持不变。</span><span class="sxs-lookup"><span data-stu-id="bfd06-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="bfd06-185">当你更改你的安全配置文件时，请生成并存储在新的安全戳`SecurityStamp`字段*AspNetUsers*表。</span><span class="sxs-lookup"><span data-stu-id="bfd06-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="bfd06-186">请注意，`SecurityStamp`字段是不同的安全 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfd06-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="bfd06-187">安全 cookie 不存储在`AspNetUsers`表 （或在标识数据库中的其他任何位置）。</span><span class="sxs-lookup"><span data-stu-id="bfd06-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="bfd06-188">使用自签名安全 cookie 令牌[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)并使用创建`UserId, SecurityStamp`和过期时间信息。</span><span class="sxs-lookup"><span data-stu-id="bfd06-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="bfd06-189">Cookie 中间件检查每个请求上的 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfd06-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="bfd06-190">`SecurityStampValidator`中的方法`Startup`类的命中率数据库和我们会定期检查安全戳指定与`validateInterval`。</span><span class="sxs-lookup"><span data-stu-id="bfd06-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="bfd06-191">除非您更改安全配置文件，这仅发生 （在我们的示例） 每隔 30 分钟。</span><span class="sxs-lookup"><span data-stu-id="bfd06-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="bfd06-192">30 分钟时间间隔内已选择最大程度减少对数据库的访问。</span><span class="sxs-lookup"><span data-stu-id="bfd06-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="bfd06-193">`SignInAsync`方法所需的安全配置文件进行任何更改时调用。</span><span class="sxs-lookup"><span data-stu-id="bfd06-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="bfd06-194">该数据库时的安全配置文件更改，是更新`SecurityStamp`字段，和而不调用`SignInAsync`方法将保持登录*仅*直到下一次 OWIN 管道命中数据库 ( `validateInterval`).</span><span class="sxs-lookup"><span data-stu-id="bfd06-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="bfd06-195">你可以通过更改测试此`SignInAsync`方法以立即返回，并设置 cookie`validateInterval`属性从 30 分钟为 5 秒：</span><span class="sxs-lookup"><span data-stu-id="bfd06-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="bfd06-196">使用上面的代码更改，你可以更改你的安全配置文件 (例如，通过更改状态的**两个因素启用**) 和你将被注销在 5 秒内时`SecurityStampValidator.OnValidateIdentity`方法失败。</span><span class="sxs-lookup"><span data-stu-id="bfd06-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="bfd06-197">删除中的返回行`SignInAsync`方法，请更改的另一个安全配置文件和你将不被注销。`SignInAsync`方法将生成新的安全 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfd06-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="bfd06-198">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="bfd06-198">Enable two-factor authentication</span></span>

<span data-ttu-id="bfd06-199">在示例应用中，你需要使用 UI 启用双因素身份验证 (2FA)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="bfd06-200">若要启用 2FA，单击你在导航栏中的用户 ID （电子邮件别名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="bfd06-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="bfd06-201">单击启用 2FA。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="bfd06-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="bfd06-202">注销，然后重新登录。</span><span class="sxs-lookup"><span data-stu-id="bfd06-202">Log out, then log back in.</span></span> <span data-ttu-id="bfd06-203">如果已启用电子邮件 (请参阅我[以前一教程](account-confirmation-and-password-recovery-with-aspnet-identity.md))，你可以选择 SMS 或 2FA 的电子邮件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="bfd06-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="bfd06-204">将显示验证代码页，你可以 （从 SMS 或电子邮件） 输入代码。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="bfd06-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="bfd06-205">单击**记住此浏览器**复选框将免除你无需使用 2FA 具有该计算机和浏览器登录。</span><span class="sxs-lookup"><span data-stu-id="bfd06-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="bfd06-206">启用 2FA 和单击**记住此浏览器**将为你提供强 2FA 保护免受恶意用户尝试访问你的帐户，只要它们无权访问你的计算机。</span><span class="sxs-lookup"><span data-stu-id="bfd06-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="bfd06-207">可以经常使用的所有专用计算机上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="bfd06-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="bfd06-208">通过设置**记住此浏览器**、 从计算机不经常使用的情况下，获取 2FA 的附加的安全性，并可以在无需在你自己的计算机上经历 2FA 方便地。</span><span class="sxs-lookup"><span data-stu-id="bfd06-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="bfd06-209">如何注册双因素身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="bfd06-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="bfd06-210">当你创建新的 MVC 项目中， *IdentityConfig.cs*文件包含以下代码以注册双因素身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="bfd06-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="bfd06-211">添加 2FA 的电话号码</span><span class="sxs-lookup"><span data-stu-id="bfd06-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="bfd06-212">`AddPhoneNumber`中的操作方法`Manage`控制器生成的安全令牌，并且发送到电话号码你已经提供。</span><span class="sxs-lookup"><span data-stu-id="bfd06-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="bfd06-213">后发送令牌，它将重定向到`VerifyPhoneNumber`操作方法，你可以在其中输入要为 2FA 注册 SMS 的代码。</span><span class="sxs-lookup"><span data-stu-id="bfd06-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="bfd06-214">在验证的电话号码之前未使用 SMS 2FA。</span><span class="sxs-lookup"><span data-stu-id="bfd06-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="bfd06-215">启用 2FA</span><span class="sxs-lookup"><span data-stu-id="bfd06-215">Enabling 2FA</span></span>

<span data-ttu-id="bfd06-216">`EnableTFA`操作方法使 2FA:</span><span class="sxs-lookup"><span data-stu-id="bfd06-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="bfd06-217">请注意`SignInAsync`必须调用，因为启用 2FA 是做的安全配置文件的更改。</span><span class="sxs-lookup"><span data-stu-id="bfd06-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="bfd06-218">启用 2FA 后，用户将需要使用 2FA 登录，使用用户已注册 （SMS 和在此示例中的电子邮件） 的 2FA 方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="bfd06-219">您可以添加多个 2FA 提供程序，如 QR 代码生成器也可以编写你自己的 (请参阅[使用 Google 身份验证器具有 ASP.NET 标识](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/))。</span><span class="sxs-lookup"><span data-stu-id="bfd06-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="bfd06-220">使用生成 2FA 代码[基于时间的一次性密码算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)和代码的有效期为 6 分钟。</span><span class="sxs-lookup"><span data-stu-id="bfd06-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="bfd06-221">如果需要六个分钟以上输入的代码，你将收到无效的代码错误消息。</span><span class="sxs-lookup"><span data-stu-id="bfd06-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>


<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="bfd06-222">合并社交和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="bfd06-222">Combine social and local login accounts</span></span>

<span data-ttu-id="bfd06-223">你可以通过单击电子邮件链接组合本地和社交帐户。</span><span class="sxs-lookup"><span data-stu-id="bfd06-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="bfd06-224">按以下顺序&quot; RickAndMSFT@gmail.com &quot;最初创建为本地登录名，但你可以创建帐户作为社交日志中的第一个，然后添加本地登录名。</span><span class="sxs-lookup"><span data-stu-id="bfd06-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="bfd06-225">单击**管理**链接。</span><span class="sxs-lookup"><span data-stu-id="bfd06-225">Click on the **Manage** link.</span></span> <span data-ttu-id="bfd06-226">请注意与此帐户关联 0 外部 （社交登录名）。</span><span class="sxs-lookup"><span data-stu-id="bfd06-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="bfd06-227">单击服务中的另一个日志的链接，接受应用程序请求。</span><span class="sxs-lookup"><span data-stu-id="bfd06-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="bfd06-228">现在合并两个帐户，你将能够使用任一帐户登录。</span><span class="sxs-lookup"><span data-stu-id="bfd06-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="bfd06-229">你可能希望用户身份验证服务中的其社交日志已关闭，或已对其社交帐户失去访问更有可能的情况下添加本地帐户。</span><span class="sxs-lookup"><span data-stu-id="bfd06-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="bfd06-230">在下图中，Tom 是一个社交登录 (您可以看到从该**外部登录名： 1**的页上显示)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="bfd06-231">单击**挑选一个密码**允许你上添加本地日志与相同的帐户关联。</span><span class="sxs-lookup"><span data-stu-id="bfd06-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="bfd06-232">帐户锁定免受暴力攻击</span><span class="sxs-lookup"><span data-stu-id="bfd06-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="bfd06-233">你可以通过启用用户锁定保护字典式攻击你的应用上的帐户。</span><span class="sxs-lookup"><span data-stu-id="bfd06-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="bfd06-234">下面的代码中`ApplicationUserManager Create`方法配置在锁住：</span><span class="sxs-lookup"><span data-stu-id="bfd06-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="bfd06-235">上面的代码中启用双重身份验证的锁定。</span><span class="sxs-lookup"><span data-stu-id="bfd06-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="bfd06-236">虽然你可以通过更改启用的登录名在锁住`shouldLockout`为 true`Login`在 account 控制器的方法，我们建议则不能启用的登录名在锁住，因为它会使该帐户容易遭受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登录名攻击。</span><span class="sxs-lookup"><span data-stu-id="bfd06-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="bfd06-237">在示例代码中，为管理员帐户创建中禁用锁定`ApplicationDbInitializer Seed`方法：</span><span class="sxs-lookup"><span data-stu-id="bfd06-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="bfd06-238">要求用户具有一个已验证电子邮件帐户</span><span class="sxs-lookup"><span data-stu-id="bfd06-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="bfd06-239">下面的代码要求用户具有一个已验证电子邮件帐户，然后它们可以在登录：</span><span class="sxs-lookup"><span data-stu-id="bfd06-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="bfd06-240">SignInManager 如何检查 2FA 要求</span><span class="sxs-lookup"><span data-stu-id="bfd06-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="bfd06-241">同时本地登录和社交日志中检查，以查看是否已启用 2FA 中。</span><span class="sxs-lookup"><span data-stu-id="bfd06-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="bfd06-242">如果启用了 2FA，`SignInManager`登录方法返回`SignInStatus.RequiresVerification`，并将用户重定向到`SendCode`操作方法，它们将需要输入代码以完成日志序列中。</span><span class="sxs-lookup"><span data-stu-id="bfd06-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="bfd06-243">如果用户具有记住我设置在用户本地 cookie 上,`SignInManager`将返回`SignInStatus.Success`，它们将不需要经历 2FA。</span><span class="sxs-lookup"><span data-stu-id="bfd06-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="bfd06-244">下面的代码演示`SendCode`操作方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="bfd06-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)使用为用户启用的所有 2FA 方法创建。</span><span class="sxs-lookup"><span data-stu-id="bfd06-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="bfd06-246">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)传递给[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx)帮助器，这样用户就可以选择 2FA 方法 （通常电子邮件和短信）。</span><span class="sxs-lookup"><span data-stu-id="bfd06-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="bfd06-247">一旦用户发送 2FA 方法中，`HTTP POST SendCode`调用操作方法，`SignInManager`发送 2FA 代码和用户重定向到`VerifyCode`它们可以在其中输入要完成的日志中的代码的操作方法。</span><span class="sxs-lookup"><span data-stu-id="bfd06-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="bfd06-248">2FA 锁定</span><span class="sxs-lookup"><span data-stu-id="bfd06-248">2FA Lockout</span></span>

<span data-ttu-id="bfd06-249">虽然可以在登录密码尝试失败次数中设置帐户锁定，这种方法使你的登录名容易遭受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)锁定。</span><span class="sxs-lookup"><span data-stu-id="bfd06-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="bfd06-250">我们建议只适用于 2FA 使用帐户锁定。</span><span class="sxs-lookup"><span data-stu-id="bfd06-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="bfd06-251">当`ApplicationUserManager`是创建，示例代码将设置 2FA 锁定和`MaxFailedAccessAttemptsBeforeLockout`为五。</span><span class="sxs-lookup"><span data-stu-id="bfd06-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="bfd06-252">一旦用户 （通过本地帐户或社交帐户） 登录，存储在 2FA 尝试每个失败，而且如果达到最大尝试次数，则锁定用户五分钟时间 (你可以设置与时间锁定`DefaultAccountLockoutTimeSpan`)。</span><span class="sxs-lookup"><span data-stu-id="bfd06-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="bfd06-253">其他资源</span><span class="sxs-lookup"><span data-stu-id="bfd06-253">Additional Resources</span></span>

- <span data-ttu-id="bfd06-254">[ASP.NET 标识的推荐资源](../getting-started/aspnet-identity-recommended-resources.md)因此链接的标识博客、 视频、 教程和出色的完整列表。</span><span class="sxs-lookup"><span data-stu-id="bfd06-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="bfd06-255">[使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)还演示如何将配置文件信息添加到用户表。</span><span class="sxs-lookup"><span data-stu-id="bfd06-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="bfd06-256">[ASP.NET MVC 和标识 2.0： 了解基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)通过 John 输入。</span><span class="sxs-lookup"><span data-stu-id="bfd06-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="bfd06-257">帐户确认和密码恢复 ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="bfd06-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="bfd06-258">ASP.NET 标识简介</span><span class="sxs-lookup"><span data-stu-id="bfd06-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="bfd06-259">[宣布推出适用的 ASP.NET 标识 2.0.0 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) Pranav Rastogi 通过。</span><span class="sxs-lookup"><span data-stu-id="bfd06-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="bfd06-260">[ASP.NET 标识 2.0： 设置帐户验证和双因素授权](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)通过 John 输入。</span><span class="sxs-lookup"><span data-stu-id="bfd06-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
