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
<a name="authentication-and-authorization-for-signalr-persistent-connections"></a>身份验证和授权 SignalR 永久性连接
====================
通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

> 本主题介绍如何强制执行的持续性连接上的授权。 有关将安全集成到 SignalR 应用程序的常规信息，请参阅[安全性简介](introduction-to-security.md)。 
> 
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 版本 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
> 
> 有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>问题和提出的意见
> 
> 请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。


## <a name="enforce-authorization"></a>强制执行授权

若要使用时强制实施授权规则[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)必须重写`AuthorizeRequest`方法。 不能使用`Authorize`与持久连接的属性。 `AuthorizeRequest`之前验证用户有权执行请求的操作的每个请求的 SignalR Framework 调用方法。 `AuthorizeRequest`不会从客户端调用方法; 相反，验证用户身份通过应用程序的标准身份验证机制。

下面的示例演示如何将请求限制为已经过身份验证的用户。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

您可以添加任何自定义的授权逻辑中的 AuthorizeRequest 方法;例如，检查用户是否属于特定角色。
