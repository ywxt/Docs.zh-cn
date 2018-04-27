---
title: 在 ASP.NET 核心 SignalR 使用中心
author: rachelappel
description: 了解如何在 ASP.NET 核心 SignalR 中使用中心。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 03/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubs
ms.openlocfilehash: 7da0c4832b1aa6a844172bf751a46b280a02f37a
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="7efb2-103">ASP.NET 核心使用 SignalR 中的中心</span><span class="sxs-lookup"><span data-stu-id="7efb2-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="7efb2-104">通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin 怪兽](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="7efb2-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

[!INCLUDE [2.1 preview notice](~/includes/2.1.md)]

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="7efb2-105">什么是 SignalR hub</span><span class="sxs-lookup"><span data-stu-id="7efb2-105">What is a SignalR hub</span></span>

<span data-ttu-id="7efb2-106">SignalR 中心 API，你可以从服务器连接的客户端上调用方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-106">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="7efb2-107">在服务器代码中，你可以定义客户端调用的方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-107">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="7efb2-108">在客户端代码中，你可以定义从服务器调用的方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-108">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="7efb2-109">SignalR 负责在后台，使实时客户端到服务器和服务器客户端通信的所有内容。</span><span class="sxs-lookup"><span data-stu-id="7efb2-109">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="7efb2-110">配置 SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="7efb2-110">Configure SignalR hubs</span></span>

<span data-ttu-id="7efb2-111">SignalR 中间件需要某些服务，通过调用配置`services.AddSignalR`。</span><span class="sxs-lookup"><span data-stu-id="7efb2-111">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=35)]

<span data-ttu-id="7efb2-112">在 SignalR 功能添加到 ASP.NET 核心应用程序时，通过调用设置 SignalR 路由`app.UseSignalR`中`Startup.Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-112">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=55-58)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="7efb2-113">创建并使用中心</span><span class="sxs-lookup"><span data-stu-id="7efb2-113">Create and use hubs</span></span>

<span data-ttu-id="7efb2-114">通过声明一个类继承自创建中心`Hub`，并向其中添加公共方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-114">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="7efb2-115">客户端可以调用方法定义为`public`。</span><span class="sxs-lookup"><span data-stu-id="7efb2-115">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/chathub.cs?range=10-13)]

<span data-ttu-id="7efb2-116">你可以指定返回类型和参数，包括复杂类型并对数组，就像在任何 C# 方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-116">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="7efb2-117">SignalR 处理的序列化和反序列化的复杂对象和数组中参数和返回值。</span><span class="sxs-lookup"><span data-stu-id="7efb2-117">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

## <a name="the-clients-object"></a><span data-ttu-id="7efb2-118">客户端对象</span><span class="sxs-lookup"><span data-stu-id="7efb2-118">The Clients object</span></span>

<span data-ttu-id="7efb2-119">每个实例`Hub`类有一个名为`Clients`包含服务器和客户端之间通信的以下成员：</span><span class="sxs-lookup"><span data-stu-id="7efb2-119">Each instance of the `Hub` class has a property named `Clients` that contains the following members for communication between server and client:</span></span>

| <span data-ttu-id="7efb2-120">属性</span><span class="sxs-lookup"><span data-stu-id="7efb2-120">Property</span></span> | <span data-ttu-id="7efb2-121">描述</span><span class="sxs-lookup"><span data-stu-id="7efb2-121">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="7efb2-122">在所有连接的客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-122">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="7efb2-123">调用 hub 方法在客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-123">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="7efb2-124">除调用的方法的客户端的所有连接客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-124">Calls a method on all connected clients except the client that invoked the method</span></span> |

<span data-ttu-id="7efb2-125">此外，`Hub`类包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="7efb2-125">Additionally, the `Hub` class contains the following methods:</span></span>

| <span data-ttu-id="7efb2-126">方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-126">Method</span></span> | <span data-ttu-id="7efb2-127">描述</span><span class="sxs-lookup"><span data-stu-id="7efb2-127">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="7efb2-128">在指定的连接除外的所有连接的客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-128">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="7efb2-129">在特定连接的客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-129">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="7efb2-130">在特定连接的客户端上调用方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-130">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="7efb2-131">将消息发送到指定的组中的所有连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-131">Sends a message to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="7efb2-132">将消息发送到指定的组，除非指定连接中的所有连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-132">Sends a message to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="7efb2-133">将一条消息发送到多个组的连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-133">Sends a message to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="7efb2-134">将一条消息发送到一组的连接，不包括客户端调用 hub 方法</span><span class="sxs-lookup"><span data-stu-id="7efb2-134">Sends a message to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="7efb2-135">将消息发送到与特定用户关联的所有连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-135">Sends a message to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="7efb2-136">将消息发送到与指定的用户相关联的所有连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-136">Sends a message to all connections associated with the specified users</span></span> |

<span data-ttu-id="7efb2-137">每个属性或方法上表中的返回一个包含对象`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="7efb2-137">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="7efb2-138">`SendAsync`方法允许你提供的名称和要调用的客户端方法的参数。</span><span class="sxs-lookup"><span data-stu-id="7efb2-138">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="7efb2-139">将消息发送到客户端</span><span class="sxs-lookup"><span data-stu-id="7efb2-139">Send messages to clients</span></span>

<span data-ttu-id="7efb2-140">若要使对特定客户端的调用，使用的属性`Clients`对象。</span><span class="sxs-lookup"><span data-stu-id="7efb2-140">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="7efb2-141">在下面的示例在以下示例中，`SendMessageToCaller`方法演示如何将消息发送到调用 hub 方法的连接。</span><span class="sxs-lookup"><span data-stu-id="7efb2-141">In the following In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="7efb2-142">`SendMessageToGroups`方法将消息发送到存储中的组`List`名为`groups`。</span><span class="sxs-lookup"><span data-stu-id="7efb2-142">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="7efb2-143">处理事件的连接</span><span class="sxs-lookup"><span data-stu-id="7efb2-143">Handle events for a connection</span></span>

<span data-ttu-id="7efb2-144">SignalR 中心 API 提供`OnConnectedAsync`和`OnDisconnectedAsync`虚拟方法，以管理和跟踪连接。</span><span class="sxs-lookup"><span data-stu-id="7efb2-144">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="7efb2-145">重写`OnConnectedAsync`虚拟方法，客户端连接到集线器，如将其添加到组时，执行操作。</span><span class="sxs-lookup"><span data-stu-id="7efb2-145">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/chathub.cs?range=26-30)]

## <a name="handle-errors"></a><span data-ttu-id="7efb2-146">处理错误</span><span class="sxs-lookup"><span data-stu-id="7efb2-146">Handle errors</span></span>

<span data-ttu-id="7efb2-147">在中心方法中引发的异常会发送到调用的方法的客户端。</span><span class="sxs-lookup"><span data-stu-id="7efb2-147">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="7efb2-148">JavaScript 客户端上`invoke`方法返回[JavaScript 承诺](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)。</span><span class="sxs-lookup"><span data-stu-id="7efb2-148">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="7efb2-149">当客户端收到错误处理程序附加到承诺使用`catch`，其调用和作为 JavaScript 传递`Error`对象。</span><span class="sxs-lookup"><span data-stu-id="7efb2-149">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/chat.js?range=20)]
[!code-javascript[Error](hubs/sample/chat.js?range=16-18)]

## <a name="related-resources"></a><span data-ttu-id="7efb2-150">相关资源</span><span class="sxs-lookup"><span data-stu-id="7efb2-150">Related resources</span></span>

[<span data-ttu-id="7efb2-151">ASP.NET 核心 SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="7efb2-151">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)