---
title: 在 ASP.NET Core SMS 的双因素身份验证
author: rick-anderson
description: 了解如何设置双因素身份验证 (2FA) 与 ASP.NET Core 应用。
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 09/22/2018
ms.custom: seodec18
uid: security/authentication/2fa
ms.openlocfilehash: 48bfc50378fc0ec212f5b9d4e7ce05bb4fc97b9d
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098881"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a><span data-ttu-id="eaf39-103">在 ASP.NET Core SMS 的双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="eaf39-103">Two-factor authentication with SMS in ASP.NET Core</span></span>

<span data-ttu-id="eaf39-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[瑞士开发人员](https://github.com/Swiss-Devs)</span><span class="sxs-lookup"><span data-stu-id="eaf39-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Swiss-Devs](https://github.com/Swiss-Devs)</span></span>

>[!WARNING]
> <span data-ttu-id="eaf39-105">两个身份验证 (2FA) 身份验证器应用程序，使用基于时间的一次性密码算法 (TOTP)，是推荐的方法用于 2FA 的行业。</span><span class="sxs-lookup"><span data-stu-id="eaf39-105">Two factor authentication (2FA) authenticator apps, using a Time-based One-time Password Algorithm (TOTP), are the industry recommended approach for 2FA.</span></span> <span data-ttu-id="eaf39-106">2FA 使用 TOTP 优于 SMS 2FA。</span><span class="sxs-lookup"><span data-stu-id="eaf39-106">2FA using TOTP is preferred to SMS 2FA.</span></span> <span data-ttu-id="eaf39-107">有关详细信息，请参阅[TOTP 中 ASP.NET Core 的身份验证器应用启用 QR 代码生成](xref:security/authentication/identity-enable-qrcodes)ASP.NET Core 2.0 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="eaf39-107">For more information, see [Enable QR Code generation for TOTP authenticator apps in ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) for ASP.NET Core 2.0 and later.</span></span>

<span data-ttu-id="eaf39-108">本教程演示如何设置双因素身份验证 (2FA) 使用短信。</span><span class="sxs-lookup"><span data-stu-id="eaf39-108">This tutorial shows how to set up two-factor authentication (2FA) using SMS.</span></span> <span data-ttu-id="eaf39-109">说明提供有关[twilio](https://www.twilio.com/)并[ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="eaf39-109">Instructions are given for [twilio](https://www.twilio.com/) and [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), but you can use any other SMS provider.</span></span> <span data-ttu-id="eaf39-110">我们建议你先完成[帐户确认和密码恢复](xref:security/authentication/accconfirm)之前开始学习本教程。</span><span class="sxs-lookup"><span data-stu-id="eaf39-110">We recommend you complete [Account Confirmation and Password Recovery](xref:security/authentication/accconfirm) before starting this tutorial.</span></span>

<span data-ttu-id="eaf39-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA)。</span><span class="sxs-lookup"><span data-stu-id="eaf39-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA).</span></span> <span data-ttu-id="eaf39-112">[如何下载](xref:index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="eaf39-112">[How to download](xref:index#how-to-download-a-sample).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="eaf39-113">创建新的 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="eaf39-113">Create a new ASP.NET Core project</span></span>

<span data-ttu-id="eaf39-114">创建新的 ASP.NET Core web 应用名为`Web2FA`与单个用户帐户。</span><span class="sxs-lookup"><span data-stu-id="eaf39-114">Create a new ASP.NET Core web app named `Web2FA` with individual user accounts.</span></span> <span data-ttu-id="eaf39-115">按照中的说明<xref:security/enforcing-ssl>设置并要求使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="eaf39-115">Follow the instructions in <xref:security/enforcing-ssl> to set up and require HTTPS.</span></span>

### <a name="create-an-sms-account"></a><span data-ttu-id="eaf39-116">创建 SMS 帐户</span><span class="sxs-lookup"><span data-stu-id="eaf39-116">Create an SMS account</span></span>

<span data-ttu-id="eaf39-117">创建一个 SMS 帐户，例如，从[twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)。</span><span class="sxs-lookup"><span data-stu-id="eaf39-117">Create an SMS account, for example, from [twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span></span> <span data-ttu-id="eaf39-118">记录身份验证凭据 (twilio: accountSid 和 authToken 的 ASPSMS:用户密钥和密码）。</span><span class="sxs-lookup"><span data-stu-id="eaf39-118">Record the authentication credentials (for twilio: accountSid and authToken, for ASPSMS: Userkey and Password).</span></span>

#### <a name="figuring-out-sms-provider-credentials"></a><span data-ttu-id="eaf39-119">找出 SMS 提供程序凭据</span><span class="sxs-lookup"><span data-stu-id="eaf39-119">Figuring out SMS Provider credentials</span></span>

<span data-ttu-id="eaf39-120">**Twilio:** 从你的 Twilio 帐户的仪表板选项卡上，复制**帐户 SID**并**身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="eaf39-120">**Twilio:** From the Dashboard tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>

<span data-ttu-id="eaf39-121">**ASPSMS:** 在帐户设置中，导航到**Userkey**并将其连同复制你**密码**。</span><span class="sxs-lookup"><span data-stu-id="eaf39-121">**ASPSMS:** From your account settings, navigate to **Userkey** and copy it together with your **Password**.</span></span>

<span data-ttu-id="eaf39-122">我们将更高版本存储中密钥的机密管理器工具使用这些值`SMSAccountIdentification`和`SMSAccountPassword`。</span><span class="sxs-lookup"><span data-stu-id="eaf39-122">We will later store these values in with the secret-manager tool within the keys `SMSAccountIdentification` and `SMSAccountPassword`.</span></span>

#### <a name="specifying-senderid--originator"></a><span data-ttu-id="eaf39-123">指定 SenderID / 原始发件人</span><span class="sxs-lookup"><span data-stu-id="eaf39-123">Specifying SenderID / Originator</span></span>

<span data-ttu-id="eaf39-124">**Twilio:** 从数字选项卡，将复制你的 Twilio**电话号码**。</span><span class="sxs-lookup"><span data-stu-id="eaf39-124">**Twilio:** From the Numbers tab, copy your Twilio **phone number**.</span></span>

<span data-ttu-id="eaf39-125">**ASPSMS:** 在解锁始发者的菜单中，解锁一个或多个原始发件人或选择字母数字发信方 （不支持的所有网络）。</span><span class="sxs-lookup"><span data-stu-id="eaf39-125">**ASPSMS:** Within the Unlock Originators Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>

<span data-ttu-id="eaf39-126">我们稍后将存储此值与中密钥的机密管理器工具`SMSAccountFrom`。</span><span class="sxs-lookup"><span data-stu-id="eaf39-126">We will later store this value with the secret-manager tool within the key `SMSAccountFrom`.</span></span>


### <a name="provide-credentials-for-the-sms-service"></a><span data-ttu-id="eaf39-127">SMS 服务提供的凭据</span><span class="sxs-lookup"><span data-stu-id="eaf39-127">Provide credentials for the SMS service</span></span>

<span data-ttu-id="eaf39-128">我们将使用[选项模式](xref:fundamentals/configuration/options)访问的用户帐户和密钥设置。</span><span class="sxs-lookup"><span data-stu-id="eaf39-128">We'll use the [Options pattern](xref:fundamentals/configuration/options) to access the user account and key settings.</span></span>

   * <span data-ttu-id="eaf39-129">创建一个类来提取安全 SMS 项。</span><span class="sxs-lookup"><span data-stu-id="eaf39-129">Create a class to fetch the secure SMS key.</span></span> <span data-ttu-id="eaf39-130">此示例中，对于`SMSoptions`中创建类*Services/SMSoptions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="eaf39-130">For this sample, the `SMSoptions` class is created in the *Services/SMSoptions.cs* file.</span></span>

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

<span data-ttu-id="eaf39-131">设置`SMSAccountIdentification`，`SMSAccountPassword`并`SMSAccountFrom`与[机密管理器工具](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="eaf39-131">Set the `SMSAccountIdentification`, `SMSAccountPassword` and `SMSAccountFrom` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="eaf39-132">例如：</span><span class="sxs-lookup"><span data-stu-id="eaf39-132">For example:</span></span>

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* <span data-ttu-id="eaf39-133">SMS 提供程序添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="eaf39-133">Add the NuGet package for the SMS provider.</span></span> <span data-ttu-id="eaf39-134">从包管理器控制台 (PMC) 运行：</span><span class="sxs-lookup"><span data-stu-id="eaf39-134">From the Package Manager Console (PMC) run:</span></span>

<span data-ttu-id="eaf39-135">**Twilio:**
`Install-Package Twilio`</span><span class="sxs-lookup"><span data-stu-id="eaf39-135">**Twilio:**
`Install-Package Twilio`</span></span>

<span data-ttu-id="eaf39-136">**ASPSMS:**
`Install-Package ASPSMS`</span><span class="sxs-lookup"><span data-stu-id="eaf39-136">**ASPSMS:**
`Install-Package ASPSMS`</span></span>


* <span data-ttu-id="eaf39-137">将代码中的添加*Services/MessageServices.cs*文件以启用短信。</span><span class="sxs-lookup"><span data-stu-id="eaf39-137">Add code in the *Services/MessageServices.cs* file to enable SMS.</span></span> <span data-ttu-id="eaf39-138">使用 Twilio 或 ASPSMS 部分：</span><span class="sxs-lookup"><span data-stu-id="eaf39-138">Use either the Twilio or the ASPSMS section:</span></span>


<span data-ttu-id="eaf39-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span><span class="sxs-lookup"><span data-stu-id="eaf39-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span></span>

<span data-ttu-id="eaf39-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span><span class="sxs-lookup"><span data-stu-id="eaf39-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span></span>

### <a name="configure-startup-to-use-smsoptions"></a><span data-ttu-id="eaf39-141">将启动要使用配置 `SMSoptions`</span><span class="sxs-lookup"><span data-stu-id="eaf39-141">Configure startup to use `SMSoptions`</span></span>

<span data-ttu-id="eaf39-142">添加`SMSoptions`对中的服务容器`ConfigureServices`中的方法*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="eaf39-142">Add `SMSoptions` to the service container in the `ConfigureServices` method in the *Startup.cs*:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a><span data-ttu-id="eaf39-143">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="eaf39-143">Enable two-factor authentication</span></span>

<span data-ttu-id="eaf39-144">打开*Views/Manage/Index.cshtml* Razor 视图文件并删除注释字符 （因此没有标记为 commnted out）。</span><span class="sxs-lookup"><span data-stu-id="eaf39-144">Open the *Views/Manage/Index.cshtml* Razor view file and remove the comment characters (so no markup is commnted out).</span></span>

## <a name="log-in-with-two-factor-authentication"></a><span data-ttu-id="eaf39-145">使用双因素身份验证登录</span><span class="sxs-lookup"><span data-stu-id="eaf39-145">Log in with two-factor authentication</span></span>

* <span data-ttu-id="eaf39-146">运行应用并注册一个新用户</span><span class="sxs-lookup"><span data-stu-id="eaf39-146">Run the app and register a new user</span></span>

![Web 应用程序注册 Microsoft Edge 中打开视图](2fa/_static/login2fa1.png)

* <span data-ttu-id="eaf39-148">点击您的用户名称，这便激活`Index`管理控制器中的操作方法。</span><span class="sxs-lookup"><span data-stu-id="eaf39-148">Tap on your user name, which activates the `Index` action method in Manage controller.</span></span> <span data-ttu-id="eaf39-149">然后点击的电话号码**添加**链接。</span><span class="sxs-lookup"><span data-stu-id="eaf39-149">Then tap the phone number **Add** link.</span></span>

![管理视图-点击"添加"链接](2fa/_static/login2fa2.png)

* <span data-ttu-id="eaf39-151">添加电话号码，它将接收验证代码，并点击**发送验证码**。</span><span class="sxs-lookup"><span data-stu-id="eaf39-151">Add a phone number that will receive the verification code, and tap **Send verification code**.</span></span>

![添加电话号码页](2fa/_static/login2fa3.png)

* <span data-ttu-id="eaf39-153">则会使用验证码的短信。</span><span class="sxs-lookup"><span data-stu-id="eaf39-153">You will get a text message with the verification code.</span></span> <span data-ttu-id="eaf39-154">输入它，然后点击**提交**</span><span class="sxs-lookup"><span data-stu-id="eaf39-154">Enter it and tap **Submit**</span></span>

![验证电话号码页](2fa/_static/login2fa4.png)

<span data-ttu-id="eaf39-156">如果没有收到短信，请参阅 twilio 日志页。</span><span class="sxs-lookup"><span data-stu-id="eaf39-156">If you don't get a text message, see twilio log page.</span></span>

* <span data-ttu-id="eaf39-157">管理视图显示已成功添加你的电话号码。</span><span class="sxs-lookup"><span data-stu-id="eaf39-157">The Manage view shows your phone number was added successfully.</span></span>

![管理视图-已成功添加电话号码](2fa/_static/login2fa5.png)

* <span data-ttu-id="eaf39-159">点击**启用**若要启用双因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="eaf39-159">Tap **Enable** to enable two-factor authentication.</span></span>

![管理视图： 启用双因素身份验证](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a><span data-ttu-id="eaf39-161">测试双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="eaf39-161">Test two-factor authentication</span></span>

* <span data-ttu-id="eaf39-162">注销。</span><span class="sxs-lookup"><span data-stu-id="eaf39-162">Log off.</span></span>

* <span data-ttu-id="eaf39-163">登录。</span><span class="sxs-lookup"><span data-stu-id="eaf39-163">Log in.</span></span>

* <span data-ttu-id="eaf39-164">用户帐户已启用双因素身份验证，因此你必须提供身份验证的第二个因素。</span><span class="sxs-lookup"><span data-stu-id="eaf39-164">The user account has enabled two-factor authentication, so you have to provide the second factor of authentication .</span></span> <span data-ttu-id="eaf39-165">在本教程中已启用电话验证。</span><span class="sxs-lookup"><span data-stu-id="eaf39-165">In this tutorial you have enabled phone verification.</span></span> <span data-ttu-id="eaf39-166">内置的模板还可以设置电子邮件作为第二个因素。</span><span class="sxs-lookup"><span data-stu-id="eaf39-166">The built in templates also allow you to set up email as the second factor.</span></span> <span data-ttu-id="eaf39-167">您可以设置其他身份验证的 QR 代码如第二个因素。</span><span class="sxs-lookup"><span data-stu-id="eaf39-167">You can set up additional second factors for authentication such as QR codes.</span></span> <span data-ttu-id="eaf39-168">点击**提交**。</span><span class="sxs-lookup"><span data-stu-id="eaf39-168">Tap **Submit**.</span></span>

![发送验证代码视图](2fa/_static/login2fa7.png)

* <span data-ttu-id="eaf39-170">输入你将获得的 SMS 消息中的代码。</span><span class="sxs-lookup"><span data-stu-id="eaf39-170">Enter the code you get in the SMS message.</span></span>

* <span data-ttu-id="eaf39-171">单击**记住此浏览器**复选框将免除你无需使用 2FA 登录时使用相同的设备和浏览器。</span><span class="sxs-lookup"><span data-stu-id="eaf39-171">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on when using the same device and browser.</span></span> <span data-ttu-id="eaf39-172">启用 2FA，并单击**记住此浏览器**将为您提供强 2FA 保护免受恶意用户尝试访问你的帐户，只要它们不能访问你的设备。</span><span class="sxs-lookup"><span data-stu-id="eaf39-172">Enabling 2FA and clicking on **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your device.</span></span> <span data-ttu-id="eaf39-173">可以在您经常使用任何专用设备上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="eaf39-173">You can do this on any private device you regularly use.</span></span> <span data-ttu-id="eaf39-174">通过设置**记住此浏览器**，请从设备不经常使用的情况下，获取 2FA 提高的安全性，您可以方便地在无需在自己的设备上经过 2FA。</span><span class="sxs-lookup"><span data-stu-id="eaf39-174">By setting  **Remember this browser**, you get the added security of 2FA from devices you don't regularly use, and you get the convenience on not having to go through 2FA on your own devices.</span></span>

![验证视图](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a><span data-ttu-id="eaf39-176">用于防范暴力破解攻击的帐户锁定</span><span class="sxs-lookup"><span data-stu-id="eaf39-176">Account lockout for protecting against brute force attacks</span></span>

<span data-ttu-id="eaf39-177">帐户锁定，建议使用 2FA。</span><span class="sxs-lookup"><span data-stu-id="eaf39-177">Account lockout is recommended with 2FA.</span></span> <span data-ttu-id="eaf39-178">用户登录后通过本地帐户或社交帐户，存储在 2FA 每次失败的尝试。</span><span class="sxs-lookup"><span data-stu-id="eaf39-178">Once a user signs in through a local account or social account, each failed attempt at 2FA is stored.</span></span> <span data-ttu-id="eaf39-179">如果达到最大的失败的访问尝试，则用户锁定 (默认值：5 分钟后锁定 5 失败访问尝试）。</span><span class="sxs-lookup"><span data-stu-id="eaf39-179">If the maximum failed access attempts is reached, the user is locked out (default: 5 minute lockout after 5 failed access attempts).</span></span> <span data-ttu-id="eaf39-180">成功的身份验证失败的访问尝试计数重置并重置时钟。</span><span class="sxs-lookup"><span data-stu-id="eaf39-180">A successful authentication resets the failed access attempts count and resets the clock.</span></span> <span data-ttu-id="eaf39-181">最大失败访问尝试，可使用设置锁定时间[MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts)并[DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan)。</span><span class="sxs-lookup"><span data-stu-id="eaf39-181">The maximum failed access attempts and lockout time can be set with [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) and [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span></span> <span data-ttu-id="eaf39-182">以下 10 分钟后访问尝试失败 10 次配置帐户锁定：</span><span class="sxs-lookup"><span data-stu-id="eaf39-182">The following configures account lockout for 10 minutes after 10 failed access attempts:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

<span data-ttu-id="eaf39-183">确认[PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync)设置`lockoutOnFailure`到`true`:</span><span class="sxs-lookup"><span data-stu-id="eaf39-183">Confirm that [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) sets `lockoutOnFailure` to `true`:</span></span>

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
