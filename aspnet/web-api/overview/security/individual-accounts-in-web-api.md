---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 保护 Web API 与单个帐户和 ASP.NET Web API 2.2 中的本地登录名 |Microsoft 文档
author: MikeWasson
description: 本主题说明如何保护 web API 使用 OAuth2 对成员资格数据库进行身份验证。 在教程的 Visual Studio 201 中使用的软件版本...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/15/2014
ms.topic: article
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: e2056e769edf972cba830b31cf37f6418148ca73
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a><span data-ttu-id="c0b0f-104">保护 Web API 与单个帐户和 ASP.NET Web API 2.2 中的本地登录名</span><span class="sxs-lookup"><span data-stu-id="c0b0f-104">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="c0b0f-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c0b0f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c0b0f-106">下载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="c0b0f-106">Download Sample App</span></span>](https://github.com/MikeWasson/LocalAccountsApp)

> <span data-ttu-id="c0b0f-107">本主题说明如何保护 web API 使用 OAuth2 对成员资格数据库进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-107">This topic shows how to secure a web API using OAuth2 to authenticate against a membership database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c0b0f-108">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="c0b0f-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="c0b0f-109">Visual Studio 2013 Update 3</span><span class="sxs-lookup"><span data-stu-id="c0b0f-109">Visual Studio 2013 Update 3</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="c0b0f-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="c0b0f-110">Web API 2.2</span></span>](../releases/whats-new-in-aspnet-web-api-22.md)
> - [<span data-ttu-id="c0b0f-111">ASP.NET 标识 2.1</span><span class="sxs-lookup"><span data-stu-id="c0b0f-111">ASP.NET Identity 2.1</span></span>](../../../identity/index.md)


<span data-ttu-id="c0b0f-112">在 Visual Studio 2013 中，Web API 项目模板也提供进行身份验证的三个选项：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-112">In Visual Studio 2013, the Web API project template gives you three options for authentication:</span></span>

- <span data-ttu-id="c0b0f-113">**个人帐户。**</span><span class="sxs-lookup"><span data-stu-id="c0b0f-113">**Individual accounts.**</span></span> <span data-ttu-id="c0b0f-114">该应用使用成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-114">The app uses a membership database.</span></span>
- <span data-ttu-id="c0b0f-115">**组织帐户。**</span><span class="sxs-lookup"><span data-stu-id="c0b0f-115">**Organizational accounts.**</span></span> <span data-ttu-id="c0b0f-116">用户使用其 Azure Active Directory、 Office 365 或本地 Active Directory 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-116">Users sign in with their Azure Active Directory, Office 365, or on-premise Active Directory credentials.</span></span>
- <span data-ttu-id="c0b0f-117">**Windows 身份验证。**</span><span class="sxs-lookup"><span data-stu-id="c0b0f-117">**Windows authentication.**</span></span> <span data-ttu-id="c0b0f-118">此选项适用于 Intranet 应用程序，并使用 Windows 身份验证 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-118">This option is intended for Intranet applications, and uses the Windows Authentication IIS module.</span></span>

<span data-ttu-id="c0b0f-119">有关这些选项的详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-119">For more details about these options, see [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).</span></span>

<span data-ttu-id="c0b0f-120">个人帐户提供了用户登录的两个方法：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-120">Individual accounts provide two ways for a user to log in:</span></span>

- <span data-ttu-id="c0b0f-121">**本地登录**。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-121">**Local login**.</span></span> <span data-ttu-id="c0b0f-122">用户注册在站点上，输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-122">The user registers at the site, entering a username and password.</span></span> <span data-ttu-id="c0b0f-123">应用程序将密码哈希存储在成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-123">The app stores the password hash in the membership database.</span></span> <span data-ttu-id="c0b0f-124">当用户登录时，ASP.NET 标识系统验证密码。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-124">When the user logs in, the ASP.NET Identity system verifies the password.</span></span>
- <span data-ttu-id="c0b0f-125">**社交登录**。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-125">**Social login**.</span></span> <span data-ttu-id="c0b0f-126">用户在使用外部服务，如 Facebook、 Microsoft 或 Google 登录。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-126">The user signs in with an external service, such as Facebook, Microsoft, or Google.</span></span> <span data-ttu-id="c0b0f-127">应用程序仍在成员资格数据库中，创建用户的条目，但不存储任何凭据。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-127">The app still creates an entry for the user in the membership database, but does not store any credentials.</span></span> <span data-ttu-id="c0b0f-128">用户通过登录到外部服务进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-128">The user authenticates by signing into the external service.</span></span>

<span data-ttu-id="c0b0f-129">本文探讨一下本地登录方案。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-129">This article looks at the local login scenario.</span></span> <span data-ttu-id="c0b0f-130">对于本地和社交登录名，Web API 使用 OAuth2 请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-130">For both local and social login, Web API uses OAuth2 to authenticate requests.</span></span> <span data-ttu-id="c0b0f-131">但是，凭据流是不同的本地和社交登录名。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-131">However, the credential flows are different for local and social login.</span></span>

<span data-ttu-id="c0b0f-132">在本文中，我将演示的简单应用程序允许用户登录，将发送到 web API 的经过身份验证的 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-132">In this article, I'll demonstrate a simple app that lets the user log in and send authenticated AJAX calls to a web API.</span></span> <span data-ttu-id="c0b0f-133">你可以下载的示例代码[此处](https://github.com/MikeWasson/LocalAccountsApp)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-133">You can download the sample code [here](https://github.com/MikeWasson/LocalAccountsApp).</span></span> <span data-ttu-id="c0b0f-134">自述文件描述如何在 Visual Studio 中从头开始创建示例。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-134">The readme describes how to create the sample from scratch in Visual Studio.</span></span>

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

<span data-ttu-id="c0b0f-135">示例应用使用数据绑定和用于发送 AJAX 请求的 jQuery Knockout.js。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-135">The sample app uses Knockout.js for data-binding and jQuery for sending AJAX requests.</span></span> <span data-ttu-id="c0b0f-136">我将 AJAX 调用中，因此无需知道这篇文章 Knockout.js 专注。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-136">I'll be focusing on the AJAX calls, so you don't need to know Knockout.js for this article.</span></span>

<span data-ttu-id="c0b0f-137">与此同时，我将介绍：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-137">Along the way, I'll describe:</span></span>

- <span data-ttu-id="c0b0f-138">客户端上，应用程序正在执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-138">What the app is doing on the client side.</span></span>
- <span data-ttu-id="c0b0f-139">在服务器上发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-139">What's happening on the server.</span></span>
- <span data-ttu-id="c0b0f-140">在中间 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-140">The HTTP traffic in the middle.</span></span>

<span data-ttu-id="c0b0f-141">首先，我们需要定义一些 OAuth2 术语。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-141">First, we need to define some OAuth2 terminology.</span></span>

- <span data-ttu-id="c0b0f-142">*资源*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-142">*Resource*.</span></span> <span data-ttu-id="c0b0f-143">一些可以保护的数据片段。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-143">Some piece of data that can be protected.</span></span>
- <span data-ttu-id="c0b0f-144">*资源服务器*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-144">*Resource server*.</span></span> <span data-ttu-id="c0b0f-145">承载资源的服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-145">The server that hosts the resource.</span></span>
- <span data-ttu-id="c0b0f-146">*资源所有者*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-146">*Resource owner*.</span></span> <span data-ttu-id="c0b0f-147">可以授予权限来访问的资源的实体。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-147">The entity that can grant permission to access a resource.</span></span> <span data-ttu-id="c0b0f-148">（通常为用户。）</span><span class="sxs-lookup"><span data-stu-id="c0b0f-148">(Typically the user.)</span></span>
- <span data-ttu-id="c0b0f-149">*客户端*： 想要对资源的访问的应用。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-149">*Client*: The app that wants access to the resource.</span></span> <span data-ttu-id="c0b0f-150">在本文中，客户端是 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-150">In this article, the client is a web browser.</span></span>
- <span data-ttu-id="c0b0f-151">*访问令牌*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-151">*Access token*.</span></span> <span data-ttu-id="c0b0f-152">授予对资源的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-152">A token that grants access to a resource.</span></span>
- <span data-ttu-id="c0b0f-153">*持有者令牌*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-153">*Bearer token*.</span></span> <span data-ttu-id="c0b0f-154">特定类型的访问令牌，与任何人都可以使用此标记的属性。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-154">A particular type of access token, with the property that anyone can use the token.</span></span> <span data-ttu-id="c0b0f-155">换而言之，客户端不需要加密的密钥或其他机密，若要使用的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-155">In other words, a client doesn't need a cryptographic key or other secret to use a bearer token.</span></span> <span data-ttu-id="c0b0f-156">为此，持有者令牌应只用于通过 HTTPS，且应具有相对较短的到期时间。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-156">For that reason, bearer tokens should only be used over a HTTPS, and should have relatively short expiration times.</span></span>
- <span data-ttu-id="c0b0f-157">*授权服务器*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-157">*Authorization server*.</span></span> <span data-ttu-id="c0b0f-158">提供访问令牌的服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-158">A server that gives out access tokens.</span></span>

<span data-ttu-id="c0b0f-159">应用程序可以充当授权服务器和资源服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-159">An application can act as both authorization server and resource server.</span></span> <span data-ttu-id="c0b0f-160">Web API 项目模板会遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-160">The Web API project template follows this pattern.</span></span>

## <a name="local-login-credential-flow"></a><span data-ttu-id="c0b0f-161">本地登录凭据流</span><span class="sxs-lookup"><span data-stu-id="c0b0f-161">Local Login Credential Flow</span></span>

<span data-ttu-id="c0b0f-162">对于本地登录名，Web API 使用[资源所有者密码流程](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)OAuth2 中定义。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-162">For local login, Web API uses the [resource owner password flow](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) defined in OAuth2.</span></span>

1. <span data-ttu-id="c0b0f-163">用户输入到客户端名称和密码。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-163">The user enters a name and password into the client.</span></span>
2. <span data-ttu-id="c0b0f-164">客户端将这些凭据发送到授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-164">The client sends these credentials to the authorization server.</span></span>
3. <span data-ttu-id="c0b0f-165">授权服务器进行身份验证凭据，并返回访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-165">The authorization server authenticates the credentials and returns an access token.</span></span>
4. <span data-ttu-id="c0b0f-166">若要访问受保护的资源，客户端，请在 HTTP 请求的 Authorization 标头中包含访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-166">To access a protected resource, the client includes the access token in the Authorization header of the HTTP request.</span></span>

![](individual-accounts-in-web-api/_static/image3.png)

<span data-ttu-id="c0b0f-167">当选择**个人帐户**在 Web API 项目模板中，该项目包括一个验证用户凭据和颁发令牌的授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-167">When you select **Individual accounts** in the Web API project template, the project includes an authorization server that validates user credentials and issues tokens.</span></span> <span data-ttu-id="c0b0f-168">下图显示根据 Web API 组件的相同凭据流。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-168">The following diagram shows the same credential flow in terms of Web API components.</span></span>

![](individual-accounts-in-web-api/_static/image4.png)

<span data-ttu-id="c0b0f-169">在此方案中，Web API 控制器充当资源服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-169">In this scenario, Web API controllers act as resource servers.</span></span> <span data-ttu-id="c0b0f-170">身份验证筛选器验证访问令牌和 **[Authorize]** 特性用于保护资源。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-170">An authentication filter validates access tokens, and the **[Authorize]** attribute is used to protect a resource.</span></span> <span data-ttu-id="c0b0f-171">当控制器或操作具有 **[Authorize]** 属性，对该控制器的所有请求或操作必须进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-171">When a controller or action has the **[Authorize]** attribute, all requests to that controller or action must be authenticated.</span></span> <span data-ttu-id="c0b0f-172">否则为授权被拒绝，然后 Web API 将返回 401 （未经授权） 的错误。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-172">Otherwise, authorization is denied, and Web API returns a 401 (Unauthorized) error.</span></span>

<span data-ttu-id="c0b0f-173">授权服务器和身份验证筛选器同时调入[OWIN 中间件](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)处理 OAuth2 的详细信息的组件。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-173">The authorization server and the authentication filter both call into an [OWIN middleware](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) component that handles the details of OAuth2.</span></span> <span data-ttu-id="c0b0f-174">在本教程后面，我将介绍更多详细信息中的设计。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-174">I'll describe the design in more detail later in this tutorial.</span></span>

## <a name="sending-an-unauthorized-request"></a><span data-ttu-id="c0b0f-175">发送未授权的请求</span><span class="sxs-lookup"><span data-stu-id="c0b0f-175">Sending an Unauthorized Request</span></span>

<span data-ttu-id="c0b0f-176">若要开始，运行应用并单击**调用 API**按钮。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-176">To get started, run the app and click the **Call API** button.</span></span> <span data-ttu-id="c0b0f-177">在请求完成后，应看到一条错误消息中的**结果**框。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-177">When the request completes, you should see an error message in the **Result** box.</span></span> <span data-ttu-id="c0b0f-178">这是因为请求不包含访问令牌，因此请求未获授权。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-178">That's because the request does not contain an access token, so the request is unauthorized.</span></span>

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

<span data-ttu-id="c0b0f-179">**调用 API**按钮时发送 AJAX 请求到 ~/api/值，这将调用 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-179">The **Call API** button sends an AJAX request to ~/api/values, which invokes a Web API controller action.</span></span> <span data-ttu-id="c0b0f-180">下面是发送 AJAX 请求的 JavaScript 代码的部分。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-180">Here is the section of JavaScript code that sends the AJAX request.</span></span> <span data-ttu-id="c0b0f-181">在示例应用中，所有 JavaScript 应用程序代码位于 Scripts\app.js 文件。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-181">In the sample app, all of the JavaScript app code is located in the Scripts\app.js file.</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

<span data-ttu-id="c0b0f-182">在用户登录，直到没有任何持有者令牌，并因此任何请求授权标头。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-182">Until the user logs in, there is no bearer token, and therefore no Authorization header in the request.</span></span> <span data-ttu-id="c0b0f-183">这将导致请求，以便返回 401 错误。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-183">This causes the request to return a 401 error.</span></span>

<span data-ttu-id="c0b0f-184">下面是 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-184">Here is the HTTP request.</span></span> <span data-ttu-id="c0b0f-185">(我使用[Fiddler](http://www.telerik.com/fiddler)捕获 HTTP 流量。)</span><span class="sxs-lookup"><span data-stu-id="c0b0f-185">(I used [Fiddler](http://www.telerik.com/fiddler) to capture the HTTP traffic.)</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

<span data-ttu-id="c0b0f-186">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-186">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

<span data-ttu-id="c0b0f-187">请注意响应使用设置为持有者质询包含 Www-authenticate 标头。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-187">Notice that the response includes a Www-Authenticate header with the challenge set to Bearer.</span></span> <span data-ttu-id="c0b0f-188">指示的服务器需要的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-188">That indicates the server expects a bearer token.</span></span>

## <a name="register-a-user"></a><span data-ttu-id="c0b0f-189">注册用户</span><span class="sxs-lookup"><span data-stu-id="c0b0f-189">Register a User</span></span>

<span data-ttu-id="c0b0f-190">在**注册**部分的应用程序中，输入的电子邮件和密码，然后单击**注册**按钮。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-190">In the **Register** section of the app, enter an email and password, and click the **Register** button.</span></span>

<span data-ttu-id="c0b0f-191">你不需要有效的电子邮件地址用于此示例中，但实际的应用程序将确认的地址。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-191">You don't need to use a valid email address for this sample, but a real app would confirm the address.</span></span> <span data-ttu-id="c0b0f-192">(请参阅[创建安全的 ASP.NET MVC 5 web 应用程序具有登录、 电子邮件确认及密码重置](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。)输入密码，使用"Password1 ！"，类似使用大写字母、 小写字母、 数字和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-192">(See [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) For the password, use something like "Password1!", with an upper case letter, lower case letter, number, and non-alpha-numeric character.</span></span> <span data-ttu-id="c0b0f-193">若要使应用程序保持简单，我向左出客户端验证，因此如果没有密码格式有问题，你将收到 400 （错误请求） 错误。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-193">To keep the app simple, I left out client-side validation, so if there is a problem with the password format, you'll get a 400 (Bad Request) error.</span></span>

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

<span data-ttu-id="c0b0f-194">**注册**按钮将 POST 请求发送到 ~/api/Account/Register /。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-194">The **Register** button sends a POST request to ~/api/Account/Register/.</span></span> <span data-ttu-id="c0b0f-195">请求正文是包含的名称和密码的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-195">The request body is a JSON object that holds the name and password.</span></span> <span data-ttu-id="c0b0f-196">以下是将请求发送的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-196">Here is the JavaScript code that sends the request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

<span data-ttu-id="c0b0f-197">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-197">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

<span data-ttu-id="c0b0f-198">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-198">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

<span data-ttu-id="c0b0f-199">通过处理此请求`AccountController`类。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-199">This request is handled by the `AccountController` class.</span></span> <span data-ttu-id="c0b0f-200">在内部，`AccountController`使用 ASP.NET 标识来管理成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-200">Internally, `AccountController` uses ASP.NET Identity to manage the membership database.</span></span>

<span data-ttu-id="c0b0f-201">如果从 Visual Studio 本地运行应用，用户帐户在 LocalDB，存储在 AspNetUsers 表。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-201">If you run the app locally from Visual Studio, user accounts are stored in LocalDB, in the AspNetUsers table.</span></span> <span data-ttu-id="c0b0f-202">若要查看 Visual Studio 中的表，请单击**视图**菜单上，选择**服务器资源管理器**，然后展开**数据连接**。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-202">To view the tables in Visual Studio, click the **View** menu, select **Server Explorer**, then expand **Data Connections**.</span></span>

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a><span data-ttu-id="c0b0f-203">获取访问令牌</span><span class="sxs-lookup"><span data-stu-id="c0b0f-203">Get an Access Token</span></span>

<span data-ttu-id="c0b0f-204">到目前为止我们尚未这样做任何 OAuth，但是现在我们将看到 OAuth 授权服务器在操作，在我们请求访问令牌时。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-204">So far we have not done any OAuth, but now we'll see the OAuth authorization server in action, when we request an access token.</span></span> <span data-ttu-id="c0b0f-205">在**Log In**区域的示例应用中，输入电子邮件和密码，然后单击**Log In**。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-205">In the **Log In** area of the sample app, enter the email and password and click **Log In**.</span></span>

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

<span data-ttu-id="c0b0f-206">**Log In**按钮向令牌终结点发送请求。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-206">The **Log In** button sends a request to the token endpoint.</span></span> <span data-ttu-id="c0b0f-207">请求正文包含以下形式的 url 编码数据：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-207">The body of the request contains the following form-url-encoded data:</span></span>

- <span data-ttu-id="c0b0f-208">授予\_类型:"密码"</span><span class="sxs-lookup"><span data-stu-id="c0b0f-208">grant\_type: "password"</span></span>
- <span data-ttu-id="c0b0f-209">用户名：&lt;用户的电子邮件&gt;</span><span class="sxs-lookup"><span data-stu-id="c0b0f-209">username: &lt;the user's email&gt;</span></span>
- <span data-ttu-id="c0b0f-210">密码：&lt;密码&gt;</span><span class="sxs-lookup"><span data-stu-id="c0b0f-210">password: &lt;password&gt;</span></span>

<span data-ttu-id="c0b0f-211">以下是发送 AJAX 请求的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-211">Here is the JavaScript code that sends the AJAX request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

<span data-ttu-id="c0b0f-212">如果请求成功，授权服务器响应正文中返回访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-212">If the request succeeds, the authorization server returns an access token in the response body.</span></span> <span data-ttu-id="c0b0f-213">请注意，我们将该令牌存储在会话存储中，以后将请求发送到 API 时使用。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-213">Notice that we store the token in session storage, to use later when sending requests to the API.</span></span> <span data-ttu-id="c0b0f-214">与不同某些形式的身份验证 （如基于 cookie 的身份验证），浏览器将自动包含访问令牌在后续请求中。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-214">Unlike some forms of authentication (such as cookie-based authentication), the browser will not automatically include the access token in subsequent requests.</span></span> <span data-ttu-id="c0b0f-215">应用程序必须明确执行相应操作。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-215">The application must do so explicitly.</span></span> <span data-ttu-id="c0b0f-216">这是一件好事，因为它限制[CSRF 漏洞](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-216">That's a good thing, because it limits [CSRF vulnerabilities](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="c0b0f-217">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-217">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

<span data-ttu-id="c0b0f-218">你可以看到该请求包含用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-218">You can see that the request contains the user's credentials.</span></span> <span data-ttu-id="c0b0f-219">你*必须*使用 HTTPS 来提供传输层安全性。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-219">You *must* use HTTPS to provide transport layer security.</span></span>

<span data-ttu-id="c0b0f-220">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-220">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

<span data-ttu-id="c0b0f-221">为了提高可读性，我缩进 JSON 并截断的访问令牌，这是相当长。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-221">For readability, I indented the JSON and truncated the access token, which is a quite long.</span></span>

<span data-ttu-id="c0b0f-222">`access_token`， `token_type`，和`expires_in`通过 OAuth2 规范定义属性。其他属性 (`userName`， `.issued`，和`.expires`) 是否仅用于信息说明。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-222">The `access_token`, `token_type`, and `expires_in` properties are defined by the OAuth2 spec. The other properties (`userName`, `.issued`, and `.expires`) are just for informational purposes.</span></span> <span data-ttu-id="c0b0f-223">你可以找到添加这些附加属性中的代码`TokenEndpoint`/Providers/ApplicationOAuthProvider.cs 文件中的方法。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-223">You can find the code that adds those additional properties in the `TokenEndpoint` method, in the /Providers/ApplicationOAuthProvider.cs file.</span></span>

## <a name="send-an-authenticated-request"></a><span data-ttu-id="c0b0f-224">发送经过身份验证的请求</span><span class="sxs-lookup"><span data-stu-id="c0b0f-224">Send an Authenticated Request</span></span>

<span data-ttu-id="c0b0f-225">现在，我们已持有者令牌，我们可以对 API 进行身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-225">Now that we have a bearer token, we can make an authenticated request to the API.</span></span> <span data-ttu-id="c0b0f-226">这可通过在请求中设置的 Authorization 标头。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-226">This is done by setting the Authorization header in the request.</span></span> <span data-ttu-id="c0b0f-227">单击**调用 API**按钮再次才能看到它。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-227">Click the **Call API** button again to see this.</span></span>

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

<span data-ttu-id="c0b0f-228">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-228">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

<span data-ttu-id="c0b0f-229">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-229">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a><span data-ttu-id="c0b0f-230">注销</span><span class="sxs-lookup"><span data-stu-id="c0b0f-230">Log Out</span></span>

<span data-ttu-id="c0b0f-231">浏览器不会缓存的凭据或访问令牌，因为注销是只需"忘记"令牌中，从会话存储中删除：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-231">Because the browser does not cache the credentials or the access token, logging out is simply a matter of "forgetting" the token, by removing it from session storage:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a><span data-ttu-id="c0b0f-232">了解各个帐户项目模板</span><span class="sxs-lookup"><span data-stu-id="c0b0f-232">Understanding the Individual Accounts Project Template</span></span>

<span data-ttu-id="c0b0f-233">当选择**个人帐户**在 ASP.NET Web 应用程序项目模板中，该项目包括：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-233">When you select **Individual Accounts** in the ASP.NET Web Application project template, the project includes:</span></span>

- <span data-ttu-id="c0b0f-234">OAuth2 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-234">An OAuth2 authorization server.</span></span>
- <span data-ttu-id="c0b0f-235">用于管理用户帐户的 Web API 终结点</span><span class="sxs-lookup"><span data-stu-id="c0b0f-235">A Web API endpoint for managing user accounts</span></span>
- <span data-ttu-id="c0b0f-236">用于存储用户帐户的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-236">An EF model for storing user accounts.</span></span>

<span data-ttu-id="c0b0f-237">下面是实现这些功能的主应用程序类：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-237">Here are the main application classes that implement these features:</span></span>

- <span data-ttu-id="c0b0f-238">`AccountController`。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-238">`AccountController`.</span></span> <span data-ttu-id="c0b0f-239">提供用于管理用户帐户的 Web API 终结点。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-239">Provides a Web API endpoint for managing user accounts.</span></span> <span data-ttu-id="c0b0f-240">`Register`操作是我们在本教程中使用只有一个。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-240">The `Register` action is the only one that we used in this tutorial.</span></span> <span data-ttu-id="c0b0f-241">在类上的其他方法支持密码重置、 社交登录名和其他功能。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-241">Other methods on the class support password reset, social logins, and other functionality.</span></span>
- <span data-ttu-id="c0b0f-242">`ApplicationUser`/Models/IdentityModels.cs 中定义。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-242">`ApplicationUser`, defined in /Models/IdentityModels.cs.</span></span> <span data-ttu-id="c0b0f-243">此类是成员资格数据库中的用户帐户的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-243">This class is the EF model for user accounts in the membership database.</span></span>
- <span data-ttu-id="c0b0f-244">`ApplicationUserManager`定义在 /App\_Start/IdentityConfig.cs 此类派生自[UserManager](https://msdn.microsoft.com/library/dn613290.aspx)和用户帐户，如创建新用户，验证密码，依此类推，对执行操作和自动保存对数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-244">`ApplicationUserManager`, defined in /App\_Start/IdentityConfig.cs This class derives from [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) and performs operations on user accounts, such as creating a new user, verifying passwords, and so forth, and automatically persists changes to the database.</span></span>
- <span data-ttu-id="c0b0f-245">`ApplicationOAuthProvider`。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-245">`ApplicationOAuthProvider`.</span></span> <span data-ttu-id="c0b0f-246">此对象插入到 OWIN 中间件，并处理由该中间件引发的事件。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-246">This object plugs into the OWIN middleware, and processes events raised by the middleware.</span></span> <span data-ttu-id="c0b0f-247">它派生自[OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-247">It derives from [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).</span></span>

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a><span data-ttu-id="c0b0f-248">配置授权服务器</span><span class="sxs-lookup"><span data-stu-id="c0b0f-248">Configuring the Authorization Server</span></span>

<span data-ttu-id="c0b0f-249">在 StartupAuth.cs，下面的代码将配置 OAuth2 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-249">In StartupAuth.cs, the following code configures the OAuth2 authorization server.</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

<span data-ttu-id="c0b0f-250">`TokenEndpointPath`属性是授权服务器终结点的 URL 路径。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-250">The `TokenEndpointPath` property is the URL path to the authorization server endpoint.</span></span> <span data-ttu-id="c0b0f-251">是一个 URL，该应用程序使用来获取持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-251">That's the URL that app uses to get the bearer tokens.</span></span>

<span data-ttu-id="c0b0f-252">`Provider`属性指定的提供程序插入到 OWIN 中间件，并通过中间件引发的事件处理。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-252">The `Provider` property specifies a provider that plugs into the OWIN middleware, and processes events raised by the middleware.</span></span>

<span data-ttu-id="c0b0f-253">下面是基本的流，当应用程序想要获取的令牌：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-253">Here is the basic flow when the app wants to get a token:</span></span>

1. <span data-ttu-id="c0b0f-254">若要获取访问令牌，该应用，将发送到的请求 ~ / 令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-254">To get an access token, the app sends a request to ~/Token.</span></span>
2. <span data-ttu-id="c0b0f-255">OAuth 中间件调用`GrantResourceOwnerCredentials`上的提供程序。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-255">The OAuth middleware calls `GrantResourceOwnerCredentials` on the provider.</span></span>
3. <span data-ttu-id="c0b0f-256">提供程序调用`ApplicationUserManager`以验证凭据并创建声明标识。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-256">The provider calls the `ApplicationUserManager` to validate the credentials and create a claims identity.</span></span>
4. <span data-ttu-id="c0b0f-257">如果成功，则提供程序创建的验证票证，用于生成令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-257">If that succeeds, the provider creates an authentication ticket, which is used to generate the token.</span></span>

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

<span data-ttu-id="c0b0f-258">OAuth 中间件不知道有关用户帐户的任何信息。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-258">The OAuth middleware doesn't know anything about the user accounts.</span></span> <span data-ttu-id="c0b0f-259">提供程序之间的中间件和 ASP.NET 标识进行通信。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-259">The provider communicates between the middleware and ASP.NET Identity.</span></span> <span data-ttu-id="c0b0f-260">有关实现授权服务器的详细信息，请参阅[OWIN OAuth 2.0 授权服务器](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-260">For more information about implementing the authorization server, see [OWIN OAuth 2.0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).</span></span>

### <a name="configuring-web-api-to-use-bearer-tokens"></a><span data-ttu-id="c0b0f-261">配置要使用持有者令牌的 Web API</span><span class="sxs-lookup"><span data-stu-id="c0b0f-261">Configuring Web API to use Bearer Tokens</span></span>

<span data-ttu-id="c0b0f-262">在`WebApiConfig.Register`方法，下面的代码将设置为 Web API 管道的身份验证：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-262">In the `WebApiConfig.Register` method, the following code sets up authentication for the Web API pipeline:</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

<span data-ttu-id="c0b0f-263">**HostAuthenticationFilter**类启用使用持有者令牌的身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-263">The **HostAuthenticationFilter** class enables authentication using bearer tokens.</span></span>

<span data-ttu-id="c0b0f-264">**SuppressDefaultHostAuthentication**方法告知 Web API，若要忽略在请求到达 Web API 管道，IIS 或 OWIN 中间件之前任何身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-264">The **SuppressDefaultHostAuthentication** method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="c0b0f-265">这样一来，我们可以限制 Web API 进行身份验证仅使用持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-265">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b0f-266">具体而言，你的应用程序的 MVC 部分可能使用窗体身份验证，这将凭据存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-266">In particular, the MVC portion of your app might use forms authentication, which stores credentials in a cookie.</span></span> <span data-ttu-id="c0b0f-267">基于 cookie 的身份验证需要使用防伪标记，以防止 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-267">Cookie-based authentication requires the use of anti-forgery tokens, to prevent CSRF attacks.</span></span> <span data-ttu-id="c0b0f-268">这是 web Api、 出现问题，因为没有 web API 的方便方法以将防伪令牌发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-268">That's a problem for web APIs, because there is no convenient way for the web API to send the anti-forgery token to the client.</span></span> <span data-ttu-id="c0b0f-269">(有关此问题的更多背景，请参阅[防止 CSRF 攻击 Web API 中](preventing-cross-site-request-forgery-csrf-attacks.md)。)调用**SuppressDefaultHostAuthentication**可确保 Web API 不会在 cookie 中存储的凭据从容易受到 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-269">(For more background on this issue, see [Preventing CSRF Attacks in Web API](preventing-cross-site-request-forgery-csrf-attacks.md).) Calling **SuppressDefaultHostAuthentication** ensures that Web API is not vulnerable to CSRF attacks from credentials stored in cookies.</span></span>


<span data-ttu-id="c0b0f-270">当客户端请求受保护的资源时，下面是在 Web API 管道中会发生什么情况：</span><span class="sxs-lookup"><span data-stu-id="c0b0f-270">When the client requests a protected resource, here is what happens in the Web API pipeline:</span></span>

1. <span data-ttu-id="c0b0f-271">**HostAuthentication**筛选器会调用 OAuth 中间件，该令牌进行验证。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-271">The **HostAuthentication** filter calls the OAuth middleware to validate the token.</span></span>
2. <span data-ttu-id="c0b0f-272">该中间件将声明标识转换为令牌。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-272">The middleware converts the token into a claims identity.</span></span>
3. <span data-ttu-id="c0b0f-273">此时，该请求是*身份验证*但不是*授权*。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-273">At this point, the request is *authenticated* but not *authorized*.</span></span>
4. <span data-ttu-id="c0b0f-274">授权筛选器检查的声明标识。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-274">The authorization filter examines the claims identity.</span></span> <span data-ttu-id="c0b0f-275">如果声明授权用户对该资源，请对请求进行授权。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-275">If the claims authorize the user for that resource, the request is authorized.</span></span> <span data-ttu-id="c0b0f-276">默认情况下， **[Authorize]** 属性将授权进行身份验证的任何请求。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-276">By default, the **[Authorize]** attribute will authorize any request that is authenticated.</span></span> <span data-ttu-id="c0b0f-277">但是，你可以授权角色或其他声明。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-277">However, you can authorize by role or by other claims.</span></span> <span data-ttu-id="c0b0f-278">有关详细信息，请参阅[身份验证和 Web API 中的授权](authentication-and-authorization-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-278">For more information, see [Authentication and Authorization in Web API](authentication-and-authorization-in-aspnet-web-api.md).</span></span>
5. <span data-ttu-id="c0b0f-279">如果前面的步骤都成功，则控制器将返回受保护的资源。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-279">If the previous steps are successful, the controller returns the protected resource.</span></span> <span data-ttu-id="c0b0f-280">否则，客户端收到 401 （未经授权） 的错误。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-280">Otherwise, the client receives a 401 (Unauthorized) error.</span></span>

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a><span data-ttu-id="c0b0f-281">其他资源</span><span class="sxs-lookup"><span data-stu-id="c0b0f-281">Additional Resources</span></span>

- [<span data-ttu-id="c0b0f-282">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="c0b0f-282">ASP.NET Identity</span></span>](../../../identity/index.md)
- <span data-ttu-id="c0b0f-283">[了解 SPA 模板中的安全功能的 VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-283">[Understanding Security Features in the SPA Template for VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx).</span></span> <span data-ttu-id="c0b0f-284">MSDN 博客帖子： Hongye Sun。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-284">MSDN blog post by Hongye Sun.</span></span>
- <span data-ttu-id="c0b0f-285">[将 Web API 个人帐户模板 – 第 2 部分： 本地帐户](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-285">[Dissecting the Web API Individual Accounts Template–Part 2: Local Accounts](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/).</span></span> <span data-ttu-id="c0b0f-286">Dominick Baier 的博客文章。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-286">Blog post by Dominick Baier.</span></span>
- <span data-ttu-id="c0b0f-287">[托管身份验证和 Web API 带 OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-287">[Host authentication and Web API with OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/).</span></span> <span data-ttu-id="c0b0f-288">介绍`SuppressDefaultHostAuthentication`和`HostAuthenticationFilter`Brock Allen 通过。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-288">A good explanation of `SuppressDefaultHostAuthentication` and `HostAuthenticationFilter` by Brock Allen.</span></span>
- <span data-ttu-id="c0b0f-289">[自定义在 ASP.NET Identity 中 VS 2013 模板中的配置文件信息](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-289">[Customizing profile information in ASP.NET Identity in VS 2013 templates](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx).</span></span> <span data-ttu-id="c0b0f-290">Pranav Rastogi 的 MSDN 博客文章。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-290">MSDN blog post by Pranav Rastogi.</span></span>
- <span data-ttu-id="c0b0f-291">[每个请求 UserManager 在 ASP.NET Identity 中的类的生存期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-291">[Per request lifetime management for UserManager class in ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).</span></span> <span data-ttu-id="c0b0f-292">通过 Suhas Joshi 详细介绍与 MSDN 博客文章`UserManager`类。</span><span class="sxs-lookup"><span data-stu-id="c0b0f-292">MSDN blog post by Suhas Joshi, with a good explanation of the `UserManager` class.</span></span>
