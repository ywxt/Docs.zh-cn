---
title: 在 ASP.NET Core SMS 的双因素身份验证
author: rick-anderson
description: 了解如何设置双因素身份验证 (2FA) 与 ASP.NET Core 应用。
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 08/15/2017
uid: security/authentication/2fa
ms.openlocfilehash: 335edfd5cd4dfbb9d223ba0ae888a6d2386cd4a5
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272304"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a><span data-ttu-id="65c1c-103">在 ASP.NET Core SMS 的双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="65c1c-103">Two-factor authentication with SMS in ASP.NET Core</span></span>

<span data-ttu-id="65c1c-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[瑞士开发人员](https://github.com/Swiss-Devs)</span><span class="sxs-lookup"><span data-stu-id="65c1c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Swiss-Devs](https://github.com/Swiss-Devs)</span></span>

<span data-ttu-id="65c1c-105">请参阅[ASP.NET Core 中的身份验证器应用启用 QR 代码生成](xref:security/authentication/identity-enable-qrcodes)ASP.NET 核心 2.0 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="65c1c-105">See [Enable QR Code generation for authenticator apps in ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) for ASP.NET Core 2.0 and later.</span></span>

<span data-ttu-id="65c1c-106">本教程演示如何设置双因素身份验证 (2FA) 使用短信。</span><span class="sxs-lookup"><span data-stu-id="65c1c-106">This tutorial shows how to set up two-factor authentication (2FA) using SMS.</span></span> <span data-ttu-id="65c1c-107">为提供的说明[twilio](https://www.twilio.com/)和[ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="65c1c-107">Instructions are given for [twilio](https://www.twilio.com/) and [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), but you can use any other SMS provider.</span></span> <span data-ttu-id="65c1c-108">我们建议你完成[帐户确认和密码恢复](xref:security/authentication/accconfirm)之前开始学习本教程。</span><span class="sxs-lookup"><span data-stu-id="65c1c-108">We recommend you complete [Account Confirmation and Password Recovery](xref:security/authentication/accconfirm) before starting this tutorial.</span></span>

<span data-ttu-id="65c1c-109">视图[已完成的示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-109">View the [completed sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA).</span></span> <span data-ttu-id="65c1c-110">[如何下载](xref:tutorials/index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-110">[How to download](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="65c1c-111">创建新的 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="65c1c-111">Create a new ASP.NET Core project</span></span>

<span data-ttu-id="65c1c-112">创建新的 ASP.NET 核心 web 应用名为`Web2FA`与单个用户帐户。</span><span class="sxs-lookup"><span data-stu-id="65c1c-112">Create a new ASP.NET Core web app named `Web2FA` with individual user accounts.</span></span> <span data-ttu-id="65c1c-113">按照中的说明[在 ASP.NET Core 应用程序强制实施 SSL](xref:security/enforcing-ssl)才能设置，并且需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="65c1c-113">Follow the instructions in [Enforce SSL in an ASP.NET Core app](xref:security/enforcing-ssl) to set up and require SSL.</span></span>

### <a name="create-an-sms-account"></a><span data-ttu-id="65c1c-114">创建 SMS 帐户</span><span class="sxs-lookup"><span data-stu-id="65c1c-114">Create an SMS account</span></span>

<span data-ttu-id="65c1c-115">创建 SMS 帐户，例如，从[twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-115">Create an SMS account, for example, from [twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span></span> <span data-ttu-id="65c1c-116">记录身份验证凭据 (twilio: accountSid 和 authToken 的 ASPSMS： 用户密钥和密码)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-116">Record the authentication credentials (for twilio: accountSid and authToken, for ASPSMS: Userkey and Password).</span></span>

#### <a name="figuring-out-sms-provider-credentials"></a><span data-ttu-id="65c1c-117">了解 SMS 提供程序凭据</span><span class="sxs-lookup"><span data-stu-id="65c1c-117">Figuring out SMS Provider credentials</span></span>

<span data-ttu-id="65c1c-118">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-118">**Twilio:**</span></span>  
<span data-ttu-id="65c1c-119">从你的 Twilio 帐户的仪表板选项卡上，复制**帐户 SID**和**身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="65c1c-119">From the Dashboard tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>

<span data-ttu-id="65c1c-120">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-120">**ASPSMS:**</span></span>  
<span data-ttu-id="65c1c-121">从你的帐户设置，导航到**用户密钥**并将其连同复制你**密码**。</span><span class="sxs-lookup"><span data-stu-id="65c1c-121">From your account settings, navigate to **Userkey** and copy it together with your **Password**.</span></span>

<span data-ttu-id="65c1c-122">我们将更高版本将存储在密钥中的密钥管理器工具使用这些值`SMSAccountIdentification`和`SMSAccountPassword`。</span><span class="sxs-lookup"><span data-stu-id="65c1c-122">We will later store these values in with the secret-manager tool within the keys `SMSAccountIdentification` and `SMSAccountPassword`.</span></span>

#### <a name="specifying-senderid--originator"></a><span data-ttu-id="65c1c-123">指定 SenderID / 发起方</span><span class="sxs-lookup"><span data-stu-id="65c1c-123">Specifying SenderID / Originator</span></span>

<span data-ttu-id="65c1c-124">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-124">**Twilio:**</span></span>  
<span data-ttu-id="65c1c-125">从数字选项卡，将复制你的 Twilio**电话号码**。</span><span class="sxs-lookup"><span data-stu-id="65c1c-125">From the Numbers tab, copy your Twilio **phone number**.</span></span> 

<span data-ttu-id="65c1c-126">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-126">**ASPSMS:**</span></span>  
<span data-ttu-id="65c1c-127">解锁原始发件人菜单上，在解锁一个或多个发送方或选择 （不支持的所有网络） 的字母数字发起方。</span><span class="sxs-lookup"><span data-stu-id="65c1c-127">Within the Unlock Originators Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span> 

<span data-ttu-id="65c1c-128">我们将更高版本存储在项的密钥管理器工具使用此值`SMSAccountFrom`。</span><span class="sxs-lookup"><span data-stu-id="65c1c-128">We will later store this value with the secret-manager tool within the key `SMSAccountFrom`.</span></span>


### <a name="provide-credentials-for-the-sms-service"></a><span data-ttu-id="65c1c-129">SMS 服务提供的凭据</span><span class="sxs-lookup"><span data-stu-id="65c1c-129">Provide credentials for the SMS service</span></span>

<span data-ttu-id="65c1c-130">我们将使用[选项模式](xref:fundamentals/configuration/options)访问的用户帐户和密钥设置。</span><span class="sxs-lookup"><span data-stu-id="65c1c-130">We'll use the [Options pattern](xref:fundamentals/configuration/options) to access the user account and key settings.</span></span> 

   * <span data-ttu-id="65c1c-131">创建一个类以提取安全 SMS 密钥。</span><span class="sxs-lookup"><span data-stu-id="65c1c-131">Create a class to fetch the secure SMS key.</span></span> <span data-ttu-id="65c1c-132">对于此示例，`SMSoptions`中创建类*Services/SMSoptions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="65c1c-132">For this sample, the `SMSoptions` class is created in the *Services/SMSoptions.cs* file.</span></span>

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

<span data-ttu-id="65c1c-133">设置`SMSAccountIdentification`，`SMSAccountPassword`和`SMSAccountFrom`与[机密管理器工具](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-133">Set the `SMSAccountIdentification`, `SMSAccountPassword` and `SMSAccountFrom` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="65c1c-134">例如：</span><span class="sxs-lookup"><span data-stu-id="65c1c-134">For example:</span></span>

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* <span data-ttu-id="65c1c-135">SMS 提供程序添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="65c1c-135">Add the NuGet package for the SMS provider.</span></span> <span data-ttu-id="65c1c-136">从包管理器控制台 (PMC) 运行：</span><span class="sxs-lookup"><span data-stu-id="65c1c-136">From the Package Manager Console (PMC) run:</span></span>

<span data-ttu-id="65c1c-137">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-137">**Twilio:**</span></span>  
`Install-Package Twilio`

<span data-ttu-id="65c1c-138">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-138">**ASPSMS:**</span></span>  
`Install-Package ASPSMS`


* <span data-ttu-id="65c1c-139">中添加代码*Services/MessageServices.cs*文件以启用 SMS。</span><span class="sxs-lookup"><span data-stu-id="65c1c-139">Add code in the *Services/MessageServices.cs* file to enable SMS.</span></span> <span data-ttu-id="65c1c-140">使用 Twilio 或 ASPSMS 部分：</span><span class="sxs-lookup"><span data-stu-id="65c1c-140">Use either the Twilio or the ASPSMS section:</span></span>


<span data-ttu-id="65c1c-141">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-141">**Twilio:**</span></span>  
[!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]

<span data-ttu-id="65c1c-142">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="65c1c-142">**ASPSMS:**</span></span>  
[!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]

### <a name="configure-startup-to-use-smsoptions"></a><span data-ttu-id="65c1c-143">配置要使用的启动 `SMSoptions`</span><span class="sxs-lookup"><span data-stu-id="65c1c-143">Configure startup to use `SMSoptions`</span></span>

<span data-ttu-id="65c1c-144">添加`SMSoptions`对中的服务容器`ConfigureServices`中的方法*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="65c1c-144">Add `SMSoptions` to the service container in the `ConfigureServices` method in the *Startup.cs*:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a><span data-ttu-id="65c1c-145">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="65c1c-145">Enable two-factor authentication</span></span>

<span data-ttu-id="65c1c-146">打开*Views/Manage/Index.cshtml* Razor 视图文件并删除注释字符 （因此没有标记出 commnted）。</span><span class="sxs-lookup"><span data-stu-id="65c1c-146">Open the *Views/Manage/Index.cshtml* Razor view file and remove the comment characters (so no markup is commnted out).</span></span>

## <a name="log-in-with-two-factor-authentication"></a><span data-ttu-id="65c1c-147">使用双因素身份验证登录</span><span class="sxs-lookup"><span data-stu-id="65c1c-147">Log in with two-factor authentication</span></span>

* <span data-ttu-id="65c1c-148">运行应用并注册新的用户</span><span class="sxs-lookup"><span data-stu-id="65c1c-148">Run the app and register a new user</span></span>

![Web 应用程序视图打开 Microsoft Edge 中的注册](2fa/_static/login2fa1.png)

* <span data-ttu-id="65c1c-150">在你激活的用户名称上点击`Index`管理控制器中的操作方法。</span><span class="sxs-lookup"><span data-stu-id="65c1c-150">Tap on your user name, which activates the `Index` action method in Manage controller.</span></span> <span data-ttu-id="65c1c-151">然后点击的电话号码**添加**链接。</span><span class="sxs-lookup"><span data-stu-id="65c1c-151">Then tap the phone number **Add** link.</span></span>

![管理视图](2fa/_static/login2fa2.png)

* <span data-ttu-id="65c1c-153">添加一个电话号码，它将接收验证代码，并点击**发送验证码**。</span><span class="sxs-lookup"><span data-stu-id="65c1c-153">Add a phone number that will receive the verification code, and tap **Send verification code**.</span></span>

![添加电话号码页](2fa/_static/login2fa3.png)

* <span data-ttu-id="65c1c-155">你将获取验证码短信。</span><span class="sxs-lookup"><span data-stu-id="65c1c-155">You will get a text message with the verification code.</span></span> <span data-ttu-id="65c1c-156">输入它，然后点击**提交**</span><span class="sxs-lookup"><span data-stu-id="65c1c-156">Enter it and tap **Submit**</span></span>

![验证电话号码页](2fa/_static/login2fa4.png)

<span data-ttu-id="65c1c-158">如果你不会获得文本消息，请参阅 twilio 日志页。</span><span class="sxs-lookup"><span data-stu-id="65c1c-158">If you don't get a text message, see twilio log page.</span></span>

* <span data-ttu-id="65c1c-159">管理视图显示你的电话号码已成功添加。</span><span class="sxs-lookup"><span data-stu-id="65c1c-159">The Manage view shows your phone number was added successfully.</span></span>

![管理视图](2fa/_static/login2fa5.png)

* <span data-ttu-id="65c1c-161">点击**启用**启用双因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="65c1c-161">Tap **Enable** to enable two-factor authentication.</span></span>

![管理视图](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a><span data-ttu-id="65c1c-163">测试两个双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="65c1c-163">Test two-factor authentication</span></span>

* <span data-ttu-id="65c1c-164">注销。</span><span class="sxs-lookup"><span data-stu-id="65c1c-164">Log off.</span></span>

* <span data-ttu-id="65c1c-165">登录。</span><span class="sxs-lookup"><span data-stu-id="65c1c-165">Log in.</span></span>

* <span data-ttu-id="65c1c-166">用户帐户已启用双因素身份验证，因此你需要提供身份验证的第二个因素。</span><span class="sxs-lookup"><span data-stu-id="65c1c-166">The user account has enabled two-factor authentication, so you have to provide the second factor of authentication .</span></span> <span data-ttu-id="65c1c-167">在本教程中已启用电话验证。</span><span class="sxs-lookup"><span data-stu-id="65c1c-167">In this tutorial you have enabled phone verification.</span></span> <span data-ttu-id="65c1c-168">内置的模板还可用于将作为第二因素的电子邮件设置。</span><span class="sxs-lookup"><span data-stu-id="65c1c-168">The built in templates also allow you to set up email as the second factor.</span></span> <span data-ttu-id="65c1c-169">你可以设置其他的第二个因素，如 QR 代码的身份验证。</span><span class="sxs-lookup"><span data-stu-id="65c1c-169">You can set up additional second factors for authentication such as QR codes.</span></span> <span data-ttu-id="65c1c-170">点击**提交**。</span><span class="sxs-lookup"><span data-stu-id="65c1c-170">Tap **Submit**.</span></span>

![发送验证代码视图](2fa/_static/login2fa7.png)

* <span data-ttu-id="65c1c-172">输入中的 SMS 消息得到的代码。</span><span class="sxs-lookup"><span data-stu-id="65c1c-172">Enter the code you get in the SMS message.</span></span>

* <span data-ttu-id="65c1c-173">单击**记住此浏览器**复选框将免除你无需使用 2FA 时使用相同的设备和浏览器登录。</span><span class="sxs-lookup"><span data-stu-id="65c1c-173">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on when using the same device and browser.</span></span> <span data-ttu-id="65c1c-174">启用 2FA 和单击**记住此浏览器**将为你提供强 2FA 保护免受恶意用户尝试访问你的帐户，只要它们无权访问你的设备。</span><span class="sxs-lookup"><span data-stu-id="65c1c-174">Enabling 2FA and clicking on **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your device.</span></span> <span data-ttu-id="65c1c-175">可以在任何您经常使用的专用设备上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="65c1c-175">You can do this on any private device you regularly use.</span></span> <span data-ttu-id="65c1c-176">通过设置**记住此浏览器**，设备不经常使用的情况下，从获取 2FA 的附加的安全性以及你可以方便地在无需在你自己的设备通过 2FA 转。</span><span class="sxs-lookup"><span data-stu-id="65c1c-176">By setting  **Remember this browser**, you get the added security of 2FA from devices you don't regularly use, and you get the convenience on not having to go through 2FA on your own devices.</span></span>

![验证视图](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a><span data-ttu-id="65c1c-178">针对暴力破解攻击提供保护的帐户锁定</span><span class="sxs-lookup"><span data-stu-id="65c1c-178">Account lockout for protecting against brute force attacks</span></span>

<span data-ttu-id="65c1c-179">帐户锁定建议的 2FA 中。</span><span class="sxs-lookup"><span data-stu-id="65c1c-179">Account lockout is recommended with 2FA.</span></span> <span data-ttu-id="65c1c-180">一旦用户通过本地帐户或社交帐户登录，则会存储 2FA 在每次失败的尝试。</span><span class="sxs-lookup"><span data-stu-id="65c1c-180">Once a user signs in through a local account or social account, each failed attempt at 2FA is stored.</span></span> <span data-ttu-id="65c1c-181">如果达到最大未成功的访问，则用户锁定 (默认： 5 分钟锁定 5 失败的访问尝试次数后)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-181">If the maximum failed access attempts is reached, the user is locked out (default: 5 minute lockout after 5 failed access attempts).</span></span> <span data-ttu-id="65c1c-182">成功的身份验证将失败的访问尝试计数重置并重置时钟。</span><span class="sxs-lookup"><span data-stu-id="65c1c-182">A successful authentication resets the failed access attempts count and resets the clock.</span></span> <span data-ttu-id="65c1c-183">最大失败的访问尝试次数，可以用来设置的锁定时间[MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts)和[DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan)。</span><span class="sxs-lookup"><span data-stu-id="65c1c-183">The maximum failed access attempts and lockout time can be set with [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) and [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span></span> <span data-ttu-id="65c1c-184">以下 10 分钟后访问尝试失败 10 次配置帐户锁定：</span><span class="sxs-lookup"><span data-stu-id="65c1c-184">The following configures account lockout for 10 minutes after 10 failed access attempts:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

<span data-ttu-id="65c1c-185">确认[PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync)设置`lockoutOnFailure`到`true`:</span><span class="sxs-lookup"><span data-stu-id="65c1c-185">Confirm that [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) sets `lockoutOnFailure` to `true`:</span></span>

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
