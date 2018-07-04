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
# <a name="use-messagepack-hub-protocol-in-signalr-for-aspnet-core"></a>使用 ASP.NET Core MessagePack 中心协议中 SignalR

通过[Brennan 勇](https://github.com/BrennanConroy)

本文假定读者熟悉中涉及的主题[开始](xref:tutorials/signalr)。

## <a name="what-is-messagepack"></a>什么是 MessagePack？

[MessagePack](https://msgpack.org/index.html)是快速且紧凑的二进制序列化格式。 在性能和带宽是一个问题，因为它将创建较小的消息相比[JSON](https://www.json.org/)。 因为它是二进制格式，则消息是不可读，除非字节将通过 MessagePack 分析器查看网络跟踪和日志时。 SignalR MessagePack 格式中，内置支持，并提供 Api，可用于客户端和服务器使用。

## <a name="configure-messagepack-on-the-server"></a>在服务器上配置 MessagePack

若要启用 MessagePack 中心协议在服务器上，安装`Microsoft.AspNetCore.SignalR.Protocols.MessagePack`应用程序中的包。 在 Startup.cs 文件中添加`AddMessagePackProtocol`到`AddSignalR`调用以启用 MessagePack 支持服务器上的。

> [!NOTE]
> 默认情况下，启用 JSON。 添加 MessagePack 能够支持 JSON 和 MessagePack 客户端。

```csharp
services.AddSignalR()
    .AddMessagePackProtocol();
```

若要自定义 MessagePack 设置你的数据的格式`AddMessagePackProtocol`采用用于配置选项的委托。 在该委托，`FormatterResolvers`属性可以用于配置 MessagePack 序列化选项。 冲突解决程序的工作原理的详细信息，请访问 MessagePack 库在[MessagePack CSharp](https://github.com/neuecc/MessagePack-CSharp)。 属性可以在你想要序列化以定义应如何处理它们的对象上使用。

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

## <a name="configure-messagepack-on-the-client"></a>在客户端上配置 MessagePack

### <a name="net-client"></a>.NET 客户端

若要启用 MessagePack.NET 客户端中的，安装`Microsoft.AspNetCore.SignalR.Protocols.MessagePack`包和调用`AddMessagePackProtocol`上`HubConnectionBuilder`。

```csharp
var hubConnection = new HubConnectionBuilder()
                        .WithUrl("/chatHub")
                        .AddMessagePackProtocol()
                        .Build();
```

> [!NOTE]
> 这`AddMessagePackProtocol`调用采用用于配置选项，就像服务器一样的委托。

### <a name="javascript-client"></a>JavaScript 客户端

由提供的 Javascript 客户端的 MessagePack 支持`@aspnet/signalr-protocol-msgpack`NPM 包。

```console
npm install @aspnet/signalr-protocol-msgpack
```

安装后 npm 包，该模块可使用直接通过 JavaScript 模块加载程序，或者导入到浏览器通过引用*node_modules\\ @aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* 文件。 在浏览器`msgpack5`也必须引用库。 使用`<script>`标记来创建的引用。 处找不到库*node_modules\msgpack5\dist\msgpack5.js*。

> [!NOTE]
> 使用时`<script>`元素的顺序非常重要。 如果*signalr 协议 msgpack.js*引用之前*msgpack5.js*，尝试与 MessagePack 连接时出错。 *signalr.js*之前也需要*signalr 协议 msgpack.js*。

```html
<script src="~/lib/signalr/signalr.js"></script>
<script src="~/lib/msgpack5/msgpack5.js"></script>
<script src="~/lib/signalr/signalr-protocol-msgpack.js"></script>
```

添加`.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())`到`HubConnectionBuilder`将配置客户端时要使用 MessagePack 协议连接到服务器。

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chatHub")
    .withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())
    .build();
```

> [!NOTE]
> 此时，没有 MessagePack 协议 JavaScript 客户端上配置的选项。

## <a name="related-resources"></a>相关资源

* [入门](xref:tutorials/signalr)
* [.NET 客户端](xref:signalr/dotnet-client)
* [JavaScript 客户端](xref:signalr/javascript-client)
