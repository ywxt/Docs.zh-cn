---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: "OWIN OAuth 2.0 授权服务器 |Microsoft 文档"
author: hongyes
description: "本教程将指导你如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。 这是该唯一 outlin 的高级的教程..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/20/2014
ms.topic: article
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: e5968f8d19191c3f44e9bd58f8e22a39d8d8faff
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="c7591-104">OWIN OAuth 2.0 授权服务器</span><span class="sxs-lookup"><span data-stu-id="c7591-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="c7591-105">通过[Hongye Sun](https://github.com/hongyes)， [Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="c7591-105">by [Hongye Sun](https://github.com/hongyes), [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="c7591-106">本教程将指导你如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。</span><span class="sxs-lookup"><span data-stu-id="c7591-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="c7591-107">这是仅概述了创建 OWIN OAuth 2.0 授权服务器的步骤的高级的教程。</span><span class="sxs-lookup"><span data-stu-id="c7591-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="c7591-108">这不是一个分步教程。</span><span class="sxs-lookup"><span data-stu-id="c7591-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="c7591-109">[下载的示例代码](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。</span><span class="sxs-lookup"><span data-stu-id="c7591-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="c7591-110">该轮廓不符合预期要用于创建安全的生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="c7591-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="c7591-111">本教程旨在提供仅概述了有关如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。</span><span class="sxs-lookup"><span data-stu-id="c7591-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
> 
> 
> ## <a name="software-versions"></a><span data-ttu-id="c7591-112">软件版本</span><span class="sxs-lookup"><span data-stu-id="c7591-112">Software versions</span></span>
> 
> | <span data-ttu-id="c7591-113">**本教程中所示**</span><span class="sxs-lookup"><span data-stu-id="c7591-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="c7591-114">**也适用于**</span><span class="sxs-lookup"><span data-stu-id="c7591-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="c7591-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c7591-115">Windows 8.1</span></span> | <span data-ttu-id="c7591-116">Windows 8, Windows 7</span><span class="sxs-lookup"><span data-stu-id="c7591-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="c7591-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c7591-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads) | <span data-ttu-id="c7591-118">[Visual Studio 2013 Express for 桌面](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)。</span><span class="sxs-lookup"><span data-stu-id="c7591-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express).</span></span> <span data-ttu-id="c7591-119">应运行最新的更新 visual Studio 2012，但本教程未进行测试，并且某些菜单选项和对话框都有所不同。</span><span class="sxs-lookup"><span data-stu-id="c7591-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="c7591-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c7591-120">.NET 4.5</span></span> |  |
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="c7591-121">问题和意见</span><span class="sxs-lookup"><span data-stu-id="c7591-121">Questions and Comments</span></span>
> 
> <span data-ttu-id="c7591-122">如果你有与本教程不直接相关的问题，可以将其在发布[GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana/)。</span><span class="sxs-lookup"><span data-stu-id="c7591-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="c7591-123">问题和意见教程本身，请参阅在页底部的注释部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="c7591-124">[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749)使第三方应用程序，以获取对 HTTP 服务的有限访问权限。</span><span class="sxs-lookup"><span data-stu-id="c7591-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="c7591-125">而不是使用资源所有者的凭据来访问受保护的资源，客户端获取访问令牌 (它是一个字符串表示特定的作用域、 生存期和其他访问属性)。</span><span class="sxs-lookup"><span data-stu-id="c7591-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="c7591-126">访问令牌被颁发给第三方客户端由授权服务器的资源所有者批准。</span><span class="sxs-lookup"><span data-stu-id="c7591-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="c7591-127">本教程将介绍：</span><span class="sxs-lookup"><span data-stu-id="c7591-127">This tutorial will cover:</span></span>

- <span data-ttu-id="c7591-128">如何创建授权服务器以支持四个授权类型，以及刷新令牌：</span><span class="sxs-lookup"><span data-stu-id="c7591-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="c7591-129">授权代码授予</span><span class="sxs-lookup"><span data-stu-id="c7591-129">Authorization code grant</span></span>
    - <span data-ttu-id="c7591-130">隐式授权</span><span class="sxs-lookup"><span data-stu-id="c7591-130">Implicit Grant</span></span>
    - <span data-ttu-id="c7591-131">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="c7591-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="c7591-132">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="c7591-132">Client Credentials Grant</span></span>
- <span data-ttu-id="c7591-133">创建访问令牌通过受保护的资源服务器。</span><span class="sxs-lookup"><span data-stu-id="c7591-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="c7591-134">创建 OAuth 2.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="c7591-135">系统必备</span><span class="sxs-lookup"><span data-stu-id="c7591-135">Prerequisites</span></span>

- <span data-ttu-id="c7591-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免费[Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)，如下所示**软件版本**页顶部。</span><span class="sxs-lookup"><span data-stu-id="c7591-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="c7591-137">带 OWIN 的熟悉程度。</span><span class="sxs-lookup"><span data-stu-id="c7591-137">Familiarity with OWIN.</span></span> <span data-ttu-id="c7591-138">请参阅[Getting Started with Katana 项目](https://msdn.microsoft.com/magazine/dn451439.aspx)和[OWIN 和 Katana 中的新增](index.md)。</span><span class="sxs-lookup"><span data-stu-id="c7591-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="c7591-139">熟悉[OAuth](http://tools.ietf.org/html/rfc6749)术语，包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)，[协议流](http://tools.ietf.org/html/rfc6749#section-1.2)，和[授权](http://tools.ietf.org/html/rfc6749#section-1.3)。</span><span class="sxs-lookup"><span data-stu-id="c7591-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="c7591-140">[OAuth 2.0 简介](http://tools.ietf.org/html/rfc6749#section-1)提供良好的介绍。</span><span class="sxs-lookup"><span data-stu-id="c7591-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="c7591-141">创建授权服务器</span><span class="sxs-lookup"><span data-stu-id="c7591-141">Create an Authorization Server</span></span>

<span data-ttu-id="c7591-142">在本教程中，我们将大致草拟如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 创建服务器的授权。</span><span class="sxs-lookup"><span data-stu-id="c7591-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="c7591-143">我们希望很快提供可供下载的已完成的示例中，因为本教程不包括每个步骤。</span><span class="sxs-lookup"><span data-stu-id="c7591-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="c7591-144">首先，创建名为的空 web 应用*AuthorizationServer*并安装以下程序包：</span><span class="sxs-lookup"><span data-stu-id="c7591-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="c7591-145">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="c7591-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="c7591-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="c7591-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="c7591-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="c7591-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="c7591-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="c7591-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="c7591-149">Microsoft.Owin.Security.Google （或任何其他社交登录如 Microsoft.Owin.Security.Facebook 程序包）</span><span class="sxs-lookup"><span data-stu-id="c7591-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="c7591-150">添加[OWIN 启动类](owin-startup-class-detection.md)名为的项目根文件夹下*启动*。</span><span class="sxs-lookup"><span data-stu-id="c7591-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="c7591-151">创建*应用\_启动*文件夹。</span><span class="sxs-lookup"><span data-stu-id="c7591-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="c7591-152">选择*应用\_启动*文件夹，然后使用 Shift + Alt + A 若要添加的下载的版本*AuthorizationServer\App\_Start\Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="c7591-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="c7591-153">上面的代码中启用应用程序/外部登录 cookie 和 Google 身份验证，授权服务器本身用于管理帐户。</span><span class="sxs-lookup"><span data-stu-id="c7591-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="c7591-154">`UseOAuthAuthorizationServer`扩展方法是设置授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c7591-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="c7591-155">安装程序选项包括：</span><span class="sxs-lookup"><span data-stu-id="c7591-155">The setup options are:</span></span>

- <span data-ttu-id="c7591-156">`AuthorizeEndpointPath`: 请求路径，其中客户端应用程序会将用户代理，以便获取用户同意颁发的令牌或代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="c7591-157">例如，具有前导斜杠，必须以"`/Authorize`"。</span><span class="sxs-lookup"><span data-stu-id="c7591-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="c7591-158">`TokenEndpointPath`: 请求路径客户端应用程序直接进行通信以获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="c7591-159">它必须以前导斜杠，如"/"开头。</span><span class="sxs-lookup"><span data-stu-id="c7591-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="c7591-160">如果颁发客户端[客户端\_机密](http://tools.ietf.org/html/rfc6749#appendix-A.2)，它必须提供给此终结点。</span><span class="sxs-lookup"><span data-stu-id="c7591-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="c7591-161">`ApplicationCanDisplayErrors`： 将设置为`true`如果 web 应用程序想要在生成的客户端验证错误的自定义错误页`/Authorize`终结点。</span><span class="sxs-lookup"><span data-stu-id="c7591-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="c7591-162">这才必需的情况下，浏览器不会重定向回客户端应用程序，例如，当`client_id`或`redirect_uri`不正确。</span><span class="sxs-lookup"><span data-stu-id="c7591-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="c7591-163">`/Authorize`终结点应该会看到"oauth。错误"、"oauth。ErrorDescription"和"oauth。ErrorUri"属性添加到 OWIN 环境中。</span><span class="sxs-lookup"><span data-stu-id="c7591-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c7591-164">如果不为 true，则授权服务器将返回的错误详细信息的默认错误页。</span><span class="sxs-lookup"><span data-stu-id="c7591-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="c7591-165">`AllowInsecureHttp`： 如果为允许授权和令牌请求到达 HTTP URI 地址，并允许传入`redirect_uri`授权请求参数，为具有 HTTP URI 地址。</span><span class="sxs-lookup"><span data-stu-id="c7591-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="c7591-166">安全-这是用于开发仅。</span><span class="sxs-lookup"><span data-stu-id="c7591-166">Security - This is for development only.</span></span>
- <span data-ttu-id="c7591-167">`Provider`： 提供了应用程序处理事件引发的授权服务器中间件的对象。</span><span class="sxs-lookup"><span data-stu-id="c7591-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="c7591-168">应用程序可能完全，实现接口或它可能会创建的实例`OAuthAuthorizationServerProvider`并分配此服务器支持的 OAuth 流程所需的委托。</span><span class="sxs-lookup"><span data-stu-id="c7591-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="c7591-169">`AuthorizationCodeProvider`： 生成单使用授权代码，以返回到客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="c7591-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="c7591-170">为 OAuth 服务器要保护的应用程序**必须**提供程序实例`AuthorizationCodeProvider`令牌由`OnCreate/OnCreateAsync`事件都被视为有效只有一个调用`OnReceive/OnReceiveAsync`。</span><span class="sxs-lookup"><span data-stu-id="c7591-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="c7591-171">`RefreshTokenProvider`： 生成可用于生成新的访问令牌时所需的刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="c7591-172">如果未提供授权服务器将不返回刷新令牌从`/Token`终结点。</span><span class="sxs-lookup"><span data-stu-id="c7591-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="c7591-173">帐户管理</span><span class="sxs-lookup"><span data-stu-id="c7591-173">Account Management</span></span>

<span data-ttu-id="c7591-174">OAuth 不介意位置和方式如何管理用户帐户信息。</span><span class="sxs-lookup"><span data-stu-id="c7591-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="c7591-175">它具有[ASP.NET 标识](../../../identity/index.md)对它负责。</span><span class="sxs-lookup"><span data-stu-id="c7591-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="c7591-176">在本教程中，我们将简化帐户管理代码并只需确保该用户可以登录使用 OWIN cookie 中间件。</span><span class="sxs-lookup"><span data-stu-id="c7591-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="c7591-177">以下是有关的简化的示例代码`AccountController`:</span><span class="sxs-lookup"><span data-stu-id="c7591-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="c7591-178">`ValidateClientRedirectUri`用于验证客户端使用其注册的重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="c7591-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="c7591-179">`ValidateClientAuthentication`检查的基本方案标头和窗体正文以获取客户端的凭据。</span><span class="sxs-lookup"><span data-stu-id="c7591-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="c7591-180">登录页如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7591-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="c7591-181">查看 IETF 的 OAuth 2[授权代码授予](http://tools.ietf.org/html/rfc6749#section-4.1)现在部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span> 

<span data-ttu-id="c7591-182">**提供程序**（在下表中） 是[OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程序，它的类型是`OAuthAuthorizationServerProvider`，其中包含所有 OAuth 服务器事件。</span><span class="sxs-lookup"><span data-stu-id="c7591-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span> 

| <span data-ttu-id="c7591-183">流步骤，可从授权代码授予部分</span><span class="sxs-lookup"><span data-stu-id="c7591-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="c7591-184">示例下载执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="c7591-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c7591-185">（A） 客户端通过将定向到授权终结点资源所有者的用户代理启动流。</span><span class="sxs-lookup"><span data-stu-id="c7591-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="c7591-186">客户端包括其客户端标识符、 请求的作用域、 本地状态中，和向其授权服务器将发送用户代理只有完成授予 （或拒绝） 访问后返回的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="c7591-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="c7591-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="c7591-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="c7591-188">（B） 授权服务器进行身份验证 （通过用户代理） 的资源所有者，并建立是否资源所有者授予或拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="c7591-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="c7591-189">**&lt;如果用户授予访问权限&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c7591-190">（C） 假定资源所有者授予访问权限，授权服务器将用户代理重定向回客户端使用重定向 URI 提供早期 （在请求中或在客户端注册）。</span><span class="sxs-lookup"><span data-stu-id="c7591-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="c7591-191">...</span><span class="sxs-lookup"><span data-stu-id="c7591-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="c7591-192">（D） 客户端通过包含上一步中收到的授权代码来从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="c7591-193">在发出请求时，使用授权服务器进行身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="c7591-194">客户端包括重定向 URI 用于获取验证的授权代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="c7591-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="c7591-196">实现示例`AuthorizationCodeProvider.CreateAsync`和`ReceiveAsync`控制创建和验证的授权代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="c7591-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="c7591-197">上面的代码中使用的内存中并发字典来存储代码和标识票证和在接收到代码后还原标识。</span><span class="sxs-lookup"><span data-stu-id="c7591-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="c7591-198">在实际应用中，必须先将它替换为永久性数据存储。</span><span class="sxs-lookup"><span data-stu-id="c7591-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="c7591-199">授权终结点是资源所有者授予对客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="c7591-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="c7591-200">通常情况下，它需要一个用户界面来允许用户单击按钮，然后确认授予。</span><span class="sxs-lookup"><span data-stu-id="c7591-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="c7591-201">OWIN OAuth 中间件允许应用程序代码来处理授权终结点。</span><span class="sxs-lookup"><span data-stu-id="c7591-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="c7591-202">在我们的示例应用程序中，我们将使用调用一个 MVC 控制器`OAuthController`进行处理。</span><span class="sxs-lookup"><span data-stu-id="c7591-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="c7591-203">下面是示例实现：</span><span class="sxs-lookup"><span data-stu-id="c7591-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="c7591-204">`Authorize`操作将首先检查是否用户已登录到授权服务器。</span><span class="sxs-lookup"><span data-stu-id="c7591-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="c7591-205">如果没有，身份验证中间件将要求调用方使用"应用程序"cookie 进行身份验证和将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="c7591-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="c7591-206">（请参阅上面的突出显示的代码。）如果用户已登录，它会呈现授权视图中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7591-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="c7591-207">如果**授予**选择按钮时，`Authorize`操作将创建新的"Bearer"标识和使用它登录。</span><span class="sxs-lookup"><span data-stu-id="c7591-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="c7591-208">它将触发授权服务器生成的持有者令牌并将其发送回客户端使用 JSON 负载。</span><span class="sxs-lookup"><span data-stu-id="c7591-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span> 

### <a name="implicit-grant"></a><span data-ttu-id="c7591-209">隐式授权</span><span class="sxs-lookup"><span data-stu-id="c7591-209">Implicit Grant</span></span>

<span data-ttu-id="c7591-210">请参阅 IETF 的 OAuth 2[隐式授权](http://tools.ietf.org/html/rfc6749#section-4.2)现在部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="c7591-211">[隐式授权](http://tools.ietf.org/html/rfc6749#section-4.2)图 4 中所示的数据流是流并映射其 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="c7591-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="c7591-212">流步骤，可从隐式授权部分</span><span class="sxs-lookup"><span data-stu-id="c7591-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="c7591-213">示例下载执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="c7591-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c7591-214">（A） 客户端通过将定向到授权终结点资源所有者的用户代理启动流。</span><span class="sxs-lookup"><span data-stu-id="c7591-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="c7591-215">客户端包括其客户端标识符、 请求的作用域、 本地状态中，和向其授权服务器将发送用户代理只有完成授予 （或拒绝） 访问后返回的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="c7591-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="c7591-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="c7591-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="c7591-217">（B） 授权服务器进行身份验证 （通过用户代理） 的资源所有者，并建立是否资源所有者授予或拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="c7591-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="c7591-218">**&lt;如果用户授予访问权限&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c7591-219">（C） 假定资源所有者授予访问权限，授权服务器将用户代理重定向回客户端使用重定向 URI 提供早期 （在请求中或在客户端注册）。</span><span class="sxs-lookup"><span data-stu-id="c7591-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="c7591-220">...</span><span class="sxs-lookup"><span data-stu-id="c7591-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="c7591-221">（D） 客户端通过包含上一步中收到的授权代码来从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="c7591-222">在发出请求时，使用授权服务器进行身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="c7591-223">客户端包括重定向 URI 用于获取验证的授权代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="c7591-224">由于我们已实现授权终结点 (`OAuthController.Authorize`操作) 的授权代码授予，它会自动启用以及隐式流。</span><span class="sxs-lookup"><span data-stu-id="c7591-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="c7591-225">注意：`Provider.ValidateClientRedirectUri`用于验证的客户端 ID 与其重定向 URL，用于防止隐式授予流发送令牌来恶意客户端的访问 ([拦截中攻击](https://www.owasp.org/index.php/Man-in-the-middle_attack))。</span><span class="sxs-lookup"><span data-stu-id="c7591-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="c7591-226">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="c7591-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="c7591-227">请参阅 IETF 的 OAuth 2[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)现在部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="c7591-228">[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)图 5 所示的数据流是流并映射其 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="c7591-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="c7591-229">流步骤，可从资源所有者密码凭据授予部分</span><span class="sxs-lookup"><span data-stu-id="c7591-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="c7591-230">示例下载执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="c7591-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c7591-231">（A） 资源所有者提供客户端使用其用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="c7591-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="c7591-232">（B) 客户端通过包括来自资源所有者的凭据从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="c7591-233">在发出请求时，使用授权服务器进行身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="c7591-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c7591-235">（C) 授权服务器对客户端进行身份验证和验证资源的所有者凭据，以及如果有效，将发出访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="c7591-236">下面是示例实现`Provider.GrantResourceOwnerCredentials`:</span><span class="sxs-lookup"><span data-stu-id="c7591-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="c7591-237">上面的代码是要解释本教程的本部分和不能在安全或生产应用。</span><span class="sxs-lookup"><span data-stu-id="c7591-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="c7591-238">它不会检查资源所有者凭据。</span><span class="sxs-lookup"><span data-stu-id="c7591-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="c7591-239">它假定每个凭据有效，并为其创建一个新的标识。</span><span class="sxs-lookup"><span data-stu-id="c7591-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="c7591-240">新的标识将用于生成访问令牌和刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="c7591-241">请将代码替换你自己的安全帐户管理代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="c7591-242">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="c7591-242">Client Credentials Grant</span></span>

<span data-ttu-id="c7591-243">请参阅 IETF 的 OAuth 2[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)现在部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="c7591-244">[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)图 6 所示的数据流是流并映射其 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="c7591-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="c7591-245">流步骤，可从客户端凭据授予部分</span><span class="sxs-lookup"><span data-stu-id="c7591-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="c7591-246">示例下载执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="c7591-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c7591-247">（A） 客户端向授权服务器进行身份验证，并从令牌的终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="c7591-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c7591-249">（B） 授权服务器验证客户端，并且如果有效，将发出访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="c7591-250">下面是示例实现`Provider.GrantClientCredentials`:</span><span class="sxs-lookup"><span data-stu-id="c7591-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="c7591-251">上面的代码是要解释本教程的本部分和不能在安全或生产应用。</span><span class="sxs-lookup"><span data-stu-id="c7591-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="c7591-252">请将代码替换你自己的安全客户端管理代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="c7591-253">刷新令牌</span><span class="sxs-lookup"><span data-stu-id="c7591-253">Refresh Token</span></span>

<span data-ttu-id="c7591-254">请参阅 IETF 的 OAuth 2[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)现在部分。</span><span class="sxs-lookup"><span data-stu-id="c7591-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="c7591-255">[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)图 2 所示的数据流是流并映射其 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="c7591-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="c7591-256">流步骤，可从客户端凭据授予部分</span><span class="sxs-lookup"><span data-stu-id="c7591-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="c7591-257">示例下载执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="c7591-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c7591-258">（G） 客户端通过使用授权服务器进行身份验证，并将提供刷新令牌请求新的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="c7591-259">客户端身份验证要求基于客户端类型而授权服务器策略。</span><span class="sxs-lookup"><span data-stu-id="c7591-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="c7591-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="c7591-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c7591-261">（H） 授权服务器对客户端进行身份验证和验证刷新令牌，以及如果有效，将发出一个新的访问令牌 （和 （可选） 新的刷新令牌）。</span><span class="sxs-lookup"><span data-stu-id="c7591-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="c7591-262">下面是示例实现`Provider.GrantRefreshToken`:</span><span class="sxs-lookup"><span data-stu-id="c7591-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span> 

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="c7591-263">创建访问令牌通过受保护的资源服务器</span><span class="sxs-lookup"><span data-stu-id="c7591-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="c7591-264">创建空 web 应用程序项目，并安装以下项目中的包：</span><span class="sxs-lookup"><span data-stu-id="c7591-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="c7591-265">Microsoft.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="c7591-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="c7591-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="c7591-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="c7591-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="c7591-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="c7591-268">创建一个 startup 类，并配置身份验证和 Web API。</span><span class="sxs-lookup"><span data-stu-id="c7591-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="c7591-269">请参阅*AuthorizationServer\ResourceServer\Startup.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="c7591-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="c7591-270">请参阅*AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="c7591-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="c7591-271">请参阅*AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="c7591-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="c7591-272">`UseCors`方法允许在所有域的 CORS。</span><span class="sxs-lookup"><span data-stu-id="c7591-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="c7591-273">`UseOAuthBearerAuthentication`方法可实现 OAuth 持有者令牌的身份验证中间它将接收并验证从 authorization 标头中请求的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="c7591-274">`Config.SuppressDefaultHostAuthenticaiton`取消显示默认承载的应用中的身份验证的主体，因此所有请求都将匿名在此调用。</span><span class="sxs-lookup"><span data-stu-id="c7591-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="c7591-275">`HostAuthenticationFilter`启用身份验证只是为了指定的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="c7591-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="c7591-276">在这种情况下，它是持有者身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="c7591-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="c7591-277">为了演示身份验证的标识，我们创建 ApiController 输出当前用户的声明。</span><span class="sxs-lookup"><span data-stu-id="c7591-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="c7591-278">如果授权服务器和资源服务器不在同一台计算机，OAuth 中间件将使用不同的计算机密钥进行加密和解密持有者访问令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="c7591-279">为了共享这两个项目之间的相同私钥，我们将同一`machinekey`设置中同时*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="c7591-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="c7591-280">创建 OAuth 2.0 客户端</span><span class="sxs-lookup"><span data-stu-id="c7591-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="c7591-281">我们使用[DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 包来简化客户端的代码。</span><span class="sxs-lookup"><span data-stu-id="c7591-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="c7591-282">授权代码授予客户端</span><span class="sxs-lookup"><span data-stu-id="c7591-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="c7591-283">此客户端是一个 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c7591-283">This client is an MVC application.</span></span> <span data-ttu-id="c7591-284">它将触发授权代码授予流来获取访问令牌从后端。</span><span class="sxs-lookup"><span data-stu-id="c7591-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="c7591-285">它具有单个页面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7591-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="c7591-286">**Authorize**按钮将浏览器重定向到授权服务器便可以通知资源所有者授予对此客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="c7591-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="c7591-287">**刷新**按钮将获取新的访问令牌和刷新令牌使用当前的刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="c7591-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="c7591-288">**访问受保护资源 API**按钮将调用以获取当前用户的声明数据并在页面上显示它们的资源服务器。</span><span class="sxs-lookup"><span data-stu-id="c7591-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="c7591-289">下面是示例代码的`HomeController`的客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="c7591-290">`DotNetOpenAuth`默认情况下需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="c7591-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="c7591-291">由于我们的演示程序使用 HTTP，你需要添加以下配置文件中的设置：</span><span class="sxs-lookup"><span data-stu-id="c7591-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="c7591-292">安全-永远不会禁用 SSL 在生产应用程序中。</span><span class="sxs-lookup"><span data-stu-id="c7591-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="c7591-293">你的登录凭据是现在以发送明文跨网络。</span><span class="sxs-lookup"><span data-stu-id="c7591-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="c7591-294">上面的代码说明仅针对本地示例调试和浏览。</span><span class="sxs-lookup"><span data-stu-id="c7591-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="c7591-295">隐式授予客户端</span><span class="sxs-lookup"><span data-stu-id="c7591-295">Implicit Grant Client</span></span>

<span data-ttu-id="c7591-296">此客户端使用 JavaScript 到：</span><span class="sxs-lookup"><span data-stu-id="c7591-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="c7591-297">打开新窗口，并将重定向到授权服务器的授权终结点。</span><span class="sxs-lookup"><span data-stu-id="c7591-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="c7591-298">从获取访问令牌 URL 片段时它将重定向回。</span><span class="sxs-lookup"><span data-stu-id="c7591-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="c7591-299">下图显示了此过程：</span><span class="sxs-lookup"><span data-stu-id="c7591-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="c7591-300">客户端应包含两页： 一个用于主页上，另一个用于回调。下面是示例 JavaScript 代码中找到*Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="c7591-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="c7591-301">下面是处理代码中的回调*SignIn.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="c7591-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="c7591-302">最佳做法是将 JavaScript 移动到外部文件，不将其嵌入到其中的 Razor 标记。</span><span class="sxs-lookup"><span data-stu-id="c7591-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="c7591-303">若要使此示例简单，现在合并它们。</span><span class="sxs-lookup"><span data-stu-id="c7591-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="c7591-304">资源所有者密码凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="c7591-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="c7591-305">我们使用的控制台应用来演示此客户端。</span><span class="sxs-lookup"><span data-stu-id="c7591-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="c7591-306">以下是代码：</span><span class="sxs-lookup"><span data-stu-id="c7591-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="c7591-307">客户端凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="c7591-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="c7591-308">与资源所有者密码凭据授予类似，此处是控制台应用程序代码：</span><span class="sxs-lookup"><span data-stu-id="c7591-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
