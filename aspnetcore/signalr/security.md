---
title: ASP.NET Core SignalR 中的安全注意事项
author: tdykstra
description: 了解如何在 ASP.NET Core SignalR 中使用身份验证和授权。
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 10/17/2018
uid: signalr/security
ms.openlocfilehash: be1dd24c40327d9a0d8f91bf75300128d3d52725
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225364"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="0a38c-103">ASP.NET Core SignalR 中的安全注意事项</span><span class="sxs-lookup"><span data-stu-id="0a38c-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="0a38c-104">通过[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="0a38c-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="0a38c-105">本文提供有关保护 SignalR 的信息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-105">This article provides information on securing SignalR.</span></span>

## <a name="cross-origin-resource-sharing"></a><span data-ttu-id="0a38c-106">跨域资源共享</span><span class="sxs-lookup"><span data-stu-id="0a38c-106">Cross-origin resource sharing</span></span>

<span data-ttu-id="0a38c-107">[跨域资源共享 (CORS)](https://www.w3.org/TR/cors/)可用于在浏览器中允许跨域 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="0a38c-107">[Cross-origin resource sharing (CORS)](https://www.w3.org/TR/cors/) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="0a38c-108">如果在不同的域从 SignalR 应用程序中托管的 JavaScript 代码[CORS 中间件](xref:security/cors)必须启用才能允许 JavaScript 才能连接到 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a38c-108">If JavaScript code is hosted on a different domain from the SignalR app, [CORS middleware](xref:security/cors) must be enabled to allow the JavaScript to connect to the SignalR app.</span></span> <span data-ttu-id="0a38c-109">允许仅从您信任的域或控件的跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0a38c-109">Allow cross-origin requests only from domains you trust or control.</span></span> <span data-ttu-id="0a38c-110">例如：</span><span class="sxs-lookup"><span data-stu-id="0a38c-110">For example:</span></span>

* <span data-ttu-id="0a38c-111">上托管你的站点 `http://www.example.com`</span><span class="sxs-lookup"><span data-stu-id="0a38c-111">Your site is hosted on `http://www.example.com`</span></span>
* <span data-ttu-id="0a38c-112">上托管您的 SignalR 应用程序 `http://signalr.example.com`</span><span class="sxs-lookup"><span data-stu-id="0a38c-112">Your SignalR app is hosted on `http://signalr.example.com`</span></span>

<span data-ttu-id="0a38c-113">应为只允许原点的 SignalR 应用中配置 CORS `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="0a38c-113">CORS should be configured in the SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="0a38c-114">配置 CORS 的详细信息，请参阅[启用跨域请求 (CORS)](xref:security/cors)。</span><span class="sxs-lookup"><span data-stu-id="0a38c-114">For more information on configuring CORS, see [Enable Cross-Origin Requests (CORS)](xref:security/cors).</span></span> <span data-ttu-id="0a38c-115">SignalR**需要**以下 CORS 策略：</span><span class="sxs-lookup"><span data-stu-id="0a38c-115">SignalR **requires** the following CORS policies:</span></span>

* <span data-ttu-id="0a38c-116">允许特定的预期的来源。</span><span class="sxs-lookup"><span data-stu-id="0a38c-116">Allow the specific expected origins.</span></span> <span data-ttu-id="0a38c-117">允许任何源，但**不**安全或建议。</span><span class="sxs-lookup"><span data-stu-id="0a38c-117">Allowing any origin is possible but is **not** secure or recommended.</span></span>
* <span data-ttu-id="0a38c-118">HTTP 方法`GET`和`POST`必须允许。</span><span class="sxs-lookup"><span data-stu-id="0a38c-118">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="0a38c-119">必须启用凭据，即使不使用身份验证。</span><span class="sxs-lookup"><span data-stu-id="0a38c-119">Credentials must be enabled, even when authentication is not used.</span></span>

<span data-ttu-id="0a38c-120">例如，以下的 CORS 策略允许 SignalR 浏览器客户端上托管`http://example.com`访问上托管的 SignalR 应用`http://signalr.example.com`:</span><span class="sxs-lookup"><span data-stu-id="0a38c-120">For example, the following CORS policy allows a SignalR browser client hosted on `http://example.com` to access the SignalR app hosted on `http://signalr.example.com`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="0a38c-121">SignalR 是不与 Azure 应用服务中内置的 CORS 功能兼容。</span><span class="sxs-lookup"><span data-stu-id="0a38c-121">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

## <a name="websocket-origin-restriction"></a><span data-ttu-id="0a38c-122">WebSocket 源限制</span><span class="sxs-lookup"><span data-stu-id="0a38c-122">WebSocket Origin Restriction</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="0a38c-123">CORS 提供的保护功能不会应用到 Websocket。</span><span class="sxs-lookup"><span data-stu-id="0a38c-123">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="0a38c-124">有关源限制对 Websocket，请阅读[Websocket 原点限制](xref:fundamentals/websockets#websocket-origin-restriction)。</span><span class="sxs-lookup"><span data-stu-id="0a38c-124">For origin restriction on WebSockets, read [WebSockets origin restriction](xref:fundamentals/websockets#websocket-origin-restriction).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="0a38c-125">CORS 提供的保护功能不会应用到 Websocket。</span><span class="sxs-lookup"><span data-stu-id="0a38c-125">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="0a38c-126">浏览器执行操作**不**:</span><span class="sxs-lookup"><span data-stu-id="0a38c-126">Browsers do **not**:</span></span>

* <span data-ttu-id="0a38c-127">执行 CORS 预检请求。</span><span class="sxs-lookup"><span data-stu-id="0a38c-127">Perform CORS pre-flight requests.</span></span>
* <span data-ttu-id="0a38c-128">遵循中指定的限制`Access-Control`标头时发出 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="0a38c-128">Respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span>

<span data-ttu-id="0a38c-129">但是，浏览器是否将发送`Origin`标头时发出 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="0a38c-129">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="0a38c-130">应用程序应配置为验证这些标头，以确保允许仅来自预期的来源的 Websocket。</span><span class="sxs-lookup"><span data-stu-id="0a38c-130">Applications should be configured to validate these headers to ensure that only WebSockets coming from the expected origins are allowed.</span></span>

<span data-ttu-id="0a38c-131">ASP.NET Core 2.1 及更高版本，可以使用放置自定义中间件实现标头验证**之前`UseSignalR`，和身份验证中间件**中`Configure`:</span><span class="sxs-lookup"><span data-stu-id="0a38c-131">In ASP.NET Core 2.1 and later, header validation can be achieved using a custom middleware placed **before `UseSignalR`, and authentication middleware** in `Configure`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet2)]

> [!NOTE]
> <span data-ttu-id="0a38c-132">`Origin`标头控制客户端和其他如`Referer`标头，可能伪造的。</span><span class="sxs-lookup"><span data-stu-id="0a38c-132">The `Origin` header is controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="0a38c-133">这些标头应**不**用作身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="0a38c-133">These headers should **not** be used as an authentication mechanism.</span></span>

::: moniker-end

## <a name="access-token-logging"></a><span data-ttu-id="0a38c-134">访问令牌的日志记录</span><span class="sxs-lookup"><span data-stu-id="0a38c-134">Access token logging</span></span>

<span data-ttu-id="0a38c-135">使用 Websocket 或服务器发送事件时，浏览器客户端将查询字符串中发送的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="0a38c-135">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="0a38c-136">接收访问令牌通过查询字符串就象通常那样使用标准安全`Authorization`标头。</span><span class="sxs-lookup"><span data-stu-id="0a38c-136">Receiving the access token via query string is generally as secure as using the standard `Authorization` header.</span></span> <span data-ttu-id="0a38c-137">但是，许多 web 服务器记录每个请求，包括查询字符串的 URL。</span><span class="sxs-lookup"><span data-stu-id="0a38c-137">However, many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="0a38c-138">日志记录 Url 可能记录的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="0a38c-138">Logging the URLs may log the access token.</span></span> <span data-ttu-id="0a38c-139">最佳做法是设置 web 服务器的日志记录设置，以防止日志记录的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="0a38c-139">A best practice is to set the web server's logging settings to prevent logging access tokens.</span></span>

## <a name="exceptions"></a><span data-ttu-id="0a38c-140">异常</span><span class="sxs-lookup"><span data-stu-id="0a38c-140">Exceptions</span></span>

<span data-ttu-id="0a38c-141">异常消息通常被视为不应泄露给客户端的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="0a38c-141">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="0a38c-142">默认情况下，SignalR 不会发送到客户端集线器方法引发的异常的详细信息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-142">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="0a38c-143">相反，客户端收到一条指示发生了错误的常规消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-143">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="0a38c-144">异常消息传递到客户端可以重写 （例如在开发或测试） 使用[ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)。</span><span class="sxs-lookup"><span data-stu-id="0a38c-144">Exception message delivery to the client can be overridden (for example in development or test) with [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options).</span></span> <span data-ttu-id="0a38c-145">不应在生产应用中的客户端公开异常消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-145">Exception messages should not be exposed to the client in production apps.</span></span>

## <a name="buffer-management"></a><span data-ttu-id="0a38c-146">缓冲区管理</span><span class="sxs-lookup"><span data-stu-id="0a38c-146">Buffer management</span></span>

<span data-ttu-id="0a38c-147">SignalR 使用每个连接缓冲区来管理传入和传出消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-147">SignalR uses per-connection buffers to manage incoming and outgoing messages.</span></span> <span data-ttu-id="0a38c-148">默认情况下，SignalR 限制为 32 KB 这些缓冲区。</span><span class="sxs-lookup"><span data-stu-id="0a38c-148">By default, SignalR limits these buffers to 32 KB.</span></span> <span data-ttu-id="0a38c-149">客户端或服务器可以发送的最大消息为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="0a38c-149">The largest message a client or server can send is 32 KB.</span></span> <span data-ttu-id="0a38c-150">消息的连接所占用的最大内存为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="0a38c-150">The maximum memory consumed by a connection for messages is 32 KB.</span></span> <span data-ttu-id="0a38c-151">如果你的消息始终小于 32 KB，可以减少了限制，其中：</span><span class="sxs-lookup"><span data-stu-id="0a38c-151">If your messages are always smaller than 32 KB, you can reduce the limit, which:</span></span>

* <span data-ttu-id="0a38c-152">防止客户端发送大消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-152">Prevents a client from being able to send a larger message.</span></span>
* <span data-ttu-id="0a38c-153">服务器永远不需要分配大型缓冲区接受的消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-153">The server will never need to allocate large buffers to accept messages.</span></span>

<span data-ttu-id="0a38c-154">如果你的消息大小大于 32 KB，则可以增加限制。</span><span class="sxs-lookup"><span data-stu-id="0a38c-154">If your messages are larger than 32 KB, you can increase the limit.</span></span> <span data-ttu-id="0a38c-155">增加此限制意味着：</span><span class="sxs-lookup"><span data-stu-id="0a38c-155">Increasing this limit means:</span></span>

* <span data-ttu-id="0a38c-156">客户端可能导致服务器分配较大内存缓冲区。</span><span class="sxs-lookup"><span data-stu-id="0a38c-156">The client can cause the server to allocate large memory buffers.</span></span>
* <span data-ttu-id="0a38c-157">大型缓冲区的服务器分配可能会降低并发连接数。</span><span class="sxs-lookup"><span data-stu-id="0a38c-157">Server allocation of large buffers may reduce the number of concurrent connections.</span></span>

<span data-ttu-id="0a38c-158">限制传入和传出消息，同时可以根据[ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options)对象中配置`MapHub`:</span><span class="sxs-lookup"><span data-stu-id="0a38c-158">There are limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="0a38c-159">`ApplicationMaxBufferSize` 表示最大字节数从客户端的服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="0a38c-159">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="0a38c-160">如果客户端尝试发送一条消息大小超过此限制，可能会关闭连接。</span><span class="sxs-lookup"><span data-stu-id="0a38c-160">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="0a38c-161">`TransportMaxBufferSize` 表示最大服务器都可以发送的字节数。</span><span class="sxs-lookup"><span data-stu-id="0a38c-161">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="0a38c-162">如果服务器尝试发送一条消息 （包括从中心的方法返回的值） 大于此限制，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="0a38c-162">If the server attempts to send a message (including return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="0a38c-163">将限制设置为`0`禁用限制。</span><span class="sxs-lookup"><span data-stu-id="0a38c-163">Setting the limit to `0` disables the limit.</span></span> <span data-ttu-id="0a38c-164">删除限制允许客户端发送任意大小的消息。</span><span class="sxs-lookup"><span data-stu-id="0a38c-164">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="0a38c-165">恶意客户端发送大消息可能会导致过多内存，并将其分配。</span><span class="sxs-lookup"><span data-stu-id="0a38c-165">Malicious clients sending large messages can cause excess memory to be allocated.</span></span> <span data-ttu-id="0a38c-166">过多内存使用情况可以显著减少并发连接数。</span><span class="sxs-lookup"><span data-stu-id="0a38c-166">Excess memory usage can significantly reduce the number of concurrent connections.</span></span>
