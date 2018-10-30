---
title: 在 ASP.NET Core razor 页授权约定
author: guardrex
description: 了解如何控制对页约定来授予用户权限和允许匿名用户访问页面的文件夹的访问。
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: 675dc8aa4bf00bb21981cc892a09a4acd0d53c15
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207259"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a><span data-ttu-id="93872-103">在 ASP.NET Core razor 页授权约定</span><span class="sxs-lookup"><span data-stu-id="93872-103">Razor Pages authorization conventions in ASP.NET Core</span></span>

<span data-ttu-id="93872-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="93872-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="93872-105">Razor 页面应用中控制访问权限的一种方法是在启动时使用授权约定。</span><span class="sxs-lookup"><span data-stu-id="93872-105">One way to control access in your Razor Pages app is to use authorization conventions at startup.</span></span> <span data-ttu-id="93872-106">这些约定，可为用户授权，并允许匿名用户访问各个页面的文件夹。</span><span class="sxs-lookup"><span data-stu-id="93872-106">These conventions allow you to authorize users and allow anonymous users to access individual pages or folders of pages.</span></span> <span data-ttu-id="93872-107">自动在本主题中所述的约定适用[授权筛选器](xref:mvc/controllers/filters#authorization-filters)来控制访问。</span><span class="sxs-lookup"><span data-stu-id="93872-107">The conventions described in this topic automatically apply [authorization filters](xref:mvc/controllers/filters#authorization-filters) to control access.</span></span>

<span data-ttu-id="93872-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="93872-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="93872-109">此示例应用程序使用[Cookie 身份验证，而无需 ASP.NET Core 标识](xref:security/authentication/cookie)。</span><span class="sxs-lookup"><span data-stu-id="93872-109">The sample app uses [Cookie authentication without ASP.NET Core Identity](xref:security/authentication/cookie).</span></span> <span data-ttu-id="93872-110">假设用户、 Maria Rodriguez 的用户帐户是硬编码到应用程序。</span><span class="sxs-lookup"><span data-stu-id="93872-110">The user account for the hypothetical user, Maria Rodriguez, is hardcoded into the app.</span></span> <span data-ttu-id="93872-111">使用电子邮件用户名"maria.rodriguez@contoso.com"和任何密码以登录用户。</span><span class="sxs-lookup"><span data-stu-id="93872-111">Use the Email username "maria.rodriguez@contoso.com" and any password to sign in the user.</span></span> <span data-ttu-id="93872-112">用户进行身份验证中`AuthenticateUser`中的方法*Pages/Account/Login.cshtml.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="93872-112">The user is authenticated in the `AuthenticateUser` method in the *Pages/Account/Login.cshtml.cs* file.</span></span> <span data-ttu-id="93872-113">在实际示例中，用户会根据数据库身份验证。</span><span class="sxs-lookup"><span data-stu-id="93872-113">In a real-world example, the user would be authenticated against a database.</span></span> <span data-ttu-id="93872-114">若要使用 ASP.NET Core 标识，请按照中的指导[ASP.NET Core 上的标识简介](xref:security/authentication/identity)主题。</span><span class="sxs-lookup"><span data-stu-id="93872-114">To use ASP.NET Core Identity, follow the guidance in the [Introduction to Identity on ASP.NET Core](xref:security/authentication/identity) topic.</span></span> <span data-ttu-id="93872-115">概念和本主题中所示的示例同样适用于使用 ASP.NET Core 标识的应用。</span><span class="sxs-lookup"><span data-stu-id="93872-115">The concepts and examples shown in this topic apply equally to apps that use ASP.NET Core Identity.</span></span>

## <a name="require-authorization-to-access-a-page"></a><span data-ttu-id="93872-116">需要授权可访问的页面</span><span class="sxs-lookup"><span data-stu-id="93872-116">Require authorization to access a page</span></span>

<span data-ttu-id="93872-117">使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到指定路径的页面：</span><span class="sxs-lookup"><span data-stu-id="93872-117">Use the [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

<span data-ttu-id="93872-118">指定的路径是视图引擎路径，即无需扩展和包含仅正斜杠的 Razor 页面根相对路径。</span><span class="sxs-lookup"><span data-stu-id="93872-118">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

<span data-ttu-id="93872-119">[AuthorizePage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)时才需要指定的授权策略可用。</span><span class="sxs-lookup"><span data-stu-id="93872-119">An [AuthorizePage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="93872-120">`AuthorizeFilter`可以应用于具有的页面模型类`[Authorize]`筛选器特性。</span><span class="sxs-lookup"><span data-stu-id="93872-120">An `AuthorizeFilter` can be applied to a page model class with the `[Authorize]` filter attribute.</span></span> <span data-ttu-id="93872-121">有关详细信息，请参阅[Authorize 筛选器属性](xref:razor-pages/filter#authorize-filter-attribute)。</span><span class="sxs-lookup"><span data-stu-id="93872-121">For more information, see [Authorize filter attribute](xref:razor-pages/filter#authorize-filter-attribute).</span></span>

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a><span data-ttu-id="93872-122">需要授权才能访问页面的文件夹</span><span class="sxs-lookup"><span data-stu-id="93872-122">Require authorization to access a folder of pages</span></span>

<span data-ttu-id="93872-123">使用[AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径处的文件夹中的页：</span><span class="sxs-lookup"><span data-stu-id="93872-123">Use the [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

<span data-ttu-id="93872-124">指定的路径是视图引擎路径，这是 Razor 页面根相对路径。</span><span class="sxs-lookup"><span data-stu-id="93872-124">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

<span data-ttu-id="93872-125">[AuthorizeFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)时才需要指定的授权策略可用。</span><span class="sxs-lookup"><span data-stu-id="93872-125">An [AuthorizeFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="require-authorization-to-access-an-area-page"></a><span data-ttu-id="93872-126">需要授权才能访问区域页</span><span class="sxs-lookup"><span data-stu-id="93872-126">Require authorization to access an area page</span></span>

<span data-ttu-id="93872-127">使用[AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到指定路径的区域页面：</span><span class="sxs-lookup"><span data-stu-id="93872-127">Use the [AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the area page at the specified path:</span></span>

```csharp
options.Conventions.AuthorizeAreaPage("Identity", "/Manage/Accounts");
```

<span data-ttu-id="93872-128">页面名称是文件的指定的区域不相对于页面根目录具有扩展名的路径。</span><span class="sxs-lookup"><span data-stu-id="93872-128">The page name is the path of the file without an extension relative to the pages root directory for the specified area.</span></span> <span data-ttu-id="93872-129">例如，该文件的页名称*Areas/Identity/Pages/Manage/Accounts.cshtml*是 */管理/帐户*。</span><span class="sxs-lookup"><span data-stu-id="93872-129">For example, the page name for the file *Areas/Identity/Pages/Manage/Accounts.cshtml* is */Manage/Accounts*.</span></span>

<span data-ttu-id="93872-130">[AuthorizeAreaPage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_)时才需要指定的授权策略可用。</span><span class="sxs-lookup"><span data-stu-id="93872-130">An [AuthorizeAreaPage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

## <a name="require-authorization-to-access-a-folder-of-areas"></a><span data-ttu-id="93872-131">需要授权才能访问区域的文件夹</span><span class="sxs-lookup"><span data-stu-id="93872-131">Require authorization to access a folder of areas</span></span>

<span data-ttu-id="93872-132">使用[AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径处的文件夹中的区域：</span><span class="sxs-lookup"><span data-stu-id="93872-132">Use the [AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the areas in a folder at the specified path:</span></span>

```csharp
options.Conventions.AuthorizeAreaFolder("Identity", "/Manage");
```

<span data-ttu-id="93872-133">文件夹路径是相对于指定区域的页面根目录文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="93872-133">The folder path is the path of the folder relative to the pages root directory for the specified area.</span></span> <span data-ttu-id="93872-134">例如下的文件的文件夹路径*领域/Identity/页/管理/* 是 */管理*。</span><span class="sxs-lookup"><span data-stu-id="93872-134">For example, the folder path for the files under *Areas/Identity/Pages/Manage/* is */Manage*.</span></span>

<span data-ttu-id="93872-135">[AuthorizeAreaFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_)时才需要指定的授权策略可用。</span><span class="sxs-lookup"><span data-stu-id="93872-135">An [AuthorizeAreaFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker-end

## <a name="allow-anonymous-access-to-a-page"></a><span data-ttu-id="93872-136">允许匿名访问的页</span><span class="sxs-lookup"><span data-stu-id="93872-136">Allow anonymous access to a page</span></span>

<span data-ttu-id="93872-137">使用[AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到指定路径处的页面：</span><span class="sxs-lookup"><span data-stu-id="93872-137">Use the [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to a page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

<span data-ttu-id="93872-138">指定的路径是视图引擎路径，即无需扩展和包含仅正斜杠的 Razor 页面根相对路径。</span><span class="sxs-lookup"><span data-stu-id="93872-138">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a><span data-ttu-id="93872-139">允许匿名访问的页面的文件夹</span><span class="sxs-lookup"><span data-stu-id="93872-139">Allow anonymous access to a folder of pages</span></span>

<span data-ttu-id="93872-140">使用[AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)若要添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到所有指定路径处的文件夹中的页：</span><span class="sxs-lookup"><span data-stu-id="93872-140">Use the [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

<span data-ttu-id="93872-141">指定的路径是视图引擎路径，这是 Razor 页面根相对路径。</span><span class="sxs-lookup"><span data-stu-id="93872-141">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

## <a name="note-on-combining-authorized-and-anonymous-access"></a><span data-ttu-id="93872-142">请注意在组合授权和匿名访问</span><span class="sxs-lookup"><span data-stu-id="93872-142">Note on combining authorized and anonymous access</span></span>

<span data-ttu-id="93872-143">它是完全有效，若要指定页面的文件夹需要授权，并指定该文件夹中的页面，允许匿名访问：</span><span class="sxs-lookup"><span data-stu-id="93872-143">It's perfectly valid to specify that a folder of pages require authorization and specify that a page within that folder allows anonymous access:</span></span>

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

<span data-ttu-id="93872-144">但是，与之相反，不是这样。</span><span class="sxs-lookup"><span data-stu-id="93872-144">The reverse, however, isn't true.</span></span> <span data-ttu-id="93872-145">不能声明为匿名访问的页面的文件夹，并指定中进行授权的页面：</span><span class="sxs-lookup"><span data-stu-id="93872-145">You can't declare a folder of pages for anonymous access and specify a page within for authorization:</span></span>

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

<span data-ttu-id="93872-146">需要专用的页上的授权不起作用，因为时同时`AllowAnonymousFilter`并`AuthorizeFilter`页上，应用了筛选器`AllowAnonymousFilter`wins 和控制的访问。</span><span class="sxs-lookup"><span data-stu-id="93872-146">Requiring authorization on the Private page won't work because when both the `AllowAnonymousFilter` and `AuthorizeFilter` filters are applied to the page, the `AllowAnonymousFilter` wins and controls access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93872-147">其他资源</span><span class="sxs-lookup"><span data-stu-id="93872-147">Additional resources</span></span>

* [<span data-ttu-id="93872-148">Razor 页面自定义路由和页面模型提供程序</span><span class="sxs-lookup"><span data-stu-id="93872-148">Razor Pages custom route and page model providers</span></span>](xref:razor-pages/razor-pages-conventions)
* <span data-ttu-id="93872-149">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection)类</span><span class="sxs-lookup"><span data-stu-id="93872-149">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) class</span></span>
