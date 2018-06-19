---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 中的身份验证筛选器 |Microsoft 文档
author: MikeWasson
description: 身份验证筛选器是对 HTTP 请求进行身份验证的组件。 Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/25/2014
ms.topic: article
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 16e451f52799625983368bc938091eff47019b52
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
ms.locfileid: "29153513"
---
<a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="9c89b-104">ASP.NET Web API 2 中的身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="9c89b-104">Authentication Filters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="9c89b-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9c89b-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="9c89b-106">身份验证筛选器是对 HTTP 请求进行身份验证的组件。</span><span class="sxs-lookup"><span data-stu-id="9c89b-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="9c89b-107">Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同，主要是在筛选器接口的命名约定。</span><span class="sxs-lookup"><span data-stu-id="9c89b-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="9c89b-108">本主题描述了 Web API 身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-108">This topic describes Web API authentication filters.</span></span>


<span data-ttu-id="9c89b-109">身份验证筛选器使你能够为各个控制器或操作设置身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9c89b-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="9c89b-110">这样一来，你的应用程序可以为不同的 HTTP 资源支持不同的身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="9c89b-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="9c89b-111">在本文中，我将展示代码从[基本身份验证](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt)示例上[http://aspnet.codeplex.com](http://aspnet.codeplex.com)。此示例演示实现 HTTP 基本访问身份验证方案 (RFC 2617) 的身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-111">In this article, I'll show code from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample on [http://aspnet.codeplex.com](http://aspnet.codeplex.com). The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="9c89b-112">名为类中实现筛选器`IdentityBasicAuthenticationAttribute`。</span><span class="sxs-lookup"><span data-stu-id="9c89b-112">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="9c89b-113">我不会显示所有的示例代码演示如何编写一个身份验证筛选器中的部分。</span><span class="sxs-lookup"><span data-stu-id="9c89b-113">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="9c89b-114">将身份验证筛选器设置</span><span class="sxs-lookup"><span data-stu-id="9c89b-114">Setting an Authentication Filter</span></span>

<span data-ttu-id="9c89b-115">与其他过滤器一样身份验证筛选器可以应用的每个控制器，每个操作或全局范围内为所有 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-115">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="9c89b-116">若要应用到的控制器的身份验证筛选器，修饰具有筛选器属性的控制器类。</span><span class="sxs-lookup"><span data-stu-id="9c89b-116">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="9c89b-117">下面的代码设置`[IdentityBasicAuthentication]`上了控制器类，它使所有控制器的操作的基本身份验证的筛选器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-117">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="9c89b-118">若要应用到一个操作筛选器，请使用筛选器修饰操作。</span><span class="sxs-lookup"><span data-stu-id="9c89b-118">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="9c89b-119">下面的代码设置`[IdentityBasicAuthentication]`在控制器上的筛选器`Post`方法。</span><span class="sxs-lookup"><span data-stu-id="9c89b-119">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="9c89b-120">若要将筛选器应用于所有的 Web API 控制器，将其添加到**GlobalConfiguration.Filters**。</span><span class="sxs-lookup"><span data-stu-id="9c89b-120">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="9c89b-121">实现 Web API 身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="9c89b-121">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="9c89b-122">在 Web API 中，身份验证筛选器实现[System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="9c89b-122">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="9c89b-123">它们还应从继承**System.Attribute**，以便作为属性被应用。</span><span class="sxs-lookup"><span data-stu-id="9c89b-123">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="9c89b-124">**IAuthenticationFilter**接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="9c89b-124">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="9c89b-125">**AuthenticateAsync**正在验证在请求中，凭据进行身份验证请求，如果存在。</span><span class="sxs-lookup"><span data-stu-id="9c89b-125">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="9c89b-126">**ChallengeAsync** HTTP 响应中，如果需要添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="9c89b-126">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="9c89b-127">这些方法对应于在中定义的身份验证流[RFC 2612](http://tools.ietf.org/html/rfc2616)和[RFC 2617](http://tools.ietf.org/html/rfc2617):</span><span class="sxs-lookup"><span data-stu-id="9c89b-127">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="9c89b-128">客户端将 Authorization 标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="9c89b-128">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="9c89b-129">这通常发生在客户端从服务器收到 401 （未经授权） 响应之后。</span><span class="sxs-lookup"><span data-stu-id="9c89b-129">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="9c89b-130">但是，客户端可以发送凭据的任何请求，而不仅仅是后获取 401。</span><span class="sxs-lookup"><span data-stu-id="9c89b-130">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="9c89b-131">如果服务器不接受凭据，则将返回 401 （未经授权） 响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-131">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="9c89b-132">响应包含 Www-authenticate 标头，包含一个或多个挑战。</span><span class="sxs-lookup"><span data-stu-id="9c89b-132">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="9c89b-133">每个质询指定服务器识别身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="9c89b-133">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="9c89b-134">服务器还可以通过匿名请求返回 401。</span><span class="sxs-lookup"><span data-stu-id="9c89b-134">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="9c89b-135">事实上，这通常是如何启动身份验证过程：</span><span class="sxs-lookup"><span data-stu-id="9c89b-135">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="9c89b-136">客户端发送的匿名请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-136">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="9c89b-137">服务器将返回 401。</span><span class="sxs-lookup"><span data-stu-id="9c89b-137">The server returns 401.</span></span>
3. <span data-ttu-id="9c89b-138">客户端重新发送凭据的请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-138">The clients resends the request with credentials.</span></span>

<span data-ttu-id="9c89b-139">此流同时包含*身份验证*和*授权*步骤。</span><span class="sxs-lookup"><span data-stu-id="9c89b-139">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="9c89b-140">身份验证证明客户端的标识。</span><span class="sxs-lookup"><span data-stu-id="9c89b-140">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="9c89b-141">授权确定客户端是否可以访问特定资源。</span><span class="sxs-lookup"><span data-stu-id="9c89b-141">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="9c89b-142">在 Web API 中，身份验证筛选器处理身份验证，但未授权。</span><span class="sxs-lookup"><span data-stu-id="9c89b-142">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="9c89b-143">应完成授权，授权筛选器或内的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9c89b-143">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="9c89b-144">下面是在 Web API 2 管道中的流：</span><span class="sxs-lookup"><span data-stu-id="9c89b-144">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="9c89b-145">在调用操作之前, Web API 创建针对该操作的身份验证筛选器列表。</span><span class="sxs-lookup"><span data-stu-id="9c89b-145">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="9c89b-146">这包括操作作用域、 控制器作用域和全局范围的筛选的器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-146">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="9c89b-147">Web API 调用**AuthenticateAsync**列表中每个筛选器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-147">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="9c89b-148">每个筛选器来验证请求中的凭据。</span><span class="sxs-lookup"><span data-stu-id="9c89b-148">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="9c89b-149">如果任何筛选器已成功验证凭据，筛选器创建**IPrincipal**并将其附加到请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-149">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="9c89b-150">筛选器还可以在此时触发错误。</span><span class="sxs-lookup"><span data-stu-id="9c89b-150">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="9c89b-151">如果是这样，则不运行的管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="9c89b-151">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="9c89b-152">假设没有错误，请求流经管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="9c89b-152">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="9c89b-153">最后，Web API 调用每个身份验证筛选器的**ChallengeAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="9c89b-153">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="9c89b-154">筛选器使用此方法将一项挑战添加到响应中，如果需要。</span><span class="sxs-lookup"><span data-stu-id="9c89b-154">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="9c89b-155">通常 （但不是总是），将发生在 401 错误响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-155">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="9c89b-156">下图显示了两种可能的情况。</span><span class="sxs-lookup"><span data-stu-id="9c89b-156">The following diagrams show two possible cases.</span></span> <span data-ttu-id="9c89b-157">在第一个，身份验证筛选器已成功验证该请求、 授权筛选器将为请求，授权和控制器操作返回 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="9c89b-157">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="9c89b-158">在第二个示例中，身份验证筛选器进行身份验证请求，但授权筛选器返回 401 （未授权）。</span><span class="sxs-lookup"><span data-stu-id="9c89b-158">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="9c89b-159">在这种情况下，不调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9c89b-159">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="9c89b-160">身份验证筛选器将 Www-authenticate 标头添加到响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-160">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="9c89b-161">其他组合可能会出现&mdash;例如，如果控制器操作允许匿名请求，你可能有一个身份验证的筛选器，但没有授权。</span><span class="sxs-lookup"><span data-stu-id="9c89b-161">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="9c89b-162">实现 AuthenticateAsync 方法</span><span class="sxs-lookup"><span data-stu-id="9c89b-162">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="9c89b-163">**AuthenticateAsync**方法尝试进行身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-163">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="9c89b-164">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="9c89b-164">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="9c89b-165">**AuthenticateAsync**方法必须执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="9c89b-165">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="9c89b-166">执行任何操作 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="9c89b-166">Nothing (no-op).</span></span>
2. <span data-ttu-id="9c89b-167">创建**IPrincipal**并将其设置针对此请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-167">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="9c89b-168">设置了错误的结果。</span><span class="sxs-lookup"><span data-stu-id="9c89b-168">Set an error result.</span></span>

<span data-ttu-id="9c89b-169">选项 (1) 表示请求中未包含任何筛选器理解的凭据。</span><span class="sxs-lookup"><span data-stu-id="9c89b-169">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="9c89b-170">选项 (2) 意味着筛选器成功通过身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-170">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="9c89b-171">选项 (3) 意味着请求具有无效凭据、 （如错误的密码），随即将会触发错误响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-171">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="9c89b-172">下面是用于实现的通用大纲**AuthenticateAsync**。</span><span class="sxs-lookup"><span data-stu-id="9c89b-172">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="9c89b-173">查找在请求中的凭据。</span><span class="sxs-lookup"><span data-stu-id="9c89b-173">Look for credentials in the request.</span></span>
2. <span data-ttu-id="9c89b-174">如果不有任何凭据，则不执行任何操作并返回 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="9c89b-174">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="9c89b-175">如果凭据，但筛选器无法识别的身份验证方案，不执行任何操作并返回 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="9c89b-175">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="9c89b-176">管道中的另一个筛选器可能理解此方案。</span><span class="sxs-lookup"><span data-stu-id="9c89b-176">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="9c89b-177">如果有筛选器理解的凭据，请尝试对它们进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c89b-177">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="9c89b-178">如果凭据错误，请通过设置返回 401 `context.ErrorResult`。</span><span class="sxs-lookup"><span data-stu-id="9c89b-178">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="9c89b-179">如果凭据有效，创建**IPrincipal**并设置`context.Principal`。</span><span class="sxs-lookup"><span data-stu-id="9c89b-179">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="9c89b-180">以下代码所示**AuthenticateAsync**方法从[基本身份验证](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt)示例。</span><span class="sxs-lookup"><span data-stu-id="9c89b-180">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample.</span></span> <span data-ttu-id="9c89b-181">注释中描述每个步骤。</span><span class="sxs-lookup"><span data-stu-id="9c89b-181">The comments indicate each step.</span></span> <span data-ttu-id="9c89b-182">代码演示几种类型的错误： 不带凭据、 格式不正确的凭据和错误的用户名/密码的 Authorization 标头。</span><span class="sxs-lookup"><span data-stu-id="9c89b-182">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="9c89b-183">设置了错误的结果</span><span class="sxs-lookup"><span data-stu-id="9c89b-183">Setting an Error Result</span></span>

<span data-ttu-id="9c89b-184">如果凭据无效，必须设置筛选器`context.ErrorResult`到**IHttpActionResult**创建错误响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-184">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="9c89b-185">有关详细信息**IHttpActionResult**，请参阅[Web API 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="9c89b-185">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="9c89b-186">基本身份验证示例包括`AuthenticationFailureResult`适合于此目的的类。</span><span class="sxs-lookup"><span data-stu-id="9c89b-186">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="9c89b-187">实现 ChallengeAsync</span><span class="sxs-lookup"><span data-stu-id="9c89b-187">Implementing ChallengeAsync</span></span>

<span data-ttu-id="9c89b-188">用途**ChallengeAsync**方法是将添加身份验证质询的响应，如果需要。</span><span class="sxs-lookup"><span data-stu-id="9c89b-188">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="9c89b-189">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="9c89b-189">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="9c89b-190">在请求管道中每个身份验证筛选器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="9c89b-190">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="9c89b-191">务必了解， **ChallengeAsync**称为*之前*HTTP 响应已创建，且可能甚至在控制器操作运行之前。</span><span class="sxs-lookup"><span data-stu-id="9c89b-191">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="9c89b-192">当**ChallengeAsync**调用时，`context.Result`包含**IHttpActionResult**，用于更高版本创建的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-192">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="9c89b-193">因此，在**ChallengeAsync**是调用，你不知道有关 HTTP 响应的任何尚未。</span><span class="sxs-lookup"><span data-stu-id="9c89b-193">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="9c89b-194">**ChallengeAsync**方法应替换的原始值`context.Result`用新**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="9c89b-194">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="9c89b-195">这**IHttpActionResult**必须包装原始`context.Result`。</span><span class="sxs-lookup"><span data-stu-id="9c89b-195">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="9c89b-196">我将调用原始**IHttpActionResult** *内部结果*，并且新**IHttpActionResult** *外部结果*。</span><span class="sxs-lookup"><span data-stu-id="9c89b-196">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="9c89b-197">外部结果必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9c89b-197">The outer result must do the following:</span></span>

1. <span data-ttu-id="9c89b-198">调用内部的结果，以创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-198">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="9c89b-199">检查该响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-199">Examine the response.</span></span>
3. <span data-ttu-id="9c89b-200">如果需要请添加身份验证质询的响应。</span><span class="sxs-lookup"><span data-stu-id="9c89b-200">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="9c89b-201">下面的示例摘自基本身份验证示例。</span><span class="sxs-lookup"><span data-stu-id="9c89b-201">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="9c89b-202">它定义**IHttpActionResult**外部的结果。</span><span class="sxs-lookup"><span data-stu-id="9c89b-202">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="9c89b-203">`InnerResult`属性包含内部**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="9c89b-203">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="9c89b-204">`Challenge`属性表示 Www 身份验证标头。</span><span class="sxs-lookup"><span data-stu-id="9c89b-204">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="9c89b-205">请注意， **ExecuteAsync**首先调用`InnerResult.ExecuteAsync`创建 HTTP 响应中，如果需要然后添加所面临的挑战。</span><span class="sxs-lookup"><span data-stu-id="9c89b-205">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="9c89b-206">添加所面临的挑战之前检查响应代码。</span><span class="sxs-lookup"><span data-stu-id="9c89b-206">Check the response code before adding the challenge.</span></span> <span data-ttu-id="9c89b-207">大多数身份验证方案只能添加一项挑战如果响应为 401，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9c89b-207">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="9c89b-208">但是，某些身份验证方案希望向成功响应添加一项挑战。</span><span class="sxs-lookup"><span data-stu-id="9c89b-208">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="9c89b-209">有关示例，请参阅[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)。</span><span class="sxs-lookup"><span data-stu-id="9c89b-209">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="9c89b-210">给定`AddChallengeOnUnauthorizedResult`类中的实际代码**ChallengeAsync**很简单。</span><span class="sxs-lookup"><span data-stu-id="9c89b-210">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="9c89b-211">你刚刚创建的结果，并将其附加到`context.Result`。</span><span class="sxs-lookup"><span data-stu-id="9c89b-211">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="9c89b-212">注意： 基本身份验证示例提取此逻辑有点，通过将其放置在扩展方法。</span><span class="sxs-lookup"><span data-stu-id="9c89b-212">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="9c89b-213">组合使用主机级身份验证的身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="9c89b-213">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="9c89b-214">"主机级身份验证"在请求到达 Web API 框架之前是由 （如 IIS)，主机的身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c89b-214">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="9c89b-215">通常情况下，你可能想要启用你的应用程序的其余部分的主机级身份验证，但禁用它为你的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="9c89b-215">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="9c89b-216">例如，典型的方案是启用表单身份验证在主机级别，但对 Web API 使用基于令牌的身份验证。</span><span class="sxs-lookup"><span data-stu-id="9c89b-216">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="9c89b-217">若要禁用 Web API 管道内的主机级身份验证，调用`config.SuppressHostPrincipal()`中你的配置。</span><span class="sxs-lookup"><span data-stu-id="9c89b-217">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="9c89b-218">这会导致 Web API 删除**IPrincipal**从输入 Web API 管道的任何请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-218">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="9c89b-219">实际上，它&quot;取消的进行身份验证&quot;请求。</span><span class="sxs-lookup"><span data-stu-id="9c89b-219">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="9c89b-220">其他资源</span><span class="sxs-lookup"><span data-stu-id="9c89b-220">Additional Resources</span></span>

<span data-ttu-id="9c89b-221">[ASP.NET Web API 安全筛选](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 杂志）</span><span class="sxs-lookup"><span data-stu-id="9c89b-221">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
