---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授权服务器 |Microsoft Docs
author: hongyes
description: 本教程将指导您如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。 这是一个高级的教程，该唯一 outlin...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 7b9ba2ca0cd0269ebb3e0e4ae056d4597a198a03
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825485"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="453f5-104">OWIN OAuth 2.0 授权服务器</span><span class="sxs-lookup"><span data-stu-id="453f5-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="453f5-105">通过[Hongye Sun](https://github.com/hongyes)， [Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="453f5-105">by [Hongye Sun](https://github.com/hongyes), [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="453f5-106">本教程将指导您如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。</span><span class="sxs-lookup"><span data-stu-id="453f5-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="453f5-107">这是一种高级的教程，仅简要介绍创建 OWIN OAuth 2.0 授权服务器的步骤。</span><span class="sxs-lookup"><span data-stu-id="453f5-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="453f5-108">这不是分步教程。</span><span class="sxs-lookup"><span data-stu-id="453f5-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="453f5-109">[下载示例代码](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。</span><span class="sxs-lookup"><span data-stu-id="453f5-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="453f5-110">此边框不符合预期要用于创建安全的生产应用。</span><span class="sxs-lookup"><span data-stu-id="453f5-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="453f5-111">本教程旨在提供仅概述了如何实现 OAuth 2.0 授权服务器使用 OWIN OAuth 中间件。</span><span class="sxs-lookup"><span data-stu-id="453f5-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
> 
> 
> ## <a name="software-versions"></a><span data-ttu-id="453f5-112">软件版本</span><span class="sxs-lookup"><span data-stu-id="453f5-112">Software versions</span></span>
> 
> | <span data-ttu-id="453f5-113">**本教程中所示**</span><span class="sxs-lookup"><span data-stu-id="453f5-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="453f5-114">**也可用于**</span><span class="sxs-lookup"><span data-stu-id="453f5-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="453f5-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="453f5-115">Windows 8.1</span></span> | <span data-ttu-id="453f5-116">Windows 8，Windows 7</span><span class="sxs-lookup"><span data-stu-id="453f5-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="453f5-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="453f5-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads) | <span data-ttu-id="453f5-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)。</span><span class="sxs-lookup"><span data-stu-id="453f5-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express).</span></span> <span data-ttu-id="453f5-119">应运行具有最新更新的 visual Studio 2012，但本教程尚未经过测试，并且某些菜单选项和对话框不同。</span><span class="sxs-lookup"><span data-stu-id="453f5-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="453f5-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="453f5-120">.NET 4.5</span></span> |  |
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="453f5-121">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="453f5-121">Questions and Comments</span></span>
> 
> <span data-ttu-id="453f5-122">如果你有与本教程不直接相关的问题，可以将其在发布[Katana 项目 GitHub 上](https://github.com/aspnet/AspNetKatana/)。</span><span class="sxs-lookup"><span data-stu-id="453f5-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="453f5-123">有关的问题和意见关于教程本身，请参阅在页面底部的注释部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="453f5-124">[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749)允许第三方应用程序以获取对 HTTP 服务的有限访问权限。</span><span class="sxs-lookup"><span data-stu-id="453f5-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="453f5-125">而不是使用资源所有者的凭据来访问受保护的资源，客户端获取访问令牌 (这是一个字符串，表示特定的作用域、 生存期和其他访问属性)。</span><span class="sxs-lookup"><span data-stu-id="453f5-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="453f5-126">访问令牌被颁发给第三方客户端通过授权服务器资源所有者的批准。</span><span class="sxs-lookup"><span data-stu-id="453f5-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="453f5-127">本教程介绍：</span><span class="sxs-lookup"><span data-stu-id="453f5-127">This tutorial will cover:</span></span>

- <span data-ttu-id="453f5-128">如何创建授权服务器以支持四种授权授予类型，以及刷新令牌：</span><span class="sxs-lookup"><span data-stu-id="453f5-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="453f5-129">授权代码授予</span><span class="sxs-lookup"><span data-stu-id="453f5-129">Authorization code grant</span></span>
    - <span data-ttu-id="453f5-130">隐式授权</span><span class="sxs-lookup"><span data-stu-id="453f5-130">Implicit Grant</span></span>
    - <span data-ttu-id="453f5-131">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="453f5-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="453f5-132">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="453f5-132">Client Credentials Grant</span></span>
- <span data-ttu-id="453f5-133">创建访问令牌通过受保护的资源服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="453f5-134">正在创建 OAuth 2.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="453f5-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="453f5-135">系统必备</span><span class="sxs-lookup"><span data-stu-id="453f5-135">Prerequisites</span></span>

- <span data-ttu-id="453f5-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免费[Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)，如下所示**软件版本**页的顶部。</span><span class="sxs-lookup"><span data-stu-id="453f5-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="453f5-137">带 OWIN 的熟悉程度。</span><span class="sxs-lookup"><span data-stu-id="453f5-137">Familiarity with OWIN.</span></span> <span data-ttu-id="453f5-138">请参阅[Katana 项目入门](https://msdn.microsoft.com/magazine/dn451439.aspx)并[新增 OWIN 和 Katana](index.md)。</span><span class="sxs-lookup"><span data-stu-id="453f5-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="453f5-139">熟悉[OAuth](http://tools.ietf.org/html/rfc6749)术语中，其中包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)，[协议流](http://tools.ietf.org/html/rfc6749#section-1.2)，以及[授权授予](http://tools.ietf.org/html/rfc6749#section-1.3)。</span><span class="sxs-lookup"><span data-stu-id="453f5-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="453f5-140">[OAuth 2.0 简介](http://tools.ietf.org/html/rfc6749#section-1)提供了详细介绍。</span><span class="sxs-lookup"><span data-stu-id="453f5-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="453f5-141">创建授权服务器</span><span class="sxs-lookup"><span data-stu-id="453f5-141">Create an Authorization Server</span></span>

<span data-ttu-id="453f5-142">在本教程中，我们将大致草图了解如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 创建服务器的授权。</span><span class="sxs-lookup"><span data-stu-id="453f5-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="453f5-143">我们希望很快提供有关已完成的示例中，可供下载本教程不包括每个步骤。</span><span class="sxs-lookup"><span data-stu-id="453f5-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="453f5-144">首先，创建名为空的 web 应用*AuthorizationServer*并安装以下包：</span><span class="sxs-lookup"><span data-stu-id="453f5-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="453f5-145">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="453f5-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="453f5-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="453f5-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="453f5-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="453f5-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="453f5-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="453f5-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="453f5-149">Microsoft.Owin.Security.Google （或任何其他社交登录名打包 Microsoft.Owin.Security.Facebook 等）</span><span class="sxs-lookup"><span data-stu-id="453f5-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="453f5-150">添加[OWIN 启动类](owin-startup-class-detection.md)名为在项目根文件夹下*启动*。</span><span class="sxs-lookup"><span data-stu-id="453f5-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="453f5-151">创建*应用程序\_启动*文件夹。</span><span class="sxs-lookup"><span data-stu-id="453f5-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="453f5-152">选择*应用程序\_启动*文件夹，然后使用 Shift + Alt + A 若要添加的下载的版本*AuthorizationServer\App\_Start\Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="453f5-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="453f5-153">上面的代码使应用程序/外部登录 cookie 和 Google 身份验证，授权服务器本身用于管理帐户。</span><span class="sxs-lookup"><span data-stu-id="453f5-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="453f5-154">`UseOAuthAuthorizationServer`扩展方法是设置授权服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="453f5-155">安装程序选项包括：</span><span class="sxs-lookup"><span data-stu-id="453f5-155">The setup options are:</span></span>

- <span data-ttu-id="453f5-156">`AuthorizeEndpointPath`: 请求路径，其中客户端应用程序会将重定向用户代理以获取用户同意使用颁发的令牌或代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="453f5-157">它必须以具有前导斜杠，例如，"`/Authorize`"。</span><span class="sxs-lookup"><span data-stu-id="453f5-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="453f5-158">`TokenEndpointPath`: 请求路径客户端应用程序直接进行通信以获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="453f5-159">它必须以具有前导斜杠，如"/token"。</span><span class="sxs-lookup"><span data-stu-id="453f5-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="453f5-160">如果客户端颁发[客户端\_机密](http://tools.ietf.org/html/rfc6749#appendix-A.2)，它必须提供给此终结点。</span><span class="sxs-lookup"><span data-stu-id="453f5-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="453f5-161">`ApplicationCanDisplayErrors`： 设置为`true`如果 web 应用程序想要在生成的客户端验证错误的自定义错误页`/Authorize`终结点。</span><span class="sxs-lookup"><span data-stu-id="453f5-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="453f5-162">这才必需的情况下，在浏览器不会重定向回客户端应用程序，例如，当`client_id`或`redirect_uri`不正确。</span><span class="sxs-lookup"><span data-stu-id="453f5-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="453f5-163">`/Authorize`终结点应该会看到"oauth。错误"、"oauth。ErrorDescription"和"oauth。ErrorUri"属性添加到 OWIN 环境。</span><span class="sxs-lookup"><span data-stu-id="453f5-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="453f5-164">如果不为 true，则授权服务器将返回默认错误页的错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="453f5-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="453f5-165">`AllowInsecureHttp`: True 以允许授权和令牌请求到达 HTTP URI 地址，并允许传入`redirect_uri`授权请求参数，具有 HTTP URI 地址。</span><span class="sxs-lookup"><span data-stu-id="453f5-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="453f5-166">安全性-这是只能在开发。</span><span class="sxs-lookup"><span data-stu-id="453f5-166">Security - This is for development only.</span></span>
- <span data-ttu-id="453f5-167">`Provider`： 处理由授权服务器中间件引发事件应用程序提供的对象。</span><span class="sxs-lookup"><span data-stu-id="453f5-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="453f5-168">应用程序可能完全实现接口，或它可能会造成的实例`OAuthAuthorizationServerProvider`并分配此服务器支持的 OAuth 流所需的委托。</span><span class="sxs-lookup"><span data-stu-id="453f5-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="453f5-169">`AuthorizationCodeProvider`： 生成一次性授权代码返回到客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="453f5-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="453f5-170">为 OAuth 服务器要保护的应用程序**必须**提供的一个实例`AuthorizationCodeProvider`由生成的令牌`OnCreate/OnCreateAsync`事件被视为有效只有一个调用`OnReceive/OnReceiveAsync`。</span><span class="sxs-lookup"><span data-stu-id="453f5-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="453f5-171">`RefreshTokenProvider`： 生成可用于生成新的访问令牌时所需的刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="453f5-172">如果未提供授权服务器不会返回的刷新令牌`/Token`终结点。</span><span class="sxs-lookup"><span data-stu-id="453f5-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="453f5-173">帐户管理</span><span class="sxs-lookup"><span data-stu-id="453f5-173">Account Management</span></span>

<span data-ttu-id="453f5-174">OAuth 并不关心其中或如何管理用户帐户信息。</span><span class="sxs-lookup"><span data-stu-id="453f5-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="453f5-175">它具有[ASP.NET 标识](../../../identity/index.md)对其负责。</span><span class="sxs-lookup"><span data-stu-id="453f5-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="453f5-176">在本教程中，我们将简化帐户管理代码，并只需确保该用户可以登录使用 OWIN cookie 中间件。</span><span class="sxs-lookup"><span data-stu-id="453f5-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="453f5-177">下面是简化的示例代码`AccountController`:</span><span class="sxs-lookup"><span data-stu-id="453f5-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="453f5-178">`ValidateClientRedirectUri` 用来验证其注册的重定向 URL 的客户端。</span><span class="sxs-lookup"><span data-stu-id="453f5-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="453f5-179">`ValidateClientAuthentication` 检查的基本方案标头和窗体正文以获取客户端的凭据。</span><span class="sxs-lookup"><span data-stu-id="453f5-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="453f5-180">登录页如下所示：</span><span class="sxs-lookup"><span data-stu-id="453f5-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="453f5-181">查看 IETF 的 OAuth 2[授权代码授予](http://tools.ietf.org/html/rfc6749#section-4.1)现在部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span> 

<span data-ttu-id="453f5-182">**提供程序**（在下表中） 是[OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程序，其类型`OAuthAuthorizationServerProvider`，其中包含所有 OAuth 服务器事件。</span><span class="sxs-lookup"><span data-stu-id="453f5-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span> 

| <span data-ttu-id="453f5-183">从授权代码授予部分流步骤</span><span class="sxs-lookup"><span data-stu-id="453f5-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="453f5-184">下载示例将执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="453f5-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="453f5-185">（A） 客户端将定向到授权终结点资源所有者的用户代理，从而启动流。</span><span class="sxs-lookup"><span data-stu-id="453f5-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="453f5-186">客户端包括客户端标识符、 请求的作用域、 本地状态和重定向 URI 的授权服务器将用户代理返回以后，即可发送授予 （或拒绝） 访问。</span><span class="sxs-lookup"><span data-stu-id="453f5-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="453f5-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="453f5-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="453f5-188">（B） 授权服务器进行身份验证资源所有者 （通过用户代理），并确定资源所有者是允许还是拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="453f5-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="453f5-189">**&lt;如果用户授予访问权限&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="453f5-190">（C） 假定资源所有者授予访问权限，授权服务器将用户代理重定向回客户端使用的重定向 URI 提供早期 （在请求中或客户端注册过程）。</span><span class="sxs-lookup"><span data-stu-id="453f5-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="453f5-191">...</span><span class="sxs-lookup"><span data-stu-id="453f5-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="453f5-192">（D) 客户端通过包含上一步中收到的授权代码授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="453f5-193">当发出请求，客户端进行身份验证与授权服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="453f5-194">客户端会包括重定向 URI 用于获取验证的授权代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="453f5-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="453f5-196">有关实现示例`AuthorizationCodeProvider.CreateAsync`和`ReceiveAsync`以控制创建和验证授权代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="453f5-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="453f5-197">上面的代码使用内存中并发字典来存储代码和标识票证和收到代码后还原标识。</span><span class="sxs-lookup"><span data-stu-id="453f5-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="453f5-198">在实际的应用程序，它将由永久性数据存储替换。</span><span class="sxs-lookup"><span data-stu-id="453f5-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="453f5-199">授权终结点适用于资源所有者授予对客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="453f5-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="453f5-200">通常情况下，它需要一个用户界面来允许用户单击一个按钮，然后确认授权。</span><span class="sxs-lookup"><span data-stu-id="453f5-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="453f5-201">OWIN OAuth 中间件允许应用程序代码来处理授权终结点。</span><span class="sxs-lookup"><span data-stu-id="453f5-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="453f5-202">在我们的示例应用，我们使用名为一个 MVC 控制器`OAuthController`若要对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="453f5-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="453f5-203">以下是示例实现：</span><span class="sxs-lookup"><span data-stu-id="453f5-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="453f5-204">`Authorize`操作将首先检查是否用户已登录到授权服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="453f5-205">如果没有，身份验证中间件质询调用方进行身份验证使用"应用程序"cookie 并将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="453f5-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="453f5-206">（请参阅上面的突出显示的代码。）如果用户已登录，它会呈现授权视图中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="453f5-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="453f5-207">如果**Grant**按钮处于选中状态，`Authorize`操作将创建新的"Bearer"标识和使用它登录。</span><span class="sxs-lookup"><span data-stu-id="453f5-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="453f5-208">它将触发授权服务器生成的持有者令牌并将其发送回客户端与 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="453f5-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span> 

### <a name="implicit-grant"></a><span data-ttu-id="453f5-209">隐式授权</span><span class="sxs-lookup"><span data-stu-id="453f5-209">Implicit Grant</span></span>

<span data-ttu-id="453f5-210">请参阅 IETF 的 OAuth 2[隐式授权](http://tools.ietf.org/html/rfc6749#section-4.2)现在部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="453f5-211">[隐式授权](http://tools.ietf.org/html/rfc6749#section-4.2)图 4 所示的流是流程和映射的 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="453f5-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="453f5-212">流步骤，可从隐式授权部分</span><span class="sxs-lookup"><span data-stu-id="453f5-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="453f5-213">下载示例将执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="453f5-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="453f5-214">（A） 客户端将定向到授权终结点资源所有者的用户代理，从而启动流。</span><span class="sxs-lookup"><span data-stu-id="453f5-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="453f5-215">客户端包括客户端标识符、 请求的作用域、 本地状态和重定向 URI 的授权服务器将用户代理返回以后，即可发送授予 （或拒绝） 访问。</span><span class="sxs-lookup"><span data-stu-id="453f5-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="453f5-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="453f5-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="453f5-217">（B） 授权服务器进行身份验证资源所有者 （通过用户代理），并确定资源所有者是允许还是拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="453f5-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="453f5-218">**&lt;如果用户授予访问权限&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="453f5-219">（C） 假定资源所有者授予访问权限，授权服务器将用户代理重定向回客户端使用的重定向 URI 提供早期 （在请求中或客户端注册过程）。</span><span class="sxs-lookup"><span data-stu-id="453f5-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="453f5-220">...</span><span class="sxs-lookup"><span data-stu-id="453f5-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="453f5-221">（D) 客户端通过包含上一步中收到的授权代码授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="453f5-222">当发出请求，客户端进行身份验证与授权服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="453f5-223">客户端会包括重定向 URI 用于获取验证的授权代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="453f5-224">由于我们已实现授权终结点 (`OAuthController.Authorize`操作) 的授权代码授予，它会自动启用隐式流。</span><span class="sxs-lookup"><span data-stu-id="453f5-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="453f5-225">注意：`Provider.ValidateClientRedirectUri`用来验证其重定向 URL，用于防止隐式授权流发送访问令牌来恶意客户端的客户端 ID ([拦截的攻击](https://www.owasp.org/index.php/Man-in-the-middle_attack))。</span><span class="sxs-lookup"><span data-stu-id="453f5-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="453f5-226">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="453f5-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="453f5-227">请参阅 IETF 的 OAuth 2[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)现在部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="453f5-228">[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)图 5 所示的流是流程和映射的 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="453f5-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="453f5-229">从资源所有者密码凭据授予部分流步骤</span><span class="sxs-lookup"><span data-stu-id="453f5-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="453f5-230">下载示例将执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="453f5-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="453f5-231">（A） 资源所有者向客户端提供其用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="453f5-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="453f5-232">（B） 客户端通过包括从资源所有者处收到的凭据从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="453f5-233">当发出请求，客户端进行身份验证与授权服务器。</span><span class="sxs-lookup"><span data-stu-id="453f5-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="453f5-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="453f5-235">（C） 授权服务器对客户端进行身份验证并验证资源所有者的凭据和有效的情况下颁发访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="453f5-236">下面是示例实现`Provider.GrantResourceOwnerCredentials`:</span><span class="sxs-lookup"><span data-stu-id="453f5-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="453f5-237">上面的代码将解释在本教程的本部分，因此不应在安全或生产应用。</span><span class="sxs-lookup"><span data-stu-id="453f5-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="453f5-238">它不会检查资源所有者凭据。</span><span class="sxs-lookup"><span data-stu-id="453f5-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="453f5-239">它假定每个凭据有效，并为其创建一个新的标识。</span><span class="sxs-lookup"><span data-stu-id="453f5-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="453f5-240">新的标识将用于生成访问令牌和刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="453f5-241">请将代码替换你自己的安全帐户管理代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="453f5-242">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="453f5-242">Client Credentials Grant</span></span>

<span data-ttu-id="453f5-243">请参阅 IETF 的 OAuth 2[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)现在部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="453f5-244">[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)图 6 所示的流是流程和映射的 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="453f5-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="453f5-245">从客户端凭据授予部分流步骤</span><span class="sxs-lookup"><span data-stu-id="453f5-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="453f5-246">下载示例将执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="453f5-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="453f5-247">（A) 客户端向授权服务器进行身份验证，并从令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="453f5-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="453f5-249">（B） 授权服务器进行身份验证客户端，并有效的情况下颁发访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="453f5-250">下面是示例实现`Provider.GrantClientCredentials`:</span><span class="sxs-lookup"><span data-stu-id="453f5-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="453f5-251">上面的代码将解释在本教程的本部分，因此不应在安全或生产应用。</span><span class="sxs-lookup"><span data-stu-id="453f5-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="453f5-252">请将代码替换你自己的安全客户端管理代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="453f5-253">刷新令牌</span><span class="sxs-lookup"><span data-stu-id="453f5-253">Refresh Token</span></span>

<span data-ttu-id="453f5-254">请参阅 IETF 的 OAuth 2[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)现在部分。</span><span class="sxs-lookup"><span data-stu-id="453f5-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="453f5-255">[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)图 2 所示的流是流程和映射的 OWIN OAuth 中间件遵循。</span><span class="sxs-lookup"><span data-stu-id="453f5-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="453f5-256">从客户端凭据授予部分流步骤</span><span class="sxs-lookup"><span data-stu-id="453f5-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="453f5-257">下载示例将执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="453f5-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="453f5-258">（G) 客户端通过使用授权服务器进行身份验证和提供刷新令牌请求新的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="453f5-259">客户端身份验证要求基于客户端类型和授权服务器策略。</span><span class="sxs-lookup"><span data-stu-id="453f5-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="453f5-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsyncRefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="453f5-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="453f5-261">（H） 授权服务器对客户端进行身份验证并验证刷新令牌和有效的情况下颁发新的访问令牌 （和 （可选） 新的刷新令牌）。</span><span class="sxs-lookup"><span data-stu-id="453f5-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="453f5-262">下面是示例实现`Provider.GrantRefreshToken`:</span><span class="sxs-lookup"><span data-stu-id="453f5-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span> 

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="453f5-263">创建访问令牌通过受保护的资源服务器</span><span class="sxs-lookup"><span data-stu-id="453f5-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="453f5-264">创建空 web 应用程序项目并安装以下项目中的包：</span><span class="sxs-lookup"><span data-stu-id="453f5-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="453f5-265">Microsoft.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="453f5-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="453f5-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="453f5-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="453f5-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="453f5-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="453f5-268">创建一个 startup 类，并配置身份验证和 Web API。</span><span class="sxs-lookup"><span data-stu-id="453f5-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="453f5-269">请参阅*AuthorizationServer\ResourceServer\Startup.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="453f5-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="453f5-270">请参阅*AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="453f5-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="453f5-271">请参阅*AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs*示例下载中。</span><span class="sxs-lookup"><span data-stu-id="453f5-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="453f5-272">`UseCors` 方法允许所有域的 CORS。</span><span class="sxs-lookup"><span data-stu-id="453f5-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="453f5-273">`UseOAuthBearerAuthentication` 方法使 OAuth 持有者令牌身份验证中间件将接收并验证从授权标头中请求的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="453f5-274">`Config.SuppressDefaultHostAuthenticaiton` 取消显示默认托管身份验证的主体从该应用程序，因此所有请求都将匿名后此调用。</span><span class="sxs-lookup"><span data-stu-id="453f5-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="453f5-275">`HostAuthenticationFilter` 启用身份验证只为指定的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="453f5-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="453f5-276">在这种情况下，它是持有者身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="453f5-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="453f5-277">为了演示已经过身份验证的标识，我们创建 ApiController 以输出当前用户的声明。</span><span class="sxs-lookup"><span data-stu-id="453f5-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="453f5-278">如果授权服务器和资源服务器不在同一台计算机上，OAuth 中间件将使用不同的计算机密钥来加密和解密持有者访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="453f5-279">为了共享这两个项目之间的相同私钥，我们添加相同`machinekey`设置中均*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="453f5-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="453f5-280">创建 OAuth 2.0 客户端</span><span class="sxs-lookup"><span data-stu-id="453f5-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="453f5-281">我们使用[DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 包来简化客户端代码。</span><span class="sxs-lookup"><span data-stu-id="453f5-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="453f5-282">授权代码授予客户端</span><span class="sxs-lookup"><span data-stu-id="453f5-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="453f5-283">此客户端是一个 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="453f5-283">This client is an MVC application.</span></span> <span data-ttu-id="453f5-284">它将触发授权代码授予流以从后端获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="453f5-285">它具有单个页面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="453f5-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="453f5-286">**Authorize**按钮将浏览器重定向到授权服务器，以通知资源所有者授予对此客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="453f5-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="453f5-287">**刷新**按钮将获取新访问令牌和刷新令牌中使用当前刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="453f5-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="453f5-288">**访问受保护资源 API**按钮，可以调用资源服务器，以获取当前用户的声明数据并在页面上显示它们。</span><span class="sxs-lookup"><span data-stu-id="453f5-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="453f5-289">下面是示例代码的`HomeController`的客户端。</span><span class="sxs-lookup"><span data-stu-id="453f5-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="453f5-290">`DotNetOpenAuth` 默认情况下需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="453f5-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="453f5-291">由于我们的演示使用 HTTP，因此需要添加以下设置配置文件中：</span><span class="sxs-lookup"><span data-stu-id="453f5-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="453f5-292">安全性-永远不会禁用 SSL 生产应用中。</span><span class="sxs-lookup"><span data-stu-id="453f5-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="453f5-293">通过线缆现在以明文发送你的登录凭据。</span><span class="sxs-lookup"><span data-stu-id="453f5-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="453f5-294">上面的代码是仅用于本地示例调试和探索。</span><span class="sxs-lookup"><span data-stu-id="453f5-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="453f5-295">隐式授予客户端</span><span class="sxs-lookup"><span data-stu-id="453f5-295">Implicit Grant Client</span></span>

<span data-ttu-id="453f5-296">此客户端使用 JavaScript 为：</span><span class="sxs-lookup"><span data-stu-id="453f5-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="453f5-297">打开新的窗口和重定向到授权服务器的授权终结点。</span><span class="sxs-lookup"><span data-stu-id="453f5-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="453f5-298">从获取访问令牌 URL 片段时它将重定向回。</span><span class="sxs-lookup"><span data-stu-id="453f5-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="453f5-299">下图显示了此过程：</span><span class="sxs-lookup"><span data-stu-id="453f5-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="453f5-300">客户端应具有两个页面： 一个用于主页上，另一个用于回调。下面是示例代码中找到的 JavaScript *Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="453f5-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="453f5-301">下面是处理代码中的回调*SignIn.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="453f5-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="453f5-302">最佳做法是将 JavaScript 移到外部文件并不将其嵌入和 Razor 标记。</span><span class="sxs-lookup"><span data-stu-id="453f5-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="453f5-303">若要使此示例简单明了，已经合并它们。</span><span class="sxs-lookup"><span data-stu-id="453f5-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="453f5-304">资源所有者密码凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="453f5-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="453f5-305">我们使用一个控制台应用程序来演示此客户端。</span><span class="sxs-lookup"><span data-stu-id="453f5-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="453f5-306">下面是代码：</span><span class="sxs-lookup"><span data-stu-id="453f5-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="453f5-307">客户端凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="453f5-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="453f5-308">与资源所有者密码凭据授予类似，下面是控制台应用程序代码：</span><span class="sxs-lookup"><span data-stu-id="453f5-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
