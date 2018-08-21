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
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="8ba66-103">ASP.NET Core SignalR JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="8ba66-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="8ba66-104">作者：[Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="8ba66-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="8ba66-105">ASP.NET Core SignalR JavaScript 客户端库，开发人员可以调用服务器端中心代码。</span><span class="sxs-lookup"><span data-stu-id="8ba66-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="8ba66-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8ba66-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="8ba66-107">安装 SignalR 客户端包</span><span class="sxs-lookup"><span data-stu-id="8ba66-107">Install the SignalR client package</span></span>

<span data-ttu-id="8ba66-108">作为提供 SignalR JavaScript 客户端库[npm](https://www.npmjs.com/)包。</span><span class="sxs-lookup"><span data-stu-id="8ba66-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="8ba66-109">如果使用 Visual Studio，运行`npm install`从**程序包管理器控制台**时的根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8ba66-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="8ba66-110">对于 Visual Studio Code 中，运行中的命令**集成终端**。</span><span class="sxs-lookup"><span data-stu-id="8ba66-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

<span data-ttu-id="8ba66-111">Npm 安装中的包内容 *node_modules\\@aspnet\signalr\dist\browser* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="8ba66-111">Npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="8ba66-112">创建一个名为的新文件夹 *signalr*下*wwwroot\\lib*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8ba66-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="8ba66-113">复制 *signalr.js* 的文件 *wwwroot\lib\signalr* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="8ba66-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="8ba66-114">使用 SignalR JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="8ba66-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="8ba66-115">引用中的 SignalR JavaScript 客户端`<script>`元素。</span><span class="sxs-lookup"><span data-stu-id="8ba66-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="8ba66-116">连接到中心</span><span class="sxs-lookup"><span data-stu-id="8ba66-116">Connect to a hub</span></span>

<span data-ttu-id="8ba66-117">下面的代码创建并启动连接。</span><span class="sxs-lookup"><span data-stu-id="8ba66-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="8ba66-118">在中心的名称是不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="8ba66-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a><span data-ttu-id="8ba66-119">跨域的连接</span><span class="sxs-lookup"><span data-stu-id="8ba66-119">Cross-origin connections</span></span>

<span data-ttu-id="8ba66-120">通常情况下，浏览器请求的页面所在的域从加载的连接。</span><span class="sxs-lookup"><span data-stu-id="8ba66-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="8ba66-121">但是，有一些情况下需要与另一个域的连接时。</span><span class="sxs-lookup"><span data-stu-id="8ba66-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="8ba66-122">若要防止恶意站点读取另一个站点中的敏感数据[跨域连接](xref:security/cors)默认处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="8ba66-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="8ba66-123">若要允许跨域请求，请启用它在`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="8ba66-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="8ba66-124">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="8ba66-124">Call hub methods from client</span></span>

<span data-ttu-id="8ba66-125">JavaScript 客户端调用公共方法上的中心使用`connection.invoke`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-125">JavaScript clients call public methods on hubs by using `connection.invoke`.</span></span> <span data-ttu-id="8ba66-126">`invoke`方法接受两个参数：</span><span class="sxs-lookup"><span data-stu-id="8ba66-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="8ba66-127">集线器方法的名称。</span><span class="sxs-lookup"><span data-stu-id="8ba66-127">The name of the hub method.</span></span> <span data-ttu-id="8ba66-128">在以下示例中，中心名称是`SendMessage`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-128">In the following example, the hub name is `SendMessage`.</span></span>
* <span data-ttu-id="8ba66-129">在集线器方法中定义的任何参数。</span><span class="sxs-lookup"><span data-stu-id="8ba66-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="8ba66-130">在以下示例中，参数名称是`message`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-130">In the following example, the argument name is `message`.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="8ba66-131">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="8ba66-131">Call client methods from hub</span></span>

<span data-ttu-id="8ba66-132">若要从中心接收消息，定义方法使用`connection.on`方法。</span><span class="sxs-lookup"><span data-stu-id="8ba66-132">To receive messages from the hub, define a method using the `connection.on` method.</span></span>

* <span data-ttu-id="8ba66-133">JavaScript 客户端方法的名称。</span><span class="sxs-lookup"><span data-stu-id="8ba66-133">The name of the JavaScript client method.</span></span> <span data-ttu-id="8ba66-134">在以下示例中，方法名称是`ReceiveMessage`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-134">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="8ba66-135">该中心将传递给方法的参数。</span><span class="sxs-lookup"><span data-stu-id="8ba66-135">Arguments the hub passes to the method.</span></span> <span data-ttu-id="8ba66-136">在以下示例中，参数值是`message`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-136">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="8ba66-137">在前面的代码`connection.on`运行时服务器端代码将调用它使用`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="8ba66-137">The preceding code in `connection.on` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="8ba66-138">SignalR 确定要进行匹配的方法名称来调用的客户端方法和参数中定义`SendAsync`和`connection.on`。</span><span class="sxs-lookup"><span data-stu-id="8ba66-138">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba66-139">最佳做法是，调用`connection.start`后`connection.on`以便接收任何消息之前注册您的处理程序。</span><span class="sxs-lookup"><span data-stu-id="8ba66-139">As a best practice, call `connection.start` after `connection.on` so your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="8ba66-140">错误处理和日志记录</span><span class="sxs-lookup"><span data-stu-id="8ba66-140">Error handling and logging</span></span>

<span data-ttu-id="8ba66-141">链`catch`方法的末尾`connection.start`方法以处理客户端错误。</span><span class="sxs-lookup"><span data-stu-id="8ba66-141">Chain a `catch` method to the end of the `connection.start` method to handle client-side errors.</span></span> <span data-ttu-id="8ba66-142">使用`console.error`向浏览器的控制台输出错误。</span><span class="sxs-lookup"><span data-stu-id="8ba66-142">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

<span data-ttu-id="8ba66-143">通过传递要进行连接时记录的记录器和事件类型的安装程序客户端的日志跟踪。</span><span class="sxs-lookup"><span data-stu-id="8ba66-143">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="8ba66-144">使用指定的日志级别和更高版本记录的消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-144">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="8ba66-145">可用日志级别为按如下所示：</span><span class="sxs-lookup"><span data-stu-id="8ba66-145">Available log levels are as follows:</span></span>

* <span data-ttu-id="8ba66-146">`signalR.LogLevel.Error` ： 错误消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-146">`signalR.LogLevel.Error` : Error messages.</span></span> <span data-ttu-id="8ba66-147">日志`Error`仅消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-147">Logs `Error` messages only.</span></span>
* <span data-ttu-id="8ba66-148">`signalR.LogLevel.Warning` ： 有关潜在错误警告消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-148">`signalR.LogLevel.Warning` : Warning messages about potential errors.</span></span> <span data-ttu-id="8ba66-149">日志`Warning`，和`Error`消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-149">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="8ba66-150">`signalR.LogLevel.Information` ： 未出现错误状态消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-150">`signalR.LogLevel.Information` : Status messages without errors.</span></span> <span data-ttu-id="8ba66-151">日志`Information`， `Warning`，和`Error`消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-151">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="8ba66-152">`signalR.LogLevel.Trace` ： 跟踪消息。</span><span class="sxs-lookup"><span data-stu-id="8ba66-152">`signalR.LogLevel.Trace` : Trace messages.</span></span> <span data-ttu-id="8ba66-153">记录所有内容，包括数据中心和客户端之间传输。</span><span class="sxs-lookup"><span data-stu-id="8ba66-153">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="8ba66-154">使用`configureLogging`方法`HubConnectionBuilder`若要配置日志级别。</span><span class="sxs-lookup"><span data-stu-id="8ba66-154">Use the `configureLogging` method on `HubConnectionBuilder` to configure the log level.</span></span> <span data-ttu-id="8ba66-155">消息会记录到浏览器控制台。</span><span class="sxs-lookup"><span data-stu-id="8ba66-155">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a><span data-ttu-id="8ba66-156">相关资源</span><span class="sxs-lookup"><span data-stu-id="8ba66-156">Related resources</span></span>

* [<span data-ttu-id="8ba66-157">中心</span><span class="sxs-lookup"><span data-stu-id="8ba66-157">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="8ba66-158">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="8ba66-158">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="8ba66-159">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="8ba66-159">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="8ba66-160">启用 ASP.NET Core 中的跨源请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="8ba66-160">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>](xref:security/cors)
