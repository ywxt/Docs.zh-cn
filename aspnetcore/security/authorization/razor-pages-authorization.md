---
title: "在 ASP.NET Core razor 页授权约定"
author: guardrex
description: "了解如何控制对约定来授予用户权限和允许匿名用户访问页或文件夹中的页的页的访问。"
manager: wpickett
ms.author: riande
ms.date: 10/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: bbef653c6cf968527e753df9c853f5972640cc03
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a><span data-ttu-id="c323c-103">在 ASP.NET Core razor 页授权约定</span><span class="sxs-lookup"><span data-stu-id="c323c-103">Razor Pages authorization conventions in ASP.NET Core</span></span>

<span data-ttu-id="c323c-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="c323c-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c323c-105">若要控制在 Razor 页面应用程序的访问的一个方法是在启动时使用授权约定。</span><span class="sxs-lookup"><span data-stu-id="c323c-105">One way to control access in your Razor Pages app is to use authorization conventions at startup.</span></span> <span data-ttu-id="c323c-106">这些约定，可以为用户授权，并允许匿名用户访问各个页的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c323c-106">These conventions allow you to authorize users and allow anonymous users to access individual pages or folders of pages.</span></span> <span data-ttu-id="c323c-107">自动本主题中所述的约定应用[授权筛选器](xref:mvc/controllers/filters#authorization-filters)来控制访问权限。</span><span class="sxs-lookup"><span data-stu-id="c323c-107">The conventions described in this topic automatically apply [authorization filters](xref:mvc/controllers/filters#authorization-filters) to control access.</span></span>

<span data-ttu-id="c323c-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="c323c-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="require-authorization-to-access-a-page"></a><span data-ttu-id="c323c-109">需要授权可访问的页面</span><span class="sxs-lookup"><span data-stu-id="c323c-109">Require authorization to access a page</span></span>

<span data-ttu-id="c323c-110">使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到页中指定的路径：</span><span class="sxs-lookup"><span data-stu-id="c323c-110">Use the [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/sample/Startup.cs?name=snippet1&highlight=2,4)]

<span data-ttu-id="c323c-111">指定的路径是视图引擎路径，这是无需扩展和包含仅正斜杠的 Razor 页根相对路径。</span><span class="sxs-lookup"><span data-stu-id="c323c-111">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

<span data-ttu-id="c323c-112">[AuthorizePage 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)当你需要指定一个授权策略才可用。</span><span class="sxs-lookup"><span data-stu-id="c323c-112">An [AuthorizePage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

## <a name="require-authorization-to-access-a-folder-of-pages"></a><span data-ttu-id="c323c-113">需要的页的文件夹的访问权</span><span class="sxs-lookup"><span data-stu-id="c323c-113">Require authorization to access a folder of pages</span></span>

<span data-ttu-id="c323c-114">使用[AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到所有指定路径上的文件夹中的页：</span><span class="sxs-lookup"><span data-stu-id="c323c-114">Use the [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/sample/Startup.cs?name=snippet1&highlight=2,5)]

<span data-ttu-id="c323c-115">指定的路径是视图引擎路径，这是 Razor 页根相对路径。</span><span class="sxs-lookup"><span data-stu-id="c323c-115">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

<span data-ttu-id="c323c-116">[AuthorizeFolder 重载](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)当你需要指定一个授权策略才可用。</span><span class="sxs-lookup"><span data-stu-id="c323c-116">An [AuthorizeFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

## <a name="allow-anonymous-access-to-a-page"></a><span data-ttu-id="c323c-117">允许匿名访问的页</span><span class="sxs-lookup"><span data-stu-id="c323c-117">Allow anonymous access to a page</span></span>

<span data-ttu-id="c323c-118">使用[AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到指定的路径下的网页：</span><span class="sxs-lookup"><span data-stu-id="c323c-118">Use the [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to a page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/sample/Startup.cs?name=snippet1&highlight=2,6)]

<span data-ttu-id="c323c-119">指定的路径是视图引擎路径，这是无需扩展和包含仅正斜杠的 Razor 页根相对路径。</span><span class="sxs-lookup"><span data-stu-id="c323c-119">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a><span data-ttu-id="c323c-120">允许匿名访问的页面的文件夹</span><span class="sxs-lookup"><span data-stu-id="c323c-120">Allow anonymous access to a folder of pages</span></span>

<span data-ttu-id="c323c-121">使用[AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder)通过约定[AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions)添加[AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到所有指定路径上的文件夹中的页：</span><span class="sxs-lookup"><span data-stu-id="c323c-121">Use the [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/sample/Startup.cs?name=snippet1&highlight=2,7)]

<span data-ttu-id="c323c-122">指定的路径是视图引擎路径，这是 Razor 页根相对路径。</span><span class="sxs-lookup"><span data-stu-id="c323c-122">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

## <a name="note-on-combining-authorized-and-anonymous-access"></a><span data-ttu-id="c323c-123">请注意有关组合授权和匿名访问</span><span class="sxs-lookup"><span data-stu-id="c323c-123">Note on combining authorized and anonymous access</span></span>

<span data-ttu-id="c323c-124">这是完全合法，若要指定的页的文件夹需要授权，并指定该文件夹中的页允许匿名访问：</span><span class="sxs-lookup"><span data-stu-id="c323c-124">It's perfectly valid to specify that a folder of pages require authorization and specify that a page within that folder allows anonymous access:</span></span>

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

<span data-ttu-id="c323c-125">但是，反过来，不是如此。</span><span class="sxs-lookup"><span data-stu-id="c323c-125">The reverse, however, isn't true.</span></span> <span data-ttu-id="c323c-126">不能声明用于匿名访问的页面的文件夹，并指定授权中的页：</span><span class="sxs-lookup"><span data-stu-id="c323c-126">You can't declare a folder of pages for anonymous access and specify a page within for authorization:</span></span>

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

<span data-ttu-id="c323c-127">需要专用的页上的授权不起作用，因为当同时`AllowAnonymousFilter`和`AuthorizeFilter`筛选器应用到页上， `AllowAnonymousFilter` wins 和控制的访问。</span><span class="sxs-lookup"><span data-stu-id="c323c-127">Requiring authorization on the Private page won't work because when both the `AllowAnonymousFilter` and `AuthorizeFilter` filters are applied to the page, the `AllowAnonymousFilter` wins and controls access.</span></span>

## <a name="see-also"></a><span data-ttu-id="c323c-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="c323c-128">See also</span></span>

* [<span data-ttu-id="c323c-129">Razor 页面自定义路由和页面模型提供程序</span><span class="sxs-lookup"><span data-stu-id="c323c-129">Razor Pages custom route and page model providers</span></span>](xref:mvc/razor-pages/razor-pages-convention-features)
* <span data-ttu-id="c323c-130">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection)类</span><span class="sxs-lookup"><span data-stu-id="c323c-130">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) class</span></span>
