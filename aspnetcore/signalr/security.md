---
title: ASP.NET Core SignalR 中的安全注意事项
author: rachelappel
description: 了解如何在 ASP.NET Core SignalR 中使用身份验证和授权。
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/security
ms.openlocfilehash: eff4542b88f24dd6c1c0675f56874e368d441fdd
ms.sourcegitcommit: 32626efaa7316c9b283c96be6516e637d548c5e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2018
ms.locfileid: "39028479"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="fdc02-103">ASP.NET Core SignalR 中的安全注意事项</span><span class="sxs-lookup"><span data-stu-id="fdc02-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="fdc02-104">通过[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="fdc02-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

## <a name="overview"></a><span data-ttu-id="fdc02-105">概述</span><span class="sxs-lookup"><span data-stu-id="fdc02-105">Overview</span></span>

<span data-ttu-id="fdc02-106">默认情况下，SignalR 提供大量的安全保护。</span><span class="sxs-lookup"><span data-stu-id="fdc02-106">SignalR provides a number of security protections by default.</span></span> <span data-ttu-id="fdc02-107">若要了解如何配置这些保护至关重要。</span><span class="sxs-lookup"><span data-stu-id="fdc02-107">It's important to understand how to configure these protections.</span></span>

### <a name="cross-origin-resource-sharing"></a><span data-ttu-id="fdc02-108">跨域资源共享</span><span class="sxs-lookup"><span data-stu-id="fdc02-108">Cross-origin resource sharing</span></span>

<span data-ttu-id="fdc02-109">[跨域资源共享 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)可用于在浏览器中允许跨域 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="fdc02-109">[Cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="fdc02-110">如果您的 JavaScript 代码托管在从 SignalR 应用不同的域名，则必须启用[ASP.NET Core CORS 中间件](xref:security/cors)以便连接。</span><span class="sxs-lookup"><span data-stu-id="fdc02-110">If your JavaScript code is hosted on a different domain name from your SignalR app, you have to enable the [ASP.NET Core CORS middleware](xref:security/cors) in order to allow the connection.</span></span> <span data-ttu-id="fdc02-111">一般情况下，允许您控制的域中仅跨域请求。</span><span class="sxs-lookup"><span data-stu-id="fdc02-111">In general, allow cross-origin requests only from domains you control.</span></span> <span data-ttu-id="fdc02-112">例如，如果您的网站上托管`http://www.example.com`和 SignalR 应用上托管`http://signalr.example.com`，应为只允许原点在 SignalR 应用程序中配置 CORS `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="fdc02-112">For example, if your site is hosted on `http://www.example.com` and your SignalR app is hosted on `http://signalr.example.com`, you should configure CORS in your SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="fdc02-113">配置 CORS 的详细信息，请参阅[有关 ASP.NET Core CORS 文档](xref:security/cors)。</span><span class="sxs-lookup"><span data-stu-id="fdc02-113">For more information on configuring CORS, see [the documentation on ASP.NET Core CORS](xref:security/cors).</span></span> <span data-ttu-id="fdc02-114">SignalR 需要以下 CORS 策略才能正常运行：</span><span class="sxs-lookup"><span data-stu-id="fdc02-114">SignalR requires the following CORS policies in order to operate correctly:</span></span>

* <span data-ttu-id="fdc02-115">该策略必须允许特定源期望的或允许任何源 （不推荐）。</span><span class="sxs-lookup"><span data-stu-id="fdc02-115">The policy must allow the specific origins you expect, or allow any origin (not recommended).</span></span>
* <span data-ttu-id="fdc02-116">HTTP 方法`GET`和`POST`必须允许。</span><span class="sxs-lookup"><span data-stu-id="fdc02-116">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="fdc02-117">甚至在不使用身份验证时，必须启用凭据。</span><span class="sxs-lookup"><span data-stu-id="fdc02-117">Credentials must be enabled, even when you aren't using authentication.</span></span>

<span data-ttu-id="fdc02-118">例如，以下的 CORS 策略允许 SignalR 浏览器客户端上托管`http://example.com`访问 SignalR 应用：</span><span class="sxs-lookup"><span data-stu-id="fdc02-118">For example, the following CORS policy allows a SignalR browser client hosted on `http://example.com` to access your SignalR app:</span></span>

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
> <span data-ttu-id="fdc02-119">SignalR 是不与 Azure 应用服务中内置的 CORS 功能兼容。</span><span class="sxs-lookup"><span data-stu-id="fdc02-119">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

### <a name="access-token-logging"></a><span data-ttu-id="fdc02-120">访问令牌的日志记录</span><span class="sxs-lookup"><span data-stu-id="fdc02-120">Access token logging</span></span>

<span data-ttu-id="fdc02-121">使用 Websocket 或服务器发送事件时，浏览器客户端将查询字符串中发送的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fdc02-121">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="fdc02-122">这就象通常那样使用标准安全`Authorization`标头，但很多 web 服务器日志每个请求的 URL，包括查询字符串。</span><span class="sxs-lookup"><span data-stu-id="fdc02-122">This is generally as secure as using the standard `Authorization` header, however many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="fdc02-123">这意味着可能会在日志中包含访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fdc02-123">This means the access token may be included in logs.</span></span> <span data-ttu-id="fdc02-124">请考虑查看 web 服务器日志记录设置，以避免日志记录此信息。</span><span class="sxs-lookup"><span data-stu-id="fdc02-124">Consider reviewing the web server's logging settings to avoid logging this information.</span></span>

### <a name="exceptions"></a><span data-ttu-id="fdc02-125">异常</span><span class="sxs-lookup"><span data-stu-id="fdc02-125">Exceptions</span></span>

<span data-ttu-id="fdc02-126">异常消息通常被视为不应泄露给客户端的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="fdc02-126">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="fdc02-127">默认情况下，SignalR 不会发送到客户端集线器方法引发的异常的详细信息。</span><span class="sxs-lookup"><span data-stu-id="fdc02-127">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="fdc02-128">相反，客户端收到一条指示发生了错误的常规消息。</span><span class="sxs-lookup"><span data-stu-id="fdc02-128">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="fdc02-129">可以通过设置替代此行为[ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)设置。</span><span class="sxs-lookup"><span data-stu-id="fdc02-129">You can override this behavior by setting the [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options) setting.</span></span>

### <a name="buffer-management"></a><span data-ttu-id="fdc02-130">缓冲区管理</span><span class="sxs-lookup"><span data-stu-id="fdc02-130">Buffer management</span></span>

<span data-ttu-id="fdc02-131">SignalR 为了管理传入和传出消息使用每个连接缓冲区。</span><span class="sxs-lookup"><span data-stu-id="fdc02-131">SignalR uses per-connection buffers in order to manage incoming and outgoing messages.</span></span> <span data-ttu-id="fdc02-132">默认情况下，SignalR 限制为 32 KB 这些缓冲区。</span><span class="sxs-lookup"><span data-stu-id="fdc02-132">By default, SignalR limits these buffers to 32KB.</span></span> <span data-ttu-id="fdc02-133">这意味着客户端或服务器可以发送的最大可能消息为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="fdc02-133">This means the largest possible message a client or server can send is 32KB.</span></span> <span data-ttu-id="fdc02-134">这也意味着消息的连接所占用的内存的最长为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="fdc02-134">This also means the maximum amount of memory consumed by a connection for messages is 32KB.</span></span> <span data-ttu-id="fdc02-135">如果您知道您的消息始终是小于此限制，可以减少此大小以防止客户端发送大消息并强制服务器分配的内存来接受它。</span><span class="sxs-lookup"><span data-stu-id="fdc02-135">If you know your messages are always smaller than this limit, you can reduce this size to prevent a client from being able to send a larger message and force the server to allocate memory to accept it.</span></span> <span data-ttu-id="fdc02-136">同样，如果您知道您的消息大小超过此限制，则可以增加它。</span><span class="sxs-lookup"><span data-stu-id="fdc02-136">Similarly, if you know your messages are larger than this limit, you can increase it.</span></span> <span data-ttu-id="fdc02-137">但是，请注意，增加此限制意味着客户端能够导致服务器分配更多内存，并可能会降低您的应用程序可以处理的并发连接数。</span><span class="sxs-lookup"><span data-stu-id="fdc02-137">However, be aware that increasing this limit means that the client is able to cause the server to allocate additional memory and may reduce the number of concurrent connections your app can handle.</span></span>

<span data-ttu-id="fdc02-138">对于传入和传出消息的单独限制，两者均可在配置[ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options)对象中配置`MapHub`:</span><span class="sxs-lookup"><span data-stu-id="fdc02-138">There are separate limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="fdc02-139">`ApplicationMaxBufferSize` 表示最大字节数从客户端的服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="fdc02-139">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="fdc02-140">如果客户端尝试发送一条消息大小超过此限制，可能会关闭连接。</span><span class="sxs-lookup"><span data-stu-id="fdc02-140">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="fdc02-141">`TransportMaxBufferSize` 表示最大服务器都可以发送的字节数。</span><span class="sxs-lookup"><span data-stu-id="fdc02-141">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="fdc02-142">如果服务器尝试发送一条消息 （包括来自集线器方法的返回值） 大于此限制，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="fdc02-142">If the server attempts to send a message (includes return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="fdc02-143">将限制设置为`0`完全禁用了限制。</span><span class="sxs-lookup"><span data-stu-id="fdc02-143">Setting the limit to `0` disables the limit entirely.</span></span> <span data-ttu-id="fdc02-144">但是，这应完成时要特别注意。</span><span class="sxs-lookup"><span data-stu-id="fdc02-144">However, this should be done with extreme caution.</span></span> <span data-ttu-id="fdc02-145">删除限制允许客户端发送任意大小的消息。</span><span class="sxs-lookup"><span data-stu-id="fdc02-145">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="fdc02-146">这可通过恶意客户端会导致过多内存，并将其分配，这样可以显著减少您的应用程序可以支持的并发连接数。</span><span class="sxs-lookup"><span data-stu-id="fdc02-146">This could be used by a malicious client to cause excess memory to be allocated, which could dramatically reduce the number of concurrent connections your app can support.</span></span>
