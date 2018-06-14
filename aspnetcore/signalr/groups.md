---
title: SignalR 中管理用户和组
author: rachelappel
description: ASP.NET 核心 SignalR 用户和组管理的概述。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/groups
ms.openlocfilehash: 2a2f129863cf7d5cdfa3c0e5b2d901af52144671
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35358427"
---
# <a name="manage-users-and-groups-in-signalr"></a><span data-ttu-id="b2bd8-103">SignalR 中管理用户和组</span><span class="sxs-lookup"><span data-stu-id="b2bd8-103">Manage users and groups in SignalR</span></span>

<span data-ttu-id="b2bd8-104">通过[Brennan 勇](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="b2bd8-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="b2bd8-105">SignalR 允许消息发送到与特定用户关联的所有连接以及名为的连接组。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-105">SignalR allows messages to be sent to all connections associated with a specific user, as well as to named groups of connections.</span></span>

<span data-ttu-id="b2bd8-106">[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="b2bd8-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="users-in-signalr"></a><span data-ttu-id="b2bd8-107">SignalR 中的用户</span><span class="sxs-lookup"><span data-stu-id="b2bd8-107">Users in SignalR</span></span>

<span data-ttu-id="b2bd8-108">SignalR 可用于将消息发送到与特定用户关联的所有连接。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-108">SignalR allows you to send messages to all connections associated with a specific user.</span></span> <span data-ttu-id="b2bd8-109">默认情况下使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符的连接。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-109">By default SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> <span data-ttu-id="b2bd8-110">单个用户可以有多个连接到 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-110">A single user can have multiple connections to a SignalR application.</span></span> <span data-ttu-id="b2bd8-111">例如，用户无法连接上他们的桌面，以及他们的电话。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-111">For example, a user could be connected on their desktop as well as their phone.</span></span> <span data-ttu-id="b2bd8-112">每个设备都有单独的 SignalR 连接，但它们可以与同一用户所有关联。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-112">Each device has a separate SignalR connection, but they are all associated with the same user.</span></span> <span data-ttu-id="b2bd8-113">如果向用户发送一条消息，所有与该用户关联的连接将收到消息。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-113">If a message is sent to the user, all of the connections associated with that user will receive the message.</span></span>

<span data-ttu-id="b2bd8-114">将一条消息发送到特定用户，通过将传递到的用户标识符`User`函数中心方法中，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="b2bd8-114">Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="b2bd8-115">用户标识符是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-115">The user identifier is case-sensitive.</span></span>

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

<span data-ttu-id="b2bd8-116">可以通过创建自定义用户标识符`IUserIdProvider`，并向在`ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-116">The user identifier can be customized by creating an `IUserIdProvider`, and registering it in `ConfigureServices`.</span></span>

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> <span data-ttu-id="b2bd8-117">注册自定义的 SignalR 服务之前，必须调用 AddSignalR。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-117">AddSignalR must be called before registering your custom SignalR services.</span></span>

## <a name="groups-in-signalr"></a><span data-ttu-id="b2bd8-118">SignalR 中的组</span><span class="sxs-lookup"><span data-stu-id="b2bd8-118">Groups in SignalR</span></span>

<span data-ttu-id="b2bd8-119">组是与名称关联的连接的集合。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-119">A group is a collection of connections associated with a name.</span></span> <span data-ttu-id="b2bd8-120">消息可以发送到一个组中的所有连接。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-120">Messages can be sent to all connections in a group.</span></span> <span data-ttu-id="b2bd8-121">组是将发送到连接或多个连接，因为组由应用程序管理的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-121">Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application.</span></span> <span data-ttu-id="b2bd8-122">连接可以是多个组的成员。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-122">A connection can be a member of multiple groups.</span></span> <span data-ttu-id="b2bd8-123">这使得组理想之选类似于下面的聊天应用程序，其中每个房间可以表示为一组。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-123">This makes groups ideal for something like a chat application, where each room can be represented as a group.</span></span> <span data-ttu-id="b2bd8-124">可以添加到连接，或将其从通过组中删除`AddToGroupAsync`和`RemoveFromGroupAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-124">Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.</span></span>

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

<span data-ttu-id="b2bd8-125">当连接重新连接时，组成员身份不会保留。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-125">Group membership isn't preserved when a connection reconnects.</span></span> <span data-ttu-id="b2bd8-126">需要重新建立时重新加入组的连接。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-126">The connection needs to rejoin the group when it's re-established.</span></span> <span data-ttu-id="b2bd8-127">不能计算组的成员，因为此信息不可用，如果应用程序扩展到多个服务器。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-127">It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.</span></span>

> [!NOTE]
> <span data-ttu-id="b2bd8-128">组名称是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b2bd8-128">Group names are case-sensitive.</span></span>

## <a name="related-resources"></a><span data-ttu-id="b2bd8-129">相关资源</span><span class="sxs-lookup"><span data-stu-id="b2bd8-129">Related resources</span></span>

* [<span data-ttu-id="b2bd8-130">入门</span><span class="sxs-lookup"><span data-stu-id="b2bd8-130">Get started</span></span>](xref:signalr/get-started)
* [<span data-ttu-id="b2bd8-131">中心</span><span class="sxs-lookup"><span data-stu-id="b2bd8-131">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="b2bd8-132">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="b2bd8-132">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
