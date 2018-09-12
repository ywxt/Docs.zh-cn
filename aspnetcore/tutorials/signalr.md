---
title: 教程：开始在 ASP.NET Core 上使用 SignalR
author: tdykstra
description: 在本教程中，创建使用适用于 ASP.NET Core 的 SignalR 的聊天应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/31/2018
uid: tutorials/signalr
ms.openlocfilehash: 6d96331a4630f766ca11edb056fd3e13b52b6ae4
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893160"
---
# <a name="tutorial-get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="e26bc-103">教程：开始在 ASP.NET Core 上使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="e26bc-103">Tutorial: Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="e26bc-104">本教程介绍生成使用 SignalR 的实时应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="e26bc-104">This tutorial teaches the basics of building a real-time app using SignalR.</span></span> <span data-ttu-id="e26bc-105">您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="e26bc-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e26bc-106">创建在 ASP.NET Core 上使用 SignalR 的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="e26bc-106">Create a web app that uses SignalR on ASP.NET Core.</span></span>
> * <span data-ttu-id="e26bc-107">在服务器上创建 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="e26bc-107">Create a SignalR hub on the server.</span></span>
> * <span data-ttu-id="e26bc-108">从 JavaScript 客户端连接到 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="e26bc-108">Connect to the SignalR hub from JavaScript clients.</span></span>
> * <span data-ttu-id="e26bc-109">使用此中心将消息从任何客户端发送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="e26bc-109">Use the hub to send messages from any client to all connected clients.</span></span>

<span data-ttu-id="e26bc-110">最终将创建一个正常运行的聊天应用：</span><span class="sxs-lookup"><span data-stu-id="e26bc-110">At the end, you'll have a working chat app:</span></span>

![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="e26bc-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="e26bc-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e26bc-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="e26bc-113">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="e26bc-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26bc-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="e26bc-115">已安装“ASP.NET 和 Web 开发”工作负载的 [Visual Studio 2017 版本 15.8 或更高版本](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e26bc-115">[Visual Studio 2017 version 15.8 or later](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="e26bc-116">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="e26bc-116">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="e26bc-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e26bc-117">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="e26bc-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e26bc-118">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="e26bc-119">.NET Core SDK 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="e26bc-119">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="e26bc-120">用于 Visual Studio Code 的 C#</span><span class="sxs-lookup"><span data-stu-id="e26bc-120">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="e26bc-121">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="e26bc-121">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="e26bc-122">Visual Studio for Mac 7.5.4 版或更高版本</span><span class="sxs-lookup"><span data-stu-id="e26bc-122">Visual Studio for Mac version 7.5.4 or later</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="e26bc-123">[.NET Core SDK 2.1 或更高版本](https://www.microsoft.com/net/download/all)（包含在 Visual Studio 安装中）</span><span class="sxs-lookup"><span data-stu-id="e26bc-123">[.NET Core SDK 2.1 or later](https://www.microsoft.com/net/download/all) (included in the Visual Studio install)</span></span>

---

## <a name="create-the-project"></a><span data-ttu-id="e26bc-124">创建项目</span><span class="sxs-lookup"><span data-stu-id="e26bc-124">Create the project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="e26bc-125">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26bc-125">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="e26bc-126">从菜单中选择“文件”>“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-126">From the menu, select **File > New Project**.</span></span>

* <span data-ttu-id="e26bc-127">在“新建项目”对话框中，选择“已安装”>“Visual C#”>“Web”>“ASP.NET Core Web 应用”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-127">In the **New Project** dialog, select **Installed > Visual C# > Web > ASP.NET Core Web Application**.</span></span> <span data-ttu-id="e26bc-128">将项目命名为“SignalRChat”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-128">Name the project *SignalRChat*.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-dialog.png)

* <span data-ttu-id="e26bc-130">选择“Web 应用”，以创建使用 Razor Pages 的项目。</span><span class="sxs-lookup"><span data-stu-id="e26bc-130">Select **Web Application** to create a project that uses Razor Pages.</span></span>

* <span data-ttu-id="e26bc-131">选择 .NET Core 的目标框架，选择 ASP.NET Core 2.1，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-131">Select a target framework of **.NET Core**, select **ASP.NET Core 2.1**, and click **OK**.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="e26bc-133">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e26bc-133">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="e26bc-134">打开可用于新项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e26bc-134">Open a folder that you can use for a new project.</span></span>

* <span data-ttu-id="e26bc-135">在“集成终端”中，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e26bc-135">In the **Integrated Terminal**, run the following command:</span></span>

   ```console
   dotnet new webapp -o SignalRChat
   ```

   [!INCLUDE[](~/includes/webapp-alias-notice.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="e26bc-136">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="e26bc-136">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="e26bc-137">从菜单中选择“文件”>“新建解决方案”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-137">From the menu, select **File > New Solution**.</span></span>

* <span data-ttu-id="e26bc-138">选择“.NET Core”>“应用”>“ASP.NET Core Web 应用”（请勿选择 ASP.NET Core Web 应用 (MVC)）。</span><span class="sxs-lookup"><span data-stu-id="e26bc-138">Select **.NET Core > App > ASP.NET Core Web App** (Don't select **ASP.NET Core Web App (MVC)**).</span></span>

* <span data-ttu-id="e26bc-139">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-139">Select **Next**.</span></span>

* <span data-ttu-id="e26bc-140">将项目命名为“SignalRChat”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-140">Name the project *SignalRChat*, and then select **Create**.</span></span>

---

## <a name="add-the-signalr-client-library"></a><span data-ttu-id="e26bc-141">添加 SignalR 客户端库</span><span class="sxs-lookup"><span data-stu-id="e26bc-141">Add the SignalR client library</span></span>

<span data-ttu-id="e26bc-142">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中包括 SignalR 服务器库。</span><span class="sxs-lookup"><span data-stu-id="e26bc-142">The SignalR server library is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="e26bc-143">JavaScript 客户端库不会自动包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="e26bc-143">The JavaScript client library isn't automatically included in the project.</span></span> <span data-ttu-id="e26bc-144">对于此教程，使用[库管理器 (LibMan)](xref:client-side/libman/index) 从 unpkg 获取客户端库。</span><span class="sxs-lookup"><span data-stu-id="e26bc-144">For this tutorial, you use [Library Manager (LibMan)](xref:client-side/libman/index) to get the client library from *unpkg*.</span></span> <span data-ttu-id="e26bc-145">[unpkg](https://unpkg.com/#/) 是一个[内容分发网络](https://wikipedia.org/wiki/Content_delivery_network)，可以分发在 [npm：Node.js 包管理器](https://www.npmjs.com/get-npm)中找到的任何内容。</span><span class="sxs-lookup"><span data-stu-id="e26bc-145">[unpkg](https://unpkg.com/#/) is a [content delivery network](https://wikipedia.org/wiki/Content_delivery_network) that can deliver anything found in [npm, the Node.js package manager](https://www.npmjs.com/get-npm).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="e26bc-146">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26bc-146">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="e26bc-147">在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “客户端库”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-147">In **Solution Explorer**, right-click the project, and select **Add** > **Client-Side Library**.</span></span>

* <span data-ttu-id="e26bc-148">在“添加客户端库”对话框中，对于“提供程序”，选择“unpkg”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-148">In the **Add Client-Side Library** dialog, for **Provider** select **unpkg**.</span></span> 

* <span data-ttu-id="e26bc-149">对于“库”，输入 @aspnet/signalr@1，然后选择不是预览版的最新版本。</span><span class="sxs-lookup"><span data-stu-id="e26bc-149">For **Library**, enter _@aspnet/signalr@1_, and select the latest version that isn't preview.</span></span>

  ![“添加客户端库”对话框 - 选择库](signalr/_static/libman1.png)

* <span data-ttu-id="e26bc-151">选择“选择特定文件”，展开“dist/browser”文件夹，然后选择“signalr.js”和“signalr.min.js”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-151">Select **Choose specific files**, expand the *dist/browser* folder, and select *signalr.js* and *signalr.min.js*.</span></span>

* <span data-ttu-id="e26bc-152">将“目标位置”设置为 wwwroot/lib/signalr/，然后选择“安装”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-152">Set **Target Location** to *wwwroot/lib/signalr/*, and select **Install**.</span></span>

  ![“添加客户端库”对话框 - 选择文件和目标](signalr/_static/libman2.png)

  <span data-ttu-id="e26bc-154">[LibMan](xref:client-side/libman/index) 创建 wwwroot/lib/signalr 文件夹并将所选文件复制到该文件夹。</span><span class="sxs-lookup"><span data-stu-id="e26bc-154">[LibMan](xref:client-side/libman/index) creates a *wwwroot/lib/signalr* folder and copies the selected files to it.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="e26bc-155">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e26bc-155">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="e26bc-156">在“集成终端”中，运行以下命令以安装 LibMan。</span><span class="sxs-lookup"><span data-stu-id="e26bc-156">In the **Integrated Terminal**, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="e26bc-157">导航到项目文件夹（包含 SignalRChat.csproj 文件的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="e26bc-157">Navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

* <span data-ttu-id="e26bc-158">使用 LibMan 运行以下命令，以获取 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="e26bc-158">Run the following command to get the SignalR client library by using LibMan.</span></span> <span data-ttu-id="e26bc-159">可能需要等待几秒钟的时间才能看到输出。</span><span class="sxs-lookup"><span data-stu-id="e26bc-159">You might have to wait a few seconds before seeing output.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot\lib\signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="e26bc-160">参数指定以下选项：</span><span class="sxs-lookup"><span data-stu-id="e26bc-160">The parameters specify the following options:</span></span>
  * <span data-ttu-id="e26bc-161">使用 unpkg 提供程序。</span><span class="sxs-lookup"><span data-stu-id="e26bc-161">Use the unpkg provider.</span></span>
  * <span data-ttu-id="e26bc-162">将文件复制到 wwwroot/lib/signalr 目标。</span><span class="sxs-lookup"><span data-stu-id="e26bc-162">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="e26bc-163">仅复制指定的文件。</span><span class="sxs-lookup"><span data-stu-id="e26bc-163">Copy only the specified files.</span></span>

  <span data-ttu-id="e26bc-164">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="e26bc-164">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot\lib\signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="e26bc-165">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="e26bc-165">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="e26bc-166">在“终端”中，运行以下命令以安装 LibMan。</span><span class="sxs-lookup"><span data-stu-id="e26bc-166">In the **Terminal**, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="e26bc-167">导航到项目文件夹（包含 SignalRChat.csproj 文件的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="e26bc-167">Navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

* <span data-ttu-id="e26bc-168">使用 LibMan 运行以下命令，以获取 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="e26bc-168">Run the following command to get the SignalR client library by using LibMan.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot\lib\signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="e26bc-169">参数指定以下选项：</span><span class="sxs-lookup"><span data-stu-id="e26bc-169">The parameters specify the following options:</span></span>
  * <span data-ttu-id="e26bc-170">使用 unpkg 提供程序。</span><span class="sxs-lookup"><span data-stu-id="e26bc-170">Use the unpkg provider.</span></span>
  * <span data-ttu-id="e26bc-171">将文件复制到 wwwroot/lib/signalr 目标。</span><span class="sxs-lookup"><span data-stu-id="e26bc-171">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="e26bc-172">仅复制指定的文件。</span><span class="sxs-lookup"><span data-stu-id="e26bc-172">Copy only the specified files.</span></span>

  <span data-ttu-id="e26bc-173">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="e26bc-173">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot\lib\signalr"
  ```

---

## <a name="create-the-signalr-hub"></a><span data-ttu-id="e26bc-174">创建 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="e26bc-174">Create the SignalR hub</span></span>

<span data-ttu-id="e26bc-175">[中心](xref:signalr/hubs)是一个类，用作处理客户端 - 服务器通信的高级管道。</span><span class="sxs-lookup"><span data-stu-id="e26bc-175">A [hub](xref:signalr/hubs) is a class that serves as a high-level pipeline that handles client-server communication.</span></span>

* <span data-ttu-id="e26bc-176">在 SignalRChat 项目文件夹中，创建 Hubs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e26bc-176">In the SignalRChat project folder, create a *Hubs* folder.</span></span>

* <span data-ttu-id="e26bc-177">在 Hubs 文件夹中，使用以下代码创建 ChatHub.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="e26bc-177">In the *Hubs* folder, create a *ChatHub.cs* file with the following code:</span></span>

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  <span data-ttu-id="e26bc-178">`ChatHub` 类继承自 SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) 类。</span><span class="sxs-lookup"><span data-stu-id="e26bc-178">The `ChatHub` class inherits from the SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) class.</span></span> <span data-ttu-id="e26bc-179">`Hub` 类管理连接、组和消息。</span><span class="sxs-lookup"><span data-stu-id="e26bc-179">The `Hub` class manages connections, groups, and messaging.</span></span>

  <span data-ttu-id="e26bc-180">任何连接客户端都可以调用 `SendMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="e26bc-180">The `SendMessage` method can be called by any connected client.</span></span> <span data-ttu-id="e26bc-181">该方法将接收到的消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="e26bc-181">It sends the received message to all clients.</span></span> <span data-ttu-id="e26bc-182">SignalR 代码是异步模式，可提供最大的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="e26bc-182">SignalR code is asynchronous to provide maximum scalability.</span></span>

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="e26bc-183">配置项目以使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="e26bc-183">Configure the project to use SignalR</span></span>

<span data-ttu-id="e26bc-184">必须配置 SignalR 服务器，以将 SignalR 请求传递到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="e26bc-184">The SignalR server must be configured to pass SignalR requests to SignalR.</span></span>

* <span data-ttu-id="e26bc-185">将以下突出显示的代码添加到 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="e26bc-185">Add the following highlighted code to the *Startup.cs* file.</span></span>

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  <span data-ttu-id="e26bc-186">这些更改将 SignalR 添加到[依赖关系注入](xref:fundamentals/dependency-injection)系统与[中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="e26bc-186">These changes add SignalR to the [dependency injection](xref:fundamentals/dependency-injection) system and the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="e26bc-187">创建 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="e26bc-187">Create the SignalR client code</span></span>

* <span data-ttu-id="e26bc-188">使用以下代码替换 Pages\Index.cshtml 中的内容：</span><span class="sxs-lookup"><span data-stu-id="e26bc-188">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  <span data-ttu-id="e26bc-189">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="e26bc-189">The preceding code:</span></span>

  * <span data-ttu-id="e26bc-190">创建名称以及消息文本的文本框和“提交”按钮。</span><span class="sxs-lookup"><span data-stu-id="e26bc-190">Creates text boxes for name and message text, and a submit button.</span></span>
  * <span data-ttu-id="e26bc-191">使用 `id="messagesList"` 创建一个列表，用于显示从 SignalR 中心接收的消息。</span><span class="sxs-lookup"><span data-stu-id="e26bc-191">Creates a list with `id="messagesList"` for displaying messages that are received from the SignalR hub.</span></span>
  * <span data-ttu-id="e26bc-192">包含对 SignalR 的脚本引用以及在下一步中创建的 chat.js 应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="e26bc-192">Includes script references to SignalR and the *chat.js* application code that you create in the next step.</span></span>

* <span data-ttu-id="e26bc-193">在 wwwroot/js 文件夹中，使用以下代码创建 chat.js 文件：</span><span class="sxs-lookup"><span data-stu-id="e26bc-193">In the *wwwroot/js* folder, create a *chat.js* file with the following code:</span></span>

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  <span data-ttu-id="e26bc-194">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="e26bc-194">The preceding code:</span></span>

  * <span data-ttu-id="e26bc-195">创建并启动连接。</span><span class="sxs-lookup"><span data-stu-id="e26bc-195">Creates and starts a connection.</span></span>
  * <span data-ttu-id="e26bc-196">向“提交”按钮添加一个用于向中心发送消息的处理程序。</span><span class="sxs-lookup"><span data-stu-id="e26bc-196">Adds to the submit button a handler that sends messages to the hub.</span></span>
  * <span data-ttu-id="e26bc-197">向连接对象添加一个用于从中心接收消息并将其添加到列表的处理程序。</span><span class="sxs-lookup"><span data-stu-id="e26bc-197">Adds to the connection object a handler that receives messages from the hub and adds them to the list.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="e26bc-198">运行应用</span><span class="sxs-lookup"><span data-stu-id="e26bc-198">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="e26bc-199">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26bc-199">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="e26bc-200">按 Ctrl+F5 可运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="e26bc-200">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="e26bc-201">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e26bc-201">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="e26bc-202">按 Ctrl+F5 可运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="e26bc-202">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="e26bc-203">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="e26bc-203">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="e26bc-204">从菜单中选择“运行”>“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="e26bc-204">From the menu, select **Run > Start Without Debugging**.</span></span>

---

* <span data-ttu-id="e26bc-205">从地址栏复制 URL，打开另一个浏览器实例或选项卡，并在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="e26bc-205">Copy the URL from the address bar, open another browser instance or tab, and paste the URL in the address bar.</span></span>

* <span data-ttu-id="e26bc-206">选择任一浏览器，输入名称和消息，然后选择“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="e26bc-206">Choose either browser, enter a name and message, and select the **Send** button.</span></span>

  <span data-ttu-id="e26bc-207">两个页面上立即显示名称和消息。</span><span class="sxs-lookup"><span data-stu-id="e26bc-207">The name and message are displayed on both pages instantly.</span></span>

  ![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> <span data-ttu-id="e26bc-209">如果应用不起作用，请打开浏览器开发人员工具 (F12) 并转到控制台。</span><span class="sxs-lookup"><span data-stu-id="e26bc-209">If the app doesn't work, open your browser developer tools (F12) and go to the console.</span></span> <span data-ttu-id="e26bc-210">可能会看到与 HTML 和 JavaScript 代码相关的错误。</span><span class="sxs-lookup"><span data-stu-id="e26bc-210">You might see errors related to your HTML and JavaScript code.</span></span> <span data-ttu-id="e26bc-211">例如，假设将 signalr.js 放在不同于系统指示的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e26bc-211">For example, suppose you put *signalr.js* in a different folder than directed.</span></span> <span data-ttu-id="e26bc-212">在这种情况下，对该文件的引用将不起作用，并且你将在控制台中看到 404 错误。</span><span class="sxs-lookup"><span data-stu-id="e26bc-212">In that case the reference to that file won't work and you'll see a 404 error in the console.</span></span>
> <span data-ttu-id="e26bc-213">![未找到 signalr.js 错误](signalr/_static/f12-console.png)</span><span class="sxs-lookup"><span data-stu-id="e26bc-213">![signalr.js not found error](signalr/_static/f12-console.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26bc-214">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e26bc-214">Next steps</span></span>

<span data-ttu-id="e26bc-215">如果希望客户端从不同的域连接到 SignalR 应用，则必须启用跨域资源共享 (CORS)。</span><span class="sxs-lookup"><span data-stu-id="e26bc-215">If you want clients to connect to a SignalR app from different domains, you have to enable Cross-Origin Resource Sharing (CORS).</span></span> <span data-ttu-id="e26bc-216">有关详细信息，请参阅[跨域资源共享](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing)。</span><span class="sxs-lookup"><span data-stu-id="e26bc-216">For more information, see [Cross-origin resource sharing](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing).</span></span>

<span data-ttu-id="e26bc-217">若要了解有关 SignalR、中心和 JavaScript 客户端的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e26bc-217">To learn more about SignalR, hubs, and JavaScript clients, see these resources:</span></span>

* [<span data-ttu-id="e26bc-218">适用于 ASP.NET Core 的 SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="e26bc-218">Introduction to SignalR for ASP.NET Core</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="e26bc-219">使用适用于 ASP.NET Core 的 SignalR 中的中心</span><span class="sxs-lookup"><span data-stu-id="e26bc-219">Use hubs in SignalR for ASP.NET Core</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="e26bc-220">ASP.NET Core SignalR JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="e26bc-220">ASP.NET Core SignalR JavaScript client</span></span>](xref:signalr/javascript-client)
