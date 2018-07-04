---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: 身份验证和 SignalR 永久性连接授权 (SignalR 1.x) |Microsoft Docs
author: pfletcher
description: 本主题介绍如何强制执行的持续性连接上的授权。 有关将安全集成到 SignalR 应用程序的常规信息...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/21/2013
ms.topic: article
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 471bce03a37a401c2afe3735afef6f838555cc26
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365105"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="987a0-104">身份验证和 SignalR 永久性连接授权 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="987a0-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>
====================
<span data-ttu-id="987a0-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="987a0-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="987a0-106">本主题介绍如何强制执行的持续性连接上的授权。</span><span class="sxs-lookup"><span data-stu-id="987a0-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="987a0-107">有关将安全集成到 SignalR 应用程序的常规信息，请参阅[安全性简介](index.md)。</span><span class="sxs-lookup"><span data-stu-id="987a0-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="987a0-108">强制执行授权</span><span class="sxs-lookup"><span data-stu-id="987a0-108">Enforce authorization</span></span>

<span data-ttu-id="987a0-109">若要使用时强制实施授权规则[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)必须重写`AuthorizeRequest`方法。</span><span class="sxs-lookup"><span data-stu-id="987a0-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="987a0-110">不能使用`Authorize`与持久连接的属性。</span><span class="sxs-lookup"><span data-stu-id="987a0-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="987a0-111">`AuthorizeRequest`之前验证用户有权执行请求的操作的每个请求的 SignalR Framework 调用方法。</span><span class="sxs-lookup"><span data-stu-id="987a0-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="987a0-112">`AuthorizeRequest`不会从客户端调用方法; 相反，验证用户身份通过应用程序的标准身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="987a0-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="987a0-113">下面的示例演示如何将请求限制为已经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="987a0-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="987a0-114">您可以添加任何自定义的授权逻辑中的 AuthorizeRequest 方法;例如，检查用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="987a0-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
