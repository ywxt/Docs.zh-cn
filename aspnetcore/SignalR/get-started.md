---
title: 要开始使用 SignalR 在 ASP.NET Core 上
author: rachelappel
description: 在本教程中，你创建使用 SignalR 为 ASP.NET Core 应用。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 03/16/2018
ms.prod: aspnet-core
ms.topic: tutorial
ms.technology: aspnet
uid: signalr/get-started
ms.openlocfilehash: 03735359bb22cc3085ddc7b34372ecfc9501a940
ms.sourcegitcommit: 07903a1be39a99dcf538d57981161592d0e658b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/20/2018
---
# <a name="get-started-with-signalr-on-aspnet-core"></a>要开始使用 SignalR 在 ASP.NET Core 上

作者：[Rachel Appel](https://twitter.com/rachelappel)

[!INCLUDE [2.1 preview notice](~/includes/2.1.md)]

本教程教生成实时应用程序使用 ASP.NET Core SignalR 的基础知识。

   ![解决方案](get-started/_static/signalr-get-started-finished.png)

本教程演示了下列 SignalR 开发任务：

> [!div class="checklist"]
> * 在 ASP.NET 核心 web 应用上创建 SignalR。
> * 创建一个 SignalR 集线器，以将内容推送到客户端。
> * 修改`Startup`类并将应用配置。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

# <a name="prerequisites"></a>系统必备

安装以下软件：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [.NET 核心 2.1.0 预览 2 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview2)或更高版本
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.7 或使用更高版本**ASP.NET 和 web 开发**工作负荷
* [npm](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [.NET 核心 2.1.0 预览 2 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview2)或更高版本
* [Visual Studio Code](https://code.visualstudio.com/download)
* [用于 Visual Studio 代码的 C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [npm](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>创建 ASP.NET Core 项目承载 SignalR 客户端和服务器

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 使用**文件** > **新项目**菜单选项，然后选择**ASP.NET 核心 Web 应用程序**。 将项目*SignalRChat*。

   ![Visual Studio 中的新建项目对话框](get-started/_static/signalr-new-project-dialog.png)

2. 选择**Web 应用程序**创建使用 Razor 页项目。 然后选择**确定**。 请确保**ASP.NET 核心 2.1**尽管 SignalR 运行在较旧版本的.NET framework 选择器，从选择。

   ![Visual Studio 中的新建项目对话框](get-started/_static/signalr-new-project-choose-type.png)

Visual Studio 包含`Microsoft.AspNetCore.SignalR`作为的一部分包含其服务器库包其**ASP.NET 核心 Web 应用程序**模板。 但是，适用于 SignalR 的 JavaScript 客户端库必须安装使用*npm*。

3. 在中运行以下命令**程序包管理器控制台**窗口，请从项目根：

    ```console
      npm init -y
      npm install @aspnet/signalr
    ```     

4. 复制*signalr.js*文件从*node_modules\\ @aspnet\signalr\dist\browser* 到*lib*项目文件夹中的。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. 从**集成终端**，运行以下命令：

    ```console
      dotnet new razor -o SignalRChat
    ```

2. 安装 JavaScript 客户端库使用*npm*。

    ```
      npm init -y
      npm install @aspnet/signalr
    ```

-----

## <a name="create-the-signalr-hub"></a>创建 SignalR Hub

允许客户端和服务器相互调用方法的高级管道作为服务的类，则集线器。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 将类添加到项目中，通过选择**文件** > **新建** > **文件**并选择**Visual C# 类**。

2. 继承自`Microsoft.AspNetCore.SignalR.Hub`。 `Hub`类包含属性和管理连接和组，以及发送和接收数据的事件。

3. 创建`SendMessage`将消息发送到所有连接的聊天客户端的方法。 请注意它将返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)，这是因为 SignalR 是异步的。 更好地缩放异步代码。

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. 打开*SignalRChat*在 Visual Studio 代码中的文件夹。

2. 将类添加到项目中，通过选择**文件** > **新文件**从菜单。

3. 继承自`Microsoft.AspNetCore.SignalR.Hub`。 `Hub`类包含属性和管理连接和组，以及向客户端发送和接收数据的事件。

4. 将 `SendMessage` 方法添加到类。 `SendMessage`方法将消息发送到所有连接的聊天客户端。 请注意它将返回[任务](/dotnet/api/system.threading.tasks.task)，这是因为 SignalR 是异步的。 更好地缩放异步代码。

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs?range=6-12)]

-----

## <a name="configure-the-project-to-use-signalr"></a>配置项目以使用 SignalR

必须配置 SignalR 服务器，这样就知道要传递给 SignalR 的请求。

1. 若要配置 SignalR 项目，请修改项目的`Startup.ConfigureServices`方法。

   `services.AddSignalR` 作为的一部分添加 SignalR[中间件](xref:fundamentals/middleware/index)管道。

2. 配置路由到你使用的中心`UseSignalR`。


   [!code-csharp[Startup](get-started/sample/Startup.cs?highlight=36,56-59)]


## <a name="create-the-signalr-client-code"></a>创建 SignalR 客户端代码

1. 替换中的内容*Pages\Index.cshtml*替换为以下代码：

   [!code-cshtml[Index](get-started/sample/Pages/Index.cshtml)]

   前面的 HTML 显示名称和消息字段和提交按钮。 请注意在底部的脚本引用： 至 SignalR 的引用和*chat.js*。

2. 添加一个名为的 JavaScript 文件*chat.js*到*wwwroot\js*文件夹。 向新文件添加以下代码：

   [!code-javascript[Index](get-started/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a>运行应用

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

1. 选择**调试** > **启动而不调试**启动浏览器并加载网站本地。 从地址栏复制 URL。

1. 打开另一个浏览器实例 （任何浏览器），然后在地址栏中粘贴该 URL。

1. 选择任一浏览器，输入名称和消息，然后单击**发送**按钮。 名称和消息会显示在两个页面上立即。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

1. 按“调试”(F5) 生成并运行程序。 运行程序将打开一个浏览器窗口。

1. 打开另一个浏览器窗口并加载在本地网站。

1. 选择任一浏览器，输入名称和消息，然后单击**发送**按钮。 名称和消息会显示在两个页面上立即。

-----

  ![解决方案](get-started/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a>相关资源

[ASP.NET 核心 SignalR 简介](introduction.md)