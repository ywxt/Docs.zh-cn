---
title: 在 ASP.NET Core razor 页授权约定
author: guardrex
description: 了解如何控制对约定来授予用户权限和允许匿名用户访问页或文件夹中的页的页的访问。
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: 8856520bf43f2f62cc12c7e883485babdb43fb3e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272670"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a>在 ASP.NET Core razor 页授权约定

作者：[Luke Latham](https://github.com/guardrex)

若要控制在 Razor 页面应用程序的访问的一个方法是在启动时使用授权约定。 这些约定，可以为用户授权，并允许匿名用户访问各个页的文件夹。 自动本主题中所述的约定应用[授权筛选器](xref:mvc/controllers/filters#authorization-filters)来控制访问权限。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

此示例应用程序使用[Cookie 身份验证，而无需 ASP.NET Core 标识](xref:security/authentication/cookie)。 假设用户，Maria Rodriguez 的用户帐户是硬编码到应用程序。 使用电子邮件用户名"maria.rodriguez@contoso.com"和任何密码以登录用户。 用户进行身份验证中`AuthenticateUser`中的方法*Pages/Account/Login.cshtml.cs*文件。 在实际示例中，对用户的身份验证将对数据库。 若要使用 ASP.NET Core 标识，请按照中的指导[ASP.NET Core 上的标识简介](xref:security/authentication/identity)主题。 概念和本主题中所示的示例同样适用于使用 ASP.NET Core 标识的应用。

## <a name="require-authorization-to-access-a-page"></a>需要授权可访问的页面

使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到页中指定的路径：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

指定的路径是视图引擎路径，这是无需扩展和包含仅正斜杠的 Razor 页根相对路径。

[AuthorizePage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)当你需要指定一个授权策略才可用。

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> `AuthorizeFilter`可以应用于具有的页面模型类`[Authorize]`筛选器属性。 有关详细信息，请参阅[Authorize 筛选器属性](xref:razor-pages/filter#authorize-filter-attribute)。

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a>需要的页的文件夹的访问权

使用[AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径上的文件夹中的页：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

指定的路径是视图引擎路径，这是 Razor 页根相对路径。

[AuthorizeFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)当你需要指定一个授权策略才可用。

## <a name="allow-anonymous-access-to-a-page"></a>允许匿名访问的页

使用[AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到指定的路径下的网页：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

指定的路径是视图引擎路径，这是无需扩展和包含仅正斜杠的 Razor 页根相对路径。

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a>允许匿名访问的页面的文件夹

使用[AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到所有指定路径上的文件夹中的页：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

指定的路径是视图引擎路径，这是 Razor 页根相对路径。

## <a name="note-on-combining-authorized-and-anonymous-access"></a>请注意有关组合授权和匿名访问

这是完全合法，若要指定的页的文件夹需要授权，并指定该文件夹中的页允许匿名访问：

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

但是，反过来，不是如此。 不能声明用于匿名访问的页面的文件夹，并指定授权中的页：

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

需要专用的页上的授权不起作用，因为当同时`AllowAnonymousFilter`和`AuthorizeFilter`筛选器应用到页上， `AllowAnonymousFilter` wins 和控制的访问。

## <a name="additional-resources"></a>其他资源

* [Razor 页面自定义路由和页面模型提供程序](xref:razor-pages/razor-pages-conventions)
* [PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection)类
