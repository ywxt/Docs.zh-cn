---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本身份验证 |Microsoft 文档
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用基本身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/02/2014
ms.topic: article
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 4b8e6410668b2db289488bb4b6cd26d881e70f4c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508126"
---
<a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="21569-103">ASP.NET Web API 中的基本身份验证</span><span class="sxs-lookup"><span data-stu-id="21569-103">Basic Authentication in ASP.NET Web API</span></span>
====================
<span data-ttu-id="21569-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="21569-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="21569-105">基本身份验证在中定义[RFC 2617、 HTTP 身份验证： 基本和摘要式访问身份验证](http://www.ietf.org/rfc/rfc2617.txt)。</span><span class="sxs-lookup"><span data-stu-id="21569-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="21569-106">缺点</span><span class="sxs-lookup"><span data-stu-id="21569-106">Disadvantages</span></span>

- <span data-ttu-id="21569-107">用户凭据在请求中发送。</span><span class="sxs-lookup"><span data-stu-id="21569-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="21569-108">以纯文本形式发送凭据。</span><span class="sxs-lookup"><span data-stu-id="21569-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="21569-109">随每个请求一起发送凭据。</span><span class="sxs-lookup"><span data-stu-id="21569-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="21569-110">无法注销，除非通过结束浏览器会话。</span><span class="sxs-lookup"><span data-stu-id="21569-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="21569-111">易受到跨站点请求伪造 (CSRF);需要反 CSRF 度量值。</span><span class="sxs-lookup"><span data-stu-id="21569-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="21569-112">优点</span><span class="sxs-lookup"><span data-stu-id="21569-112">Advantages</span></span>

- <span data-ttu-id="21569-113">Internet 标准。</span><span class="sxs-lookup"><span data-stu-id="21569-113">Internet standard.</span></span>
- <span data-ttu-id="21569-114">支持所有主要浏览器。</span><span class="sxs-lookup"><span data-stu-id="21569-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="21569-115">相对简单的协议。</span><span class="sxs-lookup"><span data-stu-id="21569-115">Relatively simple protocol.</span></span>

<span data-ttu-id="21569-116">基本身份验证工作原理如下：</span><span class="sxs-lookup"><span data-stu-id="21569-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="21569-117">如果请求要求身份验证，则服务器将返回 401 （未授权）。</span><span class="sxs-lookup"><span data-stu-id="21569-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="21569-118">响应包含 Www-authenticate 标头，，该值指示服务器支持基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="21569-119">客户端将发送另一个请求，授权标头中的客户端凭据。</span><span class="sxs-lookup"><span data-stu-id="21569-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="21569-120">凭据的格式设置为"名称： 密码"，base64 编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="21569-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="21569-121">不加密凭据。</span><span class="sxs-lookup"><span data-stu-id="21569-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="21569-122">在"领域"。 的上下文中执行基本身份验证</span><span class="sxs-lookup"><span data-stu-id="21569-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="21569-123">服务器的 Www-authenticate 标头中包含的领域的名称。</span><span class="sxs-lookup"><span data-stu-id="21569-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="21569-124">用户的凭据是在该领域内有效。</span><span class="sxs-lookup"><span data-stu-id="21569-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="21569-125">领域的确切作用域由服务器定义。</span><span class="sxs-lookup"><span data-stu-id="21569-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="21569-126">例如，你可以按顺序对分区资源定义几个领域。</span><span class="sxs-lookup"><span data-stu-id="21569-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="21569-127">将凭据发送未加密，因为基本身份验证才安全通过 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="21569-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="21569-128">请参阅[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="21569-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="21569-129">基本身份验证也是很容易受到 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="21569-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="21569-130">用户输入的凭据后，浏览器向自动发送它们在后续请求同一域中，会话的持续时间。</span><span class="sxs-lookup"><span data-stu-id="21569-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="21569-131">这包括 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="21569-131">This includes AJAX requests.</span></span> <span data-ttu-id="21569-132">请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="21569-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="21569-133">使用 IIS 基本身份验证</span><span class="sxs-lookup"><span data-stu-id="21569-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="21569-134">IIS 支持基本身份验证，但需要注意： 用户针对其 Windows 凭据进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="21569-135">这意味着用户必须具有与服务器的域帐户。</span><span class="sxs-lookup"><span data-stu-id="21569-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="21569-136">面向公众的网站，你通常想要针对 ASP.NET 成员资格提供程序进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="21569-137">若要启用基本身份验证使用 IIS，请将身份验证模式设置为 ASP.NET 项目的 Web.config 中的"Windows":</span><span class="sxs-lookup"><span data-stu-id="21569-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="21569-138">在此模式下，IIS 使用 Windows 凭据进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="21569-139">此外，你必须启用 IIS 中的基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="21569-140">在 IIS 管理器中，转到功能视图、 选择身份验证，并启用基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="21569-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="21569-141">在 Web API 项目中，添加`[Authorize]`所的任何控制器操作需要身份验证的属性。</span><span class="sxs-lookup"><span data-stu-id="21569-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="21569-142">客户端自行进行身份验证请求中设置的 Authorization 标头。</span><span class="sxs-lookup"><span data-stu-id="21569-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="21569-143">浏览器客户端自动执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="21569-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="21569-144">Nonbrowser 客户端将需要设置标头。</span><span class="sxs-lookup"><span data-stu-id="21569-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="21569-145">使用自定义成员资格基本身份验证</span><span class="sxs-lookup"><span data-stu-id="21569-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="21569-146">如前文所述，内置于 IIS 基本身份验证使用 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="21569-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="21569-147">这意味着你需要的宿主服务器上创建你的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="21569-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="21569-148">但对于 internet 应用程序，用户帐户通常存储在外部数据库。</span><span class="sxs-lookup"><span data-stu-id="21569-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="21569-149">下面的代码如何执行基本身份验证的 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="21569-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="21569-150">您可以轻松插入的 ASP.NET 成员资格提供程序中通过将`CheckPassword`方法，这是在此示例中的虚拟方法。</span><span class="sxs-lookup"><span data-stu-id="21569-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="21569-151">在 Web API 2 中，你应考虑编写[身份验证筛选器](authentication-filters.md)或[OWIN 中间件](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="21569-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="21569-152">若要启用 HTTP 模块，将以下代码添加到 web.config 文件中**system.webServer**部分：</span><span class="sxs-lookup"><span data-stu-id="21569-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="21569-153">"程序集名称"替换 （不包括"dll"扩展） 的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="21569-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="21569-154">应禁用其他身份验证方案，如窗体或 Windows 验证</span><span class="sxs-lookup"><span data-stu-id="21569-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
