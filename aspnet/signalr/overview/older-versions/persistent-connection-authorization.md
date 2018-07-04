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
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>身份验证和 SignalR 永久性连接授权 (SignalR 1.x)
====================
通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

> 本主题介绍如何强制执行的持续性连接上的授权。 有关将安全集成到 SignalR 应用程序的常规信息，请参阅[安全性简介](index.md)。


## <a name="enforce-authorization"></a>强制执行授权

若要使用时强制实施授权规则[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)必须重写`AuthorizeRequest`方法。 不能使用`Authorize`与持久连接的属性。 `AuthorizeRequest`之前验证用户有权执行请求的操作的每个请求的 SignalR Framework 调用方法。 `AuthorizeRequest`不会从客户端调用方法; 相反，验证用户身份通过应用程序的标准身份验证机制。

下面的示例演示如何将请求限制为已经过身份验证的用户。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

您可以添加任何自定义的授权逻辑中的 AuthorizeRequest 方法;例如，检查用户是否属于特定角色。
