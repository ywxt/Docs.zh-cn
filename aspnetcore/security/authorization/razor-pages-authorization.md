---
title: 在 ASP.NET Core razor 页授权约定
author: guardrex
description: 了解如何控制对页约定来授予用户权限和允许匿名用户访问页面的文件夹的访问。
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: d3ecb41765da912df68aeb829350d27e4d087e3a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824475"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a>在 ASP.NET Core razor 页授权约定

作者：[Luke Latham](https://github.com/guardrex)

Razor 页面应用中控制访问权限的一种方法是在启动时使用授权约定。 这些约定，可为用户授权，并允许匿名用户访问各个页面的文件夹。 自动在本主题中所述的约定适用[授权筛选器](xref:mvc/controllers/filters#authorization-filters)来控制访问。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

此示例应用程序使用[Cookie 身份验证，而无需 ASP.NET Core 标识](xref:security/authentication/cookie)。 假设用户、 Maria Rodriguez 的用户帐户是硬编码到应用程序。 使用电子邮件用户名"maria.rodriguez@contoso.com"和任何密码以登录用户。 用户进行身份验证中`AuthenticateUser`中的方法*Pages/Account/Login.cshtml.cs*文件。 在实际示例中，用户会根据数据库身份验证。 若要使用 ASP.NET Core 标识，请按照中的指导[ASP.NET Core 上的标识简介](xref:security/authentication/identity)主题。 概念和本主题中所示的示例同样适用于使用 ASP.NET Core 标识的应用。

## <a name="require-authorization-to-access-a-page"></a>需要授权可访问的页面

使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到指定路径的页面：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

指定的路径是视图引擎路径，即无需扩展和包含仅正斜杠的 Razor 页面根相对路径。

[AuthorizePage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)时才需要指定的授权策略可用。

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> `AuthorizeFilter`可以应用于具有的页面模型类`[Authorize]`筛选器特性。 有关详细信息，请参阅[Authorize 筛选器属性](xref:razor-pages/filter#authorize-filter-attribute)。

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a>需要授权才能访问页面的文件夹

使用[AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径处的文件夹中的页：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

指定的路径是视图引擎路径，这是 Razor 页面根相对路径。

[AuthorizeFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)时才需要指定的授权策略可用。

::: moniker range=">= aspnetcore-2.1"

## <a name="require-authorization-to-access-an-area-page"></a>需要授权才能访问区域页

使用[AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到指定路径的区域页面：

```csharp
options.Conventions.AuthorizeAreaPage("Identity", "/Manage/Accounts");
```

页面名称是文件的指定的区域不相对于页面根目录具有扩展名的路径。 例如，该文件的页名称*Areas/Identity/Pages/Manage/Accounts.cshtml*是 */管理/帐户*。

[AuthorizeAreaPage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_)时才需要指定的授权策略可用。

## <a name="require-authorization-to-access-a-folder-of-areas"></a>需要授权才能访问区域的文件夹

使用[AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径处的文件夹中的区域：

```csharp
options.Conventions.AuthorizeAreaFolder("Identity", "/Manage");
```

文件夹路径是相对于指定区域的页面根目录文件夹的路径。 例如下的文件的文件夹路径*领域/Identity/页/管理/* 是 */管理*。

[AuthorizeAreaFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_)时才需要指定的授权策略可用。

::: moniker-end

## <a name="allow-anonymous-access-to-a-page"></a>允许匿名访问的页

使用[AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到指定路径处的页面：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

指定的路径是视图引擎路径，即无需扩展和包含仅正斜杠的 Razor 页面根相对路径。

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a>允许匿名访问的页面的文件夹

使用[AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到所有指定路径处的文件夹中的页：

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

指定的路径是视图引擎路径，这是 Razor 页面根相对路径。

## <a name="note-on-combining-authorized-and-anonymous-access"></a>请注意在组合授权和匿名访问

它是完全有效，若要指定页面的文件夹需要授权，并指定该文件夹中的页面，允许匿名访问：

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

但是，与之相反，不是这样。 不能声明为匿名访问的页面的文件夹，并指定中进行授权的页面：

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

需要专用的页上的授权不起作用，因为时同时`AllowAnonymousFilter`并`AuthorizeFilter`页上，应用了筛选器`AllowAnonymousFilter`wins 和控制的访问。

## <a name="additional-resources"></a>其他资源

* [Razor 页面自定义路由和页面模型提供程序](xref:razor-pages/razor-pages-conventions)
* [PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection)类
