---
title: 使用 WS 联合身份验证在 ASP.NET 核心中的用户进行身份验证
author: chlowell
description: 本教程演示如何在 ASP.NET Core 应用程序使用 WS 联合身份验证。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/27/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/ws-federation
ms.openlocfilehash: d4621c7b97678903b9f2562e353da3883334b599
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30898799"
---
# <a name="authenticate-users-with-ws-federation-in-aspnet-core"></a><span data-ttu-id="ffabd-103">使用 WS 联合身份验证在 ASP.NET 核心中的用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="ffabd-103">Authenticate users with WS-Federation in ASP.NET Core</span></span>

<span data-ttu-id="ffabd-104">本教程演示如何使用户能够使用 WS 联合身份验证提供程序 (如 Active Directory 联合身份验证服务 (ADFS) 登录或[Azure Active Directory](/azure/active-directory/) (AAD)。</span><span class="sxs-lookup"><span data-stu-id="ffabd-104">This tutorial demonstrates how to enable users to sign in with a WS-Federation authentication provider like Active Directory Federation Services (ADFS) or [Azure Active Directory](/azure/active-directory/) (AAD).</span></span> <span data-ttu-id="ffabd-105">它使用 ASP.NET 核心 2.0 示例应用程序中所述[Facebook、 Google、 和外部提供程序身份验证](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="ffabd-105">It uses the ASP.NET Core 2.0 sample app described in [Facebook, Google, and external provider authentication](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="ffabd-106">对于 ASP.NET 核心 2.0 应用程序中，WS 联合身份验证的支持由提供[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation)。</span><span class="sxs-lookup"><span data-stu-id="ffabd-106">For ASP.NET Core 2.0 apps, WS-Federation support is provided by [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation).</span></span> <span data-ttu-id="ffabd-107">此组件移植从[Microsoft.Owin.Security.WsFederation](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation)和共享许多该组件的机制。</span><span class="sxs-lookup"><span data-stu-id="ffabd-107">This component is ported from [Microsoft.Owin.Security.WsFederation](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) and shares many of that component's mechanics.</span></span> <span data-ttu-id="ffabd-108">但是，组件的几个重要方面不同。</span><span class="sxs-lookup"><span data-stu-id="ffabd-108">However, the components differ in a couple of important ways.</span></span>

<span data-ttu-id="ffabd-109">默认情况下，新的中间件：</span><span class="sxs-lookup"><span data-stu-id="ffabd-109">By default, the new middleware:</span></span>

* <span data-ttu-id="ffabd-110">不允许未经请求的登录名。</span><span class="sxs-lookup"><span data-stu-id="ffabd-110">Doesn't allow unsolicited logins.</span></span> <span data-ttu-id="ffabd-111">这一功能的 WS 联合身份验证协议容易受到 XSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="ffabd-111">This feature of the WS-Federation protocol is vulnerable to XSRF attacks.</span></span> <span data-ttu-id="ffabd-112">但是，可以使用启用此`AllowUnsolicitedLogins`选项。</span><span class="sxs-lookup"><span data-stu-id="ffabd-112">However, it can be enabled with the `AllowUnsolicitedLogins` option.</span></span>
* <span data-ttu-id="ffabd-113">不会检查消息登录的每个窗体发布请求。</span><span class="sxs-lookup"><span data-stu-id="ffabd-113">Doesn't check every form post for sign-in messages.</span></span> <span data-ttu-id="ffabd-114">只请求在到`CallbackPath`登录程序。 检查`CallbackPath`默认为`/signin-wsfed`但可以更改。</span><span class="sxs-lookup"><span data-stu-id="ffabd-114">Only requests to the `CallbackPath` are checked for sign-ins. `CallbackPath` defaults to `/signin-wsfed` but can be changed.</span></span> <span data-ttu-id="ffabd-115">此路径可以与其他身份验证提供程序共享通过启用`SkipUnrecognizedRequests`选项。</span><span class="sxs-lookup"><span data-stu-id="ffabd-115">This path can be shared with other authentication providers by enabling the `SkipUnrecognizedRequests` option.</span></span>

## <a name="register-the-app-with-active-directory"></a><span data-ttu-id="ffabd-116">向 Active Directory 注册应用程序</span><span class="sxs-lookup"><span data-stu-id="ffabd-116">Register the app with Active Directory</span></span>

### <a name="active-directory-federation-services"></a><span data-ttu-id="ffabd-117">Active Directory 联合身份验证服务</span><span class="sxs-lookup"><span data-stu-id="ffabd-117">Active Directory Federation Services</span></span>

* <span data-ttu-id="ffabd-118">打开服务器的**添加信赖方信任向导**从 ADFS 管理控制台：</span><span class="sxs-lookup"><span data-stu-id="ffabd-118">Open the server's **Add Relying Party Trust Wizard** from the ADFS Management console:</span></span>

![添加信赖方信任向导： 欢迎](ws-federation/_static/AdfsAddTrust.png)

* <span data-ttu-id="ffabd-120">选择了手动输入数据：</span><span class="sxs-lookup"><span data-stu-id="ffabd-120">Choose to enter data manually:</span></span>

![添加信赖方信任向导： 选择数据源](ws-federation/_static/AdfsSelectDataSource.png)

* <span data-ttu-id="ffabd-122">输入信赖方的显示名称。</span><span class="sxs-lookup"><span data-stu-id="ffabd-122">Enter a display name for the relying party.</span></span> <span data-ttu-id="ffabd-123">名称并不重要到 ASP.NET 核心应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffabd-123">The name isn't important to the ASP.NET Core app.</span></span>

* <span data-ttu-id="ffabd-124">[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation)缺少用于令牌加密，因此未配置令牌加密证书的支持：</span><span class="sxs-lookup"><span data-stu-id="ffabd-124">[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) lacks support for token encryption, so don't configure a token encryption certificate:</span></span>

![添加信赖方信任向导： 配置证书](ws-federation/_static/AdfsConfigureCert.png)

* <span data-ttu-id="ffabd-126">启用支持 WS 联合身份验证被动协议，使用应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="ffabd-126">Enable support for WS-Federation Passive protocol, using the app's URL.</span></span> <span data-ttu-id="ffabd-127">验证端口正确应用：</span><span class="sxs-lookup"><span data-stu-id="ffabd-127">Verify the port is correct for the app:</span></span>

![添加信赖方信任向导： 配置 URL](ws-federation/_static/AdfsConfigureUrl.png)

> [!NOTE]
> <span data-ttu-id="ffabd-129">这必须是 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="ffabd-129">This must be an HTTPS URL.</span></span> <span data-ttu-id="ffabd-130">在开发期间托管应用程序时，IIS Express 可以提供自签名的证书。</span><span class="sxs-lookup"><span data-stu-id="ffabd-130">IIS Express can provide a self-signed certificate when hosting the app during development.</span></span> <span data-ttu-id="ffabd-131">Kestrel 需要手动证书配置。</span><span class="sxs-lookup"><span data-stu-id="ffabd-131">Kestrel requires manual certificate configuration.</span></span> <span data-ttu-id="ffabd-132">请参阅[Kestrel 文档](xref:fundamentals/servers/kestrel)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="ffabd-132">See the [Kestrel documentation](xref:fundamentals/servers/kestrel) for more details.</span></span>

* <span data-ttu-id="ffabd-133">单击**下一步**完成该向导的其余部分和**关闭**末尾。</span><span class="sxs-lookup"><span data-stu-id="ffabd-133">Click **Next** through the rest of the wizard and **Close** at the end.</span></span>

* <span data-ttu-id="ffabd-134">ASP.NET 核心标识需要**名称 ID**声明。</span><span class="sxs-lookup"><span data-stu-id="ffabd-134">ASP.NET Core Identity requires a **Name ID** claim.</span></span> <span data-ttu-id="ffabd-135">添加一个从**编辑声明规则**对话框：</span><span class="sxs-lookup"><span data-stu-id="ffabd-135">Add one from the **Edit Claim Rules** dialog:</span></span>

![编辑声明规则](ws-federation/_static/EditClaimRules.png)

* <span data-ttu-id="ffabd-137">在**添加转换声明规则向导**，保留默认**以声明方式发送 LDAP 属性**选择的模板，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ffabd-137">In the **Add Transform Claim Rule Wizard**, leave the default **Send LDAP Attributes as Claims** template selected, and click **Next**.</span></span> <span data-ttu-id="ffabd-138">添加规则映射**SAM 帐户名**LDAP 属性到**名称 ID**传出声明：</span><span class="sxs-lookup"><span data-stu-id="ffabd-138">Add a rule mapping the **SAM-Account-Name** LDAP attribute to the **Name ID** outgoing claim:</span></span>

![添加转换声明规则向导： 配置声明规则](ws-federation/_static/AddTransformClaimRule.png)

* <span data-ttu-id="ffabd-140">单击**完成** > **确定**中**编辑声明规则**窗口。</span><span class="sxs-lookup"><span data-stu-id="ffabd-140">Click **Finish** > **OK** in the **Edit Claim Rules** window.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="ffabd-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffabd-141">Azure Active Directory</span></span>

* <span data-ttu-id="ffabd-142">导航到 AAD 租户的应用注册边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffabd-142">Navigate to the AAD tenant's app registrations blade.</span></span> <span data-ttu-id="ffabd-143">单击**新应用程序注册**:</span><span class="sxs-lookup"><span data-stu-id="ffabd-143">Click **New application registration**:</span></span>

![Azure Active Directory： 应用程序注册](ws-federation/_static/AadNewAppRegistration.png)

* <span data-ttu-id="ffabd-145">输入应用程序注册的名称。</span><span class="sxs-lookup"><span data-stu-id="ffabd-145">Enter a name for the app registration.</span></span> <span data-ttu-id="ffabd-146">这并不重要到 ASP.NET 核心应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffabd-146">This isn't important to the ASP.NET Core app.</span></span>
* <span data-ttu-id="ffabd-147">输入作为侦听的应用程序的 URL**登录 URL**:</span><span class="sxs-lookup"><span data-stu-id="ffabd-147">Enter the URL the app listens on as the **Sign-on URL**:</span></span>

![Azure Active Directory： 创建应用程序注册](ws-federation/_static/AadCreateAppRegistration.png)

* <span data-ttu-id="ffabd-149">单击**终结点**并记下**联合元数据文档**URL。</span><span class="sxs-lookup"><span data-stu-id="ffabd-149">Click **Endpoints** and note the **Federation Metadata Document** URL.</span></span> <span data-ttu-id="ffabd-150">这是 WS 联合身份验证中间件的`MetadataAddress`:</span><span class="sxs-lookup"><span data-stu-id="ffabd-150">This is the WS-Federation middleware's `MetadataAddress`:</span></span>

![Azure Active Directory： 终结点](ws-federation/_static/AadFederationMetadataDocument.png)

* <span data-ttu-id="ffabd-152">导航到新的应用程序注册。</span><span class="sxs-lookup"><span data-stu-id="ffabd-152">Navigate to the new app registration.</span></span> <span data-ttu-id="ffabd-153">单击**设置** > **属性**并记下**应用程序 ID URI**。</span><span class="sxs-lookup"><span data-stu-id="ffabd-153">Click **Settings** > **Properties** and make note of the **App ID URI**.</span></span> <span data-ttu-id="ffabd-154">这是 WS 联合身份验证中间件的`Wtrealm`:</span><span class="sxs-lookup"><span data-stu-id="ffabd-154">This is the WS-Federation middleware's `Wtrealm`:</span></span>

![Azure Active Directory： 应用程序注册属性](ws-federation/_static/AadAppIdUri.png)

## <a name="add-ws-federation-as-an-external-login-provider-for-aspnet-core-identity"></a><span data-ttu-id="ffabd-156">为 ASP.NET 核心标识的外部登录提供程序中添加 WS 联合身份验证</span><span class="sxs-lookup"><span data-stu-id="ffabd-156">Add WS-Federation as an external login provider for ASP.NET Core Identity</span></span>

* <span data-ttu-id="ffabd-157">添加的依赖项[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation)到项目。</span><span class="sxs-lookup"><span data-stu-id="ffabd-157">Add a dependency on [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) to the project.</span></span>
* <span data-ttu-id="ffabd-158">添加 WS 联合身份验证到`Configure`中的方法*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="ffabd-158">Add WS-Federation to the `Configure` method in *Startup.cs*:</span></span>

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddAuthentication()
        .AddWsFederation(options =>
        {
            // MetadataAddress represents the Active Directory instance used to authenticate users.
            options.MetadataAddress = "https://<ADFS FQDN or AAD tenant>/FederationMetadata/2007-06/FederationMetadata.xml";

            // Wtrealm is the app's identifier in the Active Directory instance.
            // For ADFS, use the relying party's identifier, its WS-Federation Passive protocol URL:
            options.Wtrealm = "https://localhost:44307/";

            // For AAD, use the App ID URI from the app registration's Properties blade:
            options.Wtrealm = "https://wsfedsample.onmicrosoft.com/bf0e7e6d-056e-4e37-b9a6-2c36797b9f01";
        });

    services.AddMvc()
     // ...
    ```

[!INCLUDE [default settings configuration](social/includes/default-settings.md)]

### <a name="log-in-with-ws-federation"></a><span data-ttu-id="ffabd-159">使用 WS 联合身份验证登录</span><span class="sxs-lookup"><span data-stu-id="ffabd-159">Log in with WS-Federation</span></span>

<span data-ttu-id="ffabd-160">浏览到应用程序并单击**登录**nav 标头中的链接。</span><span class="sxs-lookup"><span data-stu-id="ffabd-160">Browse to the app and click the **Log in** link in the nav header.</span></span> <span data-ttu-id="ffabd-161">没有用于登录 WsFederation 选项：![登录页](ws-federation/_static/WsFederationButton.png)</span><span class="sxs-lookup"><span data-stu-id="ffabd-161">There's an option to log in with WsFederation: ![Log in page](ws-federation/_static/WsFederationButton.png)</span></span>

<span data-ttu-id="ffabd-162">使用作为提供程序的 ADFS，按钮将重定向到 ADFS 登录页： ![ADFS 登录页](ws-federation/_static/AdfsLoginPage.png)</span><span class="sxs-lookup"><span data-stu-id="ffabd-162">With ADFS as the provider, the button redirects to an ADFS sign-in page: ![ADFS sign-in page](ws-federation/_static/AdfsLoginPage.png)</span></span>

<span data-ttu-id="ffabd-163">与 Azure Active Directory 作为提供程序，该按钮将重定向到 AAD 登录页： ![AAD 登录页](ws-federation/_static/AadSignIn.png)</span><span class="sxs-lookup"><span data-stu-id="ffabd-163">With Azure Active Directory as the provider, the button redirects to an AAD sign-in page: ![AAD sign-in page](ws-federation/_static/AadSignIn.png)</span></span>

<span data-ttu-id="ffabd-164">成功登录的新用户将重定向到应用程序的用户注册页：![注册页](ws-federation/_static/Register.png)</span><span class="sxs-lookup"><span data-stu-id="ffabd-164">A successful sign-in for a new user redirects to the app's user registration page: ![Register page](ws-federation/_static/Register.png)</span></span>

## <a name="use-ws-federation-without-aspnet-core-identity"></a><span data-ttu-id="ffabd-165">使用 WS 联合身份验证而无需 ASP.NET 核心标识</span><span class="sxs-lookup"><span data-stu-id="ffabd-165">Use WS-Federation without ASP.NET Core Identity</span></span>

<span data-ttu-id="ffabd-166">没有标识，可以使用 WS 联合身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="ffabd-166">The WS-Federation middleware can be used without Identity.</span></span> <span data-ttu-id="ffabd-167">例如：</span><span class="sxs-lookup"><span data-stu-id="ffabd-167">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(sharedOptions =>
    {
        sharedOptions.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultSignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultChallengeScheme = WsFederationDefaults.AuthenticationScheme;
    })
    .AddWsFederation(options =>
    {
        options.Wtrealm = Configuration["wsfed:realm"];
        options.MetadataAddress = Configuration["wsfed:metadata"];
    })
    .AddCookie();
}

public void Configure(IApplicationBuilder app)
{
    app.UseAuthentication();
        // …
}
```
