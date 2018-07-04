---
title: 使用 ASP.NET Core MessagePack 中心协议中 SignalR
author: rachelappel
description: 将 MessagePack 中心协议添加到 ASP.NET Core SignalR。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/messagepackhubprotocol
ms.openlocfilehash: 702c77502868d6666cb2634b6959f029e036d14e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274984"
---
# <a name="use-messagepack-hub-protocol-in-signalr-for-aspnet-core"></a><span data-ttu-id="3a233-103">使用 ASP.NET Core MessagePack 中心协议中 SignalR</span><span class="sxs-lookup"><span data-stu-id="3a233-103">Use MessagePack Hub Protocol in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="3a233-104">通过[Brennan 勇](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="3a233-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="3a233-105">本文假定读者熟悉中涉及的主题[开始](xref:tutorials/signalr)。</span><span class="sxs-lookup"><span data-stu-id="3a233-105">This article assumes the reader is familiar with the topics covered in [Get Started](xref:tutorials/signalr).</span></span>

## <a name="what-is-messagepack"></a><span data-ttu-id="3a233-106">什么是 MessagePack？</span><span class="sxs-lookup"><span data-stu-id="3a233-106">What is MessagePack?</span></span>

<span data-ttu-id="3a233-107">[MessagePack](https://msgpack.org/index.html)是快速且紧凑的二进制序列化格式。</span><span class="sxs-lookup"><span data-stu-id="3a233-107">[MessagePack](https://msgpack.org/index.html) is a binary serialization format that is fast and compact.</span></span> <span data-ttu-id="3a233-108">在性能和带宽是一个问题，因为它将创建较小的消息相比[JSON](https://www.json.org/)。</span><span class="sxs-lookup"><span data-stu-id="3a233-108">It's useful when performance and bandwidth are a concern because it creates smaller messages compared to [JSON](https://www.json.org/).</span></span> <span data-ttu-id="3a233-109">因为它是二进制格式，则消息是不可读，除非字节将通过 MessagePack 分析器查看网络跟踪和日志时。</span><span class="sxs-lookup"><span data-stu-id="3a233-109">Because it's a binary format, messages are unreadable when looking at network traces and logs unless the bytes are passed through a MessagePack parser.</span></span> <span data-ttu-id="3a233-110">SignalR MessagePack 格式中，内置支持，并提供 Api，可用于客户端和服务器使用。</span><span class="sxs-lookup"><span data-stu-id="3a233-110">SignalR has built-in support for the MessagePack format, and provides APIs for the client and server to use.</span></span>

## <a name="configure-messagepack-on-the-server"></a><span data-ttu-id="3a233-111">在服务器上配置 MessagePack</span><span class="sxs-lookup"><span data-stu-id="3a233-111">Configure MessagePack on the server</span></span>

<span data-ttu-id="3a233-112">若要启用 MessagePack 中心协议在服务器上，安装`Microsoft.AspNetCore.SignalR.Protocols.MessagePack`应用程序中的包。</span><span class="sxs-lookup"><span data-stu-id="3a233-112">To enable the MessagePack Hub Protocol on the server, install the `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` package in your app.</span></span> <span data-ttu-id="3a233-113">在 Startup.cs 文件中添加`AddMessagePackProtocol`到`AddSignalR`调用以启用 MessagePack 支持服务器上的。</span><span class="sxs-lookup"><span data-stu-id="3a233-113">In the Startup.cs file add `AddMessagePackProtocol` to the `AddSignalR` call to enable MessagePack support on the server.</span></span>

> [!NOTE]
> <span data-ttu-id="3a233-114">默认情况下，启用 JSON。</span><span class="sxs-lookup"><span data-stu-id="3a233-114">JSON is enabled by default.</span></span> <span data-ttu-id="3a233-115">添加 MessagePack 能够支持 JSON 和 MessagePack 客户端。</span><span class="sxs-lookup"><span data-stu-id="3a233-115">Adding MessagePack enables support for both JSON and MessagePack clients.</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol();
```

<span data-ttu-id="3a233-116">若要自定义 MessagePack 设置你的数据的格式`AddMessagePackProtocol`采用用于配置选项的委托。</span><span class="sxs-lookup"><span data-stu-id="3a233-116">To customize how MessagePack will format your data, `AddMessagePackProtocol` takes a delegate for configuring options.</span></span> <span data-ttu-id="3a233-117">在该委托，`FormatterResolvers`属性可以用于配置 MessagePack 序列化选项。</span><span class="sxs-lookup"><span data-stu-id="3a233-117">In that delegate, the `FormatterResolvers` property can be used to configure MessagePack serialization options.</span></span> <span data-ttu-id="3a233-118">冲突解决程序的工作原理的详细信息，请访问 MessagePack 库在[MessagePack CSharp](https://github.com/neuecc/MessagePack-CSharp)。</span><span class="sxs-lookup"><span data-stu-id="3a233-118">For more information on how the resolvers work, visit the MessagePack library at [MessagePack-CSharp](https://github.com/neuecc/MessagePack-CSharp).</span></span> <span data-ttu-id="3a233-119">属性可以在你想要序列化以定义应如何处理它们的对象上使用。</span><span class="sxs-lookup"><span data-stu-id="3a233-119">Attributes can be used on the objects you want to serialize to define how they should be handled.</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

## <a name="configure-messagepack-on-the-client"></a><span data-ttu-id="3a233-120">在客户端上配置 MessagePack</span><span class="sxs-lookup"><span data-stu-id="3a233-120">Configure MessagePack on the client</span></span>

### <a name="net-client"></a><span data-ttu-id="3a233-121">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="3a233-121">.NET client</span></span>

<span data-ttu-id="3a233-122">若要启用 MessagePack.NET 客户端中的，安装`Microsoft.AspNetCore.SignalR.Protocols.MessagePack`包和调用`AddMessagePackProtocol`上`HubConnectionBuilder`。</span><span class="sxs-lookup"><span data-stu-id="3a233-122">To enable MessagePack in the .NET Client, install the `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` package and call `AddMessagePackProtocol` on `HubConnectionBuilder`.</span></span>

```csharp
var hubConnection = new HubConnectionBuilder()
                        .WithUrl("/chatHub")
                        .AddMessagePackProtocol()
                        .Build();
```

> [!NOTE]
> <span data-ttu-id="3a233-123">这`AddMessagePackProtocol`调用采用用于配置选项，就像服务器一样的委托。</span><span class="sxs-lookup"><span data-stu-id="3a233-123">This `AddMessagePackProtocol` call takes a delegate for configuring options just like the server.</span></span>

### <a name="javascript-client"></a><span data-ttu-id="3a233-124">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="3a233-124">JavaScript client</span></span>

<span data-ttu-id="3a233-125">由提供的 Javascript 客户端的 MessagePack 支持`@aspnet/signalr-protocol-msgpack`NPM 包。</span><span class="sxs-lookup"><span data-stu-id="3a233-125">MessagePack support for the Javascript client is provided by the `@aspnet/signalr-protocol-msgpack` NPM package.</span></span>

```console
npm install @aspnet/signalr-protocol-msgpack
```

<span data-ttu-id="3a233-126">安装后 npm 包，该模块可使用直接通过 JavaScript 模块加载程序，或者导入到浏览器通过引用*node_modules\\ @aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* 文件。</span><span class="sxs-lookup"><span data-stu-id="3a233-126">After installing the npm package, the module can be used directly via a JavaScript module loader or imported into the browser by referencing the *node_modules\\@aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* file.</span></span> <span data-ttu-id="3a233-127">在浏览器`msgpack5`也必须引用库。</span><span class="sxs-lookup"><span data-stu-id="3a233-127">In a browser the `msgpack5` library must also be referenced.</span></span> <span data-ttu-id="3a233-128">使用`<script>`标记来创建的引用。</span><span class="sxs-lookup"><span data-stu-id="3a233-128">Use a `<script>` tag to create a reference.</span></span> <span data-ttu-id="3a233-129">处找不到库*node_modules\msgpack5\dist\msgpack5.js*。</span><span class="sxs-lookup"><span data-stu-id="3a233-129">The library can be found at *node_modules\msgpack5\dist\msgpack5.js*.</span></span>

> [!NOTE]
> <span data-ttu-id="3a233-130">使用时`<script>`元素的顺序非常重要。</span><span class="sxs-lookup"><span data-stu-id="3a233-130">When using the `<script>` element, the order is important.</span></span> <span data-ttu-id="3a233-131">如果*signalr 协议 msgpack.js*引用之前*msgpack5.js*，尝试与 MessagePack 连接时出错。</span><span class="sxs-lookup"><span data-stu-id="3a233-131">If *signalr-protocol-msgpack.js* is referenced before *msgpack5.js*, an error occurs when trying to connect with MessagePack.</span></span> <span data-ttu-id="3a233-132">*signalr.js*之前也需要*signalr 协议 msgpack.js*。</span><span class="sxs-lookup"><span data-stu-id="3a233-132">*signalr.js* is also required before *signalr-protocol-msgpack.js*.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
<script src="~/lib/msgpack5/msgpack5.js"></script>
<script src="~/lib/signalr/signalr-protocol-msgpack.js"></script>
```

<span data-ttu-id="3a233-133">添加`.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())`到`HubConnectionBuilder`将配置客户端时要使用 MessagePack 协议连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="3a233-133">Adding `.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())` to the `HubConnectionBuilder` will configure the client to use the MessagePack protocol when connecting to a server.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chatHub")
    .withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())
    .build();
```

> [!NOTE]
> <span data-ttu-id="3a233-134">此时，没有 MessagePack 协议 JavaScript 客户端上配置的选项。</span><span class="sxs-lookup"><span data-stu-id="3a233-134">At this time, there are no configuration options for the MessagePack protocol on the JavaScript client.</span></span>

## <a name="related-resources"></a><span data-ttu-id="3a233-135">相关资源</span><span class="sxs-lookup"><span data-stu-id="3a233-135">Related resources</span></span>

* [<span data-ttu-id="3a233-136">入门</span><span class="sxs-lookup"><span data-stu-id="3a233-136">Get Started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="3a233-137">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="3a233-137">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="3a233-138">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="3a233-138">JavaScript client</span></span>](xref:signalr/javascript-client)
