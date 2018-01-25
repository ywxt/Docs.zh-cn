---
uid: signalr/overview/older-versions/hub-authorization
title: "身份验证和授权 SignalR 集线器的 (SignalR 1.x) |Microsoft 文档"
author: pfletcher
description: "本主题介绍如何限制哪些用户或角色可以访问中心方法。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: d73ab6c9091556a62e5d9475baf67a18e305585f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="d02cd-103">身份验证和授权 SignalR 集线器的 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="d02cd-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>
====================
<span data-ttu-id="d02cd-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d02cd-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d02cd-105">本主题介绍如何限制哪些用户或角色可以访问中心方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>


## <a name="overview"></a><span data-ttu-id="d02cd-106">概述</span><span class="sxs-lookup"><span data-stu-id="d02cd-106">Overview</span></span>

<span data-ttu-id="d02cd-107">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="d02cd-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="d02cd-108">授权属性</span><span class="sxs-lookup"><span data-stu-id="d02cd-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="d02cd-109">要求对所有中心身份验证</span><span class="sxs-lookup"><span data-stu-id="d02cd-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="d02cd-110">自定义的授权</span><span class="sxs-lookup"><span data-stu-id="d02cd-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="d02cd-111">将身份验证信息传递给客户端</span><span class="sxs-lookup"><span data-stu-id="d02cd-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="d02cd-112">用于.NET 客户端身份验证选项</span><span class="sxs-lookup"><span data-stu-id="d02cd-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="d02cd-113">使用 Forms 身份验证的 cookie</span><span class="sxs-lookup"><span data-stu-id="d02cd-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="d02cd-114">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="d02cd-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="d02cd-115">连接标头</span><span class="sxs-lookup"><span data-stu-id="d02cd-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="d02cd-116">Certificate</span><span class="sxs-lookup"><span data-stu-id="d02cd-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="d02cd-117">授权属性</span><span class="sxs-lookup"><span data-stu-id="d02cd-117">Authorize attribute</span></span>

<span data-ttu-id="d02cd-118">SignalR 提供[Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)特性来指定哪些用户或角色有权访问的中心或方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="d02cd-119">此属性位于`Microsoft.AspNet.SignalR`命名空间。</span><span class="sxs-lookup"><span data-stu-id="d02cd-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="d02cd-120">你将应用`Authorize`属性为中心或中心中的特定方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="d02cd-121">当你将`Authorize`特性应用到中心类，指定的授权要求适用于所有中心中的方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="d02cd-122">你可以将应用的授权要求的不同类型如下所示。</span><span class="sxs-lookup"><span data-stu-id="d02cd-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="d02cd-123">而无需`Authorize`属性，中心上的所有公共方法可供连接到集线器的客户端。</span><span class="sxs-lookup"><span data-stu-id="d02cd-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="d02cd-124">如果已定义 web 应用程序中名为"Admin"的角色，则可以指定该角色中的唯一用户可以访问替换为以下代码的集线器。</span><span class="sxs-lookup"><span data-stu-id="d02cd-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="d02cd-125">或者，你可以指定一个中心包含可供所有用户的一个方法，并可仅供经过身份验证的用户，如下所示的第二个方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="d02cd-126">下面的示例地址不同的授权方案：</span><span class="sxs-lookup"><span data-stu-id="d02cd-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="d02cd-127">`[Authorize]`– 仅身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="d02cd-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="d02cd-128">`[Authorize(Roles = "Admin,Manager")]`– 仅经过身份验证中的指定角色的用户</span><span class="sxs-lookup"><span data-stu-id="d02cd-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="d02cd-129">`[Authorize(Users = "user1,user2")]`– 仅经过身份验证与指定的用户名的用户</span><span class="sxs-lookup"><span data-stu-id="d02cd-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="d02cd-130">`[Authorize(RequireOutgoing=false)]`– 仅经过身份验证的用户可以调用中心，但从服务器返回到客户端的调用不受限制授权，例如，当仅某些用户可以发送一条消息，但所有其他人可以接收消息时。</span><span class="sxs-lookup"><span data-stu-id="d02cd-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="d02cd-131">RequireOutgoing 属性只能应用到整个中心，不能对中心内的个人方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="d02cd-132">RequireOutgoing 未设置为 false，满足的授权要求的用户将调用从服务器中。</span><span class="sxs-lookup"><span data-stu-id="d02cd-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="d02cd-133">要求对所有中心身份验证</span><span class="sxs-lookup"><span data-stu-id="d02cd-133">Require authentication for all hubs</span></span>

<span data-ttu-id="d02cd-134">你可以要求身份验证的所有中心和中心方法在你的应用程序通过调用[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)应用程序启动时的方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="d02cd-135">如果你有多个中心并想要为所有这些强制实施身份验证要求，可使用此方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="d02cd-136">使用此方法，不能指定角色、 用户或传出的授权。</span><span class="sxs-lookup"><span data-stu-id="d02cd-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="d02cd-137">你仅可以指定对中心方法的访问仅限于经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="d02cd-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="d02cd-138">但是，你仍可以应用 Authorize 属性为中心或方法，以指定其他要求。</span><span class="sxs-lookup"><span data-stu-id="d02cd-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="d02cd-139">除了身份验证的基本要求应用特性中指定的任何要求。</span><span class="sxs-lookup"><span data-stu-id="d02cd-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="d02cd-140">下面的示例演示将所有的中心方法限制为经过身份验证用户的 Global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="d02cd-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="d02cd-141">如果调用`RequireAuthentication()`方法处理 SignalR 请求后，会引发 SignalR`InvalidOperationException`异常。</span><span class="sxs-lookup"><span data-stu-id="d02cd-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="d02cd-142">将引发此异常，因为调用管道后，不能向非 HubPipeline 添加模块。</span><span class="sxs-lookup"><span data-stu-id="d02cd-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="d02cd-143">上面的示例演示调用`RequireAuthentication`中的方法`Application_Start`会执行一次之前处理的第一个请求的方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="d02cd-144">自定义的授权</span><span class="sxs-lookup"><span data-stu-id="d02cd-144">Customized authorization</span></span>

<span data-ttu-id="d02cd-145">如果你需要自定义如何确定授权，你可以创建一个派生自的类`AuthorizeAttribute`，并重写[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="d02cd-146">为每个请求来确定是否授权用户以完成该请求调用此方法。</span><span class="sxs-lookup"><span data-stu-id="d02cd-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="d02cd-147">在重写方法中，为你的授权方案提供必要的逻辑。</span><span class="sxs-lookup"><span data-stu-id="d02cd-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="d02cd-148">下面的示例演示如何强制实施通过基于声明的标识的授权。</span><span class="sxs-lookup"><span data-stu-id="d02cd-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="d02cd-149">将身份验证信息传递给客户端</span><span class="sxs-lookup"><span data-stu-id="d02cd-149">Pass authentication information to clients</span></span>

<span data-ttu-id="d02cd-150">你可能需要在客户端运行的代码中使用的身份验证信息。</span><span class="sxs-lookup"><span data-stu-id="d02cd-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="d02cd-151">客户端上调用方法时，你将传递所需的信息。</span><span class="sxs-lookup"><span data-stu-id="d02cd-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="d02cd-152">例如，聊天应用程序方法无法将作为参数传递的消息，同时发布的人员的用户名称如下所示。</span><span class="sxs-lookup"><span data-stu-id="d02cd-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="d02cd-153">或者，你可以创建要表示的身份验证信息并将该对象作为参数传递的对象，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d02cd-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="d02cd-154">根据恶意用户可以使用它来模拟来自该客户端的请求，应永远不会将一台客户端连接 id 传递给其他客户端。</span><span class="sxs-lookup"><span data-stu-id="d02cd-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="d02cd-155">用于.NET 客户端身份验证选项</span><span class="sxs-lookup"><span data-stu-id="d02cd-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="d02cd-156">当你有.NET 客户端，例如，控制台应用程序，与被限制为身份验证的用户的集线器交互时，您可以传递在 cookie、 连接标头或证书的身份验证凭据。</span><span class="sxs-lookup"><span data-stu-id="d02cd-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="d02cd-157">此部分中的示例演示如何使用这些不同的方法，以便进行用户身份验证。</span><span class="sxs-lookup"><span data-stu-id="d02cd-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="d02cd-158">它们不是功能完整的 SignalR 应用。</span><span class="sxs-lookup"><span data-stu-id="d02cd-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="d02cd-159">有关使用 SignalR 的.NET 客户端的详细信息，请参阅[中心 API 指南-.NET 客户端](../guide-to-the-api/hubs-api-guide-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="d02cd-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="d02cd-160">Cookie</span><span class="sxs-lookup"><span data-stu-id="d02cd-160">Cookie</span></span>

<span data-ttu-id="d02cd-161">当.NET 客户端与使用 ASP.NET 窗体身份验证的集线器交互时，你将需要手动对连接设置身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="d02cd-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="d02cd-162">添加到 cookie`CookieContainer`属性[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="d02cd-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="d02cd-163">下面的示例演示在网页上检索身份验证 cookie 并将该 cookie 添加到连接的控制台应用。</span><span class="sxs-lookup"><span data-stu-id="d02cd-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="d02cd-164">URL`https://www.contoso.com/RemoteLogin`到一个网页，你将需要创建示例点中。</span><span class="sxs-lookup"><span data-stu-id="d02cd-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="d02cd-165">该页面将检索已发布的用户名和密码，并尝试登录用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="d02cd-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="d02cd-166">控制台应用程序发送到 www.contoso.com/RemoteLogin 无法引用包含下面的代码隐藏文件的空页的凭据。</span><span class="sxs-lookup"><span data-stu-id="d02cd-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="d02cd-167">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="d02cd-167">Windows authentication</span></span>

<span data-ttu-id="d02cd-168">当使用 Windows 身份验证，您可以通过传递当前用户的凭据[在](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="d02cd-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="d02cd-169">在的值设置为连接的凭据。</span><span class="sxs-lookup"><span data-stu-id="d02cd-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="d02cd-170">连接标头</span><span class="sxs-lookup"><span data-stu-id="d02cd-170">Connection header</span></span>

<span data-ttu-id="d02cd-171">如果你的应用程序不使用 cookie，你可以连接标头中传递用户信息。</span><span class="sxs-lookup"><span data-stu-id="d02cd-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="d02cd-172">例如，你可以连接标头中传递一个令牌。</span><span class="sxs-lookup"><span data-stu-id="d02cd-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="d02cd-173">然后，在中心，你将验证用户的令牌。</span><span class="sxs-lookup"><span data-stu-id="d02cd-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="d02cd-174">证书</span><span class="sxs-lookup"><span data-stu-id="d02cd-174">Certificate</span></span>

<span data-ttu-id="d02cd-175">你可以传递一个客户端证书来验证用户。</span><span class="sxs-lookup"><span data-stu-id="d02cd-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="d02cd-176">创建连接时添加证书。</span><span class="sxs-lookup"><span data-stu-id="d02cd-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="d02cd-177">下面的示例演示如何将客户端证书添加到连接;它不显示完整的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="d02cd-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="d02cd-178">它使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)提供多种不同的方式来创建证书的类。</span><span class="sxs-lookup"><span data-stu-id="d02cd-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
