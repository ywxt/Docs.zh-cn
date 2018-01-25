---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: "身份验证和 ASP.NET Web API 中的授权 |Microsoft 文档"
author: MikeWasson
description: "ASP.NET Web API 中提供了身份验证和授权的常规概述。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/27/2012
ms.topic: article
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 2a4b5ed8a712b061b4afdf5a3adc9378dd72b37f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="9c9d9-103">身份验证和 ASP.NET Web API 中的授权</span><span class="sxs-lookup"><span data-stu-id="9c9d9-103">Authentication and Authorization in ASP.NET Web API</span></span>
====================
<span data-ttu-id="9c9d9-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9c9d9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9c9d9-105">您已经创建 web API，但现在你想要控制对它的访问。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="9c9d9-106">在此系列文章中，我们将查看从未经授权的用户保护 web API 的一些选项。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="9c9d9-107">这一系列将介绍身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="9c9d9-108">*身份验证*知道用户的标识。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="9c9d9-109">例如，Alice 使用她的用户名和密码，登录和服务器使用密码进行身份验证 Alice。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="9c9d9-110">*授权*确定是否允许用户执行操作。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="9c9d9-111">例如，Alice 已获取资源，但不是创建资源的权限。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="9c9d9-112">序列中的第一篇文章提供了 ASP.NET Web API 中的身份验证和授权的常规概述。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="9c9d9-113">其他主题说明为 Web API 的常见身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="9c9d9-114">感谢人都可以查看这一系列并提供有价值的反馈： Rick Anderson、 Levi Broderick、 Barry Dorrans、 Tom Dykstra、 Hongmei Ge、 David Matson、 Daniel Roth、 Tim Teebken。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>


## <a name="authentication"></a><span data-ttu-id="9c9d9-115">身份验证</span><span class="sxs-lookup"><span data-stu-id="9c9d9-115">Authentication</span></span>

<span data-ttu-id="9c9d9-116">Web API 假定该身份验证发生在主机。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="9c9d9-117">对于 web 承载的该主机是 IIS，使用 HTTP 模块进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="9c9d9-118">你可以配置你的项目中使用任何内置于 IIS 或 ASP.NET 中，身份验证模块或编写自己的 HTTP 模块来执行自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="9c9d9-119">当主机对用户进行身份验证时，它将创建*主体*，即[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)表示运行代码的安全上下文的对象。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="9c9d9-120">主机将主体附加到当前线程，通过设置**Thread.CurrentPrincipal**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="9c9d9-121">主体包含一个关联**标识**对象，其中包含有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="9c9d9-122">如果用户进行身份验证， **Identity.IsAuthenticated**属性返回**true**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="9c9d9-123">对于匿名请求， **IsAuthenticated**返回**false**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="9c9d9-124">有关主体的详细信息，请参阅[基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="9c9d9-125">HTTP 消息处理程序进行身份验证</span><span class="sxs-lookup"><span data-stu-id="9c9d9-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="9c9d9-126">而不是使用进行身份验证的主机，你可以将身份验证逻辑注入[HTTP 消息处理程序](../advanced/http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="9c9d9-127">在这种情况下，消息处理程序将检查 HTTP 请求和设置的主体。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="9c9d9-128">如果应将消息处理程序用于身份验证？</span><span class="sxs-lookup"><span data-stu-id="9c9d9-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="9c9d9-129">下面是一些的折衷方案：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="9c9d9-130">HTTP 模块会看到通过 ASP.NET 管道的所有请求。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="9c9d9-131">消息处理程序只看到路由到 Web API 的请求。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="9c9d9-132">你可以设置每个路由消息处理程序，，这样就可以应用于特定的路由的身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="9c9d9-133">HTTP 模块是特定于 IIS。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="9c9d9-134">消息处理程序是主机无关，因此它们可以用于 web 承载和自承载。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="9c9d9-135">HTTP 模块参与 IIS 日志记录、 审核和等等。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="9c9d9-136">HTTP 模块运行之前在管道中。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="9c9d9-137">如果处理消息处理程序中的身份验证时，主体不获取或设置处理程序运行之前。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="9c9d9-138">此外，主体数据库将恢复到以前的主体时响应离开的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="9c9d9-139">通常，如果你不需要支持自承载，则 HTTP 模块是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="9c9d9-140">如果你需要支持自承载，请考虑消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="9c9d9-141">设置主体</span><span class="sxs-lookup"><span data-stu-id="9c9d9-141">Setting the Principal</span></span>

<span data-ttu-id="9c9d9-142">如果你的应用程序执行的任何自定义身份验证逻辑，则必须在两个位置上设置主体：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="9c9d9-143">**Thread.CurrentPrincipal**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="9c9d9-144">此属性是在.NET 中设置线程的主体的标准方式。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="9c9d9-145">**HttpContext.Current.User**.</span><span class="sxs-lookup"><span data-stu-id="9c9d9-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="9c9d9-146">此属性是特定于 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="9c9d9-147">下面的代码演示如何设置主体：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="9c9d9-148">对于 web 承载的您必须在这两个位置; 设置主体否则的安全上下文可能会变得不一致。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="9c9d9-149">对于自承载，但是， **HttpContext.Current**为 null。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="9c9d9-150">若要确保你的代码是不可知的主机，因此，null 之前检查向分配**HttpContext.Current**，如所示。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="9c9d9-151">授权</span><span class="sxs-lookup"><span data-stu-id="9c9d9-151">Authorization</span></span>

<span data-ttu-id="9c9d9-152">授权发生更高版本在管道中，更接近于控制器。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="9c9d9-153">该视图使你作出更精细的选择，如果您授予对资源的访问。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="9c9d9-154">*授权筛选器*之前的控制器操作运行。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="9c9d9-155">如果请求未被授权，筛选器将返回错误响应，并且未调用的操作。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="9c9d9-156">中的控制器操作，你可以从当前主体**ApiController.User**属性。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="9c9d9-157">例如，您可以筛选基于用户名称的资源的列表返回只能属于该用户的资源。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="9c9d9-158">使用 [授权] 属性</span><span class="sxs-lookup"><span data-stu-id="9c9d9-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="9c9d9-159">Web API 提供了内置授权筛选器， [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="9c9d9-160">此筛选器检查用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="9c9d9-161">否则，它将返回 HTTP 状态代码 401 （未经授权），而无需调用该操作。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="9c9d9-162">你可以应用筛选器全局范围内，在控制器级别，或 inidivual 操作级别。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-162">You can apply the filter globally, at the controller level, or at the level of inidivual actions.</span></span>

<span data-ttu-id="9c9d9-163">**全局**： 若要限制访问每个 Web API 控制器，请添加**AuthorizeAttribute**到全局筛选器列表的筛选器：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="9c9d9-164">**控制器**： 若要限制为特定控制器的访问，筛选器作为属性添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="9c9d9-165">**操作**： 来限制对特定操作，请将属性添加到操作方法：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="9c9d9-166">或者，你可以限制控制器，然后通过使用允许匿名访问特定操作`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="9c9d9-167">在下面的示例中，`Post`方法是受限制，但`Get`方法允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="9c9d9-168">在前面的示例中，筛选器允许任何经过身份验证的用户才能访问受限制的方法;仅匿名用户将保留。您还可以限制对特定用户或特定角色中的用户访问权限：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="9c9d9-169">**AuthorizeAttribute** Web API 控制器的筛选器位于**System.Web.Http**命名空间。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="9c9d9-170">没有用于 MVC 控制器中的类似筛选器**System.Web.Mvc**命名空间，与 Web API 控制器不兼容。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>


### <a name="custom-authorization-filters"></a><span data-ttu-id="9c9d9-171">自定义授权筛选器</span><span class="sxs-lookup"><span data-stu-id="9c9d9-171">Custom Authorization Filters</span></span>

<span data-ttu-id="9c9d9-172">若要编写自定义授权筛选器，派生自这些类型之一：</span><span class="sxs-lookup"><span data-stu-id="9c9d9-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="9c9d9-173">**AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="9c9d9-174">可扩展此类以执行基于当前用户和用户的角色的授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="9c9d9-175">**AuthorizationFilterAttribute**。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="9c9d9-176">可扩展此类以执行在当前用户或角色不一定基于同步的授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="9c9d9-177">**IAuthorizationFilter**.</span><span class="sxs-lookup"><span data-stu-id="9c9d9-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="9c9d9-178">实现此接口可执行异步授权逻辑;例如，如果你的授权逻辑执行异步 I/O 或网络调用。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="9c9d9-179">(如果你的授权逻辑是 CPU 绑定的它会更易于派生自**AuthorizationFilterAttribute**，因为不需要编写的异步方法。)</span><span class="sxs-lookup"><span data-stu-id="9c9d9-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="9c9d9-180">下图显示的类层次结构**AuthorizeAttribute**类。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="9c9d9-181">内的控制器操作的授权</span><span class="sxs-lookup"><span data-stu-id="9c9d9-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="9c9d9-182">在某些情况下，可能允许继续，但更改基于主体的行为的请求。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="9c9d9-183">例如，返回的信息可能会更改具体取决于用户的角色。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="9c9d9-184">在控制器方法中，你可以从当前的原则**ApiController.User**属性。</span><span class="sxs-lookup"><span data-stu-id="9c9d9-184">Within a controller method, you can get the current principle from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
