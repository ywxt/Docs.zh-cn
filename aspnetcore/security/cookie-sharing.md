---
title: 与 ASP.NET 和 ASP.NET Core 共享在应用之间的 cookie
author: rick-anderson
description: 了解如何共享身份验证 cookie 之间 ASP.NET 4.x 和 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 01/19/2017
uid: security/cookie-sharing
ms.openlocfilehash: 2636688fa50fb36a8cbd07549e8038474ffa30ca
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278461"
---
# <a name="share-cookies-among-apps-with-aspnet-and-aspnet-core"></a>与 ASP.NET 和 ASP.NET Core 共享在应用之间的 cookie

通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Luke Latham](https://github.com/guardrex)

网站通常包含单独的 web 应用程序协同工作。 若要提供单一登录 (SSO) 体验，在站点内的 web 应用程序必须共享身份验证 cookie。 若要支持这种情况下，数据保护堆栈允许在共享 Katana cookie 身份验证和 ASP.NET Core cookie 身份验证票证。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

此示例阐释了在使用 cookie 身份验证的三个应用间共享的 cookie:

* ASP.NET Core 2.0 Razor 页应用而无需使用[ASP.NET Core 标识](xref:security/authentication/identity)
* 使用 ASP.NET Core 标识的 ASP.NET Core 2.0 MVC 应用程序
* 使用 ASP.NET Identity 的 ASP.NET Framework 4.6.1 MVC 应用程序

在下面的示例：

* 身份验证 cookie 名称设置为的一个常见值`.AspNet.SharedCookie`。
* `AuthenticationType`设置为`Identity.Application`显式或默认情况下。
* 常见的应用程序名称用于启用数据保护系统共享数据保护密钥 (`SharedCookieApp`)。
* `Identity.Application` 使用作为身份验证方案。 使用任何方案，它必须一致地使用*内和跨*共享的 cookie 应用的默认架构或通过显式设置。 加密和解密 cookie，因此必须跨应用使用一致的方案时，则使用方案。
* 一个常见[数据保护密钥](xref:security/data-protection/implementation/key-management)使用存储位置。 示例应用使用名为的文件夹*KeyRing*根目录下的解决方案，用于保存数据保护密钥。
* 在 ASP.NET Core 应用中， [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)用于设置的密钥存储位置。 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)用于配置公用的共享应用程序名。
* 在.NET Framework 应用中，cookie 身份验证中间件使用的实现[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)。 `DataProtectionProvider` 提供对身份验证 cookie 负载数据进行加密和解密的数据保护服务。 `DataProtectionProvider`实例都独立于所使用的应用程序的其他部分的数据保护系统。
  * [DataProtectionProvider.Create (System.IO.DirectoryInfo、 操作\<IDataProtectionBuilder >)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_System_Action_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder__)接受[DirectoryInfo](/dotnet/api/system.io.directoryinfo)指定用于数据保护密钥存储的位置。 示例应用程序提供的路径*KeyRing*文件夹`DirectoryInfo`。 [DataProtectionBuilderExtensions.SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionBuilderExtensions_SetApplicationName_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_)设置常见的应用程序名称。
  * [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)需要[Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet 包。 若要对 ASP.NET Core 2.1 和更高版本的应用程序中获取此包，引用[Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)。 如果目标.NET Framework，添加对的包引用`Microsoft.AspNetCore.DataProtection.Extensions`。

## <a name="share-authentication-cookies-among-aspnet-core-apps"></a>共享 ASP.NET Core 应用之间的身份验证 cookie

当使用 ASP.NET Core标识：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

在`ConfigureServices`方法，请使用[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie)扩展方法，以设置 cookie 数据保护服务。

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

必须在应用之间共享数据保护密钥和应用程序名称。 在示例应用中，`GetKeyRingDirInfo`返回到的公共密钥存储位置[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)方法。 使用[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)配置公用的共享应用程序名 (`SharedCookieApp`示例中)。 有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。

请参阅*CookieAuthWithIdentity.Core*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

在`Configure`方法，请使用[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions)设置：

* Cookie 数据保护服务。
* `AuthenticationScheme`以匹配 ASP.NET 4.x。

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

当直接使用 cookie:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]

必须在应用之间共享数据保护密钥和应用程序名称。 在示例应用中，`GetKeyRingDirInfo`返回到的公共密钥存储位置[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)方法。 使用[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)配置公用的共享应用程序名 (`SharedCookieApp`示例中)。 有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。 

请参阅*CookieAuth.Core*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
});
```

---

## <a name="encrypting-data-protection-keys-at-rest"></a>加密存放的数据保护密钥

对于生产部署，配置`DataProtectionProvider`来加密存放使用 DPAPI 或 x509 证书的密钥。 请参阅[将加密密钥在 Rest](xref:security/data-protection/implementation/key-encryption-at-rest)有关详细信息。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .ProtectKeysWithCertificate("thumbprint");
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

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

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-apps"></a>共享身份验证 cookie 之间 ASP.NET 4.x 和 ASP.NET Core 应用

ASP.NET 4.x 应用程序使用 Katana cookie 身份验证中间件该对话框可以配置为生成与 ASP.NET Core cookie 身份验证中间件兼容的身份验证 cookie。 这样，段落将大型站点的单个应用升级时站点内提供顺畅的 SSO 体验。

当应用使用 Katana cookie 身份验证中间件时，它将调用`UseCookieAuthentication`在项目的*Startup.Auth.cs*文件。 ASP.NET 4.x web 应用程序项目创建与 Visual Studio 2013 和更高版本默认情况下使用 Katana cookie 身份验证中间件。 尽管`UseCookieAuthentication`已过时，不支持对于 ASP.NET Core 应用程序，调用`UseCookieAuthentication`在 ASP.NET 4.x 应用程序使用 Katana cookie 身份验证中间件是有效的。

ASP.NET 4.x 应用程序必须面向.NET Framework 4.5.1 或更高版本。 否则，所需的 NuGet 包将无法安装。

若要共享 ASP.NET 4.x 应用程序和 ASP.NET Core 应用程序之间的身份验证 cookie，如前所述，将 ASP.NET Core 应用配置，然后通过执行以下步骤配置 ASP.NET 4.x 应用程序：

1. 安装包[Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/)到每个 ASP.NET 4.x 应用程序。

2. 在*Startup.Auth.cs*，找到调用`UseCookieAuthentication`和对其进行修改，如下所示。 更改要匹配使用 ASP.NET Core cookie 身份验证中间件的名称的 cookie 名称。 提供的一个实例`DataProtectionProvider`初始化为常见的数据保护密钥的存储位置。 请确保应用程序名称设置为使用共享 cookie 的所有应用程序的常见应用程序名称`SharedCookieApp`示例应用中。

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]

请参阅*CookieAuthWithIdentity.NETFramework*项目中[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([如何下载](xref:tutorials/index#how-to-download-a-sample))。

身份验证类型时生成的用户标识，必须与匹配中定义的类型`AuthenticationType`设置`UseCookieAuthentication`。

*Models/IdentityModels.cs*:

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]

## <a name="use-a-common-user-database"></a>使用常见的用户数据库

确认每个应用程序的标识系统指向相同的用户数据库。 否则，标识系统会生成在运行时失败时它尝试匹配针对其数据库中的信息的身份验证 cookie 中的信息。
