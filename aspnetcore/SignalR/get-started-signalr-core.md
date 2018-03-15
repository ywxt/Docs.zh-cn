---
title: "要开始使用 SignalR 在 ASP.NET Core 上"
author: rachelappel
description: "了解生成实时应用程序使用 ASP.NET Core SignalR 的基础知识。"
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/06/2018
ms.prod: aspnet-core
ms.technology: dotnet-signalr
ms.topic: tutorial
uid: signalr/get-started-signalr-core
ms.openlocfilehash: 79af59fc8c2ada71d764ada95a431e10f4f00f27
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="tutorial-get-started-with-signalr-for-aspnet-core"></a><span data-ttu-id="56500-103">教程： 开始使用 SignalR 为 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="56500-103">Tutorial: Get started with SignalR for ASP.NET Core</span></span>

<span data-ttu-id="56500-104">作者：[Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="56500-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="56500-105">本教程教生成实时应用程序使用 ASP.NET Core SignalR 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="56500-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)

<span data-ttu-id="56500-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="56500-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="56500-108">本教程演示了下列 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="56500-108">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56500-109">创建 ASP.NET 核心 web 应用。</span><span class="sxs-lookup"><span data-stu-id="56500-109">Create an ASP.NET Core web app.</span></span>
> * <span data-ttu-id="56500-110">创建一个 SignalR 集线器，以将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="56500-110">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="56500-111">使用 SignalR JavaScript 库发送消息，并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="56500-111">Use the SignalR JavaScript library to send messages and display updates from the hub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56500-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="56500-112">Prerequisites</span></span>

<span data-ttu-id="56500-113">安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="56500-113">Install the following software:</span></span>

* <span data-ttu-id="56500-114">[.NET 核心 2.1.0 预览 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1)或更高版本</span><span class="sxs-lookup"><span data-stu-id="56500-114">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* <span data-ttu-id="56500-115">[Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 或与 ASP.NET 和 web 开发工作负荷更高版本</span><span class="sxs-lookup"><span data-stu-id="56500-115">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.6 or later with the ASP.NET and web development workload</span></span>
* [<span data-ttu-id="56500-116">npm</span><span class="sxs-lookup"><span data-stu-id="56500-116">npm</span></span>](https://www.npmjs.com/get-npm)

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="56500-117">创建 ASP.NET Core 项目承载 SignalR 客户端和服务器</span><span class="sxs-lookup"><span data-stu-id="56500-117">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

1. <span data-ttu-id="56500-118">使用**文件** > **新项目**菜单选项，然后选择**ASP.NET 核心 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="56500-118">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="56500-119">将项目命名为 `SignalRChat`。</span><span class="sxs-lookup"><span data-stu-id="56500-119">Name the project `SignalRChat`.</span></span>

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="56500-121">选择**Web 应用程序**创建使用 Razor 页项目。</span><span class="sxs-lookup"><span data-stu-id="56500-121">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="56500-122">然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="56500-122">Then select **Ok**.</span></span> <span data-ttu-id="56500-123">请确保**ASP.NET 核心 2.1**尽管 SignalR 运行在较旧版本的.NET framework 选择器，从选择。</span><span class="sxs-lookup"><span data-stu-id="56500-123">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-choose-type.png)

  <span data-ttu-id="56500-125">承载 SignalR 服务器端代码的库都包括在项目模板中。</span><span class="sxs-lookup"><span data-stu-id="56500-125">The libraries that host SignalR server-side code are included in the project template.</span></span> <span data-ttu-id="56500-126">安装客户端 JavaScript 使用分别[npm](https://www.npmjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="56500-126">Install the client-side JavaScript separately with [npm](https://www.npmjs.com/).</span></span>

  ```console
   npm install @aspnet/signalr
  ```

3. <span data-ttu-id="56500-127">复制*signalr.js*从*node_modules\\ @aspnet\signalr\dist\browser* 到*wwwroot\lib*项目文件夹中的。</span><span class="sxs-lookup"><span data-stu-id="56500-127">Copy the *signalr.js* from *node_modules\\@aspnet\signalr\dist\browser* to the *wwwroot\lib* folder in your project.</span></span>

## <a name="create-the-signalr-hub"></a><span data-ttu-id="56500-128">创建 SignalR Hub</span><span class="sxs-lookup"><span data-stu-id="56500-128">Create the SignalR Hub</span></span>

<span data-ttu-id="56500-129">允许客户端和服务器相互调用方法的高级管道作为服务的类，则集线器。</span><span class="sxs-lookup"><span data-stu-id="56500-129">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

1. <span data-ttu-id="56500-130">将类添加到项目中，通过选择**文件** > **新建** > **文件**并选择**Visual C# 类**。</span><span class="sxs-lookup"><span data-stu-id="56500-130">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span> 

1. <span data-ttu-id="56500-131">继承自`Microsoft.AspNetCore.SignalR.Hub`。</span><span class="sxs-lookup"><span data-stu-id="56500-131">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="56500-132">`Hub`类包含属性和管理连接和组，以及发送和接收数据的事件。</span><span class="sxs-lookup"><span data-stu-id="56500-132">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

1. <span data-ttu-id="56500-133">创建`Send`将消息发送到所有连接的聊天客户端的方法。</span><span class="sxs-lookup"><span data-stu-id="56500-133">Create the `Send` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="56500-134">请注意它将返回`Task`，这是因为 SignalR 是异步的。</span><span class="sxs-lookup"><span data-stu-id="56500-134">Notice it returns a `Task`, because SignalR is asynchronous.</span></span> <span data-ttu-id="56500-135">更好地缩放异步代码。</span><span class="sxs-lookup"><span data-stu-id="56500-135">Asynchronous code scales better.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="56500-136">配置项目以使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="56500-136">Configure the project to use SignalR</span></span>

<span data-ttu-id="56500-137">必须配置 SignalR 服务器，这样就知道要传递给 SignalR 的请求。</span><span class="sxs-lookup"><span data-stu-id="56500-137">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="56500-138">若要配置 SignalR 项目，请修改`ConfigureServices`方法在应用程序的`Startup`类的方法是插入调用`services.AddSignalR`。</span><span class="sxs-lookup"><span data-stu-id="56500-138">To configure a SignalR project, modify the `ConfigureServices` method of the application's `Startup` class by inserting a call to `services.AddSignalR`.</span></span>

  <span data-ttu-id="56500-139">`services.AddSignalR` 作为的一部分添加 SignalR [ASP.NET Core 中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="56500-139">`services.AddSignalR` adds SignalR as part of the [ASP.NET Core middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

1. <span data-ttu-id="56500-140">配置路由到你使用的中心`UseSignalR`。</span><span class="sxs-lookup"><span data-stu-id="56500-140">Configure routes to your hubs using `UseSignalR`.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="56500-141">创建 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="56500-141">Create the SignalR client code</span></span>

1. <span data-ttu-id="56500-142">替换中的内容*Pages\Index.cshtml*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="56500-142">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](get-started-signalr-core/sample/Pages/Index.cshtml)]

  <span data-ttu-id="56500-143">前面的 HTML 显示名称和消息字段和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="56500-143">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="56500-144">请注意在底部的脚本引用： 至 SignalR 的引用和*chat.js*。</span><span class="sxs-lookup"><span data-stu-id="56500-144">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

1. <span data-ttu-id="56500-145">添加到 JavaScript 文件*wwwroot\js*文件夹名为*chat.js*并向其中添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="56500-145">Add a JavaScript file to the *wwwroot\js* folder named *chat.js* and add the following code to it:</span></span>

  [!code-javascript[Index](get-started-signalr-core/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a><span data-ttu-id="56500-146">运行应用</span><span class="sxs-lookup"><span data-stu-id="56500-146">Run the app</span></span>

1. <span data-ttu-id="56500-147">选择**调试** > **启动而不调试**启动浏览器并加载网站本地。</span><span class="sxs-lookup"><span data-stu-id="56500-147">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="56500-148">从地址栏复制 URL。</span><span class="sxs-lookup"><span data-stu-id="56500-148">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="56500-149">打开另一个浏览器实例 （任何浏览器），然后在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="56500-149">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="56500-150">选择任一浏览器，输入名称和消息，然后单击**发送**按钮。</span><span class="sxs-lookup"><span data-stu-id="56500-150">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="56500-151">名称和消息会显示在两个页面上立即。</span><span class="sxs-lookup"><span data-stu-id="56500-151">The name and message are displayed on both pages instantly.</span></span>

  ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)
