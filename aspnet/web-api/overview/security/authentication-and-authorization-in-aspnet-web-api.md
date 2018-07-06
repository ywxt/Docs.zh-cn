---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: 身份验证和 ASP.NET Web API 中的授权 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 中提供身份验证和授权的一般的概述。
ms.author: aspnetcontent
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f882a9bb2922d0eb28eee7cdba0896bdc5318c2a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812829"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="397ef-103">身份验证和 ASP.NET Web API 中的授权</span><span class="sxs-lookup"><span data-stu-id="397ef-103">Authentication and Authorization in ASP.NET Web API</span></span>
====================
<span data-ttu-id="397ef-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="397ef-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="397ef-105">您已经创建的 web API，但现在你想要控制对它的访问。</span><span class="sxs-lookup"><span data-stu-id="397ef-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="397ef-106">在本系列的文章，我们将介绍一些选项用于保护 web API 从未经授权的用户。</span><span class="sxs-lookup"><span data-stu-id="397ef-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="397ef-107">本系列教程将介绍身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="397ef-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="397ef-108">*身份验证*知道用户的标识。</span><span class="sxs-lookup"><span data-stu-id="397ef-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="397ef-109">例如，Alice 使用她的用户名和密码，登录和服务器使用密码进行身份验证 Alice。</span><span class="sxs-lookup"><span data-stu-id="397ef-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="397ef-110">*授权*确定是否允许用户执行的操作。</span><span class="sxs-lookup"><span data-stu-id="397ef-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="397ef-111">例如，Alice 有权获取资源，但不是创建资源。</span><span class="sxs-lookup"><span data-stu-id="397ef-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="397ef-112">序列中的第一篇文章为 ASP.NET Web API 中提供了身份验证和授权的一般概述。</span><span class="sxs-lookup"><span data-stu-id="397ef-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="397ef-113">其他主题介绍的 Web API 的常见身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="397ef-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="397ef-114">衷心感谢查看这一系列和提供有价值的反馈的人员： Rick Anderson、 Levi Broderick、 Barry Dorrans、 Tom Dykstra、 Hongmei Ge、 David Matson、 Daniel Roth、 Tim Teebken。</span><span class="sxs-lookup"><span data-stu-id="397ef-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>


## <a name="authentication"></a><span data-ttu-id="397ef-115">身份验证</span><span class="sxs-lookup"><span data-stu-id="397ef-115">Authentication</span></span>

<span data-ttu-id="397ef-116">Web API 假定该身份验证发生在主机中。</span><span class="sxs-lookup"><span data-stu-id="397ef-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="397ef-117">对于 web 承载的该主机是 IIS，使用 HTTP 模块进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="397ef-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="397ef-118">可以将项目配置为使用任何 IIS 或 ASP.NET 中，在中内置的身份验证模块，也可以编写自己的 HTTP 模块来执行自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="397ef-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="397ef-119">当主机对用户进行身份验证时，它会创建*主体*，即[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)表示运行代码的安全上下文的对象。</span><span class="sxs-lookup"><span data-stu-id="397ef-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="397ef-120">主机的设置将主体附加到当前线程**Thread.CurrentPrincipal**。</span><span class="sxs-lookup"><span data-stu-id="397ef-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="397ef-121">主体包含一个关联**标识**对象，其中包含有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="397ef-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="397ef-122">如果用户进行身份验证， **Identity.IsAuthenticated**属性将返回**true**。</span><span class="sxs-lookup"><span data-stu-id="397ef-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="397ef-123">对于匿名请求，请**IsAuthenticated**返回**false**。</span><span class="sxs-lookup"><span data-stu-id="397ef-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="397ef-124">有关主体的详细信息，请参阅[基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="397ef-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="397ef-125">HTTP 消息处理程序进行身份验证</span><span class="sxs-lookup"><span data-stu-id="397ef-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="397ef-126">而不是使用主机进行身份验证，您可以将身份验证逻辑注入[HTTP 消息处理程序](../advanced/http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="397ef-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="397ef-127">在这种情况下，消息处理程序将检查 HTTP 请求和设置的主体。</span><span class="sxs-lookup"><span data-stu-id="397ef-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="397ef-128">何时应使用消息处理程序进行身份验证？</span><span class="sxs-lookup"><span data-stu-id="397ef-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="397ef-129">下面是一些相关的利弊：</span><span class="sxs-lookup"><span data-stu-id="397ef-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="397ef-130">一个 HTTP 模块，会看到通过 ASP.NET 管道的所有请求。</span><span class="sxs-lookup"><span data-stu-id="397ef-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="397ef-131">消息处理程序只看到路由到 Web API 的请求。</span><span class="sxs-lookup"><span data-stu-id="397ef-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="397ef-132">可以该对话框允许你将身份验证方案应用于特定的路由设置每个路由消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="397ef-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="397ef-133">HTTP 模块是特定于 IIS。</span><span class="sxs-lookup"><span data-stu-id="397ef-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="397ef-134">消息处理程序主机不可知的以便它们可以与 web 宿主和自承载使用。</span><span class="sxs-lookup"><span data-stu-id="397ef-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="397ef-135">HTTP 模块加入 IIS 日志记录、 审核和等等。</span><span class="sxs-lookup"><span data-stu-id="397ef-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="397ef-136">HTTP 模块前面在管道中运行。</span><span class="sxs-lookup"><span data-stu-id="397ef-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="397ef-137">如果处理消息处理程序中的身份验证，该主体不会不获取或设置处理程序运行之前。</span><span class="sxs-lookup"><span data-stu-id="397ef-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="397ef-138">此外，该主体会还原为以前的主体时在响应离开消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="397ef-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="397ef-139">通常情况下，如果您不需要以支持自托管，HTTP 模块是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="397ef-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="397ef-140">如果你需要支持自托管，请考虑消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="397ef-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="397ef-141">设置主体</span><span class="sxs-lookup"><span data-stu-id="397ef-141">Setting the Principal</span></span>

<span data-ttu-id="397ef-142">如果你的应用程序执行的任何自定义身份验证逻辑，则必须在两个位置上设置主体：</span><span class="sxs-lookup"><span data-stu-id="397ef-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="397ef-143">**Thread.CurrentPrincipal**。</span><span class="sxs-lookup"><span data-stu-id="397ef-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="397ef-144">此属性是在.NET 中设置线程的主体的标准方法。</span><span class="sxs-lookup"><span data-stu-id="397ef-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="397ef-145">**HttpContext.Current.User**。</span><span class="sxs-lookup"><span data-stu-id="397ef-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="397ef-146">此属性是特定于 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="397ef-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="397ef-147">下面的代码演示如何设置主体：</span><span class="sxs-lookup"><span data-stu-id="397ef-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="397ef-148">对于 web 承载的必须设置主体，在这两个位置;否则的安全上下文可能会变得不一致。</span><span class="sxs-lookup"><span data-stu-id="397ef-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="397ef-149">对于自承载，但是， **HttpContext.Current**为 null。</span><span class="sxs-lookup"><span data-stu-id="397ef-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="397ef-150">若要确保你的代码与主机无关，因此之前, 检查 null 分配到**HttpContext.Current**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="397ef-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="397ef-151">授权</span><span class="sxs-lookup"><span data-stu-id="397ef-151">Authorization</span></span>

<span data-ttu-id="397ef-152">授权发生在管道中，更高版本更接近于该控制器。</span><span class="sxs-lookup"><span data-stu-id="397ef-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="397ef-153">允许您授予对资源的访问时进行更精细的选择。</span><span class="sxs-lookup"><span data-stu-id="397ef-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="397ef-154">*授权筛选器*控制器操作之前运行。</span><span class="sxs-lookup"><span data-stu-id="397ef-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="397ef-155">如果请求未获得授权，筛选器返回错误响应，并不调用操作。</span><span class="sxs-lookup"><span data-stu-id="397ef-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="397ef-156">中的控制器操作，可以获取从当前的主体**ApiController.User**属性。</span><span class="sxs-lookup"><span data-stu-id="397ef-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="397ef-157">例如，您可能会筛选基于用户名称的资源的列表返回属于该用户的资源。</span><span class="sxs-lookup"><span data-stu-id="397ef-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="397ef-158">使用 [授权] 属性</span><span class="sxs-lookup"><span data-stu-id="397ef-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="397ef-159">Web API 提供了内置的授权筛选器， [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="397ef-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="397ef-160">此筛选器检查用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="397ef-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="397ef-161">如果没有，它将返回 HTTP 状态代码 401 （未经授权），而无需调用该操作。</span><span class="sxs-lookup"><span data-stu-id="397ef-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="397ef-162">您可以应用筛选器全局范围内，在控制器级别，或在单个操作级别。</span><span class="sxs-lookup"><span data-stu-id="397ef-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="397ef-163">**全局**： 若要限制访问的每个 Web API 控制器，请添加**AuthorizeAttribute**向全局筛选器列表的筛选器：</span><span class="sxs-lookup"><span data-stu-id="397ef-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="397ef-164">**控制器**： 若要限制访问特定控制器，请添加筛选器作为属性到控制器：</span><span class="sxs-lookup"><span data-stu-id="397ef-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="397ef-165">**操作**： 若要限制特定操作的访问权限，请将属性添加到操作方法：</span><span class="sxs-lookup"><span data-stu-id="397ef-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="397ef-166">或者，可以限制控制器并再允许匿名访问特定操作使用`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="397ef-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="397ef-167">在以下示例中，`Post`方法受到限制，但`Get`方法允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="397ef-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="397ef-168">在上一示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;仅匿名用户进行。您还可以限制对特定用户或特定角色的用户访问：</span><span class="sxs-lookup"><span data-stu-id="397ef-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="397ef-169">**AuthorizeAttribute** Web API 控制器的筛选器位于**System.Web.Http**命名空间。</span><span class="sxs-lookup"><span data-stu-id="397ef-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="397ef-170">还有一个类似的筛选器中的 MVC 控制器**System.Web.Mvc**命名空间，与 Web API 控制器不兼容。</span><span class="sxs-lookup"><span data-stu-id="397ef-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>


### <a name="custom-authorization-filters"></a><span data-ttu-id="397ef-171">自定义授权筛选器</span><span class="sxs-lookup"><span data-stu-id="397ef-171">Custom Authorization Filters</span></span>

<span data-ttu-id="397ef-172">若要编写自定义授权筛选器，派生自其中一种类型：</span><span class="sxs-lookup"><span data-stu-id="397ef-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="397ef-173">**AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="397ef-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="397ef-174">扩展此类来执行基于当前用户和用户的角色的授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="397ef-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="397ef-175">**AuthorizationFilterAttribute**。</span><span class="sxs-lookup"><span data-stu-id="397ef-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="397ef-176">扩展此类来执行不一定是基于当前用户或角色的同步的授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="397ef-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="397ef-177">**IAuthorizationFilter**。</span><span class="sxs-lookup"><span data-stu-id="397ef-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="397ef-178">实现此接口可执行异步授权逻辑;例如，如果你的授权逻辑执行异步 I/O 或网络调用。</span><span class="sxs-lookup"><span data-stu-id="397ef-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="397ef-179">(如果授权逻辑是 CPU 绑定的它会更易于派生自**AuthorizationFilterAttribute**，因为不需要编写异步方法。)</span><span class="sxs-lookup"><span data-stu-id="397ef-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="397ef-180">下图显示的类层次结构**AuthorizeAttribute**类。</span><span class="sxs-lookup"><span data-stu-id="397ef-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="397ef-181">在控制器操作中的授权</span><span class="sxs-lookup"><span data-stu-id="397ef-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="397ef-182">在某些情况下，可能允许继续，但更改行为基于主体的请求。</span><span class="sxs-lookup"><span data-stu-id="397ef-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="397ef-183">例如，返回的信息可能会更改具体取决于用户的角色。</span><span class="sxs-lookup"><span data-stu-id="397ef-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="397ef-184">在控制器方法中，可以获取从当前的原则**ApiController.User**属性。</span><span class="sxs-lookup"><span data-stu-id="397ef-184">Within a controller method, you can get the current principle from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
