---
title: 将身份验证和标识迁移到 ASP.NET 核心 2.0
author: scottaddie
description: 本文概述了迁移 ASP.NET Core 1.x 身份验证和标识为 ASP.NET 核心 2.0 的最常见步骤。
ms.author: scaddie
ms.date: 10/26/2017
uid: migration/1x-to-2x/identity-2x
ms.openlocfilehash: 0485b1bdf8be550de35a49803a24666c026b3d9b
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276414"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core-20"></a><span data-ttu-id="9e4e7-103">将身份验证和标识迁移到 ASP.NET 核心 2.0</span><span class="sxs-lookup"><span data-stu-id="9e4e7-103">Migrate authentication and Identity to ASP.NET Core 2.0</span></span>

<span data-ttu-id="9e4e7-104">通过[Scott Addie](https://github.com/scottaddie)和[Hao 永远](https://github.com/HaoK)</span><span class="sxs-lookup"><span data-stu-id="9e4e7-104">By [Scott Addie](https://github.com/scottaddie) and [Hao Kung](https://github.com/HaoK)</span></span>

<span data-ttu-id="9e4e7-105">ASP.NET 核心 2.0 具有用于身份验证的新模型和[标识](xref:security/authentication/identity)这简化了使用服务的配置。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-105">ASP.NET Core 2.0 has a new model for authentication and [Identity](xref:security/authentication/identity) which simplifies configuration by using services.</span></span> <span data-ttu-id="9e4e7-106">ASP.NET 核心 1.x 应用程序使用身份验证或标识可以更新以使用新的模型，如下所述。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-106">ASP.NET Core 1.x applications that use authentication or Identity can be updated to use the new model as outlined below.</span></span>

<a name="auth-middleware"></a>

## <a name="authentication-middleware-and-services"></a><span data-ttu-id="9e4e7-107">身份验证中间件和服务</span><span class="sxs-lookup"><span data-stu-id="9e4e7-107">Authentication Middleware and services</span></span>
<span data-ttu-id="9e4e7-108">在 1.x 项目中，通过中间件配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-108">In 1.x projects, authentication is configured via middleware.</span></span> <span data-ttu-id="9e4e7-109">中间件方法调用每个你想要支持的身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-109">A middleware method is invoked for each authentication scheme you want to support.</span></span>

<span data-ttu-id="9e4e7-110">下面的 1.x 示例将 Facebook 身份验证配置中标识*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-110">The following 1.x example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory)
{
    app.UseIdentity();
    app.UseFacebookAuthentication(new FacebookOptions { 
        AppId = Configuration["auth:facebook:appid"],
        AppSecret = Configuration["auth:facebook:appsecret"]
    });
} 
```

<span data-ttu-id="9e4e7-111">在 2.0 项目中，通过服务配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-111">In 2.0 projects, authentication is configured via services.</span></span> <span data-ttu-id="9e4e7-112">在中注册每个身份验证方案`ConfigureServices`方法*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-112">Each authentication scheme is registered in the `ConfigureServices` method of *Startup.cs*.</span></span> <span data-ttu-id="9e4e7-113">`UseIdentity`方法将替换`UseAuthentication`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-113">The `UseIdentity` method is replaced with `UseAuthentication`.</span></span>

<span data-ttu-id="9e4e7-114">下面的 2.0 示例将 Facebook 身份验证配置中标识*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-114">The following 2.0 example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();

    // If you want to tweak Identity cookies, they're no longer part of IdentityOptions.
    services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory) {
    app.UseAuthentication();
}
```

<span data-ttu-id="9e4e7-115">`UseAuthentication`方法将添加一个单一的身份验证中间件组件，它负责自动身份验证和远程身份验证请求的处理。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-115">The `UseAuthentication` method adds a single authentication middleware component which is responsible for automatic authentication and the handling of remote authentication requests.</span></span> <span data-ttu-id="9e4e7-116">它将替换所有单独的中间件组件与单个，常见的中间件组件。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-116">It replaces all of the individual middleware components with a single, common middleware component.</span></span>

<span data-ttu-id="9e4e7-117">以下是每个主要身份验证方案的 2.0 迁移说明。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-117">Below are 2.0 migration instructions for each major authentication scheme.</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="9e4e7-118">基于 cookie 的身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-118">Cookie-based authentication</span></span>
<span data-ttu-id="9e4e7-119">选择以下两个选项之一，然后进行必要的更改在*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-119">Select one of the two options below, and make the necessary changes in *Startup.cs*:</span></span>

1. <span data-ttu-id="9e4e7-120">标识与使用 cookie</span><span class="sxs-lookup"><span data-stu-id="9e4e7-120">Use cookies with Identity</span></span>
    - <span data-ttu-id="9e4e7-121">替换`UseIdentity`与`UseAuthentication`中`Configure`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-121">Replace `UseIdentity` with `UseAuthentication` in the `Configure` method:</span></span>

        ```csharp
        app.UseAuthentication();
        ```

    - <span data-ttu-id="9e4e7-122">调用`AddIdentity`中的方法`ConfigureServices`方法将添加 cookie 身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-122">Invoke the `AddIdentity` method in the `ConfigureServices` method to add the cookie authentication services.</span></span>
    - <span data-ttu-id="9e4e7-123">（可选） 调用`ConfigureApplicationCookie`或`ConfigureExternalCookie`中的方法`ConfigureServices`方法来调整标识 cookie 设置。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-123">Optionally, invoke the `ConfigureApplicationCookie` or `ConfigureExternalCookie` method in the `ConfigureServices` method to tweak the Identity cookie settings.</span></span>

        ```csharp
        services.AddIdentity<ApplicationUser, IdentityRole>()
                .AddEntityFrameworkStores<ApplicationDbContext>()
                .AddDefaultTokenProviders();
    
        services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
        ```

2. <span data-ttu-id="9e4e7-124">使用 cookie，而无需标识</span><span class="sxs-lookup"><span data-stu-id="9e4e7-124">Use cookies without Identity</span></span>
    - <span data-ttu-id="9e4e7-125">替换`UseCookieAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-125">Replace the `UseCookieAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
  
        ```csharp
        app.UseAuthentication();
        ```
 
    - <span data-ttu-id="9e4e7-126">调用`AddAuthentication`和`AddCookie`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-126">Invoke the `AddAuthentication` and `AddCookie` methods in the `ConfigureServices` method:</span></span>

        ```csharp
        // If you don't want the cookie to be automatically authenticated and assigned to HttpContext.User, 
        // remove the CookieAuthenticationDefaults.AuthenticationScheme parameter passed to AddAuthentication.
        services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
                .AddCookie(options => 
                {
                    options.LoginPath = "/Account/LogIn";
                    options.LogoutPath = "/Account/LogOff";
                });
        ```

### <a name="jwt-bearer-authentication"></a><span data-ttu-id="9e4e7-127">JWT 持有者身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-127">JWT Bearer Authentication</span></span>
<span data-ttu-id="9e4e7-128">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-128">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9e4e7-129">替换`UseJwtBearerAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-129">Replace the `UseJwtBearerAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-130">调用`AddJwtBearer`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-130">Invoke the `AddJwtBearer` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddJwtBearer(options => 
            {
                options.Audience = "http://localhost:5001/";
                options.Authority = "http://localhost:5000/";
            });
    ```

    <span data-ttu-id="9e4e7-131">此代码段不使用标识，因此应通过将传递设置的默认方案`JwtBearerDefaults.AuthenticationScheme`到`AddAuthentication`方法。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-131">This code snippet doesn't use Identity, so the default scheme should be set by passing `JwtBearerDefaults.AuthenticationScheme` to the `AddAuthentication` method.</span></span>

### <a name="openid-connect-oidc-authentication"></a><span data-ttu-id="9e4e7-132">OpenID 连接 (OIDC) 身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-132">OpenID Connect (OIDC) authentication</span></span>
<span data-ttu-id="9e4e7-133">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-133">Make the following changes in *Startup.cs*:</span></span>

- <span data-ttu-id="9e4e7-134">替换`UseOpenIdConnectAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-134">Replace the `UseOpenIdConnectAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-135">调用`AddOpenIdConnect`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-135">Invoke the `AddOpenIdConnect` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(options => 
    {
        options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
    })
    .AddCookie()
    .AddOpenIdConnect(options => 
    {
        options.Authority = Configuration["auth:oidc:authority"];
        options.ClientId = Configuration["auth:oidc:clientid"];
    });
    ```

### <a name="facebook-authentication"></a><span data-ttu-id="9e4e7-136">facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-136">Facebook authentication</span></span>
<span data-ttu-id="9e4e7-137">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-137">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9e4e7-138">替换`UseFacebookAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-138">Replace the `UseFacebookAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-139">调用`AddFacebook`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-139">Invoke the `AddFacebook` method in the `ConfigureServices` method:</span></span>
    
    ```csharp
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
    ```

### <a name="google-authentication"></a><span data-ttu-id="9e4e7-140">Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-140">Google authentication</span></span>
<span data-ttu-id="9e4e7-141">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-141">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9e4e7-142">替换`UseGoogleAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-142">Replace the `UseGoogleAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-143">调用`AddGoogle`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-143">Invoke the `AddGoogle` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddGoogle(options => 
            {
                options.ClientId = Configuration["auth:google:clientid"];
                options.ClientSecret = Configuration["auth:google:clientsecret"];
            });    
    ```

### <a name="microsoft-account-authentication"></a><span data-ttu-id="9e4e7-144">Microsoft 帐户身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-144">Microsoft Account authentication</span></span>
<span data-ttu-id="9e4e7-145">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-145">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9e4e7-146">替换`UseMicrosoftAccountAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-146">Replace the `UseMicrosoftAccountAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-147">调用`AddMicrosoftAccount`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-147">Invoke the `AddMicrosoftAccount` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddMicrosoftAccount(options => 
            {
                options.ClientId = Configuration["auth:microsoft:clientid"];
                options.ClientSecret = Configuration["auth:microsoft:clientsecret"];
            });
    ``` 

### <a name="twitter-authentication"></a><span data-ttu-id="9e4e7-148">Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="9e4e7-148">Twitter authentication</span></span>
<span data-ttu-id="9e4e7-149">进行中的以下更改*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-149">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9e4e7-150">替换`UseTwitterAuthentication`方法调用`Configure`方法替换`UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-150">Replace the `UseTwitterAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9e4e7-151">调用`AddTwitter`中的方法`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-151">Invoke the `AddTwitter` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddTwitter(options => 
            {
                options.ConsumerKey = Configuration["auth:twitter:consumerkey"];
                options.ConsumerSecret = Configuration["auth:twitter:consumersecret"];
            });
    ```

### <a name="setting-default-authentication-schemes"></a><span data-ttu-id="9e4e7-152">设置默认身份验证方案</span><span class="sxs-lookup"><span data-stu-id="9e4e7-152">Setting default authentication schemes</span></span>
<span data-ttu-id="9e4e7-153">在 1.x`AutomaticAuthenticate`和`AutomaticChallenge`属性[AuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1)基类用于设置在单一身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-153">In 1.x, the `AutomaticAuthenticate` and `AutomaticChallenge` properties of the [AuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1) base class were intended to be set on a single authentication scheme.</span></span> <span data-ttu-id="9e4e7-154">没有良好方法来强制执行此。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-154">There was no good way to enforce this.</span></span>

<span data-ttu-id="9e4e7-155">在 2.0 中，这两个属性已删除作为属性对各个`AuthenticationOptions`实例。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-155">In 2.0, these two properties have been removed as properties on the individual `AuthenticationOptions` instance.</span></span> <span data-ttu-id="9e4e7-156">它们可以在中配置`AddAuthentication`内的方法调用`ConfigureServices`方法*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-156">They can be configured in the `AddAuthentication` method call within the `ConfigureServices` method of *Startup.cs*:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme);
```

<span data-ttu-id="9e4e7-157">在前面的代码段中，默认方案设置为`CookieAuthenticationDefaults.AuthenticationScheme`("Cookie")。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-157">In the preceding code snippet, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme` ("Cookies").</span></span>

<span data-ttu-id="9e4e7-158">或者，使用一个重载的版本的`AddAuthentication`方法以设置多个属性。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-158">Alternatively, use an overloaded version of the `AddAuthentication` method to set more than one property.</span></span> <span data-ttu-id="9e4e7-159">在下面的重载的方法示例中，默认方案设置为`CookieAuthenticationDefaults.AuthenticationScheme`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-159">In the following overloaded method example, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme`.</span></span> <span data-ttu-id="9e4e7-160">或者可能在个人中指定的身份验证方案`[Authorize]`属性或授权策略。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-160">The authentication scheme may alternatively be specified within your individual `[Authorize]` attributes or authorization policies.</span></span>

```csharp
services.AddAuthentication(options => 
{
    options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
});
```

<span data-ttu-id="9e4e7-161">如果下列条件之一为 true，请在 2.0 中定义了默认的方案：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-161">Define a default scheme in 2.0 if one of the following conditions is true:</span></span>
- <span data-ttu-id="9e4e7-162">你希望用户可自动登录</span><span class="sxs-lookup"><span data-stu-id="9e4e7-162">You want the user to be automatically signed in</span></span>
- <span data-ttu-id="9e4e7-163">你使用`[Authorize]`而无需指定方案的属性或授权策略</span><span class="sxs-lookup"><span data-stu-id="9e4e7-163">You use the `[Authorize]` attribute or authorization policies without specifying schemes</span></span>

<span data-ttu-id="9e4e7-164">此规则的唯一例外是`AddIdentity`方法。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-164">An exception to this rule is the `AddIdentity` method.</span></span> <span data-ttu-id="9e4e7-165">此方法将为您和设置默认值进行身份验证以及与应用程序 cookie 质询方案添加 cookie `IdentityConstants.ApplicationScheme`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-165">This method adds cookies for you and sets the default authenticate and challenge schemes to the application cookie `IdentityConstants.ApplicationScheme`.</span></span> <span data-ttu-id="9e4e7-166">此外，它将默认登录方案设置为外部 cookie `IdentityConstants.ExternalScheme`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-166">Additionally, it sets the default sign-in scheme to the external cookie `IdentityConstants.ExternalScheme`.</span></span>

<a name="obsolete-interface"></a>

## <a name="use-httpcontext-authentication-extensions"></a><span data-ttu-id="9e4e7-167">使用 HttpContext 身份验证扩展插件</span><span class="sxs-lookup"><span data-stu-id="9e4e7-167">Use HttpContext authentication extensions</span></span>
<span data-ttu-id="9e4e7-168">`IAuthenticationManager`接口是 1.x 身份验证系统的主入口点。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-168">The `IAuthenticationManager` interface is the main entry point into the 1.x authentication system.</span></span> <span data-ttu-id="9e4e7-169">它已替换为一组新的`HttpContext`中的扩展方法`Microsoft.AspNetCore.Authentication`命名空间。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-169">It has been replaced with a new set of `HttpContext` extension methods in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

<span data-ttu-id="9e4e7-170">例如，1.x 项目引用`Authentication`属性：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-170">For example, 1.x projects reference an `Authentication` property:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<span data-ttu-id="9e4e7-171">在 2.0 项目中，导入`Microsoft.AspNetCore.Authentication`命名空间，并删除`Authentication`属性引用：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-171">In 2.0 projects, import the `Microsoft.AspNetCore.Authentication` namespace, and delete the `Authentication` property references:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="windows-auth-changes"></a>

## <a name="windows-authentication-httpsys--iisintegration"></a><span data-ttu-id="9e4e7-172">Windows 身份验证 (HTTP.sys / IISIntegration)</span><span class="sxs-lookup"><span data-stu-id="9e4e7-172">Windows Authentication (HTTP.sys / IISIntegration)</span></span>
<span data-ttu-id="9e4e7-173">有两种变体 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-173">There are two variations of Windows authentication:</span></span>
1. <span data-ttu-id="9e4e7-174">主机仅允许经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9e4e7-174">The host only allows authenticated users</span></span>
2. <span data-ttu-id="9e4e7-175">主机允许同时匿名和身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9e4e7-175">The host allows both anonymous and authenticated users</span></span>

<span data-ttu-id="9e4e7-176">上面所述的第一个变体不受 2.0 的更改。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-176">The first variation described above is unaffected by the 2.0 changes.</span></span>

<span data-ttu-id="9e4e7-177">2.0 更改的情况下，会影响上面所述的第二个变体。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-177">The second variation described above is affected by the 2.0 changes.</span></span> <span data-ttu-id="9e4e7-178">例如，你可能将以允许匿名用户到你的应用程序在 IIS 或[HTTP.sys](xref:fundamentals/servers/weblistener)层在控制器级别但授权用户。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-178">As an example, you may be allowing anonymous users into your application at the IIS or [HTTP.sys](xref:fundamentals/servers/weblistener) layer but authorizing users at the Controller level.</span></span> <span data-ttu-id="9e4e7-179">在此方案中，设置默认方案为`IISDefaults.AuthenticationScheme`中`ConfigureServices`方法*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-179">In this scenario, set the default scheme to `IISDefaults.AuthenticationScheme` in the `ConfigureServices` method of *Startup.cs*:</span></span>

```csharp
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

<span data-ttu-id="9e4e7-180">相应地，如果设置的默认方案会使质询无法正常工作的授权请求。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-180">Failure to set the default scheme accordingly prevents the authorize request to challenge from working.</span></span>

<a name="identity-cookie-options"></a>

## <a name="identitycookieoptions-instances"></a><span data-ttu-id="9e4e7-181">IdentityCookieOptions 实例</span><span class="sxs-lookup"><span data-stu-id="9e4e7-181">IdentityCookieOptions instances</span></span>
<span data-ttu-id="9e4e7-182">2.0 更改的副作用是时切换到使用名为而不是 cookie 选项实例的选项。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-182">A side effect of the 2.0 changes is the switch to using named options instead of cookie options instances.</span></span> <span data-ttu-id="9e4e7-183">删除自定义标识 cookie 方案名称的能力。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-183">The ability to customize the Identity cookie scheme names is removed.</span></span>

<span data-ttu-id="9e4e7-184">例如，1.x 项目使用[构造函数注入](xref:mvc/controllers/dependency-injection#constructor-injection)传递`IdentityCookieOptions`参数转换*AccountController.cs*。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-184">For example, 1.x projects use [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) to pass an `IdentityCookieOptions` parameter into *AccountController.cs*.</span></span> <span data-ttu-id="9e4e7-185">从提供的实例访问外部 cookie 身份验证方案：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-185">The external cookie authentication scheme is accessed from the provided instance:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor&highlight=4,11)]

<span data-ttu-id="9e4e7-186">前面提到的构造函数注入将成为在 2.0 项目中，不必要和`_externalCookieScheme`可以删除字段：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-186">The aforementioned constructor injection becomes unnecessary in 2.0 projects, and the `_externalCookieScheme` field can be deleted:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor)]

<span data-ttu-id="9e4e7-187">`IdentityConstants.ExternalScheme`可以直接使用常量：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-187">The `IdentityConstants.ExternalScheme` constant can be used directly:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="navigation-properties"></a>

## <a name="add-identityuser-poco-navigation-properties"></a><span data-ttu-id="9e4e7-188">添加 POCO IdentityUser 导航属性</span><span class="sxs-lookup"><span data-stu-id="9e4e7-188">Add IdentityUser POCO navigation properties</span></span>
<span data-ttu-id="9e4e7-189">基的 Entity Framework (EF) 核心导航属性`IdentityUser`POCO （普通旧 CLR 对象） 已被删除。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-189">The Entity Framework (EF) Core navigation properties of the base `IdentityUser` POCO (Plain Old CLR Object) have been removed.</span></span> <span data-ttu-id="9e4e7-190">如果你 1.x 的项目使用这些属性，手动将它们添加回 2.0 项目：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-190">If your 1.x project used these properties, manually add them back to the 2.0 project:</span></span>

```csharp
/// <summary>
/// Navigation property for the roles this user belongs to.
/// </summary>
public virtual ICollection<IdentityUserRole<int>> Roles { get; } = new List<IdentityUserRole<int>>();

/// <summary>
/// Navigation property for the claims this user possesses.
/// </summary>
public virtual ICollection<IdentityUserClaim<int>> Claims { get; } = new List<IdentityUserClaim<int>>();

/// <summary>
/// Navigation property for this users login accounts.
/// </summary>
public virtual ICollection<IdentityUserLogin<int>> Logins { get; } = new List<IdentityUserLogin<int>>();
```

<span data-ttu-id="9e4e7-191">若要防止重复的外键，运行 EF 核心迁移时，将以下代码添加到你`IdentityDbContext`类的`OnModelCreating`方法 (后`base.OnModelCreating();`调用):</span><span class="sxs-lookup"><span data-stu-id="9e4e7-191">To prevent duplicate foreign keys when running EF Core Migrations, add the following to your `IdentityDbContext` class' `OnModelCreating` method (after the `base.OnModelCreating();` call):</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder builder)
{
    base.OnModelCreating(builder);
    // Customize the ASP.NET Identity model and override the defaults if needed.
    // For example, you can rename the ASP.NET Identity table names and more.
    // Add your customizations after calling base.OnModelCreating(builder);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Claims)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Logins)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Roles)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);
}
```

<a name="synchronous-method-removal"></a>

## <a name="replace-getexternalauthenticationschemes"></a><span data-ttu-id="9e4e7-192">替换 GetExternalAuthenticationSchemes</span><span class="sxs-lookup"><span data-stu-id="9e4e7-192">Replace GetExternalAuthenticationSchemes</span></span>
<span data-ttu-id="9e4e7-193">同步方法`GetExternalAuthenticationSchemes`已删除为支持的异步版本。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-193">The synchronous method `GetExternalAuthenticationSchemes` was removed in favor of an asynchronous version.</span></span> <span data-ttu-id="9e4e7-194">1.x 项目有以下代码*ManageController.cs*:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-194">1.x projects have the following code in *ManageController.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemes)]

<span data-ttu-id="9e4e7-195">此方法将出现在*Login.cshtml*太：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-195">This method appears in *Login.cshtml* too:</span></span>

[!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Account/Login.cshtml?range=62,75-84)]

<span data-ttu-id="9e4e7-196">在 2.0 项目中，使用`GetExternalAuthenticationSchemesAsync`方法：</span><span class="sxs-lookup"><span data-stu-id="9e4e7-196">In 2.0 projects, use the `GetExternalAuthenticationSchemesAsync` method:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemesAsync)]

<span data-ttu-id="9e4e7-197">在*Login.cshtml*、`AuthenticationScheme`中访问属性`foreach`循环更改为`Name`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-197">In *Login.cshtml*, the `AuthenticationScheme` property accessed in the `foreach` loop changes to `Name`:</span></span>

[!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Views/Account/Login.cshtml?range=62,75-84)]

<a name="property-change"></a>

## <a name="manageloginsviewmodel-property-change"></a><span data-ttu-id="9e4e7-198">ManageLoginsViewModel 属性更改</span><span class="sxs-lookup"><span data-stu-id="9e4e7-198">ManageLoginsViewModel property change</span></span>
<span data-ttu-id="9e4e7-199">A`ManageLoginsViewModel`对象将用于`ManageLogins`操作*ManageController.cs*。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-199">A `ManageLoginsViewModel` object is used in the `ManageLogins` action of *ManageController.cs*.</span></span> <span data-ttu-id="9e4e7-200">1.x 项目，该对象中`OtherLogins`属性的返回类型是`IList<AuthenticationDescription>`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-200">In 1.x projects, the object's `OtherLogins` property return type is `IList<AuthenticationDescription>`.</span></span> <span data-ttu-id="9e4e7-201">此返回类型需要导入`Microsoft.AspNetCore.Http.Authentication`:</span><span class="sxs-lookup"><span data-stu-id="9e4e7-201">This return type requires an import of `Microsoft.AspNetCore.Http.Authentication`:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<span data-ttu-id="9e4e7-202">在 2.0 项目中，返回类型更改为`IList<AuthenticationScheme>`。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-202">In 2.0 projects, the return type changes to `IList<AuthenticationScheme>`.</span></span> <span data-ttu-id="9e4e7-203">此新的返回类型需要替换`Microsoft.AspNetCore.Http.Authentication`使用导入`Microsoft.AspNetCore.Authentication`导入。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-203">This new return type requires replacing the `Microsoft.AspNetCore.Http.Authentication` import with a `Microsoft.AspNetCore.Authentication` import.</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<a name="additional-resources"></a>

## <a name="additional-resources"></a><span data-ttu-id="9e4e7-204">其他资源</span><span class="sxs-lookup"><span data-stu-id="9e4e7-204">Additional resources</span></span>
<span data-ttu-id="9e4e7-205">有关其他详细信息和讨论，请参阅[针对身份验证 2.0 讨论](https://github.com/aspnet/Security/issues/1338)GitHub 上的问题。</span><span class="sxs-lookup"><span data-stu-id="9e4e7-205">For additional details and discussion, see the [Discussion for Auth 2.0](https://github.com/aspnet/Security/issues/1338) issue on GitHub.</span></span>
