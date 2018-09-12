---
title: 在 ASP.NET Core SignalR 使用中心
author: tdykstra
description: 了解如何在 ASP.NET Core SignalR 中使用中心。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/01/2018
uid: signalr/hubs
ms.openlocfilehash: e583676ab0eed45aeaf6391d8cdf8c1485aa914e
ms.sourcegitcommit: e7e1e531b80b3f4117ff119caadbebf4dcf5dcb7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "44510332"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="e2c49-103">ASP.NET Core 使用 SignalR 中的中心</span><span class="sxs-lookup"><span data-stu-id="e2c49-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="e2c49-104">通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin Griffin](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="e2c49-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

<span data-ttu-id="e2c49-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="e2c49-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="e2c49-106">SignalR 中心是什么</span><span class="sxs-lookup"><span data-stu-id="e2c49-106">What is a SignalR hub</span></span>

<span data-ttu-id="e2c49-107">SignalR 中心 API，可从服务器在连接的客户端上调用方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-107">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="e2c49-108">在服务器代码中，定义客户端调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-108">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="e2c49-109">在客户端代码中，定义从服务器调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-109">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="e2c49-110">SignalR 负责在后台实现实时的客户端到服务器和服务器到客户端通信的所有内容。</span><span class="sxs-lookup"><span data-stu-id="e2c49-110">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="e2c49-111">配置 SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="e2c49-111">Configure SignalR hubs</span></span>

<span data-ttu-id="e2c49-112">SignalR 中间件需要某些服务，通过调用配置`services.AddSignalR`。</span><span class="sxs-lookup"><span data-stu-id="e2c49-112">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

<span data-ttu-id="e2c49-113">在 SignalR 功能添加到 ASP.NET Core 应用程序时，通过调用设置 SignalR 路由`app.UseSignalR`中`Startup.Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-113">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="e2c49-114">创建和使用中心</span><span class="sxs-lookup"><span data-stu-id="e2c49-114">Create and use hubs</span></span>

<span data-ttu-id="e2c49-115">通过声明继承的类创建一个中心`Hub`，并向其添加公共方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-115">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="e2c49-116">客户端可以调用方法定义为`public`。</span><span class="sxs-lookup"><span data-stu-id="e2c49-116">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

<span data-ttu-id="e2c49-117">您可以指定返回类型和参数，包括复杂类型和数组，就像在任何 C# 方法中。</span><span class="sxs-lookup"><span data-stu-id="e2c49-117">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="e2c49-118">SignalR 处理序列化和反序列化复杂对象和数组中参数和返回值。</span><span class="sxs-lookup"><span data-stu-id="e2c49-118">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

## <a name="the-context-object"></a><span data-ttu-id="e2c49-119">上下文对象</span><span class="sxs-lookup"><span data-stu-id="e2c49-119">The Context object</span></span>

<span data-ttu-id="e2c49-120">`Hub`类具有`Context`属性，其中包含以下属性与连接有关的信息：</span><span class="sxs-lookup"><span data-stu-id="e2c49-120">The `Hub` class has a `Context` property that contains the following properties with information about the connection:</span></span>

| <span data-ttu-id="e2c49-121">属性</span><span class="sxs-lookup"><span data-stu-id="e2c49-121">Property</span></span> | <span data-ttu-id="e2c49-122">描述</span><span class="sxs-lookup"><span data-stu-id="e2c49-122">Description</span></span> |
| ------ | ----------- |
| `ConnectionId` | <span data-ttu-id="e2c49-123">获取用于此连接，由 SignalR 分配的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="e2c49-123">Gets the unique ID for the connection, assigned by SignalR.</span></span> <span data-ttu-id="e2c49-124">没有为每个连接的一个连接 ID。</span><span class="sxs-lookup"><span data-stu-id="e2c49-124">There is one connection ID for each connection.</span></span>|
| `UserIdentifier` | <span data-ttu-id="e2c49-125">获取[用户标识符](xref:signalr/groups)。</span><span class="sxs-lookup"><span data-stu-id="e2c49-125">Gets the [user identifier](xref:signalr/groups).</span></span> <span data-ttu-id="e2c49-126">默认情况下，使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符连接相关联。</span><span class="sxs-lookup"><span data-stu-id="e2c49-126">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> |
| `User` | <span data-ttu-id="e2c49-127">获取`ClaimsPrincipal`与当前用户相关联。</span><span class="sxs-lookup"><span data-stu-id="e2c49-127">Gets the `ClaimsPrincipal` associated with the current user.</span></span> |
| `Items` | <span data-ttu-id="e2c49-128">获取可用于共享此连接的作用域内的数据的键/值集合。</span><span class="sxs-lookup"><span data-stu-id="e2c49-128">Gets a key/value collection that can be used to share data within the scope of this connection.</span></span> <span data-ttu-id="e2c49-129">数据可以存储在此集合中，它将连接在不同的集线器方法调用中保持原样。</span><span class="sxs-lookup"><span data-stu-id="e2c49-129">Data can be stored in this collection and it will persist for the connection across different hub method invocations.</span></span> |
| `Features` | <span data-ttu-id="e2c49-130">获取在连接上的可用功能的集合。</span><span class="sxs-lookup"><span data-stu-id="e2c49-130">Gets the collection of features available on the connection.</span></span> <span data-ttu-id="e2c49-131">现在，此集合不需要在大多数情况下，因此它不尚未记录在详细信息。</span><span class="sxs-lookup"><span data-stu-id="e2c49-131">For now, this collection isn't needed in most scenarios, so it isn't documented in detail yet.</span></span> |
| `ConnectionAborted` | <span data-ttu-id="e2c49-132">获取`CancellationToken`，时连接中止通知。</span><span class="sxs-lookup"><span data-stu-id="e2c49-132">Gets a `CancellationToken` that notifies when the connection is aborted.</span></span> |

<span data-ttu-id="e2c49-133">`Hub.Context` 此外包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="e2c49-133">`Hub.Context` also contains the following methods:</span></span>

| <span data-ttu-id="e2c49-134">方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-134">Method</span></span> | <span data-ttu-id="e2c49-135">描述</span><span class="sxs-lookup"><span data-stu-id="e2c49-135">Description</span></span> |
| ------ | ----------- |
| `GetHttpContext` | <span data-ttu-id="e2c49-136">返回`HttpContext`用于此连接，或`null`如果连接不是与 HTTP 请求相关联。</span><span class="sxs-lookup"><span data-stu-id="e2c49-136">Returns the `HttpContext` for the connection, or `null` if the connection is not associated with an HTTP request.</span></span> <span data-ttu-id="e2c49-137">对于 HTTP 连接，可以使用此方法以获取 HTTP 标头和查询字符串等信息。</span><span class="sxs-lookup"><span data-stu-id="e2c49-137">For HTTP connections, you can use this method to get information such as HTTP headers and query strings.</span></span> |
| `Abort` | <span data-ttu-id="e2c49-138">中止的连接。</span><span class="sxs-lookup"><span data-stu-id="e2c49-138">Aborts the connection.</span></span> |

## <a name="the-clients-object"></a><span data-ttu-id="e2c49-139">客户端对象</span><span class="sxs-lookup"><span data-stu-id="e2c49-139">The Clients object</span></span>

<span data-ttu-id="e2c49-140">`Hub`类具有`Clients`属性，其中包含服务器和客户端之间通信的以下属性：</span><span class="sxs-lookup"><span data-stu-id="e2c49-140">The `Hub` class has a `Clients` property that contains the following properties for communication between server and client:</span></span>

| <span data-ttu-id="e2c49-141">属性</span><span class="sxs-lookup"><span data-stu-id="e2c49-141">Property</span></span> | <span data-ttu-id="e2c49-142">描述</span><span class="sxs-lookup"><span data-stu-id="e2c49-142">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="e2c49-143">在所有连接的客户端上调用的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-143">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="e2c49-144">在客户端调用集线器方法调用的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-144">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="e2c49-145">除调用该方法的客户端的所有已连接客户端上调用的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-145">Calls a method on all connected clients except the client that invoked the method</span></span> |


<span data-ttu-id="e2c49-146">`Hub.Clients` 此外包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="e2c49-146">`Hub.Clients` also contains the following methods:</span></span>

| <span data-ttu-id="e2c49-147">方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-147">Method</span></span> | <span data-ttu-id="e2c49-148">描述</span><span class="sxs-lookup"><span data-stu-id="e2c49-148">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="e2c49-149">除了指定连接的所有已连接客户端上调用的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-149">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="e2c49-150">调用特定连接的客户端上的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-150">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="e2c49-151">调用特定连接的客户端上的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-151">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="e2c49-152">调用指定的组中的所有连接到的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-152">Calls a method to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="e2c49-153">调用中指定的组，除非指定连接到的所有连接的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-153">Calls a method to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="e2c49-154">调用到多个组的连接方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-154">Calls a method to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="e2c49-155">调用到一组连接，不包括客户端调用集线器方法的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-155">Calls a method to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="e2c49-156">调用与特定用户关联的所有连接到的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-156">Calls a method to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="e2c49-157">调用到与指定的用户相关联的所有连接的方法</span><span class="sxs-lookup"><span data-stu-id="e2c49-157">Calls a method to all connections associated with the specified users</span></span> |

<span data-ttu-id="e2c49-158">每个属性或方法上表中的返回一个包含对象`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-158">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="e2c49-159">`SendAsync`方法允许您提供的名称和要调用的客户端方法的参数。</span><span class="sxs-lookup"><span data-stu-id="e2c49-159">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="e2c49-160">将消息发送到客户端</span><span class="sxs-lookup"><span data-stu-id="e2c49-160">Send messages to clients</span></span>

<span data-ttu-id="e2c49-161">若要使对特定的客户端的调用，使用的属性`Clients`对象。</span><span class="sxs-lookup"><span data-stu-id="e2c49-161">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="e2c49-162">在以下示例中，`SendMessageToCaller`方法演示如何将消息发送到调用集线器方法的连接。</span><span class="sxs-lookup"><span data-stu-id="e2c49-162">In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="e2c49-163">`SendMessageToGroups`方法将消息发送到存储中的组`List`名为`groups`。</span><span class="sxs-lookup"><span data-stu-id="e2c49-163">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="e2c49-164">处理连接事件</span><span class="sxs-lookup"><span data-stu-id="e2c49-164">Handle events for a connection</span></span>

<span data-ttu-id="e2c49-165">SignalR 中心 API 提供了`OnConnectedAsync`和`OnDisconnectedAsync`管理和跟踪连接的虚拟方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-165">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="e2c49-166">重写`OnConnectedAsync`虚拟方法，客户端连接到中心，如将其添加到组时，执行操作。</span><span class="sxs-lookup"><span data-stu-id="e2c49-166">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a><span data-ttu-id="e2c49-167">处理错误</span><span class="sxs-lookup"><span data-stu-id="e2c49-167">Handle errors</span></span>

<span data-ttu-id="e2c49-168">集线器方法中引发的异常将发送到的客户端的调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e2c49-168">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="e2c49-169">在 JavaScript 客户端`invoke`方法将返回[JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)。</span><span class="sxs-lookup"><span data-stu-id="e2c49-169">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="e2c49-170">当客户端收到的错误处理程序附加到承诺使用`catch`，它具有调用，并且作为 JavaScript 传递`Error`对象。</span><span class="sxs-lookup"><span data-stu-id="e2c49-170">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a><span data-ttu-id="e2c49-171">相关资源</span><span class="sxs-lookup"><span data-stu-id="e2c49-171">Related resources</span></span>

* [<span data-ttu-id="e2c49-172">ASP.NET Core SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="e2c49-172">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="e2c49-173">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="e2c49-173">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="e2c49-174">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="e2c49-174">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
