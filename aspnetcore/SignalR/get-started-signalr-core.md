---
title: "要开始使用 SignalR 在 ASP.NET Core 上"
author: rachelappel
description: "在本教程中，你创建使用 SignalR 为 ASP.NET Core 应用。"
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/16/2018
ms.prod: aspnet-core
ms.topic: tutorial
ms.technology: aspnet
uid: signalr/get-started-signalr-core
ms.openlocfilehash: 139da5a2d0dadf51fece94b7c54ccd531e0ae8c2
ms.sourcegitcommit: 6548a3dd0cd1e3e92ac2310dee757ddad9fd6456
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2018
---
# <a name="tutorial-get-started-with-signalr-for-aspnet-core"></a><span data-ttu-id="977fb-103">教程： 开始使用 SignalR 为 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="977fb-103">Tutorial: Get started with SignalR for ASP.NET Core</span></span>

<span data-ttu-id="977fb-104">作者：[Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="977fb-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="977fb-105">本教程教生成实时应用程序使用 ASP.NET Core SignalR 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="977fb-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)

<span data-ttu-id="977fb-107">本教程演示了下列 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="977fb-107">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="977fb-108">在 ASP.NET 核心 web 应用上创建 SignalR。</span><span class="sxs-lookup"><span data-stu-id="977fb-108">Create a SignalR on ASP.NET Core web app.</span></span>
> * <span data-ttu-id="977fb-109">创建一个 SignalR 集线器，以将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="977fb-109">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="977fb-110">修改`Startup`类并将应用配置。</span><span class="sxs-lookup"><span data-stu-id="977fb-110">Modify the `Startup` class and configure the app.</span></span>

<span data-ttu-id="977fb-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="977fb-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="prerequisites"></a><span data-ttu-id="977fb-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="977fb-112">Prerequisites</span></span>

<span data-ttu-id="977fb-113">安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="977fb-113">Install the following software:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="977fb-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="977fb-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="977fb-115">[.NET 核心 2.1.0 预览 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1)或更高版本</span><span class="sxs-lookup"><span data-stu-id="977fb-115">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* <span data-ttu-id="977fb-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 或使用更高版本**ASP.NET 和 web 开发**工作负荷</span><span class="sxs-lookup"><span data-stu-id="977fb-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.6 or later with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="977fb-117">npm</span><span class="sxs-lookup"><span data-stu-id="977fb-117">npm</span></span>](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="977fb-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="977fb-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="977fb-119">[.NET 核心 2.1.0 预览 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1)或更高版本</span><span class="sxs-lookup"><span data-stu-id="977fb-119">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* [<span data-ttu-id="977fb-120">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="977fb-120">Visual Studio Code</span></span>](https://code.visualstudio.com/download) 
* [<span data-ttu-id="977fb-121">用于 Visual Studio 代码的 C#</span><span class="sxs-lookup"><span data-stu-id="977fb-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="977fb-122">npm</span><span class="sxs-lookup"><span data-stu-id="977fb-122">npm</span></span>](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="977fb-123">创建 ASP.NET Core 项目承载 SignalR 客户端和服务器</span><span class="sxs-lookup"><span data-stu-id="977fb-123">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="977fb-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="977fb-124">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="977fb-125">使用**文件** > **新项目**菜单选项，然后选择**ASP.NET 核心 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="977fb-125">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="977fb-126">将项目*SignalRChat*。</span><span class="sxs-lookup"><span data-stu-id="977fb-126">Name the project *SignalRChat*.</span></span>

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="977fb-128">选择**Web 应用程序**创建使用 Razor 页项目。</span><span class="sxs-lookup"><span data-stu-id="977fb-128">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="977fb-129">然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="977fb-129">Then select **OK**.</span></span> <span data-ttu-id="977fb-130">请确保**ASP.NET 核心 2.1**尽管 SignalR 运行在较旧版本的.NET framework 选择器，从选择。</span><span class="sxs-lookup"><span data-stu-id="977fb-130">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

  ![Visual Studio 中的新建项目对话框](get-started-signalr-core/_static/signalr-new-project-choose-type.png)

3. <span data-ttu-id="977fb-132">右键单击中的项目**解决方案资源管理器** > **添加** > **新项** > **npm 配置文件**.</span><span class="sxs-lookup"><span data-stu-id="977fb-132">Right-click the project in **Solution Explorer** > **Add** > **New Item** > **npm Configuration File**.</span></span> <span data-ttu-id="977fb-133">命名该文件*package.json*。</span><span class="sxs-lookup"><span data-stu-id="977fb-133">Name the file *package.json*.</span></span>

4. <span data-ttu-id="977fb-134">在中运行以下命令**程序包管理器控制台**窗口，请从项目根：</span><span class="sxs-lookup"><span data-stu-id="977fb-134">Run the following command in the **Package Manager Console** window, from the project root:</span></span>

    ```console
      npm install @aspnet/signalr
    ```
5. <span data-ttu-id="977fb-135">复制*signalr.js*文件从*node_modules\\ @aspnet\signalr\dist\browser* 到*wwwroot\lib*项目文件夹中的。</span><span class="sxs-lookup"><span data-stu-id="977fb-135">Copy the *signalr.js* file from *node_modules\\@aspnet\signalr\dist\browser* to the *wwwroot\lib* folder in your project.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="977fb-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="977fb-136">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="977fb-137">从**集成终端**，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="977fb-137">From the **Integrated Terminal**, run the following command:</span></span>
 
    ```console
      dotnet new razor -o SignalRChat
    ```

2. <span data-ttu-id="977fb-138">安装 JavaScript 客户端库使用*npm*。</span><span class="sxs-lookup"><span data-stu-id="977fb-138">Install the JavaScript client library using *npm*.</span></span>

    ```
      npm init -y
      npm install @aspnet/signalr
    ```

-----

## <a name="create-the-signalr-hub"></a><span data-ttu-id="977fb-139">创建 SignalR Hub</span><span class="sxs-lookup"><span data-stu-id="977fb-139">Create the SignalR Hub</span></span>

<span data-ttu-id="977fb-140">允许客户端和服务器相互调用方法的高级管道作为服务的类，则集线器。</span><span class="sxs-lookup"><span data-stu-id="977fb-140">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="977fb-141">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="977fb-141">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="977fb-142">将类添加到项目中，通过选择**文件** > **新建** > **文件**并选择**Visual C# 类**。</span><span class="sxs-lookup"><span data-stu-id="977fb-142">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span>

1. <span data-ttu-id="977fb-143">继承自`Microsoft.AspNetCore.SignalR.Hub`。</span><span class="sxs-lookup"><span data-stu-id="977fb-143">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="977fb-144">`Hub`类包含属性和管理连接和组，以及发送和接收数据的事件。</span><span class="sxs-lookup"><span data-stu-id="977fb-144">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

1. <span data-ttu-id="977fb-145">创建`SendMessage`将消息发送到所有连接的聊天客户端的方法。</span><span class="sxs-lookup"><span data-stu-id="977fb-145">Create the `SendMessage` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="977fb-146">请注意它将返回[任务](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task(v=vs.110).aspx)，这是因为 SignalR 是异步的。</span><span class="sxs-lookup"><span data-stu-id="977fb-146">Notice it returns a [Task](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task(v=vs.110).aspx), because SignalR is asynchronous.</span></span> <span data-ttu-id="977fb-147">更好地缩放异步代码。</span><span class="sxs-lookup"><span data-stu-id="977fb-147">Asynchronous code scales better.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="977fb-148">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="977fb-148">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="977fb-149">打开*SignalRChat*在 Visual Studio 代码中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="977fb-149">Open the *SignalRChat* folder in Visual Studio Code.</span></span>

1. <span data-ttu-id="977fb-150">将类添加到项目中，通过选择**文件** > **新文件**从菜单。</span><span class="sxs-lookup"><span data-stu-id="977fb-150">Add a class to the project by selecting **File** > **New File** from the menu.</span></span>

1. <span data-ttu-id="977fb-151">继承自`Microsoft.AspNetCore.SignalR.Hub`。</span><span class="sxs-lookup"><span data-stu-id="977fb-151">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="977fb-152">`Hub`类包含属性和管理连接和组，以及向客户端发送和接收数据的事件。</span><span class="sxs-lookup"><span data-stu-id="977fb-152">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data to clients.</span></span>

1. <span data-ttu-id="977fb-153">将 `SendMessage` 方法添加到类。</span><span class="sxs-lookup"><span data-stu-id="977fb-153">Add a `SendMessage` method to the class.</span></span> <span data-ttu-id="977fb-154">`SendMessage`方法将消息发送到所有连接的聊天客户端。</span><span class="sxs-lookup"><span data-stu-id="977fb-154">The `SendMessage` method sends a message to all connected chat clients.</span></span> <span data-ttu-id="977fb-155">请注意它将返回[任务](/dotnet/api/system.threading.tasks.task)，这是因为 SignalR 是异步的。</span><span class="sxs-lookup"><span data-stu-id="977fb-155">Notice it returns a [Task](/dotnet/api/system.threading.tasks.task), because SignalR is asynchronous.</span></span> <span data-ttu-id="977fb-156">更好地缩放异步代码。</span><span class="sxs-lookup"><span data-stu-id="977fb-156">Asynchronous code scales better.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

-----

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="977fb-157">配置项目以使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="977fb-157">Configure the project to use SignalR</span></span>

<span data-ttu-id="977fb-158">必须配置 SignalR 服务器，这样就知道要传递给 SignalR 的请求。</span><span class="sxs-lookup"><span data-stu-id="977fb-158">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="977fb-159">若要配置 SignalR 项目，请修改项目的`Startup.ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="977fb-159">To configure a SignalR project, modify the project's `Startup.ConfigureServices` method.</span></span>

  <span data-ttu-id="977fb-160">`services.AddSignalR` 作为的一部分添加 SignalR[中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="977fb-160">`services.AddSignalR` adds SignalR as part of the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

1. <span data-ttu-id="977fb-161">配置路由到你使用的中心`UseSignalR`。</span><span class="sxs-lookup"><span data-stu-id="977fb-161">Configure routes to your hubs using `UseSignalR`.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="977fb-162">创建 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="977fb-162">Create the SignalR client code</span></span>

1. <span data-ttu-id="977fb-163">替换中的内容*Pages\Index.cshtml*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="977fb-163">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](get-started-signalr-core/sample/Pages/Index.cshtml)]

  <span data-ttu-id="977fb-164">前面的 HTML 显示名称和消息字段和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="977fb-164">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="977fb-165">请注意在底部的脚本引用： 至 SignalR 的引用和*chat.js*。</span><span class="sxs-lookup"><span data-stu-id="977fb-165">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

1. <span data-ttu-id="977fb-166">添加一个名为的 JavaScript 文件*chat.js*到*wwwroot\js*文件夹。</span><span class="sxs-lookup"><span data-stu-id="977fb-166">Add a JavaScript file, named *chat.js*, to the *wwwroot\js* folder.</span></span> <span data-ttu-id="977fb-167">向新文件添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="977fb-167">Add the following code to it:</span></span>

  [!code-javascript[Index](get-started-signalr-core/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a><span data-ttu-id="977fb-168">运行应用</span><span class="sxs-lookup"><span data-stu-id="977fb-168">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="977fb-169">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="977fb-169">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="977fb-170">选择**调试** > **启动而不调试**启动浏览器并加载网站本地。</span><span class="sxs-lookup"><span data-stu-id="977fb-170">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="977fb-171">从地址栏复制 URL。</span><span class="sxs-lookup"><span data-stu-id="977fb-171">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="977fb-172">打开另一个浏览器实例 （任何浏览器），然后在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="977fb-172">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="977fb-173">选择任一浏览器，输入名称和消息，然后单击**发送**按钮。</span><span class="sxs-lookup"><span data-stu-id="977fb-173">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="977fb-174">名称和消息会显示在两个页面上立即。</span><span class="sxs-lookup"><span data-stu-id="977fb-174">The name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="977fb-175">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="977fb-175">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="977fb-176">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="977fb-176">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="977fb-177">运行程序将打开一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="977fb-177">Running the program opens a browser window.</span></span>

1. <span data-ttu-id="977fb-178">打开另一个浏览器窗口并加载在本地网站。</span><span class="sxs-lookup"><span data-stu-id="977fb-178">Open another browser window and load the website locally in it.</span></span>

1. <span data-ttu-id="977fb-179">选择任一浏览器，输入名称和消息，然后单击**发送**按钮。</span><span class="sxs-lookup"><span data-stu-id="977fb-179">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="977fb-180">名称和消息会显示在两个页面上立即。</span><span class="sxs-lookup"><span data-stu-id="977fb-180">The name and message are displayed on both pages instantly.</span></span>

-----

  ![解决方案](get-started-signalr-core/_static/signalr-get-started-finished.png)