---
uid: signalr/overview/security/persistent-connection-authorization
title: 身份验证和授权 SignalR 永久性连接 |Microsoft Docs
author: pfletcher
description: 本主题介绍如何强制执行的持续性连接上的授权。 有关将安全集成到 SignalR 应用程序的常规信息...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: e7ae160cbe4c5f6cdb393768758f5bdec4203dbf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830665"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="95276-104">身份验证和授权 SignalR 永久性连接</span><span class="sxs-lookup"><span data-stu-id="95276-104">Authentication and Authorization for SignalR Persistent Connections</span></span>
====================
<span data-ttu-id="95276-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="95276-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="95276-106">本主题介绍如何强制执行的持续性连接上的授权。</span><span class="sxs-lookup"><span data-stu-id="95276-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="95276-107">有关将安全集成到 SignalR 应用程序的常规信息，请参阅[安全性简介](introduction-to-security.md)。</span><span class="sxs-lookup"><span data-stu-id="95276-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="95276-108">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="95276-108">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="95276-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="95276-109">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="95276-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="95276-110">.NET 4.5</span></span>
> - <span data-ttu-id="95276-111">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="95276-111">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="95276-112">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="95276-112">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="95276-113">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="95276-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="95276-114">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="95276-114">Questions and comments</span></span>
> 
> <span data-ttu-id="95276-115">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="95276-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="95276-116">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="95276-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="95276-117">强制执行授权</span><span class="sxs-lookup"><span data-stu-id="95276-117">Enforce authorization</span></span>

<span data-ttu-id="95276-118">若要使用时强制实施授权规则[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)必须重写`AuthorizeRequest`方法。</span><span class="sxs-lookup"><span data-stu-id="95276-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="95276-119">不能使用`Authorize`与持久连接的属性。</span><span class="sxs-lookup"><span data-stu-id="95276-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="95276-120">`AuthorizeRequest`之前验证用户有权执行请求的操作的每个请求的 SignalR Framework 调用方法。</span><span class="sxs-lookup"><span data-stu-id="95276-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="95276-121">`AuthorizeRequest`不会从客户端调用方法; 相反，验证用户身份通过应用程序的标准身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="95276-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="95276-122">下面的示例演示如何将请求限制为已经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="95276-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="95276-123">您可以添加任何自定义的授权逻辑中的 AuthorizeRequest 方法;例如，检查用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="95276-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
