---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 教程： 开始使用 SignalR 1.x |Microsoft 文档
author: pfletcher
description: 使用 ASP.NET SignalR 生成 HTML 页中的实时聊天应用程序。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: ce4953a0abf64af28ef4dbc5a62bb2d989343d99
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28044729"
---
<a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="e48d9-103">教程： 开始使用 SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="e48d9-103">Tutorial: Getting Started with SignalR 1.x</span></span>
====================
<span data-ttu-id="e48d9-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="e48d9-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

> <span data-ttu-id="e48d9-105">本教程介绍如何使用 SignalR 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="e48d9-106">你将添加到空的 ASP.NET web 应用程序的 SignalR 和创建 HTML 页以便发送并显示消息。</span><span class="sxs-lookup"><span data-stu-id="e48d9-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>


## <a name="overview"></a><span data-ttu-id="e48d9-107">概述</span><span class="sxs-lookup"><span data-stu-id="e48d9-107">Overview</span></span>

<span data-ttu-id="e48d9-108">本教程介绍如何构建一个简单的基于浏览器的聊天应用程序通过引入了 SignalR 开发。</span><span class="sxs-lookup"><span data-stu-id="e48d9-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="e48d9-109">将 SignalR 库添加到空的 ASP.NET web 应用程序，创建一个中心类，将消息发送到客户端，并创建 HTML 页，从而让用户发送和接收聊天消息。</span><span class="sxs-lookup"><span data-stu-id="e48d9-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="e48d9-110">有关演示如何在 MVC 4 中创建的聊天应用程序使用的 MVC 视图的类似教程，请参阅[开始使用 SignalR 和 MVC 4](index.md)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e48d9-111">本教程使用 SignalR 的版本 (1.x) 版本。</span><span class="sxs-lookup"><span data-stu-id="e48d9-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="e48d9-112">有关 SignalR 之间的更改的详细信息 1.x 和 2.0，请参阅[升级 SignalR 1.x 项目](../releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="e48d9-113">SignalR 是用于构建 web 应用程序需要实时用户交互或实时数据更新一个开放源代码.NET 库。</span><span class="sxs-lookup"><span data-stu-id="e48d9-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="e48d9-114">示例包括社交应用程序、 多用户游戏、 业务协作和新闻，天气或财务更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="e48d9-115">这些通常称为实时应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-115">These are often called real-time applications.</span></span>

<span data-ttu-id="e48d9-116">SignalR 简化了生成实时应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="e48d9-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="e48d9-117">它包括 ASP.NET server 库和一个要更加轻松地管理客户端-服务器连接并将内容更新推送到客户端的 JavaScript 客户端库。</span><span class="sxs-lookup"><span data-stu-id="e48d9-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="e48d9-118">可以将 SignalR 库添加到现有的 ASP.NET 应用程序，以获取实时功能。</span><span class="sxs-lookup"><span data-stu-id="e48d9-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="e48d9-119">本教程演示了下列 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="e48d9-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="e48d9-120">将 SignalR 库添加到 ASP.NET web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="e48d9-121">创建用于将内容推送到客户端的中心类。</span><span class="sxs-lookup"><span data-stu-id="e48d9-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="e48d9-122">使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="e48d9-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="e48d9-123">下面的屏幕截图显示在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="e48d9-124">每个新用户可以发表评论，并查看添加用户加入聊天后的注释。</span><span class="sxs-lookup"><span data-stu-id="e48d9-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![聊天实例](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="e48d9-126">各节：</span><span class="sxs-lookup"><span data-stu-id="e48d9-126">Sections:</span></span>

- [<span data-ttu-id="e48d9-127">将项目设置</span><span class="sxs-lookup"><span data-stu-id="e48d9-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="e48d9-128">运行示例</span><span class="sxs-lookup"><span data-stu-id="e48d9-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="e48d9-129">检查代码</span><span class="sxs-lookup"><span data-stu-id="e48d9-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="e48d9-130">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e48d9-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="e48d9-131">将项目设置</span><span class="sxs-lookup"><span data-stu-id="e48d9-131">Set up the Project</span></span>

<span data-ttu-id="e48d9-132">本部分演示如何创建空的 ASP.NET web 应用程序，添加 SignalR，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="e48d9-133">先决条件：</span><span class="sxs-lookup"><span data-stu-id="e48d9-133">Prerequisites:</span></span>

- <span data-ttu-id="e48d9-134">Visual Studio 2010 SP1 或 2012年。</span><span class="sxs-lookup"><span data-stu-id="e48d9-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="e48d9-135">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2012 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="e48d9-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="e48d9-136">[Microsoft ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="e48d9-137">对于 Visual Studio 2012，此安装程序将添加新的 ASP.NET 功能包括到 Visual Studio 的 SignalR 模板。</span><span class="sxs-lookup"><span data-stu-id="e48d9-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="e48d9-138">对于 Visual Studio 2010 SP1，安装程序不可用，但你可以通过安装 SignalR NuGet 包的安装步骤中所述完成本教程。</span><span class="sxs-lookup"><span data-stu-id="e48d9-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="e48d9-139">以下步骤使用 Visual Studio 2012 创建 ASP.NET 空 Web 应用程序并将添加 SignalR 库：</span><span class="sxs-lookup"><span data-stu-id="e48d9-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="e48d9-140">在 Visual Studio 中创建 ASP.NET 空 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![创建空 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="e48d9-142">打开**程序包管理器控制台**通过选择**工具 |库包管理器 |程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-142">Open the **Package Manager Console** by selecting **Tools | Library Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="e48d9-143">控制台窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e48d9-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="e48d9-144">此命令将安装 SignalR 的最新版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="e48d9-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="e48d9-145">在**解决方案资源管理器**，右键单击项目，选择**添加 |类**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="e48d9-146">将新类**ChatHub**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="e48d9-147">在**解决方案资源管理器**展开脚本节点。</span><span class="sxs-lookup"><span data-stu-id="e48d9-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="e48d9-148">用于 jQuery 和 SignalR 的脚本库是在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="e48d9-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![库引用](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="e48d9-150">中的代码替换**ChatHub**类替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e48d9-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="e48d9-151">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="e48d9-152">在**添加新项**对话框中，选择**全局应用程序类**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![添加全局](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="e48d9-154">添加以下`using`后面提供语句`using`Global.asax.cs 类中的语句。</span><span class="sxs-lookup"><span data-stu-id="e48d9-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="e48d9-155">添加以下行中的代码`Application_Start`要注册的默认路径为 SignalR 集线器的全局类的方法。</span><span class="sxs-lookup"><span data-stu-id="e48d9-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="e48d9-156">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="e48d9-157">在**添加新项**对话框，选择 Html 页，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="e48d9-158">在**解决方案资源管理器**，右键单击你刚刚创建的 HTML 页面，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="e48d9-159">在 HTML 页中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e48d9-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="e48d9-160">**保存所有**项目。</span><span class="sxs-lookup"><span data-stu-id="e48d9-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="e48d9-161">运行示例</span><span class="sxs-lookup"><span data-stu-id="e48d9-161">Run the Sample</span></span>

1. <span data-ttu-id="e48d9-162">按 F5 以在调试模式下运行该项目。</span><span class="sxs-lookup"><span data-stu-id="e48d9-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="e48d9-163">HTML 页加载中的浏览器实例并提示输入用户名。</span><span class="sxs-lookup"><span data-stu-id="e48d9-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="e48d9-165">输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="e48d9-165">Enter a user name.</span></span>
3. <span data-ttu-id="e48d9-166">从浏览器的地址行中复制 URL，并使用它来打开两个多个浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="e48d9-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="e48d9-167">在每个浏览器实例中，输入唯一的用户名。</span><span class="sxs-lookup"><span data-stu-id="e48d9-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="e48d9-168">在每个浏览器实例中，添加注释并单击**发送**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="e48d9-169">注释应该显示在所有浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="e48d9-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e48d9-170">此简单的聊天应用程序不维护服务器上的讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="e48d9-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="e48d9-171">中心广播到所有当前用户的注释。</span><span class="sxs-lookup"><span data-stu-id="e48d9-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="e48d9-172">加入这次聊天更高版本的用户将看到消息从时间添加加入。</span><span class="sxs-lookup"><span data-stu-id="e48d9-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="e48d9-173">下面的屏幕快照显示三个浏览器实例，所有这些更新时将消息发送的一个实例中运行的聊天应用程序：</span><span class="sxs-lookup"><span data-stu-id="e48d9-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="e48d9-175">在**解决方案资源管理器**，检查**脚本文档**运行的应用程序的节点。</span><span class="sxs-lookup"><span data-stu-id="e48d9-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="e48d9-176">没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。</span><span class="sxs-lookup"><span data-stu-id="e48d9-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="e48d9-177">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="e48d9-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![生成的中心脚本](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="e48d9-179">检查代码</span><span class="sxs-lookup"><span data-stu-id="e48d9-179">Examine the Code</span></span>

<span data-ttu-id="e48d9-180">SignalR 聊天应用程序演示两个基本的 SignalR 开发任务： 与主协调对象在服务器上，创建一个中心并使用 SignalR jQuery 库来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="e48d9-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="e48d9-181">SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="e48d9-181">SignalR Hubs</span></span>

<span data-ttu-id="e48d9-182">中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。</span><span class="sxs-lookup"><span data-stu-id="e48d9-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="e48d9-183">派生自**中心**类是提供有用的方法来构建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="e48d9-184">你可以在您的中心类上创建公共方法，然后通过调用这些方法从 web 页中的 jQuery 脚本中访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="e48d9-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="e48d9-185">在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。</span><span class="sxs-lookup"><span data-stu-id="e48d9-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="e48d9-186">中心反过来将消息发送到所有客户端，通过调用**Clients.All.broadcastMessage**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="e48d9-187">**发送**方法演示了多个中心概念：</span><span class="sxs-lookup"><span data-stu-id="e48d9-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="e48d9-188">公共方法声明的中心，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="e48d9-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="e48d9-189">使用**Microsoft.AspNet.SignalR.Hub.Clients**动态属性来访问所有客户端连接到此集线器。</span><span class="sxs-lookup"><span data-stu-id="e48d9-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="e48d9-190">客户端上调用 jQuery 函数 (如`broadcastMessage`函数) 来更新客户端。</span><span class="sxs-lookup"><span data-stu-id="e48d9-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="e48d9-191">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="e48d9-191">SignalR and jQuery</span></span>

<span data-ttu-id="e48d9-192">HTML 页中的代码示例演示如何使用 SignalR jQuery 库与 SignalR hub 进行通信。</span><span class="sxs-lookup"><span data-stu-id="e48d9-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="e48d9-193">在代码中的基本任务声明一个代理，以引用的中心，声明该服务器可以将内容推送到客户端，调用的函数和启动的连接将消息发送到中心。</span><span class="sxs-lookup"><span data-stu-id="e48d9-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="e48d9-194">下面的代码声明一个中心的代理。</span><span class="sxs-lookup"><span data-stu-id="e48d9-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="e48d9-195">在 jQuery 到的服务器类及其成员的引用位于 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="e48d9-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="e48d9-196">引用的代码示例的 C# **ChatHub**类中作为 jQuery **chatHub**。</span><span class="sxs-lookup"><span data-stu-id="e48d9-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>


<span data-ttu-id="e48d9-197">下面的代码是如何在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="e48d9-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="e48d9-198">在服务器上的中心类调用此函数可将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="e48d9-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="e48d9-199">HTML 对内容编码显示之前的两行都是可选的并显示一种简单的方法，以防止脚本注入。</span><span class="sxs-lookup"><span data-stu-id="e48d9-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="e48d9-200">下面的代码演示如何使用中心打开连接。</span><span class="sxs-lookup"><span data-stu-id="e48d9-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="e48d9-201">代码启动连接，然后将它传递函数来处理 click 事件上**发送**在 HTML 页的按钮。</span><span class="sxs-lookup"><span data-stu-id="e48d9-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="e48d9-202">此方法将确保事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="e48d9-202">This approach insures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e48d9-203">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e48d9-203">Next Steps</span></span>

<span data-ttu-id="e48d9-204">你已了解 SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e48d9-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="e48d9-205">你还了解了多个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建一个中心类，以及如何发送和从中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="e48d9-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="e48d9-206">你可以使示例应用程序在本教程或其他 SignalR 应用程序可通过 Internet 将它们部署到托管提供商。</span><span class="sxs-lookup"><span data-stu-id="e48d9-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="e48d9-207">Microsoft 提供了可用的 web 宿主中可用的最多 10 个网站[Windows Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="e48d9-208">有关如何部署示例 SignalR 应用程序的演练，请参阅[发布 SignalR 入门示例作为 Windows Azure 网站](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="e48d9-209">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[部署 ASP.NET 应用程序到 Windows Azure 网站](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e48d9-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="e48d9-210">(注意： WebSocket 传输目前不支持为 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="e48d9-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="e48d9-211">当 WebSocket 传输不可用，SignalR 使用其他可用传输的传输部分中所述[简介 SignalR 主题](index.md)。)</span><span class="sxs-lookup"><span data-stu-id="e48d9-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="e48d9-212">若要了解更多高级的 SignalR 最新开发进展概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="e48d9-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="e48d9-213">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="e48d9-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="e48d9-214">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="e48d9-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="e48d9-215">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="e48d9-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
