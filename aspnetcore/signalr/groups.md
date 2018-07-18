---
title: SignalR 中管理用户和组
author: tdykstra
description: ASP.NET Core SignalR 用户和组管理的概述。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/groups
ms.openlocfilehash: d54ab2a113345f98e26425a88cad165d67b8d456
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095016"
---
# <a name="manage-users-and-groups-in-signalr"></a><span data-ttu-id="edc1d-103">SignalR 中管理用户和组</span><span class="sxs-lookup"><span data-stu-id="edc1d-103">Manage users and groups in SignalR</span></span>

<span data-ttu-id="edc1d-104">通过[brennan，第 Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="edc1d-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="edc1d-105">SignalR 允许消息发送到与特定用户关联的所有连接，以及要命名的连接组。</span><span class="sxs-lookup"><span data-stu-id="edc1d-105">SignalR allows messages to be sent to all connections associated with a specific user, as well as to named groups of connections.</span></span>

<span data-ttu-id="edc1d-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="edc1d-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="users-in-signalr"></a><span data-ttu-id="edc1d-107">SignalR 中的用户</span><span class="sxs-lookup"><span data-stu-id="edc1d-107">Users in SignalR</span></span>

<span data-ttu-id="edc1d-108">SignalR，可将消息发送到与特定用户关联的所有连接。</span><span class="sxs-lookup"><span data-stu-id="edc1d-108">SignalR allows you to send messages to all connections associated with a specific user.</span></span> <span data-ttu-id="edc1d-109">默认情况下，使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符连接相关联。</span><span class="sxs-lookup"><span data-stu-id="edc1d-109">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> <span data-ttu-id="edc1d-110">单个用户可以向 SignalR 应用程序的多个连接。</span><span class="sxs-lookup"><span data-stu-id="edc1d-110">A single user can have multiple connections to a SignalR app.</span></span> <span data-ttu-id="edc1d-111">例如，用户无法连接其桌面，以及他们的手机上。</span><span class="sxs-lookup"><span data-stu-id="edc1d-111">For example, a user could be connected on their desktop as well as their phone.</span></span> <span data-ttu-id="edc1d-112">每个设备都有单独的 SignalR 连接，但它们具有相同的用户所有关联。</span><span class="sxs-lookup"><span data-stu-id="edc1d-112">Each device has a separate SignalR connection, but they're all associated with the same user.</span></span> <span data-ttu-id="edc1d-113">如果向用户发送一条消息，所有与该用户关联的连接收到的消息。</span><span class="sxs-lookup"><span data-stu-id="edc1d-113">If a message is sent to the user, all of the connections associated with that user receive the message.</span></span> <span data-ttu-id="edc1d-114">可以通过访问连接的用户标识符`Context.UserIdentifier`中心中的属性。</span><span class="sxs-lookup"><span data-stu-id="edc1d-114">The user identifier for a connection can be accessed by the `Context.UserIdentifier` property in your hub.</span></span>

<span data-ttu-id="edc1d-115">向特定用户发送消息，通过将传递到的用户标识符`User`函数集线器方法中，在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="edc1d-115">Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="edc1d-116">用户标识符是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="edc1d-116">The user identifier is case-sensitive.</span></span>

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

<span data-ttu-id="edc1d-117">可以通过创建自定义用户标识符`IUserIdProvider`，并在注册`ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="edc1d-117">The user identifier can be customized by creating an `IUserIdProvider`, and registering it in `ConfigureServices`.</span></span>

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> <span data-ttu-id="edc1d-118">注册自定义 SignalR 服务之前，必须调用 AddSignalR。</span><span class="sxs-lookup"><span data-stu-id="edc1d-118">AddSignalR must be called before registering your custom SignalR services.</span></span>

## <a name="groups-in-signalr"></a><span data-ttu-id="edc1d-119">SignalR 中的组</span><span class="sxs-lookup"><span data-stu-id="edc1d-119">Groups in SignalR</span></span>

<span data-ttu-id="edc1d-120">组是与名称相关联的连接的集合。</span><span class="sxs-lookup"><span data-stu-id="edc1d-120">A group is a collection of connections associated with a name.</span></span> <span data-ttu-id="edc1d-121">可以将消息发送到组中的所有连接。</span><span class="sxs-lookup"><span data-stu-id="edc1d-121">Messages can be sent to all connections in a group.</span></span> <span data-ttu-id="edc1d-122">组是发送到的连接或多个连接，因为组管理的应用程序的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="edc1d-122">Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application.</span></span> <span data-ttu-id="edc1d-123">连接可以是多个组的成员。</span><span class="sxs-lookup"><span data-stu-id="edc1d-123">A connection can be a member of multiple groups.</span></span> <span data-ttu-id="edc1d-124">这使得组理想之选类似的聊天应用程序，其中每个房间可以表示为一个组。</span><span class="sxs-lookup"><span data-stu-id="edc1d-124">This makes groups ideal for something like a chat application, where each room can be represented as a group.</span></span> <span data-ttu-id="edc1d-125">可以添加到连接或通过组中删除`AddToGroupAsync`和`RemoveFromGroupAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="edc1d-125">Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.</span></span>

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

<span data-ttu-id="edc1d-126">当连接重新连接时，不会保留组成员身份。</span><span class="sxs-lookup"><span data-stu-id="edc1d-126">Group membership isn't preserved when a connection reconnects.</span></span> <span data-ttu-id="edc1d-127">需要重新建立时重新加入组的连接。</span><span class="sxs-lookup"><span data-stu-id="edc1d-127">The connection needs to rejoin the group when it's re-established.</span></span> <span data-ttu-id="edc1d-128">不能进行计数的一组成员，因为此信息不可用，如果应用程序扩展到多个服务器。</span><span class="sxs-lookup"><span data-stu-id="edc1d-128">It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.</span></span>

> [!NOTE]
> <span data-ttu-id="edc1d-129">组名称是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="edc1d-129">Group names are case-sensitive.</span></span>

## <a name="related-resources"></a><span data-ttu-id="edc1d-130">相关资源</span><span class="sxs-lookup"><span data-stu-id="edc1d-130">Related resources</span></span>

* [<span data-ttu-id="edc1d-131">入门</span><span class="sxs-lookup"><span data-stu-id="edc1d-131">Get started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="edc1d-132">中心</span><span class="sxs-lookup"><span data-stu-id="edc1d-132">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="edc1d-133">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="edc1d-133">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
