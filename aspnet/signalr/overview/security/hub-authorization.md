---
uid: signalr/overview/security/hub-authorization
title: 身份验证和授权 SignalR 集线器的 |Microsoft 文档
author: pfletcher
description: 本主题介绍如何限制哪些用户或角色可以访问中心方法。 本主题中的软件版本使用，Visual Studio 2013.NET 4.5 SignalR 遇到...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/05/2015
ms.topic: article
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8e3bc8889efb1be80c57084fb04dc8030b386601
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="b7969-104">身份验证和授权 SignalR 集线器的</span><span class="sxs-lookup"><span data-stu-id="b7969-104">Authentication and Authorization for SignalR Hubs</span></span>
====================
<span data-ttu-id="b7969-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b7969-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b7969-106">本主题介绍如何限制哪些用户或角色可以访问中心方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-106">This topic describes how to restrict which users or roles can access hub methods.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b7969-107">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="b7969-107">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="b7969-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b7969-108">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="b7969-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b7969-109">.NET 4.5</span></span>
> - <span data-ttu-id="b7969-110">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="b7969-110">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="b7969-111">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="b7969-111">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="b7969-112">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b7969-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="b7969-113">问题和意见</span><span class="sxs-lookup"><span data-stu-id="b7969-113">Questions and comments</span></span>
> 
> <span data-ttu-id="b7969-114">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="b7969-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b7969-115">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="b7969-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="b7969-116">概述</span><span class="sxs-lookup"><span data-stu-id="b7969-116">Overview</span></span>

<span data-ttu-id="b7969-117">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="b7969-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="b7969-118">授权属性</span><span class="sxs-lookup"><span data-stu-id="b7969-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="b7969-119">要求对所有中心身份验证</span><span class="sxs-lookup"><span data-stu-id="b7969-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="b7969-120">自定义的授权</span><span class="sxs-lookup"><span data-stu-id="b7969-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="b7969-121">将身份验证信息传递给客户端</span><span class="sxs-lookup"><span data-stu-id="b7969-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="b7969-122">用于.NET 客户端身份验证选项</span><span class="sxs-lookup"><span data-stu-id="b7969-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="b7969-123">使用 Forms 身份验证的 cookie</span><span class="sxs-lookup"><span data-stu-id="b7969-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="b7969-124">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="b7969-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="b7969-125">连接标头</span><span class="sxs-lookup"><span data-stu-id="b7969-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="b7969-126">Certificate</span><span class="sxs-lookup"><span data-stu-id="b7969-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="b7969-127">授权属性</span><span class="sxs-lookup"><span data-stu-id="b7969-127">Authorize attribute</span></span>

<span data-ttu-id="b7969-128">SignalR 提供[Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)特性来指定哪些用户或角色有权访问的中心或方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="b7969-129">此属性位于`Microsoft.AspNet.SignalR`命名空间。</span><span class="sxs-lookup"><span data-stu-id="b7969-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="b7969-130">你将应用`Authorize`属性为中心或中心中的特定方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="b7969-131">当你将`Authorize`特性应用到中心类，指定的授权要求适用于所有中心中的方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="b7969-132">本主题提供您可以将应用的授权要求的不同类型的示例。</span><span class="sxs-lookup"><span data-stu-id="b7969-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="b7969-133">而无需`Authorize`特性，连接客户端可以访问集线器上的任何公共方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="b7969-134">如果已定义 web 应用程序中名为"Admin"的角色，则可以指定该角色中的唯一用户可以访问替换为以下代码的集线器。</span><span class="sxs-lookup"><span data-stu-id="b7969-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="b7969-135">或者，你可以指定一个中心包含可供所有用户的一个方法，并可仅供经过身份验证的用户，如下所示的第二个方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="b7969-136">下面的示例地址不同的授权方案：</span><span class="sxs-lookup"><span data-stu-id="b7969-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="b7969-137">`[Authorize]` – 仅身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="b7969-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="b7969-138">`[Authorize(Roles = "Admin,Manager")]` – 仅经过身份验证中的指定角色的用户</span><span class="sxs-lookup"><span data-stu-id="b7969-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="b7969-139">`[Authorize(Users = "user1,user2")]` – 仅经过身份验证与指定的用户名的用户</span><span class="sxs-lookup"><span data-stu-id="b7969-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="b7969-140">`[Authorize(RequireOutgoing=false)]` – 仅经过身份验证的用户可以调用中心，但从服务器返回到客户端的调用不受限制授权，例如，当仅某些用户可以发送一条消息，但所有其他人可以接收消息时。</span><span class="sxs-lookup"><span data-stu-id="b7969-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="b7969-141">RequireOutgoing 属性只能应用到整个中心，不能对中心内的个人方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="b7969-142">RequireOutgoing 未设置为 false，满足的授权要求的用户将调用从服务器中。</span><span class="sxs-lookup"><span data-stu-id="b7969-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="b7969-143">要求对所有中心身份验证</span><span class="sxs-lookup"><span data-stu-id="b7969-143">Require authentication for all hubs</span></span>

<span data-ttu-id="b7969-144">你可以要求身份验证的所有中心和中心方法在你的应用程序通过调用[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)应用程序启动时的方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="b7969-145">如果你有多个中心并想要为所有这些强制实施身份验证要求，可使用此方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="b7969-146">使用此方法，不能指定角色、 用户或传出的授权的要求。</span><span class="sxs-lookup"><span data-stu-id="b7969-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="b7969-147">你仅可以指定对中心方法的访问仅限于经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="b7969-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="b7969-148">但是，你仍可以应用 Authorize 属性为中心或方法，以指定其他要求。</span><span class="sxs-lookup"><span data-stu-id="b7969-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="b7969-149">在属性中指定的任何要求添加到身份验证的基本要求。</span><span class="sxs-lookup"><span data-stu-id="b7969-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="b7969-150">下面的示例演示的启动文件，后者限制给已经过身份验证的用户所有的中心方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="b7969-151">如果调用`RequireAuthentication()`方法处理 SignalR 请求后，会引发 SignalR`InvalidOperationException`异常。</span><span class="sxs-lookup"><span data-stu-id="b7969-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="b7969-152">SignalR 引发此异常，因为调用管道后，不能向非 HubPipeline 添加模块。</span><span class="sxs-lookup"><span data-stu-id="b7969-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="b7969-153">上面的示例演示调用`RequireAuthentication`中的方法`Configuration`会执行一次之前处理的第一个请求的方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="b7969-154">自定义的授权</span><span class="sxs-lookup"><span data-stu-id="b7969-154">Customized authorization</span></span>

<span data-ttu-id="b7969-155">如果你需要自定义如何确定授权，你可以创建一个派生自的类`AuthorizeAttribute`，并重写[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="b7969-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="b7969-156">对于每个请求，SignalR 调用此方法来确定用户是否有权完成请求。</span><span class="sxs-lookup"><span data-stu-id="b7969-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="b7969-157">在重写方法中，为你的授权方案提供必要的逻辑。</span><span class="sxs-lookup"><span data-stu-id="b7969-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="b7969-158">下面的示例演示如何强制实施通过基于声明的标识的授权。</span><span class="sxs-lookup"><span data-stu-id="b7969-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="b7969-159">将身份验证信息传递给客户端</span><span class="sxs-lookup"><span data-stu-id="b7969-159">Pass authentication information to clients</span></span>

<span data-ttu-id="b7969-160">你可能需要在客户端运行的代码中使用的身份验证信息。</span><span class="sxs-lookup"><span data-stu-id="b7969-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="b7969-161">客户端上调用方法时，你将传递所需的信息。</span><span class="sxs-lookup"><span data-stu-id="b7969-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="b7969-162">例如，聊天应用程序方法无法将作为参数传递的消息，同时发布的人员的用户名称如下所示。</span><span class="sxs-lookup"><span data-stu-id="b7969-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="b7969-163">或者，你可以创建要表示的身份验证信息并将该对象作为参数传递的对象，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b7969-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="b7969-164">根据恶意用户可以使用它来模拟来自该客户端的请求，应永远不会将一台客户端连接 id 传递给其他客户端。</span><span class="sxs-lookup"><span data-stu-id="b7969-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="b7969-165">用于.NET 客户端身份验证选项</span><span class="sxs-lookup"><span data-stu-id="b7969-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="b7969-166">当你有.NET 客户端，例如，控制台应用程序，与被限制为身份验证的用户的集线器交互时，您可以传递在 cookie、 连接标头或证书的身份验证凭据。</span><span class="sxs-lookup"><span data-stu-id="b7969-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="b7969-167">此部分中的示例演示如何使用这些不同的方法，以便进行用户身份验证。</span><span class="sxs-lookup"><span data-stu-id="b7969-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="b7969-168">它们不是功能完整的 SignalR 应用。</span><span class="sxs-lookup"><span data-stu-id="b7969-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="b7969-169">有关使用 SignalR 的.NET 客户端的详细信息，请参阅[中心 API 指南-.NET 客户端](../guide-to-the-api/hubs-api-guide-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="b7969-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="b7969-170">Cookie</span><span class="sxs-lookup"><span data-stu-id="b7969-170">Cookie</span></span>

<span data-ttu-id="b7969-171">当.NET 客户端与使用 ASP.NET 窗体身份验证的集线器交互时，你将需要手动对连接设置身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="b7969-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="b7969-172">添加到 cookie`CookieContainer`属性[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="b7969-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="b7969-173">下面的示例演示在网页上检索身份验证 cookie 并将该 cookie 添加到连接的控制台应用。</span><span class="sxs-lookup"><span data-stu-id="b7969-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="b7969-174">控制台应用程序发送到的凭据<strong>www.contoso.com/RemoteLogin</strong>其引用了包含下面的代码隐藏文件的空页。</span><span class="sxs-lookup"><span data-stu-id="b7969-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="b7969-175">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="b7969-175">Windows authentication</span></span>

<span data-ttu-id="b7969-176">当使用 Windows 身份验证，您可以通过传递当前用户的凭据[在](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="b7969-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="b7969-177">在的值设置为连接的凭据。</span><span class="sxs-lookup"><span data-stu-id="b7969-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="b7969-178">连接标头</span><span class="sxs-lookup"><span data-stu-id="b7969-178">Connection header</span></span>

<span data-ttu-id="b7969-179">如果你的应用程序不使用 cookie，你可以连接标头中传递用户信息。</span><span class="sxs-lookup"><span data-stu-id="b7969-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="b7969-180">例如，你可以连接标头中传递一个令牌。</span><span class="sxs-lookup"><span data-stu-id="b7969-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="b7969-181">然后，在中心，你将验证用户的令牌。</span><span class="sxs-lookup"><span data-stu-id="b7969-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="b7969-182">证书</span><span class="sxs-lookup"><span data-stu-id="b7969-182">Certificate</span></span>

<span data-ttu-id="b7969-183">你可以传递一个客户端证书来验证用户。</span><span class="sxs-lookup"><span data-stu-id="b7969-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="b7969-184">创建连接时添加证书。</span><span class="sxs-lookup"><span data-stu-id="b7969-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="b7969-185">下面的示例演示如何将客户端证书添加到连接;它不显示完整的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="b7969-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="b7969-186">它使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)提供多种不同的方式来创建证书的类。</span><span class="sxs-lookup"><span data-stu-id="b7969-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
