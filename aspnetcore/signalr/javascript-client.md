---
title: ASP.NET Core SignalR JavaScript 客户端
author: tdykstra
description: ASP.NET Core SignalR JavaScript 客户端的概述。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/29/2018
uid: signalr/javascript-client
ms.openlocfilehash: c13c41b0344b0c880e842f2799d6ee97bd7fff7e
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095419"
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET Core SignalR JavaScript 客户端

作者：[Rachel Appel](http://twitter.com/rachelappel)

ASP.NET Core SignalR JavaScript 客户端库，开发人员可以调用服务器端中心代码。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="install-the-signalr-client-package"></a>安装 SignalR 客户端包

作为提供 SignalR JavaScript 客户端库[npm](https://www.npmjs.com/)包。 如果使用 Visual Studio，运行`npm install`从**程序包管理器控制台**时的根文件夹中。 对于 Visual Studio Code 中，运行中的命令**集成终端**。

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

Npm 安装中的包内容 *node_modules\\@aspnet\signalr\dist\browser* 文件夹。 创建一个名为的新文件夹 *signalr*下*wwwroot\\lib*文件夹。 复制 *signalr.js* 的文件 *wwwroot\lib\signalr* 文件夹。

## <a name="use-the-signalr-javascript-client"></a>使用 SignalR JavaScript 客户端

引用中的 SignalR JavaScript 客户端`<script>`元素。

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>连接到中心

下面的代码创建并启动连接。 在中心的名称是不区分大小写。

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a>跨域的连接

通常情况下，浏览器请求的页面所在的域从加载的连接。 但是，有一些情况下需要与另一个域的连接时。

若要防止恶意站点读取另一个站点中的敏感数据[跨域连接](xref:security/cors)默认处于禁用状态。 若要允许跨域请求，请启用它在`Startup`类。

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a>从客户端调用集线器方法

JavaScript 客户端调用公共方法上的中心使用`connection.invoke`。 `invoke`方法接受两个参数：

* 集线器方法的名称。 在以下示例中，中心名称是`SendMessage`。
* 在集线器方法中定义的任何参数。 在以下示例中，参数名称是`message`。

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a>从集线器调用客户端方法

若要从中心接收消息，定义方法使用`connection.on`方法。

* JavaScript 客户端方法的名称。 在以下示例中，方法名称是`ReceiveMessage`。
* 该中心将传递给方法的参数。 在以下示例中，参数值是`message`。

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

在前面的代码`connection.on`运行时服务器端代码将调用它使用`SendAsync`方法。

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR 确定要进行匹配的方法名称来调用的客户端方法和参数中定义`SendAsync`和`connection.on`。

> [!NOTE]
> 最佳做法是，调用`connection.start`后`connection.on`以便接收任何消息之前注册您的处理程序。

## <a name="error-handling-and-logging"></a>错误处理和日志记录

链`catch`方法的末尾`connection.start`方法以处理客户端错误。 使用`console.error`向浏览器的控制台输出错误。

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

通过传递要进行连接时记录的记录器和事件类型的安装程序客户端的日志跟踪。 使用指定的日志级别和更高版本记录的消息。 可用日志级别为按如下所示：

* `signalR.LogLevel.Error` ： 错误消息。 日志`Error`仅消息。
* `signalR.LogLevel.Warning` ： 有关潜在错误警告消息。 日志`Warning`，和`Error`消息。
* `signalR.LogLevel.Information` ： 未出现错误状态消息。 日志`Information`， `Warning`，和`Error`消息。
* `signalR.LogLevel.Trace` ： 跟踪消息。 记录所有内容，包括数据中心和客户端之间传输。

使用`configureLogging`方法`HubConnectionBuilder`若要配置日志级别。 消息会记录到浏览器控制台。

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a>相关资源

* [中心](xref:signalr/hubs)
* [.NET 客户端](xref:signalr/dotnet-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
* [启用 ASP.NET Core 中的跨源请求 (CORS)](xref:security/cors)
