---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: 使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用程序 |Microsoft 文档
author: Rick-Anderson
description: 本教程演示了如何生成使用双因素身份验证的 ASP.NET MVC 5 web 应用程序。 您应该完成与创建安全的 ASP.NET MVC 5 web 应用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/20/2015
ms.topic: article
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 5e1c54b3901f2c8c85134445c1fa91ee9f2e0d59
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873607"
---
<a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="f0ead-104">使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用程序</span><span class="sxs-lookup"><span data-stu-id="f0ead-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>
====================
<span data-ttu-id="f0ead-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f0ead-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="f0ead-106">本教程演示了如何生成使用双因素身份验证的 ASP.NET MVC 5 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f0ead-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="f0ead-107">您应该完成[创建安全的 ASP.NET MVC 5 web 应用程序具有登录、 电子邮件确认及密码重置](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f0ead-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="f0ead-108">你可以下载已完成的应用程序[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="f0ead-109">下载包含能让你无需设置电子邮件或 SMS 提供程序中测试电子邮件确认和短信的调试帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f0ead-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="f0ead-110">本教程编写的[Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。</span><span class="sxs-lookup"><span data-stu-id="f0ead-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


- [<span data-ttu-id="f0ead-111">创建 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="f0ead-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="f0ead-112">设置 SMS 进行双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="f0ead-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="f0ead-113">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="f0ead-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="f0ead-114">其他资源</span><span class="sxs-lookup"><span data-stu-id="f0ead-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="f0ead-115">创建 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="f0ead-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="f0ead-116">首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="f0ead-117">安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f0ead-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="f0ead-118">警告： 您应该完成[创建安全的 ASP.NET MVC 5 web 应用程序具有登录、 电子邮件确认及密码重置](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f0ead-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="f0ead-119">必须安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本以完成本教程。</span><span class="sxs-lookup"><span data-stu-id="f0ead-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="f0ead-120">创建一个新的 ASP.NET Web 项目，然后选择 MVC 模板中。</span><span class="sxs-lookup"><span data-stu-id="f0ead-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="f0ead-121">Web 窗体还支持 ASP.NET 标识，因此无法执行类似的步骤，在 web 窗体应用程序中。</span><span class="sxs-lookup"><span data-stu-id="f0ead-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="f0ead-122">保留默认的身份验证作为**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="f0ead-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="f0ead-123">如果你想要托管该应用程序在 Azure 中的，保留选中复选框。</span><span class="sxs-lookup"><span data-stu-id="f0ead-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="f0ead-124">稍后在本教程中我们将部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f0ead-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="f0ead-125">你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="f0ead-126">设置[项目以使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="f0ead-127">设置 SMS 进行双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="f0ead-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="f0ead-128">本教程提供有关使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="f0ead-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="f0ead-129">**使用 SMS 提供程序创建的用户帐户**</span><span class="sxs-lookup"><span data-stu-id="f0ead-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="f0ead-130">创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。</span><span class="sxs-lookup"><span data-stu-id="f0ead-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="f0ead-131">**安装其他包或添加服务引用**</span><span class="sxs-lookup"><span data-stu-id="f0ead-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="f0ead-132">Twilio:</span><span class="sxs-lookup"><span data-stu-id="f0ead-132">Twilio:</span></span>  
   <span data-ttu-id="f0ead-133">在程序包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f0ead-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="f0ead-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="f0ead-134">ASPSMS:</span></span>  
   <span data-ttu-id="f0ead-135">下面的服务引用需要添加：</span><span class="sxs-lookup"><span data-stu-id="f0ead-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="f0ead-136">地址:</span><span class="sxs-lookup"><span data-stu-id="f0ead-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="f0ead-137">命名空间:</span><span class="sxs-lookup"><span data-stu-id="f0ead-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="f0ead-138">**了解 SMS 提供程序用户凭据**</span><span class="sxs-lookup"><span data-stu-id="f0ead-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="f0ead-139">Twilio:</span><span class="sxs-lookup"><span data-stu-id="f0ead-139">Twilio:</span></span>  
   <span data-ttu-id="f0ead-140">从**仪表板**选项卡上的 Twilio 帐户，复制**帐户 SID**和**身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="f0ead-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="f0ead-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="f0ead-141">ASPSMS:</span></span>  
   <span data-ttu-id="f0ead-142">从你的帐户设置，导航到**用户密钥**并将其复制以及你自定义**密码**。</span><span class="sxs-lookup"><span data-stu-id="f0ead-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="f0ead-143">我们将更高版本将存储这些值*web.config*中密钥文件`"SMSAccountIdentification"`和`"SMSAccountPassword"`。</span><span class="sxs-lookup"><span data-stu-id="f0ead-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="f0ead-144">**指定 SenderID / 发起方**</span><span class="sxs-lookup"><span data-stu-id="f0ead-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="f0ead-145">Twilio:</span><span class="sxs-lookup"><span data-stu-id="f0ead-145">Twilio:</span></span>  
   <span data-ttu-id="f0ead-146">从**数字**选项卡上，复制你的 Twilio 电话号码。</span><span class="sxs-lookup"><span data-stu-id="f0ead-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="f0ead-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="f0ead-147">ASPSMS:</span></span>  
   <span data-ttu-id="f0ead-148">在**解锁原始发件人**菜单上，解锁一个或多个发送方或选择 （不支持的所有网络） 的字母数字发起方。</span><span class="sxs-lookup"><span data-stu-id="f0ead-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="f0ead-149">我们将更高版本存储中的此值*web.config*文件在项`"SMSAccountFrom"`。</span><span class="sxs-lookup"><span data-stu-id="f0ead-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="f0ead-150">**将 SMS 提供程序凭据传输到应用程序**</span><span class="sxs-lookup"><span data-stu-id="f0ead-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="f0ead-151">提供的凭据和发件人的电话号码向应用程序。</span><span class="sxs-lookup"><span data-stu-id="f0ead-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="f0ead-152">为了简单起见我们将存储这些值*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f0ead-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="f0ead-153">当我们将部署到 Azure 时，我们可以将安全地在值存储**应用设置**网站上的部分配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="f0ead-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="f0ead-154">安全-永远不会存储在源代码中敏感数据。</span><span class="sxs-lookup"><span data-stu-id="f0ead-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="f0ead-155">帐户和凭据添加到上面为了让示例比较简单的代码。</span><span class="sxs-lookup"><span data-stu-id="f0ead-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="f0ead-156">请参阅[用于密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="f0ead-157">**数据传输到 SMS 提供程序的实现**</span><span class="sxs-lookup"><span data-stu-id="f0ead-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="f0ead-158">配置`SmsService`类*应用\_Start\IdentityConfig.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="f0ead-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="f0ead-159">具体取决于使用 SMS 提供程序激活或者**Twilio**或**ASPSMS**部分：</span><span class="sxs-lookup"><span data-stu-id="f0ead-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="f0ead-160">更新*Views\Manage\Index.cshtml* Razor 视图: (注意： 不只需删除现有代码中的注释，使用下面的代码。)</span><span class="sxs-lookup"><span data-stu-id="f0ead-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="f0ead-161">验证`EnableTwoFactorAuthentication`和`DisableTwoFactorAuthentication`中的操作方法`ManageController`具有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性：</span><span class="sxs-lookup"><span data-stu-id="f0ead-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="f0ead-162">运行应用程序和你之前注册的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="f0ead-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="f0ead-163">单击你的用户 ID，将激活`Index`中的操作方法`Manage`控制器。</span><span class="sxs-lookup"><span data-stu-id="f0ead-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="f0ead-164">单击添加。</span><span class="sxs-lookup"><span data-stu-id="f0ead-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="f0ead-165">`AddPhoneNumber`操作方法会显示一个对话框，输入电话号码可以接收 SMS 消息。</span><span class="sxs-lookup"><span data-stu-id="f0ead-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="f0ead-166">几秒钟后你将获取验证码短信。</span><span class="sxs-lookup"><span data-stu-id="f0ead-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="f0ead-167">输入它，然后按**提交**。</span><span class="sxs-lookup"><span data-stu-id="f0ead-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="f0ead-168">管理视图显示已添加你的电话号码。</span><span class="sxs-lookup"><span data-stu-id="f0ead-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="f0ead-169">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="f0ead-169">Enable two-factor authentication</span></span>

<span data-ttu-id="f0ead-170">在模板生成应用程序中，你需要使用 UI 启用双因素身份验证 (2FA)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="f0ead-171">若要启用 2FA，单击你在导航栏中的用户 ID （电子邮件别名）。</span><span class="sxs-lookup"><span data-stu-id="f0ead-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="f0ead-172">单击启用 2FA。</span><span class="sxs-lookup"><span data-stu-id="f0ead-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="f0ead-173">注销，然后注销再重新登录。</span><span class="sxs-lookup"><span data-stu-id="f0ead-173">Logout, then log back in.</span></span> <span data-ttu-id="f0ead-174">如果已启用电子邮件 (请参阅我[以前一教程](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md))，你可以选择 SMS 或 2FA 的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f0ead-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="f0ead-175">将显示验证代码页，你可以 （从 SMS 或电子邮件） 输入代码。</span><span class="sxs-lookup"><span data-stu-id="f0ead-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="f0ead-176">单击**记住此浏览器**复选框将免除你无需使用 2FA 以要求在登录时使用的浏览器和设备选中的复选框的位置。</span><span class="sxs-lookup"><span data-stu-id="f0ead-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="f0ead-177">只要恶意用户无法访问你的设备，启用 2FA 和单击**记住此浏览器**将为你提供方便的一次性密码访问权限，同时还可以保留的所有访问的强 2FA 保护从非受信任的设备。</span><span class="sxs-lookup"><span data-stu-id="f0ead-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="f0ead-178">可以在任何您经常使用的专用设备上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f0ead-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="f0ead-179">本教程提供了启用 2FA 上新的 ASP.NET MVC 应用程序的快速介绍。</span><span class="sxs-lookup"><span data-stu-id="f0ead-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="f0ead-180">我的教程[双因素身份验证使用 SMS 和电子邮件与 ASP.NET 标识](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)进入后面的示例代码中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f0ead-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="f0ead-181">其他资源</span><span class="sxs-lookup"><span data-stu-id="f0ead-181">Additional Resources</span></span>

- <span data-ttu-id="f0ead-182">[具有 ASP.NET 标识使用 SMS 和电子邮件的双因素身份验证](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)进入双因素身份验证的详细信息</span><span class="sxs-lookup"><span data-stu-id="f0ead-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="f0ead-183">指向 ASP.NET Identity 的推荐资源</span><span class="sxs-lookup"><span data-stu-id="f0ead-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="f0ead-184">[帐户确认和密码恢复具有 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)进入密码恢复和帐户确认的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f0ead-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="f0ead-185">[使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程演示如何编写使用 Facebook 和 Google oauth2 授权 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f0ead-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="f0ead-186">它还演示如何向标识数据库中添加额外的数据。</span><span class="sxs-lookup"><span data-stu-id="f0ead-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="f0ead-187">[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用程序部署到 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="f0ead-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="f0ead-188">本教程将添加 Azure 部署，如何保护使用角色，对应用程序如何使用成员资格 API 来添加用户和角色，以及其他安全功能。</span><span class="sxs-lookup"><span data-stu-id="f0ead-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="f0ead-189">创建 oauth2 的 Google 应用和将应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="f0ead-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="f0ead-190">在 Facebook 中创建应用并将应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="f0ead-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="f0ead-191">在项目中的 SSL 设置</span><span class="sxs-lookup"><span data-stu-id="f0ead-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
