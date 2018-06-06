---
title: 与 ASP.NET 和 ASP.NET Core 共享在应用之间的 cookie
author: rick-anderson
description: 了解如何共享身份验证 cookie 之间 ASP.NET 4.x 和 ASP.NET Core 应用。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/19/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/cookie-sharing
ms.openlocfilehash: f6d62d5f6e446e3e2001ed6bde72a6c409aa2833
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34734674"
---
# <a name="share-cookies-among-apps-with-aspnet-and-aspnet-core"></a><span data-ttu-id="b28da-103">与 ASP.NET 和 ASP.NET Core 共享在应用之间的 cookie</span><span class="sxs-lookup"><span data-stu-id="b28da-103">Share cookies among apps with ASP.NET and ASP.NET Core</span></span>

<span data-ttu-id="b28da-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b28da-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b28da-105">网站通常包含单独的 web 应用程序协同工作。</span><span class="sxs-lookup"><span data-stu-id="b28da-105">Websites often consist of individual web apps working together.</span></span> <span data-ttu-id="b28da-106">若要提供单一登录 (SSO) 体验，在站点内的 web 应用程序必须共享身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="b28da-106">To provide a single sign-on (SSO) experience, web apps within a site must share authentication cookies.</span></span> <span data-ttu-id="b28da-107">若要支持这种情况下，数据保护堆栈允许在共享 Katana cookie 身份验证和 ASP.NET Core cookie 身份验证票证。</span><span class="sxs-lookup"><span data-stu-id="b28da-107">To support this scenario, the data protection stack allows sharing Katana cookie authentication and ASP.NET Core cookie authentication tickets.</span></span>

<span data-ttu-id="b28da-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="b28da-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="b28da-109">此示例阐释了在使用 cookie 身份验证的三个应用间共享的 cookie:</span><span class="sxs-lookup"><span data-stu-id="b28da-109">The sample illustrates cookie sharing across three apps that use cookie authentication:</span></span>

* <span data-ttu-id="b28da-110">ASP.NET 核心 2.0 Razor 页应用而无需使用[ASP.NET 核心标识](xref:security/authentication/identity)</span><span class="sxs-lookup"><span data-stu-id="b28da-110">ASP.NET Core 2.0 Razor Pages app without using [ASP.NET Core Identity](xref:security/authentication/identity)</span></span>
* <span data-ttu-id="b28da-111">使用 ASP.NET Core 标识的 ASP.NET Core 2.0 MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="b28da-111">ASP.NET Core 2.0 MVC app with ASP.NET Core Identity</span></span>
* <span data-ttu-id="b28da-112">使用 ASP.NET Identity 的 ASP.NET Framework 4.6.1 MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="b28da-112">ASP.NET Framework 4.6.1 MVC app with ASP.NET Identity</span></span>

<span data-ttu-id="b28da-113">在下面的示例：</span><span class="sxs-lookup"><span data-stu-id="b28da-113">In the examples that follow:</span></span>

* <span data-ttu-id="b28da-114">身份验证 cookie 名称设置为的一个常见值`.AspNet.SharedCookie`。</span><span class="sxs-lookup"><span data-stu-id="b28da-114">The authentication cookie name is set to a common value of `.AspNet.SharedCookie`.</span></span>
* <span data-ttu-id="b28da-115">`AuthenticationType`设置为`Identity.Application`显式或默认情况下。</span><span class="sxs-lookup"><span data-stu-id="b28da-115">The `AuthenticationType` is set to `Identity.Application` either explicitly or by default.</span></span>
* <span data-ttu-id="b28da-116">常见的应用程序名称用于启用数据保护系统共享数据保护密钥 (`SharedCookieApp`)。</span><span class="sxs-lookup"><span data-stu-id="b28da-116">A common app name is used to enable the data protection system to share data protection keys (`SharedCookieApp`).</span></span>
* <span data-ttu-id="b28da-117">`Identity.Application` 使用作为身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="b28da-117">`Identity.Application` is used as the authentication scheme.</span></span> <span data-ttu-id="b28da-118">使用任何方案，它必须一致地使用*内和跨*共享的 cookie 应用的默认架构或通过显式设置。</span><span class="sxs-lookup"><span data-stu-id="b28da-118">Whatever scheme is used, it must be used consistently *within and across* the shared cookie apps either as the default scheme or by explicitly setting it.</span></span> <span data-ttu-id="b28da-119">加密和解密 cookie，因此必须跨应用使用一致的方案时，则使用方案。</span><span class="sxs-lookup"><span data-stu-id="b28da-119">The scheme is used when encrypting and decrypting cookies, so a consistent scheme must be used across apps.</span></span>
* <span data-ttu-id="b28da-120">一个常见[数据保护密钥](xref:security/data-protection/implementation/key-management)使用存储位置。</span><span class="sxs-lookup"><span data-stu-id="b28da-120">A common [data protection key](xref:security/data-protection/implementation/key-management) storage location is used.</span></span> <span data-ttu-id="b28da-121">示例应用使用名为的文件夹*KeyRing*根目录下的解决方案，用于保存数据保护密钥。</span><span class="sxs-lookup"><span data-stu-id="b28da-121">The sample app uses a folder named *KeyRing* at the root of the solution to hold the data protection keys.</span></span>
* <span data-ttu-id="b28da-122">在 ASP.NET Core 应用中， [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)用于设置的密钥存储位置。</span><span class="sxs-lookup"><span data-stu-id="b28da-122">In the ASP.NET Core apps, [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) is used to set the key storage location.</span></span> <span data-ttu-id="b28da-123">[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)用于配置公用的共享应用程序名。</span><span class="sxs-lookup"><span data-stu-id="b28da-123">[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) is used to configure a common shared app name.</span></span>
* <span data-ttu-id="b28da-124">在.NET Framework 应用中，cookie 身份验证中间件使用的实现[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)。</span><span class="sxs-lookup"><span data-stu-id="b28da-124">In the .NET Framework app, the cookie authentication middleware uses an implementation of [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider).</span></span> <span data-ttu-id="b28da-125">`DataProtectionProvider` 提供对身份验证 cookie 负载数据进行加密和解密的数据保护服务。</span><span class="sxs-lookup"><span data-stu-id="b28da-125">`DataProtectionProvider` provides data protection services for the encryption and decryption of authentication cookie payload data.</span></span> <span data-ttu-id="b28da-126">`DataProtectionProvider`实例都独立于所使用的应用程序的其他部分的数据保护系统。</span><span class="sxs-lookup"><span data-stu-id="b28da-126">The `DataProtectionProvider` instance is isolated from the data protection system used by other parts of the app.</span></span>
  * <span data-ttu-id="b28da-127">[DataProtectionProvider.Create (System.IO.DirectoryInfo、 操作\<IDataProtectionBuilder >)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_System_Action_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder__)接受[DirectoryInfo](/dotnet/api/system.io.directoryinfo)指定用于数据保护密钥存储的位置。</span><span class="sxs-lookup"><span data-stu-id="b28da-127">[DataProtectionProvider.Create(System.IO.DirectoryInfo, Action\<IDataProtectionBuilder>)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_System_Action_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder__) accepts a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) to specify the location for data protection key storage.</span></span> <span data-ttu-id="b28da-128">示例应用程序提供的路径*KeyRing*文件夹`DirectoryInfo`。</span><span class="sxs-lookup"><span data-stu-id="b28da-128">The sample app provides the path of the *KeyRing* folder to `DirectoryInfo`.</span></span> <span data-ttu-id="b28da-129">[DataProtectionBuilderExtensions.SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionBuilderExtensions_SetApplicationName_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_)设置常见的应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="b28da-129">[DataProtectionBuilderExtensions.SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionBuilderExtensions_SetApplicationName_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_) sets the common app name.</span></span>
  * <span data-ttu-id="b28da-130">[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)需要[Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b28da-130">[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) requires the [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet package.</span></span> <span data-ttu-id="b28da-131">若要对 ASP.NET 核心 2.1 和更高版本的应用程序中获取此包，引用[Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)。</span><span class="sxs-lookup"><span data-stu-id="b28da-131">To obtain this package for ASP.NET Core 2.1 and later apps, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="b28da-132">如果目标.NET Framework，添加对的包引用`Microsoft.AspNetCore.DataProtection.Extensions`。</span><span class="sxs-lookup"><span data-stu-id="b28da-132">When targeting the .NET Framework, add a package reference to `Microsoft.AspNetCore.DataProtection.Extensions`.</span></span>

## <a name="share-authentication-cookies-among-aspnet-core-apps"></a><span data-ttu-id="b28da-133">共享 ASP.NET Core 应用之间的身份验证 cookie</span><span class="sxs-lookup"><span data-stu-id="b28da-133">Share authentication cookies among ASP.NET Core apps</span></span>

<span data-ttu-id="b28da-134">当使用 ASP.NET 核心标识：</span><span class="sxs-lookup"><span data-stu-id="b28da-134">When using ASP.NET Core Identity:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b28da-135">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b28da-135">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="b28da-136">在`ConfigureServices`方法，请使用[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie)扩展方法，以设置 cookie 数据保护服务。</span><span class="sxs-lookup"><span data-stu-id="b28da-136">In the `ConfigureServices` method, use the [ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie) extension method to set up the data protection service for cookies.</span></span>

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

<span data-ttu-id="b28da-137">必须在应用之间共享数据保护密钥和应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="b28da-137">Data protection keys and the app name must be shared among apps.</span></span> <span data-ttu-id="b28da-138">在示例应用中，`GetKeyRingDirInfo`返回到的公共密钥存储位置[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)方法。</span><span class="sxs-lookup"><span data-stu-id="b28da-138">In the sample apps, `GetKeyRingDirInfo` returns the common key storage location to the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) method.</span></span> <span data-ttu-id="b28da-139">使用[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)配置公用的共享应用程序名 (`SharedCookieApp`示例中)。</span><span class="sxs-lookup"><span data-stu-id="b28da-139">Use [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) to configure a common shared app name (`SharedCookieApp` in the sample).</span></span> <span data-ttu-id="b28da-140">有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="b28da-140">For more information, see [Configuring Data Protection](xref:security/data-protection/configuration/overview).</span></span>

<span data-ttu-id="b28da-141">请参阅*CookieAuthWithIdentity.Core*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="b28da-141">See the *CookieAuthWithIdentity.Core* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b28da-142">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b28da-142">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="b28da-143">在`Configure`方法，请使用[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions)设置：</span><span class="sxs-lookup"><span data-stu-id="b28da-143">In the `Configure` method, use the [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions) to set up:</span></span>

* <span data-ttu-id="b28da-144">Cookie 数据保护服务。</span><span class="sxs-lookup"><span data-stu-id="b28da-144">The data protection service for cookies.</span></span>
* <span data-ttu-id="b28da-145">`AuthenticationScheme`以匹配 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="b28da-145">The `AuthenticationScheme` to match ASP.NET 4.x.</span></span>

```csharp
app.AddIdentity<ApplicationUser, IdentityRole>(options =>
{
    options.Cookies.ApplicationCookie.AuthenticationScheme = 
        "ApplicationCookie";

    var protectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"));

    options.Cookies.ApplicationCookie.DataProtectionProvider = 
        protectionProvider;

    options.Cookies.ApplicationCookie.TicketDataFormat = 
        new TicketDataFormat(protectionProvider.CreateProtector(
            "Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware", 
            "Cookies", 
            "v2"));
});
```

---

<span data-ttu-id="b28da-146">当直接使用 cookie:</span><span class="sxs-lookup"><span data-stu-id="b28da-146">When using cookies directly:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b28da-147">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b28da-147">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]

<span data-ttu-id="b28da-148">必须在应用之间共享数据保护密钥和应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="b28da-148">Data protection keys and the app name must be shared among apps.</span></span> <span data-ttu-id="b28da-149">在示例应用中，`GetKeyRingDirInfo`返回到的公共密钥存储位置[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)方法。</span><span class="sxs-lookup"><span data-stu-id="b28da-149">In the sample apps, `GetKeyRingDirInfo` returns the common key storage location to the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) method.</span></span> <span data-ttu-id="b28da-150">使用[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)配置公用的共享应用程序名 (`SharedCookieApp`示例中)。</span><span class="sxs-lookup"><span data-stu-id="b28da-150">Use [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) to configure a common shared app name (`SharedCookieApp` in the sample).</span></span> <span data-ttu-id="b28da-151">有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="b28da-151">For more information, see [Configuring Data Protection](xref:security/data-protection/configuration/overview).</span></span> 

<span data-ttu-id="b28da-152">请参阅*CookieAuth.Core*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="b28da-152">See the *CookieAuth.Core* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b28da-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b28da-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
});
```

---

## <a name="encrypting-data-protection-keys-at-rest"></a><span data-ttu-id="b28da-154">加密存放的数据保护密钥</span><span class="sxs-lookup"><span data-stu-id="b28da-154">Encrypting data protection keys at rest</span></span>

<span data-ttu-id="b28da-155">对于生产部署，配置`DataProtectionProvider`来加密存放使用 DPAPI 或 x509 证书的密钥。</span><span class="sxs-lookup"><span data-stu-id="b28da-155">For production deployments, configure the `DataProtectionProvider` to encrypt keys at rest with DPAPI or an X509Certificate.</span></span> <span data-ttu-id="b28da-156">请参阅[将加密密钥在 Rest](xref:security/data-protection/implementation/key-encryption-at-rest)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="b28da-156">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more information.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b28da-157">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b28da-157">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .ProtectKeysWithCertificate("thumbprint");
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b28da-158">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b28da-158">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = DataProtectionProvider.Create(
        new DirectoryInfo(@"PATH_TO_KEY_RING"),
        configure =>
        {
            configure.ProtectKeysWithCertificate("thumbprint");
        })
});
```

---

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-apps"></a><span data-ttu-id="b28da-159">共享身份验证 cookie 之间 ASP.NET 4.x 和 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="b28da-159">Sharing authentication cookies between ASP.NET 4.x and ASP.NET Core apps</span></span>

<span data-ttu-id="b28da-160">ASP.NET 4.x 应用程序使用 Katana cookie 身份验证中间件该对话框可以配置为生成与 ASP.NET Core cookie 身份验证中间件兼容的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="b28da-160">ASP.NET 4.x apps which use Katana cookie authentication middleware can be configured to generate authentication cookies that are compatible with the ASP.NET Core cookie authentication middleware.</span></span> <span data-ttu-id="b28da-161">这样，段落将大型站点的单个应用升级时站点内提供顺畅的 SSO 体验。</span><span class="sxs-lookup"><span data-stu-id="b28da-161">This allows upgrading a large site's individual apps piecemeal while providing a smooth SSO experience across the site.</span></span>

> [!TIP]
> <span data-ttu-id="b28da-162">当应用使用 Katana cookie 身份验证中间件时，它将调用`UseCookieAuthentication`在项目的*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="b28da-162">When an app uses Katana cookie authentication middleware, it calls `UseCookieAuthentication` in the project's *Startup.Auth.cs* file.</span></span> <span data-ttu-id="b28da-163">ASP.NET 4.x web 应用程序项目创建与 Visual Studio 2013 和更高版本默认情况下使用 Katana cookie 身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="b28da-163">ASP.NET 4.x web app projects created with Visual Studio 2013 and later use the Katana cookie authentication middleware by default.</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-164">ASP.NET 4.x 应用程序必须面向.NET Framework 4.5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="b28da-164">An ASP.NET 4.x app must target .NET Framework 4.5.1 or higher.</span></span> <span data-ttu-id="b28da-165">否则，所需的 NuGet 包将无法安装。</span><span class="sxs-lookup"><span data-stu-id="b28da-165">Otherwise, the necessary NuGet packages fail to install.</span></span>

<span data-ttu-id="b28da-166">若要共享的 ASP.NET 4.x 应用程序和 ASP.NET Core 应用之间的身份验证 cookie，如前所述，将 ASP.NET Core 应用配置，然后通过执行以下步骤配置 ASP.NET 4.x 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b28da-166">To share authentication cookies among ASP.NET 4.x apps and ASP.NET Core apps, configure the ASP.NET Core app as stated above, then configure the ASP.NET 4.x apps by following the steps below.</span></span>

1. <span data-ttu-id="b28da-167">安装包[Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/)到每个 ASP.NET 4.x 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b28da-167">Install the package [Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/) into each ASP.NET 4.x app.</span></span>

2. <span data-ttu-id="b28da-168">在*Startup.Auth.cs*，找到调用`UseCookieAuthentication`和对其进行修改，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b28da-168">In *Startup.Auth.cs*, locate the call to `UseCookieAuthentication` and modify it as follows.</span></span> <span data-ttu-id="b28da-169">更改要匹配使用 ASP.NET Core cookie 身份验证中间件的名称的 cookie 名称。</span><span class="sxs-lookup"><span data-stu-id="b28da-169">Change the cookie name to match the name used by the ASP.NET Core cookie authentication middleware.</span></span> <span data-ttu-id="b28da-170">提供的一个实例`DataProtectionProvider`初始化为常见的数据保护密钥的存储位置。</span><span class="sxs-lookup"><span data-stu-id="b28da-170">Provide an instance of a `DataProtectionProvider` initialized to the common data protection key storage location.</span></span> <span data-ttu-id="b28da-171">请确保应用程序名称设置为使用共享 cookie 的所有应用程序的常见应用程序名称`SharedCookieApp`示例应用中。</span><span class="sxs-lookup"><span data-stu-id="b28da-171">Make sure that the app name is set to the common app name used by all apps that share cookies, `SharedCookieApp` in the sample app.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b28da-172">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b28da-172">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]

<span data-ttu-id="b28da-173">请参阅*CookieAuthWithIdentity.NETFramework*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="b28da-173">See the *CookieAuthWithIdentity.NETFramework* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

<span data-ttu-id="b28da-174">身份验证类型时生成的用户标识，必须与匹配中定义的类型`AuthenticationType`设置`UseCookieAuthentication`。</span><span class="sxs-lookup"><span data-stu-id="b28da-174">When generating a user identity, the authentication type must match the type defined in `AuthenticationType` set with `UseCookieAuthentication`.</span></span>

<span data-ttu-id="b28da-175">*Models/IdentityModels.cs*:</span><span class="sxs-lookup"><span data-stu-id="b28da-175">*Models/IdentityModels.cs*:</span></span>

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b28da-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b28da-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="b28da-177">设置`CookieManager`互操作`ChunkingCookieManager`以便块区格式不兼容。</span><span class="sxs-lookup"><span data-stu-id="b28da-177">Set the `CookieManager` to interop `ChunkingCookieManager` so the chunking format is compatible.</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
    CookieName = ".AspNetCore.Cookies",
    // CookieName = ".AspNetCore.ApplicationCookie", (if using ASP.NET Identity)
    // CookiePath = "...", (if necessary)
    // ...
    TicketDataFormat = new AspNetTicketDataFormat(
        new DataProtectorShim(
            DataProtectionProvider.Create(
                new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
            .CreateProtector(
                "Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware",
                "Cookies", 
                "v2"))),
    CookieManager = new ChunkingCookieManager()
});
```

---

## <a name="use-a-common-user-database"></a><span data-ttu-id="b28da-178">使用常见的用户数据库</span><span class="sxs-lookup"><span data-stu-id="b28da-178">Use a common user database</span></span>

<span data-ttu-id="b28da-179">确认每个应用程序的标识系统指向相同的用户数据库。</span><span class="sxs-lookup"><span data-stu-id="b28da-179">Confirm that the identity system for each app is pointed at the same user database.</span></span> <span data-ttu-id="b28da-180">否则，标识系统会生成在运行时失败时它尝试匹配针对其数据库中的信息的身份验证 cookie 中的信息。</span><span class="sxs-lookup"><span data-stu-id="b28da-180">Otherwise, the identity system produces failures at runtime when it attempts to match the information in the authentication cookie against the information in its database.</span></span>
