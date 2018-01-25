---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: "使用 Web API 中的 SSL |Microsoft 文档"
author: MikeWasson
description: "演示如何使用 SSL 与 ASP.NET Web API，包括使用 SSL 客户端证书。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 127b336cb628e55bd59481ecb1c4df83960dc25b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="working-with-ssl-in-web-api"></a><span data-ttu-id="04257-103">使用 Web API 中的 SSL</span><span class="sxs-lookup"><span data-stu-id="04257-103">Working with SSL in Web API</span></span>
====================
<span data-ttu-id="04257-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="04257-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="04257-105">通过一般 HTTP 几种常见的身份验证方案不安全。</span><span class="sxs-lookup"><span data-stu-id="04257-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="04257-106">具体而言，基本身份验证和窗体身份验证发送未加密的凭据。</span><span class="sxs-lookup"><span data-stu-id="04257-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="04257-107">若要是安全的这些身份验证方案*必须*使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="04257-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="04257-108">此外，可以使用 SSL 客户端证书进行身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="04257-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="04257-109">启用服务器上的 SSL</span><span class="sxs-lookup"><span data-stu-id="04257-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="04257-110">若要配置 IIS 7 或更高版本的 SSL 设置：</span><span class="sxs-lookup"><span data-stu-id="04257-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="04257-111">创建或获取证书。</span><span class="sxs-lookup"><span data-stu-id="04257-111">Create or get a certificate.</span></span> <span data-ttu-id="04257-112">用于测试，你可以创建自签名的证书。</span><span class="sxs-lookup"><span data-stu-id="04257-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="04257-113">将添加 HTTPS 绑定。</span><span class="sxs-lookup"><span data-stu-id="04257-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="04257-114">有关详细信息，请参阅[如何设置 SSL 在 IIS 7 上](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="04257-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="04257-115">对于本地测试，您可以启用在 IIS Express 从 Visual Studio 中的 SSL。</span><span class="sxs-lookup"><span data-stu-id="04257-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="04257-116">在属性窗口中，设置**启用 SSL**到**True**。</span><span class="sxs-lookup"><span data-stu-id="04257-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="04257-117">记下的值**SSL URL**; 使用此 URL 用于测试 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="04257-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="04257-118">强制实施 SSL Web API 控制器中</span><span class="sxs-lookup"><span data-stu-id="04257-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="04257-119">如果你有 HTTPS 和 HTTP 绑定，客户端仍可以使用 HTTP 访问站点。</span><span class="sxs-lookup"><span data-stu-id="04257-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="04257-120">你可能会使某些资源，可通过 HTTP，而其他资源需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="04257-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="04257-121">在这种情况下，使用操作筛选器要求将 SSL 用于受保护的资源。</span><span class="sxs-lookup"><span data-stu-id="04257-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="04257-122">下面的代码演示检查 SSL 的 Web API 身份验证筛选器：</span><span class="sxs-lookup"><span data-stu-id="04257-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="04257-123">将此筛选器添加到要求使用 SSL 的任何 Web API 操作：</span><span class="sxs-lookup"><span data-stu-id="04257-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="04257-124">SSL 客户端证书</span><span class="sxs-lookup"><span data-stu-id="04257-124">SSL Client Certificates</span></span>

<span data-ttu-id="04257-125">SSL 通过使用公钥基础结构证书提供身份验证。</span><span class="sxs-lookup"><span data-stu-id="04257-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="04257-126">服务器必须提供客户端到服务器进行身份验证的证书。</span><span class="sxs-lookup"><span data-stu-id="04257-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="04257-127">较不常用于客户端提供一个证书到服务器，但这是用于身份验证客户端的一个选项。</span><span class="sxs-lookup"><span data-stu-id="04257-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="04257-128">若要使用 SSL 客户端证书，你需要分配到你的用户的签名的证书的方法。</span><span class="sxs-lookup"><span data-stu-id="04257-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="04257-129">对于许多应用程序类型，这不会获得良好的用户体验，但在某些环境中 （例如，企业），它可能是一种可行。</span><span class="sxs-lookup"><span data-stu-id="04257-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="04257-130">优点</span><span class="sxs-lookup"><span data-stu-id="04257-130">Advantages</span></span> | <span data-ttu-id="04257-131">缺点</span><span class="sxs-lookup"><span data-stu-id="04257-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="04257-132">-证书凭据都比用户名/密码更强。</span><span class="sxs-lookup"><span data-stu-id="04257-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="04257-133">-SSL 提供了完整的安全通道，使用身份验证、 消息完整性和消息加密。</span><span class="sxs-lookup"><span data-stu-id="04257-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="04257-134">-你必须获取并管理 PKI 证书。</span><span class="sxs-lookup"><span data-stu-id="04257-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="04257-135">-客户端平台必须支持 SSL 客户端证书。</span><span class="sxs-lookup"><span data-stu-id="04257-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="04257-136">若要配置 IIS 以接受客户端证书，打开 IIS 管理器，然后执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="04257-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="04257-137">单击树视图中的站点节点。</span><span class="sxs-lookup"><span data-stu-id="04257-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="04257-138">双击**SSL 设置**在中间窗格中的功能。</span><span class="sxs-lookup"><span data-stu-id="04257-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="04257-139">下**客户端证书**，选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="04257-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="04257-140">**接受**: IIS 将接受来自客户端的证书，但不要求。</span><span class="sxs-lookup"><span data-stu-id="04257-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="04257-141">**需要**： 需要客户端证书。</span><span class="sxs-lookup"><span data-stu-id="04257-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="04257-142">（若要启用此选项，你还必须选择"要求 SSL"）</span><span class="sxs-lookup"><span data-stu-id="04257-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="04257-143">你也可以在 ApplicationHost.config 文件中设置这些选项：</span><span class="sxs-lookup"><span data-stu-id="04257-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="04257-144">**SslNegotiateCert** IIS 将接受来自客户端的证书，但不需要进行一次 （等效于"接受"选项在 IIS 管理器） 的标记表示。</span><span class="sxs-lookup"><span data-stu-id="04257-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="04257-145">如果需要证书，请设置**SslRequireCert**标志。</span><span class="sxs-lookup"><span data-stu-id="04257-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="04257-146">用于测试，你还可以设置这些选项在 IIS Express 中，在本地 applicationhost。位于"Documents\IISExpress\config"中的配置文件。</span><span class="sxs-lookup"><span data-stu-id="04257-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="04257-147">创建客户端证书以便进行测试</span><span class="sxs-lookup"><span data-stu-id="04257-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="04257-148">出于测试目的，你可以使用[MakeCert.exe](https://msdn.microsoft.com/library/bfsktky3.aspx)创建客户端证书。</span><span class="sxs-lookup"><span data-stu-id="04257-148">For testing purposes, you can use [MakeCert.exe](https://msdn.microsoft.com/library/bfsktky3.aspx) to create a client certificate.</span></span> <span data-ttu-id="04257-149">首先，创建测试根颁发机构：</span><span class="sxs-lookup"><span data-stu-id="04257-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="04257-150">Makecert 将提示你输入私钥的密码。</span><span class="sxs-lookup"><span data-stu-id="04257-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="04257-151">接下来，将证书添加到测试服务器的"受信任根证书颁发机构"存储，，如下所示：</span><span class="sxs-lookup"><span data-stu-id="04257-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="04257-152">打开 MMC。</span><span class="sxs-lookup"><span data-stu-id="04257-152">Open MMC.</span></span>
2. <span data-ttu-id="04257-153">下**文件**，选择**添加/删除管理单元中**。</span><span class="sxs-lookup"><span data-stu-id="04257-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="04257-154">选择**计算机帐户**。</span><span class="sxs-lookup"><span data-stu-id="04257-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="04257-155">选择**本地计算机**并完成向导。</span><span class="sxs-lookup"><span data-stu-id="04257-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="04257-156">在导航窗格中，展开"受信任根证书颁发机构"节点。</span><span class="sxs-lookup"><span data-stu-id="04257-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="04257-157">上**操作**菜单上，指向**所有任务**，然后单击**导入**以启动证书导入向导。</span><span class="sxs-lookup"><span data-stu-id="04257-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="04257-158">浏览到证书文件，TempCA.cer。</span><span class="sxs-lookup"><span data-stu-id="04257-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="04257-159">单击**打开**，然后单击**下一步**并完成向导。</span><span class="sxs-lookup"><span data-stu-id="04257-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="04257-160">（你将会提示您重新输入密码。）</span><span class="sxs-lookup"><span data-stu-id="04257-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="04257-161">现在创建的第一个证书由签名的客户端证书：</span><span class="sxs-lookup"><span data-stu-id="04257-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="04257-162">在 Web API 中使用客户端证书</span><span class="sxs-lookup"><span data-stu-id="04257-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="04257-163">在服务器端中，可以获取客户端证书，通过调用[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)请求消息。</span><span class="sxs-lookup"><span data-stu-id="04257-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="04257-164">该方法返回没有客户端证书的情况下为 null。</span><span class="sxs-lookup"><span data-stu-id="04257-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="04257-165">否则，它将返回**X509Certificate2**实例。</span><span class="sxs-lookup"><span data-stu-id="04257-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="04257-166">使用此对象获取的证书，如签发者和使用者中的信息。</span><span class="sxs-lookup"><span data-stu-id="04257-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="04257-167">然后你可以使用此信息用于身份验证和/或授权。</span><span class="sxs-lookup"><span data-stu-id="04257-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
