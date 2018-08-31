---
title: 教程：开始在 ASP.NET Core 上使用 SignalR
author: tdykstra
description: 在本教程中，创建使用适用于 ASP.NET Core 的 SignalR 的聊天应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/20/2018
uid: tutorials/signalr
ms.openlocfilehash: db7f31963f6a4280069f1f4f82a547e2879e64bb
ms.sourcegitcommit: d27317c16f113e7c111583042ec7e4c5a26adf6f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "41751425"
---
# <a name="tutorial-get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="974f1-103">教程：开始在 ASP.NET Core 上使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="974f1-103">Tutorial: Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="974f1-104">本教程介绍生成使用 SignalR 的实时应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="974f1-104">This tutorial teaches the basics of building a real-time app using SignalR.</span></span> <span data-ttu-id="974f1-105">您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="974f1-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="974f1-106">创建在 ASP.NET Core 上使用 SignalR 的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="974f1-106">Create a web app that uses SignalR on ASP.NET Core.</span></span>
> * <span data-ttu-id="974f1-107">在服务器上创建 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="974f1-107">Create a SignalR hub on the server.</span></span>
> * <span data-ttu-id="974f1-108">从 JavaScript 客户端连接到 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="974f1-108">Connect to the SignalR hub from JavaScript clients.</span></span>
> * <span data-ttu-id="974f1-109">使用此中心将消息从任何客户端发送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="974f1-109">Use the hub to send messages from any client to all connected clients.</span></span>

<span data-ttu-id="974f1-110">最终将创建一个正常运行的聊天应用：</span><span class="sxs-lookup"><span data-stu-id="974f1-110">At the end, you'll have a working chat app:</span></span>

![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="974f1-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="974f1-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="974f1-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="974f1-113">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="974f1-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974f1-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="974f1-115">已安装“ASP.NET 和 Web 开发”工作负载的 [Visual Studio 2017 15.7.3 版或更高版本](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="974f1-115">[Visual Studio 2017 version 15.7.3 or later](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="974f1-116">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="974f1-116">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="974f1-117">[npm](https://www.npmjs.com/get-npm)（适用于 Node.js 的包管理器，用于 SignalR JavaScript 客户端库。）</span><span class="sxs-lookup"><span data-stu-id="974f1-117">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="974f1-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="974f1-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="974f1-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="974f1-119">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="974f1-120">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="974f1-120">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="974f1-121">用于 Visual Studio Code 的 C#</span><span class="sxs-lookup"><span data-stu-id="974f1-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* <span data-ttu-id="974f1-122">[npm](https://www.npmjs.com/get-npm)（适用于 Node.js 的包管理器，用于 SignalR JavaScript 客户端库。）</span><span class="sxs-lookup"><span data-stu-id="974f1-122">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="974f1-123">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="974f1-123">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="974f1-124">Visual Studio for Mac 7.5.4 版或更高版本</span><span class="sxs-lookup"><span data-stu-id="974f1-124">Visual Studio for Mac version 7.5.4 or later</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="974f1-125">[.NET Core SDK 2.1 或更高版本](https://www.microsoft.com/net/download/all)（包含在 Visual Studio 安装中）</span><span class="sxs-lookup"><span data-stu-id="974f1-125">[.NET Core SDK 2.1 or later](https://www.microsoft.com/net/download/all) (included in the Visual Studio install)</span></span>
* <span data-ttu-id="974f1-126">[npm](https://www.npmjs.com/get-npm)（适用于 Node.js 的包管理器，用于 SignalR JavaScript 客户端库。）</span><span class="sxs-lookup"><span data-stu-id="974f1-126">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

---

## <a name="create-the-project"></a><span data-ttu-id="974f1-127">创建项目</span><span class="sxs-lookup"><span data-stu-id="974f1-127">Create the project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="974f1-128">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974f1-128">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="974f1-129">从菜单中选择“文件”>“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="974f1-129">From the menu, select **File > New Project**.</span></span>

* <span data-ttu-id="974f1-130">在“新建项目”对话框中，选择“已安装”>“Visual C#”>“Web”>“ASP.NET Core Web 应用”。</span><span class="sxs-lookup"><span data-stu-id="974f1-130">In the **New Project** dialog, select **Installed > Visual C# > Web > ASP.NET Core Web Application**.</span></span> <span data-ttu-id="974f1-131">将项目命名为“SignalRChat”。</span><span class="sxs-lookup"><span data-stu-id="974f1-131">Name the project *SignalRChat*.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-dialog.png)

* <span data-ttu-id="974f1-133">选择“Web 应用”，以创建使用 Razor Pages 的项目。</span><span class="sxs-lookup"><span data-stu-id="974f1-133">Select **Web Application** to create a project that uses Razor Pages.</span></span>

* <span data-ttu-id="974f1-134">选择 .NET Core 的目标框架，选择 ASP.NET Core 2.1，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="974f1-134">Select a target framework of **.NET Core**, select **ASP.NET Core 2.1**, and click **OK**.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="974f1-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="974f1-136">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="974f1-137">打开可用于新项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-137">Open a folder that you can use for a new project.</span></span>

* <span data-ttu-id="974f1-138">在“集成终端”中，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="974f1-138">In the **Integrated Terminal**, run the following command:</span></span>

   ```console
   dotnet new webapp -o SignalRChat
   ```

   [!INCLUDE[](~/includes/webapp-alias-notice.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="974f1-139">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="974f1-139">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="974f1-140">从菜单中选择“文件”>“新建解决方案”。</span><span class="sxs-lookup"><span data-stu-id="974f1-140">From the menu, select **File > New Solution**.</span></span>

* <span data-ttu-id="974f1-141">选择“.NET Core”>“应用”>“ASP.NET Core Web 应用”（请勿选择 ASP.NET Core Web 应用 (MVC)）。</span><span class="sxs-lookup"><span data-stu-id="974f1-141">Select **.NET Core > App > ASP.NET Core Web App** (Don't select **ASP.NET Core Web App (MVC)**).</span></span>

* <span data-ttu-id="974f1-142">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="974f1-142">Select **Next**.</span></span>

* <span data-ttu-id="974f1-143">将项目命名为“SignalRChat”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="974f1-143">Name the project *SignalRChat*, and then select **Create**.</span></span>

---

## <a name="add-the-signalr-client-library"></a><span data-ttu-id="974f1-144">添加 SignalR 客户端库</span><span class="sxs-lookup"><span data-stu-id="974f1-144">Add the SignalR client library</span></span>

<span data-ttu-id="974f1-145">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中包括 SignalR 服务器库。</span><span class="sxs-lookup"><span data-stu-id="974f1-145">The SignalR server library is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="974f1-146">但必须从 npm（即 Node.js 包管理器）获取 JavaScript 客户端库。</span><span class="sxs-lookup"><span data-stu-id="974f1-146">But you have to get the JavaScript client library from npm, the Node.js package manager.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="974f1-147">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974f1-147">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="974f1-148">在“包管理器控制台”(PMC) 中，切换到项目文件夹（其包含 SignalRChat.csproj 文件）。</span><span class="sxs-lookup"><span data-stu-id="974f1-148">In **Package Manager Console** (PMC), change to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

  ```console
  cd SignalRChat
  ```

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="974f1-149">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="974f1-149">Visual Studio Code</span></span>](#tab/visual-studio-code/)

2. <span data-ttu-id="974f1-150">切换到该新项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-150">Change to the new project folder.</span></span>

  ```console
  cd SignalRChat
  ``` 

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="974f1-151">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="974f1-151">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="974f1-152">在“终端”中，导航到项目文件夹（其包含 SignalRChat.csproj 文件）。</span><span class="sxs-lookup"><span data-stu-id="974f1-152">In the **Terminal**, navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

---

* <span data-ttu-id="974f1-153">运行 npm 初始化表达式，以创建 package.json 文件：</span><span class="sxs-lookup"><span data-stu-id="974f1-153">Run the npm initializer to create a *package.json* file:</span></span>

  ```console
  npm init -y
  ```

  <span data-ttu-id="974f1-154">该命令创建类似于以下示例的输出：</span><span class="sxs-lookup"><span data-stu-id="974f1-154">The command creates output similar to the following example:</span></span>

  ```console
  Wrote to C:\tmp\SignalRChat\package.json:
  {
    "name": "SignalRChat",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"0
  }
  ```

* <span data-ttu-id="974f1-155">安装客户端库包：</span><span class="sxs-lookup"><span data-stu-id="974f1-155">Install the client library package:</span></span>

  ```console
  npm install @aspnet/signalr
  ```

  <span data-ttu-id="974f1-156">该命令创建类似于以下示例的输出：</span><span class="sxs-lookup"><span data-stu-id="974f1-156">The command creates output similar to the following example:</span></span>

  ```
  npm notice created a lockfile as package-lock.json. You should commit this file.
  npm WARN signalrchat@1.0.0 No description
  npm WARN signalrchat@1.0.0 No repository field.

  + @aspnet/signalr@1.0.2
  added 1 package in 0.98s
  ```

<span data-ttu-id="974f1-157">`npm install` 命令将 JavaScript 客户端库下载到 node_modules 下的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-157">The `npm install` command downloaded the JavaScript client library to a subfolder under *node_modules*.</span></span> <span data-ttu-id="974f1-158">将其从此处复制到 wwwroot 下的文件夹，以便从聊天应用网页中引用该文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-158">Copy it from there to a folder under *wwwroot* that you can reference from the chat app web page.</span></span>

* <span data-ttu-id="974f1-159">在 wwwroot/lib 中创建 signalr 文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-159">Create a *signalr* folder in *wwwroot/lib*.</span></span>

* <span data-ttu-id="974f1-160">将 signalr.js 文件从 node_modules/@aspnet/signalr/dist/browser 复制到新的 wwwroot/lib/signalr 文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-160">Copy the *signalr.js* file from *node_modules/@aspnet/signalr/dist/browser* to the new *wwwroot/lib/signalr* folder.</span></span>

## <a name="create-the-signalr-hub"></a><span data-ttu-id="974f1-161">创建 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="974f1-161">Create the SignalR hub</span></span>

<span data-ttu-id="974f1-162">[中心](xref:signalr/hubs)是一个类，用作处理客户端 - 服务器通信的高级管道。</span><span class="sxs-lookup"><span data-stu-id="974f1-162">A [hub](xref:signalr/hubs) is a class that serves as a high-level pipeline that handles client-server communication.</span></span>

* <span data-ttu-id="974f1-163">在 SignalRChat 项目文件夹中，创建 Hubs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="974f1-163">In the SignalRChat project folder, create a *Hubs* folder.</span></span>

* <span data-ttu-id="974f1-164">在 Hubs 文件夹中，使用以下代码创建 ChatHub.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="974f1-164">In the *Hubs* folder, create a *ChatHub.cs* file with the following code:</span></span>

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  <span data-ttu-id="974f1-165">`ChatHub` 类继承自 SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) 类。</span><span class="sxs-lookup"><span data-stu-id="974f1-165">The `ChatHub` class inherits from the SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) class.</span></span> <span data-ttu-id="974f1-166">`Hub` 类管理连接、组和消息。</span><span class="sxs-lookup"><span data-stu-id="974f1-166">The `Hub` class manages connections, groups, and messaging.</span></span>

  <span data-ttu-id="974f1-167">任何连接客户端都可以调用 `SendMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="974f1-167">The `SendMessage` method can be called by any connected client.</span></span> <span data-ttu-id="974f1-168">该方法将接收到的消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="974f1-168">It sends the received message to all clients.</span></span> <span data-ttu-id="974f1-169">SignalR 代码是异步模式，可提供最大的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="974f1-169">SignalR code is asynchronous to provide maximum scalability.</span></span>

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="974f1-170">配置项目以使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="974f1-170">Configure the project to use SignalR</span></span>

<span data-ttu-id="974f1-171">必须配置 SignalR 服务器，以将 SignalR 请求传递到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="974f1-171">The SignalR server must be configured to pass SignalR requests to SignalR.</span></span>

* <span data-ttu-id="974f1-172">将以下突出显示的代码添加到 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="974f1-172">Add the following highlighted code to the *Startup.cs* file.</span></span>

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  <span data-ttu-id="974f1-173">这些更改将 SignalR 添加到[依赖关系注入](xref:fundamentals/dependency-injection)系统与[中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="974f1-173">These changes add SignalR to the [dependency injection](xref:fundamentals/dependency-injection) system and the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="974f1-174">创建 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="974f1-174">Create the SignalR client code</span></span>

* <span data-ttu-id="974f1-175">将 Pages\Index.cshtml 中的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="974f1-175">Replace the content in *Pages\Index.cshtml* with the following:</span></span>

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  <span data-ttu-id="974f1-176">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="974f1-176">The preceding code:</span></span>

  * <span data-ttu-id="974f1-177">创建名称以及消息文本的文本框和“提交”按钮。</span><span class="sxs-lookup"><span data-stu-id="974f1-177">Creates text boxes for name and message text, and a submit button.</span></span>
  * <span data-ttu-id="974f1-178">使用 `id="messagesList"` 创建一个列表，用于显示从 SignalR 中心接收的消息。</span><span class="sxs-lookup"><span data-stu-id="974f1-178">Creates a list with `id="messagesList"` for displaying messages that are received from the SignalR hub.</span></span>
  * <span data-ttu-id="974f1-179">包含对 SignalR 的脚本引用以及在下一步中创建的 chat.js 应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="974f1-179">Includes script references to SignalR and the *chat.js* application code that you create in the next step.</span></span>

* <span data-ttu-id="974f1-180">在 wwwroot/js 文件夹中，使用以下代码创建 chat.js 文件：</span><span class="sxs-lookup"><span data-stu-id="974f1-180">In the *wwwroot/js* folder, create a *chat.js* file with the following code:</span></span>

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  <span data-ttu-id="974f1-181">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="974f1-181">The preceding code:</span></span>

  * <span data-ttu-id="974f1-182">创建并启动连接。</span><span class="sxs-lookup"><span data-stu-id="974f1-182">Creates and starts a connection.</span></span>
  * <span data-ttu-id="974f1-183">向“提交”按钮添加一个用于向中心发送消息的处理程序。</span><span class="sxs-lookup"><span data-stu-id="974f1-183">Adds to the submit button a handler that sends messages to the hub.</span></span>
  * <span data-ttu-id="974f1-184">向连接对象添加一个用于从中心接收消息并将其添加到列表的处理程序。</span><span class="sxs-lookup"><span data-stu-id="974f1-184">Adds to the connection object a handler that receives messages from the hub and adds them to the list.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="974f1-185">运行应用</span><span class="sxs-lookup"><span data-stu-id="974f1-185">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="974f1-186">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974f1-186">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="974f1-187">按 Ctrl+F5 可运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="974f1-187">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="974f1-188">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="974f1-188">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="974f1-189">按 Ctrl+F5 可运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="974f1-189">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="974f1-190">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="974f1-190">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="974f1-191">从菜单中选择“运行”>“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="974f1-191">From the menu, select **Run > Start Without Debugging**.</span></span>

---

* <span data-ttu-id="974f1-192">从地址栏复制 URL，打开另一个浏览器实例或选项卡，并在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="974f1-192">Copy the URL from the address bar, open another browser instance or tab, and paste the URL in the address bar.</span></span>

* <span data-ttu-id="974f1-193">选择任一浏览器，输入名称和消息，然后选择“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="974f1-193">Choose either browser, enter a name and message, and select the **Send** button.</span></span>

  <span data-ttu-id="974f1-194">两个页面上立即显示名称和消息。</span><span class="sxs-lookup"><span data-stu-id="974f1-194">The name and message are displayed on both pages instantly.</span></span>

  ![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> <span data-ttu-id="974f1-196">如果应用不起作用，请打开浏览器开发人员工具 (F12) 并转到控制台。</span><span class="sxs-lookup"><span data-stu-id="974f1-196">If the app doesn't work, open your browser developer tools (F12) and go to the console.</span></span> <span data-ttu-id="974f1-197">可能会看到与 HTML 和 JavaScript 代码相关的错误。</span><span class="sxs-lookup"><span data-stu-id="974f1-197">You might see errors related to your HTML and JavaScript code.</span></span> <span data-ttu-id="974f1-198">例如，假设将 signalr.js 放在不同于系统指示的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="974f1-198">For example, suppose you put *signalr.js* in a different folder than directed.</span></span> <span data-ttu-id="974f1-199">在这种情况下，对该文件的引用将不起作用，并且你将在控制台中看到 404 错误。</span><span class="sxs-lookup"><span data-stu-id="974f1-199">In that case the reference to that file won't work and you'll see a 404 error in the console.</span></span>
> <span data-ttu-id="974f1-200">![未找到 signalr.js 错误](signalr/_static/f12-console.png)</span><span class="sxs-lookup"><span data-stu-id="974f1-200">![signalr.js not found error](signalr/_static/f12-console.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="974f1-201">后续步骤</span><span class="sxs-lookup"><span data-stu-id="974f1-201">Next steps</span></span>

<span data-ttu-id="974f1-202">如果希望客户端从不同的域连接到 SignalR 应用，则必须启用跨域资源共享 (CORS)。</span><span class="sxs-lookup"><span data-stu-id="974f1-202">If you want clients to connect to a SignalR app from different domains, you have to enable Cross-Origin Resource Sharing (CORS).</span></span> <span data-ttu-id="974f1-203">有关详细信息，请参阅[跨域资源共享](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing)。</span><span class="sxs-lookup"><span data-stu-id="974f1-203">For more information, see [Cross-origin resource sharing](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing).</span></span>

<span data-ttu-id="974f1-204">若要了解有关 SignalR、中心和 JavaScript 客户端的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="974f1-204">To learn more about SignalR, hubs, and JavaScript clients, see these resources:</span></span>

* [<span data-ttu-id="974f1-205">适用于 ASP.NET Core 的 SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="974f1-205">Introduction to SignalR for ASP.NET Core</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="974f1-206">使用适用于 ASP.NET Core 的 SignalR 中的中心</span><span class="sxs-lookup"><span data-stu-id="974f1-206">Use hubs in SignalR for ASP.NET Core</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="974f1-207">ASP.NET Core SignalR JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="974f1-207">ASP.NET Core SignalR JavaScript client</span></span>](xref:signalr/javascript-client)
