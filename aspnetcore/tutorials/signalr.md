---
title: 开始在 ASP.NET Core 上使用 SignalR
author: rachelappel
description: 在本教程中，使用适用于 ASP.NET Core 的 SignalR 创建应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/22/2018
uid: tutorials/signalr
ms.openlocfilehash: 6b8222ee04573ca7157b4e1125ed5a4453b2b9a9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830550"
---
# <a name="get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="5b834-103">开始在 ASP.NET Core 上使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="5b834-103">Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="5b834-104">作者：[Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="5b834-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="5b834-105">本教程介绍使用适用于 ASP.NET Core 的 SignalR 生成实时应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="5b834-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![解决方案](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="5b834-107">本教程演示以下 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="5b834-107">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5b834-108">在 ASP.NET Core Web 应用上创建 SignalR。</span><span class="sxs-lookup"><span data-stu-id="5b834-108">Create a SignalR on ASP.NET Core web app.</span></span>
> * <span data-ttu-id="5b834-109">创建 SignalR 中心以将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="5b834-109">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="5b834-110">修改 `Startup` 类并配置应用。</span><span class="sxs-lookup"><span data-stu-id="5b834-110">Modify the `Startup` class and configure the app.</span></span>

<span data-ttu-id="5b834-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="5b834-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b834-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="5b834-112">Prerequisites</span></span>

<span data-ttu-id="5b834-113">安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="5b834-113">Install the following software:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5b834-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b834-114">Visual Studio</span></span>](#tab/visual-studio)

* [<span data-ttu-id="5b834-115">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="5b834-115">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="5b834-116">已安装“ASP.NET 和 Web 开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.7.3 版或更高版本</span><span class="sxs-lookup"><span data-stu-id="5b834-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.7.3 or later with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="5b834-117">npm</span><span class="sxs-lookup"><span data-stu-id="5b834-117">npm</span></span>](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5b834-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b834-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="5b834-119">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="5b834-119">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="5b834-120">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b834-120">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="5b834-121">用于 Visual Studio Code 的 C#</span><span class="sxs-lookup"><span data-stu-id="5b834-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="5b834-122">npm</span><span class="sxs-lookup"><span data-stu-id="5b834-122">npm</span></span>](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="5b834-123">创建托管 SignalR 客户端和服务器的 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="5b834-123">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5b834-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b834-124">Visual Studio</span></span>](#tab/visual-studio/)

1. <span data-ttu-id="5b834-125">使用“文件” > “新建项目”菜单选项，然后选择“ASP.NET Core Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="5b834-125">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="5b834-126">将项目命名为“SignalRChat”。</span><span class="sxs-lookup"><span data-stu-id="5b834-126">Name the project *SignalRChat*.</span></span>

   ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="5b834-128">选择“Web 应用程序”，以使用 Razor Pages 创建项目。</span><span class="sxs-lookup"><span data-stu-id="5b834-128">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="5b834-129">然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="5b834-129">Then select **OK**.</span></span> <span data-ttu-id="5b834-130">请确保从框架选择器选中“ASP.NET Core 2.1”，尽管 SignalR 在较低版本的 .NET 上运行。</span><span class="sxs-lookup"><span data-stu-id="5b834-130">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

   ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-choose-type.png)

<span data-ttu-id="5b834-132">Visual Studio 包含 `Microsoft.AspNetCore.SignalR` 包，该包包含其服务器库作为“ASP.NET Core Web 应用程序”模板的一部分。</span><span class="sxs-lookup"><span data-stu-id="5b834-132">Visual Studio includes the `Microsoft.AspNetCore.SignalR` package containing its server libraries as part of its **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="5b834-133">但是，适用于 SignalR 的 JavaScript 客户端库必须使用 npm 安装。</span><span class="sxs-lookup"><span data-stu-id="5b834-133">However, the JavaScript client library for SignalR must be installed using *npm*.</span></span>

3. <span data-ttu-id="5b834-134">在项目根的“包管理器控制台”窗口中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5b834-134">Run the following commands in the **Package Manager Console** window, from the project root:</span></span>

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

4. <span data-ttu-id="5b834-135">在项目的 lib 文件夹中创建名为“signalr”的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="5b834-135">Create a new folder named "signalr" inside the  *lib* folder in your project.</span></span> <span data-ttu-id="5b834-136">将 signalr.js 文件从 node_modules\\@aspnet\signalr\dist\browser 复制到此文件夹。</span><span class="sxs-lookup"><span data-stu-id="5b834-136">Copy the *signalr.js* file from *node_modules\\@aspnet\signalr\dist\browser* to this folder.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5b834-137">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b834-137">Visual Studio Code</span></span>](#tab/visual-studio-code/)

1. <span data-ttu-id="5b834-138">从“集成终端”运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5b834-138">From the **Integrated Terminal**, run the following command:</span></span>

    ```console
    dotnet new webapp -o SignalRChat
    ```

    [!INCLUDE[](~/includes/webapp-alias-notice.md)]

2. <span data-ttu-id="5b834-139">使用 npm 安装 JavaScript 客户端库。</span><span class="sxs-lookup"><span data-stu-id="5b834-139">Install the JavaScript client library using *npm*.</span></span>

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

3. <span data-ttu-id="5b834-140">在项目的 lib 文件夹中创建名为“signalr”的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="5b834-140">Create a new folder named "signalr" inside the  *lib* folder in your project.</span></span> <span data-ttu-id="5b834-141">将 signalr.js 文件从 node_modules\\@aspnet\signalr\dist\browser 复制到此文件夹。</span><span class="sxs-lookup"><span data-stu-id="5b834-141">Copy the *signalr.js* file from *node_modules\\@aspnet\signalr\dist\browser* to this folder.</span></span>

---

## <a name="create-the-signalr-hub"></a><span data-ttu-id="5b834-142">创建 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="5b834-142">Create the SignalR Hub</span></span>

<span data-ttu-id="5b834-143">中心是用作高级管道的类，它允许客户端和服务器互相调用方法。</span><span class="sxs-lookup"><span data-stu-id="5b834-143">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5b834-144">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b834-144">Visual Studio</span></span>](#tab/visual-studio/)

1. <span data-ttu-id="5b834-145">选择“文件” > “新建” > “文件”，然后选择“Visual C# 类”，将类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="5b834-145">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span> <span data-ttu-id="5b834-146">将类命名为 `ChatHub` 并将文件命名为 ChatHub.cs。</span><span class="sxs-lookup"><span data-stu-id="5b834-146">Name the class `ChatHub` and the file *ChatHub.cs*.</span></span>

2. <span data-ttu-id="5b834-147">继承自 `Microsoft.AspNetCore.SignalR.Hub`。</span><span class="sxs-lookup"><span data-stu-id="5b834-147">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="5b834-148">`Hub` 类包含管理连接和组以及发送和接收数据的属性和事件。</span><span class="sxs-lookup"><span data-stu-id="5b834-148">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

3. <span data-ttu-id="5b834-149">创建将消息发送到所有连接聊天客户端的 `SendMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="5b834-149">Create the `SendMessage` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="5b834-150">请注意它会返回一个[任务](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)，这是因为 SignalR 是异步的。</span><span class="sxs-lookup"><span data-stu-id="5b834-150">Notice it returns a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx), because SignalR is asynchronous.</span></span> <span data-ttu-id="5b834-151">异步代码可以更好地进行缩放。</span><span class="sxs-lookup"><span data-stu-id="5b834-151">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5b834-152">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b834-152">Visual Studio Code</span></span>](#tab/visual-studio-code/)

1. <span data-ttu-id="5b834-153">在 Visual Studio Code 中打开 SignalRChat。</span><span class="sxs-lookup"><span data-stu-id="5b834-153">Open the *SignalRChat* folder in Visual Studio Code.</span></span>

2. <span data-ttu-id="5b834-154">从菜单中选择“文件” > “新建文件”，将类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="5b834-154">Add a class to the project by selecting **File** > **New File** from the menu.</span></span> <span data-ttu-id="5b834-155">将类命名为 `ChatHub` 并将文件命名为 ChatHub.cs。</span><span class="sxs-lookup"><span data-stu-id="5b834-155">Name the class `ChatHub` and the file *ChatHub.cs*.</span></span>

3. <span data-ttu-id="5b834-156">继承自 `Microsoft.AspNetCore.SignalR.Hub`。</span><span class="sxs-lookup"><span data-stu-id="5b834-156">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="5b834-157">`Hub` 类包含管理连接和组以及与客户端之间发送和接收数据的属性和事件。</span><span class="sxs-lookup"><span data-stu-id="5b834-157">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data to clients.</span></span>

4. <span data-ttu-id="5b834-158">将 `SendMessage` 方法添加到类。</span><span class="sxs-lookup"><span data-stu-id="5b834-158">Add a `SendMessage` method to the class.</span></span> <span data-ttu-id="5b834-159">`SendMessage` 方法将消息发送到所有连接聊天客户端。</span><span class="sxs-lookup"><span data-stu-id="5b834-159">The `SendMessage` method sends a message to all connected chat clients.</span></span> <span data-ttu-id="5b834-160">请注意它会返回一个[任务](/dotnet/api/system.threading.tasks.task)，这是因为 SignalR 是异步的。</span><span class="sxs-lookup"><span data-stu-id="5b834-160">Notice it returns a [Task](/dotnet/api/system.threading.tasks.task), because SignalR is asynchronous.</span></span> <span data-ttu-id="5b834-161">异步代码可以更好地进行缩放。</span><span class="sxs-lookup"><span data-stu-id="5b834-161">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

-----

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="5b834-162">配置项目以使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="5b834-162">Configure the project to use SignalR</span></span>

<span data-ttu-id="5b834-163">必须配置 SignalR 服务器，这样它才知道将请求传递到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="5b834-163">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="5b834-164">若要配置 SignalR 项目，请修改项目的 `Startup.ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="5b834-164">To configure a SignalR project, modify the project's `Startup.ConfigureServices` method.</span></span>

   <span data-ttu-id="5b834-165">`services.AddSignalR` 使 SignalR 服务可用于[依赖项注入](xref:fundamentals/dependency-injection)系统。</span><span class="sxs-lookup"><span data-stu-id="5b834-165">`services.AddSignalR` makes the SignalR services available to the [dependency injection](xref:fundamentals/dependency-injection) system.</span></span>

1. <span data-ttu-id="5b834-166">在 `Configure` 方法中使用 `UseSignalR` 将路由配置到中心。</span><span class="sxs-lookup"><span data-stu-id="5b834-166">Configure routes to your hubs with `UseSignalR` in the `Configure` method.</span></span> <span data-ttu-id="5b834-167">`app.UseSignalR` 将 SignalR 添加到[中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="5b834-167">`app.UseSignalR` adds SignalR to the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

   [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=37,57-60)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="5b834-168">创建 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="5b834-168">Create the SignalR client code</span></span>

1. <span data-ttu-id="5b834-169">将一个名为 chat.js 的 JavaScript 文件添加到 wwwroot\js 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5b834-169">Add a JavaScript file, named *chat.js*, to the *wwwroot\js* folder.</span></span> <span data-ttu-id="5b834-170">向新文件添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="5b834-170">Add the following code to it:</span></span>

   [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

2. <span data-ttu-id="5b834-171">使用以下代码替换 Pages\Index.cshtml 中的内容：</span><span class="sxs-lookup"><span data-stu-id="5b834-171">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

   [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

   <span data-ttu-id="5b834-172">前面的 HTML 显示名称、消息字段和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="5b834-172">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="5b834-173">请注意底部的脚本引用：对 SignalR 和 chat.js 的引用。</span><span class="sxs-lookup"><span data-stu-id="5b834-173">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="5b834-174">运行应用</span><span class="sxs-lookup"><span data-stu-id="5b834-174">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5b834-175">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b834-175">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="5b834-176">选择“调试” > “开始执行(不调试)”启动浏览器，然后本地加载网站。</span><span class="sxs-lookup"><span data-stu-id="5b834-176">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="5b834-177">从地址栏复制 URL。</span><span class="sxs-lookup"><span data-stu-id="5b834-177">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="5b834-178">打开另一个浏览器实例（任何浏览器），然后在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="5b834-178">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="5b834-179">选择任一浏览器，输入名称和消息，然后单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="5b834-179">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="5b834-180">两个页面上立即显示名称和消息。</span><span class="sxs-lookup"><span data-stu-id="5b834-180">The name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5b834-181">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5b834-181">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="5b834-182">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="5b834-182">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="5b834-183">运行程序将打开一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="5b834-183">Running the program opens a browser window.</span></span>

1. <span data-ttu-id="5b834-184">打开另一个浏览器窗口并在其中本地加载网站。</span><span class="sxs-lookup"><span data-stu-id="5b834-184">Open another browser window and load the website locally in it.</span></span>

1. <span data-ttu-id="5b834-185">选择任一浏览器，输入名称和消息，然后单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="5b834-185">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="5b834-186">两个页面上立即显示名称和消息。</span><span class="sxs-lookup"><span data-stu-id="5b834-186">The name and message are displayed on both pages instantly.</span></span>

---

  ![解决方案](signalr/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a><span data-ttu-id="5b834-188">相关资源</span><span class="sxs-lookup"><span data-stu-id="5b834-188">Related resources</span></span>

[<span data-ttu-id="5b834-189">ASP.NET Core SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="5b834-189">Introduction to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
