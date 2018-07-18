---
title: ASP.NET Core SignalR 中的安全注意事项
author: tdykstra
description: 了解如何在 ASP.NET Core SignalR 中使用身份验证和授权。
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/security
ms.openlocfilehash: b66c7fbfbaee4c70a68f3132875fbc81018c3e20
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095127"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a>ASP.NET Core SignalR 中的安全注意事项

通过[Andrew Stanton-nurse](https://twitter.com/anurse)

## <a name="overview"></a>概述

默认情况下，SignalR 提供大量的安全保护。 若要了解如何配置这些保护至关重要。

### <a name="cross-origin-resource-sharing"></a>跨域资源共享

[跨域资源共享 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)可用于在浏览器中允许跨域 SignalR 连接。 如果您的 JavaScript 代码托管在从 SignalR 应用不同的域名，则必须启用[ASP.NET Core CORS 中间件](xref:security/cors)以便连接。 一般情况下，允许您控制的域中仅跨域请求。 例如，如果您的网站上托管 `http://www.example.com` 和 SignalR 应用上托管 `http://signalr.example.com`，应为只允许原点在 SignalR 应用程序中配置 CORS `www.example.com`。

配置 CORS 的详细信息，请参阅[有关 ASP.NET Core CORS 文档](xref:security/cors)。 SignalR 需要以下 CORS 策略才能正常运行：

* 该策略必须允许特定源期望的或允许任何源 （不推荐）。
* HTTP 方法`GET`和`POST`必须允许。
* 甚至在不使用身份验证时，必须启用凭据。

例如，以下的 CORS 策略允许 SignalR 浏览器客户端上托管 `http://example.com` 访问 SignalR 应用：

```csharp
public void Configure(IApplicationBuilder app)
{
    // ... other middleware ...

    // Make sure the CORS middleware is ahead of SignalR.
    app.UseCors(builder => {
        builder.WithOrigins("http://example.com")
            .AllowAnyHeader()
            .WithMethods("GET", "POST")
            .AllowCredentials();
    });

    // ... other middleware ...

    app.UseSignalR();

    // ... other middleware ...
}
```

> [!NOTE]
> SignalR 是不与 Azure 应用服务中内置的 CORS 功能兼容。

### <a name="access-token-logging"></a>访问令牌的日志记录

使用 Websocket 或服务器发送事件时，浏览器客户端将查询字符串中发送的访问令牌。 这就象通常那样使用标准安全`Authorization`标头，但很多 web 服务器日志每个请求的 URL，包括查询字符串。 这意味着可能会在日志中包含访问令牌。 请考虑查看 web 服务器日志记录设置，以避免日志记录此信息。

### <a name="exceptions"></a>异常

异常消息通常被视为不应泄露给客户端的敏感数据。 默认情况下，SignalR 不会发送到客户端集线器方法引发的异常的详细信息。 相反，客户端收到一条指示发生了错误的常规消息。 可以通过设置替代此行为[ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)设置。

### <a name="buffer-management"></a>缓冲区管理

SignalR 为了管理传入和传出消息使用每个连接缓冲区。 默认情况下，SignalR 限制为 32 KB 这些缓冲区。 这意味着客户端或服务器可以发送的最大可能消息为 32 KB。 这也意味着消息的连接所占用的内存的最长为 32 KB。 如果您知道您的消息始终是小于此限制，可以减少此大小以防止客户端发送大消息并强制服务器分配的内存来接受它。 同样，如果您知道您的消息大小超过此限制，则可以增加它。 但是，请注意，增加此限制意味着客户端能够导致服务器分配更多内存，并可能会降低您的应用程序可以处理的并发连接数。

对于传入和传出消息的单独限制，两者均可在配置[ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options)对象中配置`MapHub`:

* `ApplicationMaxBufferSize` 表示最大字节数从客户端的服务器缓冲区。 如果客户端尝试发送一条消息大小超过此限制，可能会关闭连接。
* `TransportMaxBufferSize` 表示最大服务器都可以发送的字节数。 如果服务器尝试发送一条消息 （包括来自集线器方法的返回值） 大于此限制，将引发异常。

将限制设置为`0`完全禁用了限制。 但是，这应完成时要特别注意。 删除限制允许客户端发送任意大小的消息。 这可通过恶意客户端会导致过多内存，并将其分配，这样可以显著减少您的应用程序可以支持的并发连接数。
