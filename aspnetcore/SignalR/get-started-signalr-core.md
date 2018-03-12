---
title: "要开始使用 SignalR 在 ASP.NET Core 上"
author: rachelappel
ms.author: rachelap
description: "在本教程中，你创建使用 SignalR 为 ASP.NET Core 应用。"
manager: wpickett
ms.date: 03/06/2018
ms.topic: tutorial
ms.technology: dotnet-signalr
ms.prod: aspnet-core
ms.custom: mvc
uid: signalr/get-started-signalr-core
ms.openlocfilehash: 4afb9785fc3d0f472226a745537acbc77adefb4c
ms.sourcegitcommit: 9622bdc6326c28c3322c70000468a80ef21ad376
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2018
---
# <a name="tutorial-get-started-with-signalr-for-aspnet-core"></a>教程： 开始使用 SignalR 为 ASP.NET Core

作者：[Rachel Appel](https://twitter.com/rachelappel)

本教程教生成实时应用程序使用 ASP.NET Core SignalR 的基础知识。

   ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

本教程演示了下列 SignalR 开发任务：

> [!div class="checklist"]
> * 创建 ASP.NET 核心 web 应用。
> * 创建一个 SignalR 集线器，以将内容推送到客户端。
> * 使用 SignalR JavaScript 库发送消息，并显示从中心的更新。

## <a name="prerequisites"></a>系统必备

安装以下软件：

* [.NET 核心 2.1.0 预览 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1)或更高版本
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 或与 ASP.NET 和 web 开发工作负荷更高版本
* [npm](https://www.npmjs.com/get-npm)

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>创建 ASP.NET Core 项目承载 SignalR 客户端和服务器

1. 使用**文件** > **新项目**菜单选项，然后选择**ASP.NET 核心 Web 应用程序**。 将项目命名为 `SignalRChat`。

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-dialog.png)

2. 选择**Web 应用程序**创建使用 Razor 页项目。 然后选择**确定**。 请确保**ASP.NET 核心 2.1**尽管 SignalR 运行在较旧版本的.NET framework 选择器，从选择。

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-choose-type.png)

  承载 SignalR 服务器端代码的库都包括在项目模板中。 安装客户端 JavaScript 使用分别[npm](https://www.npmjs.com/)。

  ```console
   npm install @aspnet/signalr
  ```

3. 复制*signalr.js*从*node_modules\\ @aspnet\signalr\dist\browser* 到*wwwroot\lib*项目文件夹中的。

## <a name="create-the-signalr-hub"></a>创建 SignalR Hub

允许客户端和服务器相互调用方法的高级管道作为服务的类，则集线器。

1. 将类添加到项目中，通过选择**文件** > **新建** > **文件**并选择**Visual C# 类**。 

1. 继承自`Microsoft.AspNetCore.SignalR.Hub`。 `Hub`类包含属性和管理连接和组，以及发送和接收数据的事件。

1. 创建`Send`将消息发送到所有连接的聊天客户端的方法。 请注意它将返回`Task`，这是因为 SignalR 是异步的。 更好地缩放异步代码。

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

## <a name="configure-the-project-to-use-signalr"></a>配置项目以使用 SignalR

必须配置 SignalR 服务器，这样就知道要传递给 SignalR 的请求。

1. 若要配置 SignalR 项目，请修改`ConfigureServices`方法在应用程序的`Startup`类的方法是插入调用`services.AddSignalR`。

  `services.AddSignalR` 作为的一部分添加 SignalR [ASP.NET Core 中间件](xref:fundamentals/middleware/index)管道。

1. 配置路由到你使用的中心`UseSignalR`。

  [!code-csharp[Startup](get-started-signalr-core/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a>创建 SignalR 客户端代码

1. 替换中的内容*Pages\Index.cshtml*替换为以下代码：

  [!code-cshtml[Index](get-started-signalr-core/sample/Pages/Index.cshtml)]

  前面的 HTML 显示名称和消息字段和提交按钮。 请注意在底部的脚本引用： 至 SignalR 的引用和*chat.js*。

1. 添加到 JavaScript 文件*wwwroot\js*文件夹名为*chat.js*并向其中添加以下代码：

  [!code-javascript[Index](get-started-signalr-core/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a>运行应用

1. 选择**调试** > **启动而不调试**启动浏览器并加载网站本地。 从地址栏复制 URL。

1. 打开另一个浏览器实例 （任何浏览器），然后在地址栏中粘贴该 URL。

1. 选择任一浏览器，输入名称和消息，然后单击**发送**按钮。 名称和消息会显示在两个页面上立即。

  ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)
