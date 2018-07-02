---
title: 开始在 ASP.NET Core 上使用 SignalR
author: rachelappel
description: 在本教程中，使用适用于 ASP.NET Core 的 SignalR 创建应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/22/2018
uid: tutorials/signalr
ms.openlocfilehash: 8762a4be1032d58014dd32dfdd3707197e14c6f9
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36297196"
---
# <a name="get-started-with-signalr-on-aspnet-core"></a>开始在 ASP.NET Core 上使用 SignalR

作者：[Rachel Appel](https://twitter.com/rachelappel)

本教程介绍使用适用于 ASP.NET Core 的 SignalR 生成实时应用的基础知识。

   ![解决方案](signalr/_static/signalr-get-started-finished.png)

本教程演示以下 SignalR 开发任务：

> [!div class="checklist"]
> * 在 ASP.NET Core Web 应用上创建 SignalR。
> * 创建 SignalR 中心以将内容推送到客户端。
> * 修改 `Startup` 类并配置应用。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

# <a name="prerequisites"></a>系统必备

安装以下软件：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [.NET Core SDK 2.1 或更高版本](https://www.microsoft.com/net/download/all)
* 已安装“ASP.NET 和 Web 开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.7 版或更高版本
* [npm](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [.NET Core SDK 2.1 或更高版本](https://www.microsoft.com/net/download/all)
* [Visual Studio Code](https://code.visualstudio.com/download)
* [用于 Visual Studio Code 的 C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [npm](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>创建托管 SignalR 客户端和服务器的 ASP.NET Core 项目

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 使用“文件” > “新建项目”菜单选项，然后选择“ASP.NET Core Web 应用程序”。 将项目命名为“SignalRChat”。

   ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-dialog.png)

2. 选择“Web 应用程序”，以使用 Razor Pages 创建项目。 然后选择“确定”。 请确保从框架选择器选中“ASP.NET Core 2.1”，尽管 SignalR 在较低版本的 .NET 上运行。

   ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-choose-type.png)

Visual Studio 包含 `Microsoft.AspNetCore.SignalR` 包，该包包含其服务器库作为“ASP.NET Core Web 应用程序”模板的一部分。 但是，适用于 SignalR 的 JavaScript 客户端库必须使用 npm 安装。

3. 在项目根的“包管理器控制台”窗口中运行以下命令：

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

4. 在项目的 lib 文件夹中创建名为“signalr”的新文件夹。 将 signalr.js 文件从 node_modules\\@aspnet\signalr\dist\browser 复制到此文件夹。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. 从“集成终端”运行以下命令：

    ```console
    dotnet new webapp -o SignalRChat
    ```

    [!INCLUDE[](~/includes/webapp-alias-notice.md)]

2. 使用 npm 安装 JavaScript 客户端库。

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

3. 在项目的 lib 文件夹中创建名为“signalr”的新文件夹。 将 signalr.js 文件从 node_modules\\@aspnet\signalr\dist\browser 复制到此文件夹。

---

## <a name="create-the-signalr-hub"></a>创建 SignalR 中心

中心是用作高级管道的类，它允许客户端和服务器互相调用方法。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 选择“文件” > “新建” > “文件”，然后选择“Visual C# 类”，将类添加到项目。 将文件命名为“ChatHub”。

2. 继承自 `Microsoft.AspNetCore.SignalR.Hub`。 `Hub` 类包含管理连接和组以及发送和接收数据的属性和事件。

3. 创建将消息发送到所有连接聊天客户端的 `SendMessage` 方法。 请注意它会返回一个[任务](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)，这是因为 SignalR 是异步的。 异步代码可以更好地进行缩放。

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. 在 Visual Studio Code 中打开 SignalRChat。

2. 从菜单中选择“文件” > “新建文件”，将类添加到项目。

3. 继承自 `Microsoft.AspNetCore.SignalR.Hub`。 `Hub` 类包含管理连接和组以及与客户端之间发送和接收数据的属性和事件。

4. 将 `SendMessage` 方法添加到类。 `SendMessage` 方法将消息发送到所有连接聊天客户端。 请注意它会返回一个[任务](/dotnet/api/system.threading.tasks.task)，这是因为 SignalR 是异步的。 异步代码可以更好地进行缩放。

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs?range=6-12)]

-----

## <a name="configure-the-project-to-use-signalr"></a>配置项目以使用 SignalR

必须配置 SignalR 服务器，这样它才知道将请求传递到 SignalR。

1. 若要配置 SignalR 项目，请修改项目的 `Startup.ConfigureServices` 方法。

   `services.AddSignalR` 将 SignalR 添加为[中间件](xref:fundamentals/middleware/index)管道的一部分。

2. 使用 `UseSignalR` 将路由配置到中心。

   [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=37,57-60)]

## <a name="create-the-signalr-client-code"></a>创建 SignalR 客户端代码

1. 将一个名为 chat.js 的 JavaScript 文件添加到 wwwroot\js 文件夹。 向新文件添加以下代码：

   [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

2. 使用以下代码替换 Pages\Index.cshtml 中的内容：

   [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

   前面的 HTML 显示名称、消息字段和提交按钮。 请注意底部的脚本引用：对 SignalR 和 chat.js 的引用。

## <a name="run-the-app"></a>运行应用

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

1. 选择“调试” > “开始执行(不调试)”启动浏览器，然后本地加载网站。 从地址栏复制 URL。

1. 打开另一个浏览器实例（任何浏览器），然后在地址栏中粘贴该 URL。

1. 选择任一浏览器，输入名称和消息，然后单击“发送”按钮。 两个页面上立即显示名称和消息。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

1. 按“调试”(F5) 生成并运行程序。 运行程序将打开一个浏览器窗口。

1. 打开另一个浏览器窗口并在其中本地加载网站。

1. 选择任一浏览器，输入名称和消息，然后单击“发送”按钮。 两个页面上立即显示名称和消息。

---

  ![解决方案](signalr/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a>相关资源

[ASP.NET Core SignalR 简介](xref:signalr/introduction)
