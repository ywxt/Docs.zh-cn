---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: "身份验证和授权的 SignalR 永久性连接 (SignalR 1.x) |Microsoft 文档"
author: pfletcher
description: "本主题介绍如何强制在持续性连接上的进行授权。 有关将安全集成到 SignalR 应用程序的常规信息..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/21/2013
ms.topic: article
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 2e97dfd03c61b110325c41a992b4af490fcd17de
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="da6dc-104">身份验证和授权的 SignalR 永久性连接 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="da6dc-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>
====================
<span data-ttu-id="da6dc-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="da6dc-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="da6dc-106">本主题介绍如何强制在持续性连接上的进行授权。</span><span class="sxs-lookup"><span data-stu-id="da6dc-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="da6dc-107">有关将安全集成到 SignalR 应用程序的常规信息，请参阅[安全性简介](index.md)。</span><span class="sxs-lookup"><span data-stu-id="da6dc-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="da6dc-108">强制授权</span><span class="sxs-lookup"><span data-stu-id="da6dc-108">Enforce authorization</span></span>

<span data-ttu-id="da6dc-109">若要强制实施授权规则，当使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)必须重写`AuthorizeRequest`方法。</span><span class="sxs-lookup"><span data-stu-id="da6dc-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="da6dc-110">不能使用`Authorize`具有永久连接属性。</span><span class="sxs-lookup"><span data-stu-id="da6dc-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="da6dc-111">`AuthorizeRequest`方法由每个请求，以验证用户有权执行所请求的操作之前的 SignalR Framework 调用。</span><span class="sxs-lookup"><span data-stu-id="da6dc-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="da6dc-112">`AuthorizeRequest`方法不从客户端调用; 相反，验证用户身份通过应用程序的标准身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="da6dc-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="da6dc-113">下面的示例演示如何限制请求发送到经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="da6dc-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="da6dc-114">你可以在 AuthorizeRequest 方法中; 中添加任何自定义的授权逻辑例如，检查用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="da6dc-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
