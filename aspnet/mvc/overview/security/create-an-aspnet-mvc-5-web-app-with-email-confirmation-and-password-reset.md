---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何生成电子邮件确认和密码重置使用 ASP.NET 标识成员资格系统的 ASP.NET MVC 5 web 应用。 Ca...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 5092476c6cf59bea6fab6fa6f169ff11ec4c9c4a
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207480"
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="c8254-104">安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置 (C#)</span><span class="sxs-lookup"><span data-stu-id="c8254-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>
====================
<span data-ttu-id="c8254-105">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="c8254-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="c8254-106">本教程演示如何生成电子邮件确认和密码重置使用 ASP.NET 标识成员资格系统的 ASP.NET MVC 5 web 应用。</span><span class="sxs-lookup"><span data-stu-id="c8254-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="c8254-107">你可以下载已完成的应用程序[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。</span><span class="sxs-lookup"><span data-stu-id="c8254-107">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="c8254-108">下载内容包含调试帮助程序，使你可以测试电子邮件确认和短信，而无需设置电子邮件或 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8254-108">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="c8254-109">本教程由编写[Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。</span><span class="sxs-lookup"><span data-stu-id="c8254-109">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="c8254-110">创建 ASP.NET MVC 应用</span><span class="sxs-lookup"><span data-stu-id="c8254-110">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="c8254-111">首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="c8254-111">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="c8254-112">安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="c8254-112">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="c8254-113">警告： 您必须安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本，若要完成本教程。</span><span class="sxs-lookup"><span data-stu-id="c8254-113">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="c8254-114">创建新的 ASP.NET Web 项目并选择 MVC 模板。</span><span class="sxs-lookup"><span data-stu-id="c8254-114">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="c8254-115">Web 窗体还支持 ASP.NET 标识，因此无法执行类似的步骤，在 web 窗体应用中。</span><span class="sxs-lookup"><span data-stu-id="c8254-115">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="c8254-116">将保留为默认的身份验证**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="c8254-116">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="c8254-117">如果你想要托管该应用程序在 Azure 中的，将选中该复选框。</span><span class="sxs-lookup"><span data-stu-id="c8254-117">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="c8254-118">稍后在本教程中我们将部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c8254-118">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="c8254-119">你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="c8254-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="c8254-120">设置[项目，以使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="c8254-120">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="c8254-121">运行该应用程序中，单击**注册**链接并注册用户。</span><span class="sxs-lookup"><span data-stu-id="c8254-121">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="c8254-122">在此情况下，电子邮件的唯一验证是使用[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="c8254-122">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="c8254-123">在服务器资源管理器，导航到**数据 Connections\DefaultConnection\Tables\AspNetUsers**，右键单击并选择**打开表定义**。</span><span class="sxs-lookup"><span data-stu-id="c8254-123">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="c8254-124">下图显示了`AspNetUsers`架构：</span><span class="sxs-lookup"><span data-stu-id="c8254-124">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="c8254-125">右键单击**AspNetUsers**表，然后选择**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="c8254-125">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="c8254-126">此时该电子邮件尚未被确认。</span><span class="sxs-lookup"><span data-stu-id="c8254-126">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="c8254-127">单击对应的行并选择删除。</span><span class="sxs-lookup"><span data-stu-id="c8254-127">Click on the row and select delete.</span></span> <span data-ttu-id="c8254-128">将在下一步中，再次添加此电子邮件并发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-128">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="c8254-129">电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="c8254-129">Email confirmation</span></span>

<span data-ttu-id="c8254-130">它是最佳做法以确认新的用户注册，以验证它们不模拟其他人的电子邮件地址 （也就是说，他们尚未注册与其他人的电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="c8254-130">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="c8254-131">假设你有讨论论坛，你会想要防止`"bob@example.com"`注册为`"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="c8254-131">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="c8254-132">而无需电子邮件确认`"joe@contoso.com"`无法收到您的应用程序不需要的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-132">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="c8254-133">假设 Bob 意外注册为`"bib@example.com"`没有注意到，他将无法使用密码恢复，因为此应用没有其正确的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-133">Suppose Bob accidently registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="c8254-134">电子邮件确认从智能机器人提供有限的保护，并不会从确定垃圾邮件发送者提供保护，它们具有许多可用于注册的工作电子邮件别名。</span><span class="sxs-lookup"><span data-stu-id="c8254-134">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="c8254-135">你通常想要阻止新用户之前他们确认已通过电子邮件、 短信或另一种机制将发布到网站的任何数据。</span><span class="sxs-lookup"><span data-stu-id="c8254-135">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="c8254-136">在以下部分中，我们将启用电子邮件确认，并修改代码以防止新注册的用户登录之前确认其电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-136">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="c8254-137">将挂接到 SendGrid</span><span class="sxs-lookup"><span data-stu-id="c8254-137">Hook up SendGrid</span></span>

<span data-ttu-id="c8254-138">在本部分中的说明进行操作不是最新的。</span><span class="sxs-lookup"><span data-stu-id="c8254-138">The instructions in this section are not current.</span></span> <span data-ttu-id="c8254-139">请参阅[配置 SendGrid 电子邮件提供商](/aspnet/core/security/authentication/accconfirm#configure-email-provider)更新的说明。</span><span class="sxs-lookup"><span data-stu-id="c8254-139">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="c8254-140">虽然本教程仅演示了如何添加通过电子邮件通知[SendGrid](http://sendgrid.com/)，可以发送电子邮件使用 SMTP 和其他机制 (请参阅[的其他资源](#addRes))。</span><span class="sxs-lookup"><span data-stu-id="c8254-140">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="c8254-141">在包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="c8254-141">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="c8254-142">转到[Azure SendGrid 注册页面](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)并注册一个免费的 SendGrid 帐户。</span><span class="sxs-lookup"><span data-stu-id="c8254-142">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="c8254-143">通过添加类似于中的以下代码来配置 SendGrid *App_Start/IdentityConfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="c8254-143">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="c8254-144">你将需要添加下列内容包括：</span><span class="sxs-lookup"><span data-stu-id="c8254-144">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="c8254-145">若要使此示例简单明了，我们将存储中的应用设置*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="c8254-145">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="c8254-146">安全性-永远不会存储在源代码中敏感数据。</span><span class="sxs-lookup"><span data-stu-id="c8254-146">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="c8254-147">AppSetting 中存储的帐户和凭据。</span><span class="sxs-lookup"><span data-stu-id="c8254-147">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="c8254-148">在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8254-148">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="c8254-149">请参阅[的密码和其他敏感数据部署到 ASP.NET 和 Azure 最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="c8254-149">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>


### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="c8254-150">启用帐户控制器中的电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="c8254-150">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="c8254-151">验证是否*Views\Account\ConfirmEmail.cshtml*文件具有正确的 razor 语法。</span><span class="sxs-lookup"><span data-stu-id="c8254-151">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="c8254-152">(@ 字符在第一个行可能会丢失。</span><span class="sxs-lookup"><span data-stu-id="c8254-152">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="c8254-153">)</span><span class="sxs-lookup"><span data-stu-id="c8254-153">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="c8254-154">运行应用并单击注册链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-154">Run the app and click the Register link.</span></span> <span data-ttu-id="c8254-155">一旦提交注册表单，你已登录。</span><span class="sxs-lookup"><span data-stu-id="c8254-155">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="c8254-156">检查你的电子邮件帐户，并单击链接以确认你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-156">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="c8254-157">需要电子邮件确认之前登录</span><span class="sxs-lookup"><span data-stu-id="c8254-157">Require email confirmation before log in</span></span>

<span data-ttu-id="c8254-158">当前用户完成注册表单之后, 将它们记录。</span><span class="sxs-lookup"><span data-stu-id="c8254-158">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="c8254-159">你通常想要在中登录之前确认其电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c8254-159">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="c8254-160">在下面的部分中，我们将修改要要求新用户在登录之前能够确认电子邮件 （通过身份验证） 的代码。</span><span class="sxs-lookup"><span data-stu-id="c8254-160">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="c8254-161">更新`HttpPost Register`有以下突出显示更改的方法：</span><span class="sxs-lookup"><span data-stu-id="c8254-161">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="c8254-162">通过注释掉`SignInAsync`方法，用户将未进行签名在注册的。</span><span class="sxs-lookup"><span data-stu-id="c8254-162">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="c8254-163">`TempData["ViewBagLink"] = callbackUrl;`行可用于[调试应用程序](#dbg)并测试而不发送电子邮件的注册。</span><span class="sxs-lookup"><span data-stu-id="c8254-163">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="c8254-164">`ViewBag.Message` 用于显示的确认说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="c8254-164">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="c8254-165">[下载示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含代码来测试电子邮件确认，而无需设置电子邮件，并且还可用于调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8254-165">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="c8254-166">创建`Views\Shared\Info.cshtml`文件，并添加以下 razor 标记：</span><span class="sxs-lookup"><span data-stu-id="c8254-166">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="c8254-167">添加[Authorize 属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)到`Contact`主页控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="c8254-167">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="c8254-168">你可以单击**联系人**链接以验证匿名用户无权访问和身份验证的用户具有访问权限。</span><span class="sxs-lookup"><span data-stu-id="c8254-168">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="c8254-169">您还必须更新`HttpPost Login`操作方法：</span><span class="sxs-lookup"><span data-stu-id="c8254-169">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="c8254-170">更新*Views\Shared\Error.cshtml*视图以显示错误消息：</span><span class="sxs-lookup"><span data-stu-id="c8254-170">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="c8254-171">删除中的任何帐户**AspNetUsers**包含你想要测试的电子邮件别名的表。</span><span class="sxs-lookup"><span data-stu-id="c8254-171">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="c8254-172">运行应用并验证直到您已确认你的电子邮件地址不能登录。</span><span class="sxs-lookup"><span data-stu-id="c8254-172">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="c8254-173">一旦确认电子邮件地址，请单击**联系人**链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-173">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="c8254-174">密码恢复/重置</span><span class="sxs-lookup"><span data-stu-id="c8254-174">Password recovery/reset</span></span>

<span data-ttu-id="c8254-175">删除注释字符从`HttpPost ForgotPassword`帐户控制器中的操作方法：</span><span class="sxs-lookup"><span data-stu-id="c8254-175">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="c8254-176">删除中的注释字符`ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)中*Views\Account\Login.cshtml* razor 视图文件：</span><span class="sxs-lookup"><span data-stu-id="c8254-176">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="c8254-177">登录页现在将显示用于重置密码的链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-177">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="c8254-178">重新发送电子邮件确认链接</span><span class="sxs-lookup"><span data-stu-id="c8254-178">Resend email confirmation link</span></span>

<span data-ttu-id="c8254-179">一旦用户创建新的本地帐户时，它们是电子邮件通知他们需要使用在登录之前确认链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-179">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="c8254-180">如果用户意外删除的确认电子邮件，或者永远不会收到电子邮件，他们将需要再次发送的确认链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-180">If the user accidently deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="c8254-181">以下代码更改演示如何启用此功能。</span><span class="sxs-lookup"><span data-stu-id="c8254-181">The following code changes show how to enable this.</span></span>

<span data-ttu-id="c8254-182">将以下帮助器方法添加到底部*Controllers\AccountController.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="c8254-182">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="c8254-183">更新要使用新的帮助程序的注册方法：</span><span class="sxs-lookup"><span data-stu-id="c8254-183">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="c8254-184">更新要重新发送密码，如果尚未被确认用户帐户的登录方法：</span><span class="sxs-lookup"><span data-stu-id="c8254-184">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="c8254-185">合并的社交和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="c8254-185">Combine social and local login accounts</span></span>

<span data-ttu-id="c8254-186">您可以通过单击电子邮件链接组合本地和社交帐户。</span><span class="sxs-lookup"><span data-stu-id="c8254-186">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="c8254-187">按以下顺序**RickAndMSFT@gmail.com**首次创建为本地登录名，但可以作为第一个，一个社交登录创建帐户，然后添加本地登录名。</span><span class="sxs-lookup"><span data-stu-id="c8254-187">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="c8254-188">单击**管理**链接。</span><span class="sxs-lookup"><span data-stu-id="c8254-188">Click on the **Manage** link.</span></span> <span data-ttu-id="c8254-189">请注意**外部登录名： 0**与此帐户关联。</span><span class="sxs-lookup"><span data-stu-id="c8254-189">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="c8254-190">单击服务中的另一个日志的链接，接受应用程序请求。</span><span class="sxs-lookup"><span data-stu-id="c8254-190">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="c8254-191">已合并两个帐户，你将能够使用任一帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c8254-191">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="c8254-192">可能希望用户在身份验证服务中的其社交日志已关闭，或已为其社交帐户失去访问更有可能的情况下添加本地帐户。</span><span class="sxs-lookup"><span data-stu-id="c8254-192">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="c8254-193">在下图中，Tom 是社交登录 (其中可以看到从**外部登录名： 1**的页上显示)。</span><span class="sxs-lookup"><span data-stu-id="c8254-193">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="c8254-194">单击**选取一个密码**允许你上添加本地日志使用相同的帐户相关联。</span><span class="sxs-lookup"><span data-stu-id="c8254-194">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="c8254-195">中更深入的电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="c8254-195">Email confirmation in more depth</span></span>

<span data-ttu-id="c8254-196">我的教程[帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)将进入此主题具有更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="c8254-196">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="c8254-197">调试应用</span><span class="sxs-lookup"><span data-stu-id="c8254-197">Debugging the app</span></span>

<span data-ttu-id="c8254-198">如果没有收到电子邮件包含的链接：</span><span class="sxs-lookup"><span data-stu-id="c8254-198">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="c8254-199">请检查垃圾邮件或垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="c8254-199">Check your junk or spam folder.</span></span>
- <span data-ttu-id="c8254-200">登录到你的 SendGrid 帐户，然后单击[电子邮件活动链接](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="c8254-200">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="c8254-201">若要测试没有电子邮件验证链接，下载[已完成的示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。</span><span class="sxs-lookup"><span data-stu-id="c8254-201">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="c8254-202">将在页上显示的确认链接和确认代码。</span><span class="sxs-lookup"><span data-stu-id="c8254-202">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="c8254-203">其他资源</span><span class="sxs-lookup"><span data-stu-id="c8254-203">Additional Resources</span></span>

- [<span data-ttu-id="c8254-204">ASP.NET 标识的链接的推荐资源</span><span class="sxs-lookup"><span data-stu-id="c8254-204">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="c8254-205">[帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)进入密码恢复和帐户确认的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c8254-205">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="c8254-206">[MVC 5 应用程序使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程演示如何编写 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth 2 授权。</span><span class="sxs-lookup"><span data-stu-id="c8254-206">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="c8254-207">它还演示如何将其他数据添加到标识数据库。</span><span class="sxs-lookup"><span data-stu-id="c8254-207">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="c8254-208">[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="c8254-208">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="c8254-209">本教程将添加 Azure 部署中，如何保护使用角色，对应用程序如何使用成员资格 API 来添加用户和角色，以及其他安全功能。</span><span class="sxs-lookup"><span data-stu-id="c8254-209">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="c8254-210">为 OAuth 2 中创建的 Google 应用程序和应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="c8254-210">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="c8254-211">在 Facebook 中创建应用并将应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="c8254-211">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="c8254-212">设置项目中的 SSL</span><span class="sxs-lookup"><span data-stu-id="c8254-212">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
