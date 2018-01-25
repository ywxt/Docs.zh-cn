---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: "教程： 开始使用 SignalR 2 |Microsoft 文档"
author: pfletcher
description: "本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加空的 ASP.NET web 应用程序，并创建 HTML pa..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8be851f5a2b1cca39f5f8f284ff1c002c486d7e8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="tutorial-getting-started-with-signalr-2"></a><span data-ttu-id="6fb9c-104">教程： 开始使用 SignalR 2</span><span class="sxs-lookup"><span data-stu-id="6fb9c-104">Tutorial: Getting Started with SignalR 2</span></span>
====================
<span data-ttu-id="6fb9c-105">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="6fb9c-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="6fb9c-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="6fb9c-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

> <span data-ttu-id="6fb9c-107">本教程介绍如何使用 SignalR 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-107">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="6fb9c-108">你将添加到空的 ASP.NET web 应用程序的 SignalR 和创建 HTML 页以便发送并显示消息。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-108">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6fb9c-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6fb9c-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="6fb9c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6fb9c-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="6fb9c-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6fb9c-111">.NET 4.5</span></span>
> - <span data-ttu-id="6fb9c-112">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="6fb9c-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="6fb9c-113">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6fb9c-113">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="6fb9c-114">若要使用本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-114">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="6fb9c-115">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)的最新版本。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-115">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="6fb9c-116">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-116">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="6fb9c-117">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web Tools for Visual Studio 2012 的 2013.1**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-117">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="6fb9c-118">这将安装 SignalR 类的 Visual Studio 模板，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-118">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="6fb9c-119">某些模板 (如**OWIN Startup 类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-119">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="6fb9c-120">教程版本</span><span class="sxs-lookup"><span data-stu-id="6fb9c-120">Tutorial versions</span></span>
> 
> <span data-ttu-id="6fb9c-121">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-121">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="6fb9c-122">问题和意见</span><span class="sxs-lookup"><span data-stu-id="6fb9c-122">Questions and comments</span></span>
> 
> <span data-ttu-id="6fb9c-123">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-123">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6fb9c-124">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-124">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="6fb9c-125">概述</span><span class="sxs-lookup"><span data-stu-id="6fb9c-125">Overview</span></span>

<span data-ttu-id="6fb9c-126">本教程介绍如何构建一个简单的基于浏览器的聊天应用程序通过引入了 SignalR 开发。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-126">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="6fb9c-127">将 SignalR 库添加到空的 ASP.NET web 应用程序，创建一个中心类，将消息发送到客户端，并创建 HTML 页，从而让用户发送和接收聊天消息。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-127">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="6fb9c-128">有关演示如何在 MVC 5 中创建的聊天应用程序使用的 MVC 视图的类似教程，请参阅[SignalR 2 和 MVC 5 入门](tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-128">For a similar tutorial that shows how to create a chat application in MVC 5 using an MVC view, see [Getting Started with SignalR 2 and MVC 5](tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6fb9c-129">本教程演示如何在版本 2 中创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-129">This tutorial demonstrates how to create SignalR applications in version 2.</span></span> <span data-ttu-id="6fb9c-130">有关 SignalR 之间的更改的详细信息 1.x 和 2，请参阅[升级 SignalR 1.x 项目](../releases/upgrading-signalr-1x-projects-to-20.md)和[Visual Studio 2013 发行说明](../../../visual-studio/overview/2013/release-notes.md#TOC13)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-130">For details on changes between SignalR 1.x and 2, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md) and [Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md#TOC13).</span></span>

<span data-ttu-id="6fb9c-131">SignalR 是用于构建 web 应用程序需要实时用户交互或实时数据更新一个开放源代码.NET 库。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-131">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="6fb9c-132">示例包括社交应用程序、 多用户游戏、 业务协作和新闻，天气或财务更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-132">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="6fb9c-133">这些通常称为实时应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-133">These are often called real-time applications.</span></span>

<span data-ttu-id="6fb9c-134">SignalR 简化了生成实时应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-134">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="6fb9c-135">它包括 ASP.NET server 库和一个要更加轻松地管理客户端-服务器连接并将内容更新推送到客户端的 JavaScript 客户端库。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-135">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="6fb9c-136">可以将 SignalR 库添加到现有的 ASP.NET 应用程序，以获取实时功能。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-136">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="6fb9c-137">本教程演示了下列 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-137">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="6fb9c-138">将 SignalR 库添加到 ASP.NET web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-138">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="6fb9c-139">创建用于将内容推送到客户端的中心类。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-139">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="6fb9c-140">创建配置该应用程序的 OWIN 启动类。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-140">Creating an OWIN startup class to configure the application.</span></span>
- <span data-ttu-id="6fb9c-141">使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-141">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="6fb9c-142">下面的屏幕截图显示在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-142">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="6fb9c-143">每个新用户可以发表评论，并查看添加用户加入聊天后的注释。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-143">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![聊天实例](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="6fb9c-145">各节：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-145">Sections:</span></span>

- [<span data-ttu-id="6fb9c-146">将项目设置</span><span class="sxs-lookup"><span data-stu-id="6fb9c-146">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="6fb9c-147">运行示例</span><span class="sxs-lookup"><span data-stu-id="6fb9c-147">Run the Sample</span></span>](#run)
- [<span data-ttu-id="6fb9c-148">检查代码</span><span class="sxs-lookup"><span data-stu-id="6fb9c-148">Examine the Code</span></span>](#code)
- [<span data-ttu-id="6fb9c-149">后续步骤</span><span class="sxs-lookup"><span data-stu-id="6fb9c-149">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="6fb9c-150">将项目设置</span><span class="sxs-lookup"><span data-stu-id="6fb9c-150">Set up the Project</span></span>

<span data-ttu-id="6fb9c-151">本部分演示如何使用 Visual Studio 2013 和 SignalR 版本 2 创建空的 ASP.NET web 应用程序，添加 SignalR，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-151">This section shows how to use Visual Studio 2013 and SignalR version 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="6fb9c-152">先决条件：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-152">Prerequisites:</span></span>

- <span data-ttu-id="6fb9c-153">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6fb9c-153">Visual Studio 2013.</span></span> <span data-ttu-id="6fb9c-154">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-154">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="6fb9c-155">以下步骤使用 Visual Studio 2013 创建 ASP.NET 空 Web 应用程序并添加 SignalR 库：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-155">The following steps use Visual Studio 2013 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="6fb9c-156">在 Visual Studio 中，创建 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-156">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="6fb9c-158">在**新建 ASP.NET 项目**窗口中，保留**空**选择和单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-158">In the **New ASP.NET Project** window, leave **Empty** selected and click **Create Project**.</span></span>

    ![创建空 web](tutorial-getting-started-with-signalr/_static/image3.png)
3. <span data-ttu-id="6fb9c-160">在**解决方案资源管理器**，右键单击项目，选择**添加 |SignalR Hub 类 (v2)**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-160">In **Solution Explorer**, right-click the project, select **Add | SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="6fb9c-161">将类**ChatHub.cs**并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-161">Name the class **ChatHub.cs** and add it to the project.</span></span> <span data-ttu-id="6fb9c-162">此步骤将创建**ChatHub**类并将一组的脚本文件和支持 SignalR 的程序集引用添加到项目。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-162">This step creates the **ChatHub** class and adds to the project a set of script files and assembly references that support SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fb9c-163">你还可以将 SignalR 通过打开添加到项目**工具 |库包管理器 |程序包管理器控制台**并运行命令：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-163">You can also add SignalR to a project by opening the **Tools | Library Package Manager | Package Manager Console** and running a command:</span></span>

    `install-package Microsoft.AspNet.SignalR`

    <span data-ttu-id="6fb9c-164">如果你使用控制台添加 SignalR，单独的步骤创建 SignalR hub 类后添加 SignalR。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-164">If you use the console to add SignalR, create the SignalR hub class as a separate step after you add SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fb9c-165">如果你正在使用 Visual Studio 2012， **SignalR Hub Class (v2)**模板将不可用。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-165">If you are using Visual Studio 2012, the **SignalR Hub Class (v2)** template will not be available.</span></span> <span data-ttu-id="6fb9c-166">你可以添加普通**类**调用`ChatHub`相反。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-166">You can add a plain **Class** called `ChatHub` instead.</span></span>
4. <span data-ttu-id="6fb9c-167">在**解决方案资源管理器**，展开脚本节点。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-167">In **Solution Explorer**, expand the Scripts node.</span></span> <span data-ttu-id="6fb9c-168">用于 jQuery 和 SignalR 的脚本库是在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-168">Script libraries for jQuery and SignalR are visible in the project.</span></span>
5. <span data-ttu-id="6fb9c-169">将在新代码**ChatHub**类替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-169">Replace the code in the new **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="6fb9c-170">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |OWIN Startup 类**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-170">In **Solution Explorer**, right-click the project, then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="6fb9c-171">将新类`Startup`并单击确定。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-171">Name the new class `Startup` and click OK.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fb9c-172">如果你正在使用 Visual Studio 2012， **OWIN Startup 类**模板将不可用。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-172">If you are using Visual Studio 2012, the **OWIN Startup Class** template will not be available.</span></span> <span data-ttu-id="6fb9c-173">你可以添加普通**类**调用`Startup`相反。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-173">You can add a plain **Class** called `Startup` instead.</span></span>
7. <span data-ttu-id="6fb9c-174">将新的启动类的内容更改为以下。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-174">Change the contents of the new Startup class to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="6fb9c-175">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |HTML 页**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-175">In **Solution Explorer**, right-click the project, then click **Add | HTML Page**.</span></span> <span data-ttu-id="6fb9c-176">将新该页命名为`index.html`。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-176">Name the new page `index.html`.</span></span>
    >[!NOTE]
    ><span data-ttu-id="6fb9c-177">你可能需要更改的对 JQuery 和 SignalR 的库的引用的版本号</span><span class="sxs-lookup"><span data-stu-id="6fb9c-177">You might need to change the version numbers for the references to JQuery and SignalR libraries</span></span>
9. <span data-ttu-id="6fb9c-178">在**解决方案资源管理器**，右键单击你刚刚创建的 HTML 页面，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-178">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
10. <span data-ttu-id="6fb9c-179">在 HTML 页中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-179">Replace the default code in the HTML page with the following code.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fb9c-180">可能的包管理器安装 SignalR 脚本的更高版本。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-180">A later version of the SignalR scripts may be installed by the package manager.</span></span> <span data-ttu-id="6fb9c-181">验证以下脚本参考对应于在项目中 （它们将位于不同，如果你添加了 SignalR 使用 NuGet，而不是添加 hub。） 的脚本文件的版本</span><span class="sxs-lookup"><span data-stu-id="6fb9c-181">Verify that the script references below correspond to the versions of the script files in the project (they will be different if you added SignalR using NuGet rather than adding a hub.)</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]
11. <span data-ttu-id="6fb9c-182">**保存所有**项目。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-182">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="6fb9c-183">运行示例</span><span class="sxs-lookup"><span data-stu-id="6fb9c-183">Run the Sample</span></span>

1. <span data-ttu-id="6fb9c-184">按 F5 以在调试模式下运行该项目。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-184">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="6fb9c-185">HTML 页加载中的浏览器实例并提示输入用户名。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-185">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image4.png)
2. <span data-ttu-id="6fb9c-187">输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-187">Enter a user name.</span></span>
3. <span data-ttu-id="6fb9c-188">从浏览器的地址行中复制 URL，并使用它来打开两个多个浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-188">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="6fb9c-189">在每个浏览器实例中，输入唯一的用户名。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-189">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="6fb9c-190">在每个浏览器实例中，添加注释并单击**发送**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-190">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="6fb9c-191">注释应该显示在所有浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-191">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fb9c-192">此简单的聊天应用程序不维护服务器上的讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-192">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="6fb9c-193">中心广播到所有当前用户的注释。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-193">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="6fb9c-194">加入这次聊天更高版本的用户将看到消息从时间添加加入。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-194">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="6fb9c-195">下面的屏幕快照显示三个浏览器实例，所有这些更新时将消息发送的一个实例中运行的聊天应用程序：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-195">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr/_static/image5.png)
5. <span data-ttu-id="6fb9c-197">在**解决方案资源管理器**，检查**脚本文档**运行的应用程序的节点。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-197">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="6fb9c-198">没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-198">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="6fb9c-199">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-199">This file manages the communication between jQuery script and server-side code.</span></span>

    ![](tutorial-getting-started-with-signalr/_static/image6.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="6fb9c-200">检查代码</span><span class="sxs-lookup"><span data-stu-id="6fb9c-200">Examine the Code</span></span>

<span data-ttu-id="6fb9c-201">SignalR 聊天应用程序演示两个基本的 SignalR 开发任务： 与主协调对象在服务器上，创建一个中心并使用 SignalR jQuery 库来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-201">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="6fb9c-202">SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="6fb9c-202">SignalR Hubs</span></span>

<span data-ttu-id="6fb9c-203">中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-203">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="6fb9c-204">派生自**中心**类是提供有用的方法来构建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-204">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="6fb9c-205">你可以在你的中心类上创建公共方法，然后通过调用这些方法从 web 页中的脚本中访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-205">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="6fb9c-206">在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-206">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="6fb9c-207">中心反过来将消息发送到所有客户端，通过调用**Clients.All.broadcastMessage**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-207">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="6fb9c-208">**发送**方法演示了多个中心概念：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-208">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="6fb9c-209">公共方法声明的中心，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-209">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="6fb9c-210">使用**Microsoft.AspNet.SignalR.Hub.Clients**动态属性来访问所有客户端连接到此集线器。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-210">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="6fb9c-211">客户端上调用的函数 (如`broadcastMessage`函数) 来更新客户端。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-211">Call a function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="6fb9c-212">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="6fb9c-212">SignalR and jQuery</span></span>

<span data-ttu-id="6fb9c-213">HTML 页中的代码示例演示如何使用 SignalR jQuery 库与 SignalR hub 进行通信。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-213">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="6fb9c-214">在代码中的基本任务声明一个代理，以引用的中心，声明该服务器可以将内容推送到客户端，调用的函数和启动的连接将消息发送到中心。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-214">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="6fb9c-215">下面的代码声明对中心代理的引用。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-215">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="6fb9c-216">在 JavaScript 到的服务器类及其成员的引用位于 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-216">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="6fb9c-217">引用的代码示例的 C# **ChatHub**类中作为**chatHub**。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-217">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span>


<span data-ttu-id="6fb9c-218">下面的代码是如何在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-218">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="6fb9c-219">在服务器上的中心类调用此函数可将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-219">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="6fb9c-220">HTML 对内容编码显示之前的两行都是可选的并显示一种简单的方法，以防止脚本注入。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-220">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="6fb9c-221">下面的代码演示如何使用中心打开连接。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-221">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="6fb9c-222">代码启动连接，然后将它传递函数来处理 click 事件上**发送**在 HTML 页的按钮。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-222">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="6fb9c-223">此方法确保事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-223">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6fb9c-224">后续步骤</span><span class="sxs-lookup"><span data-stu-id="6fb9c-224">Next Steps</span></span>

<span data-ttu-id="6fb9c-225">你已了解 SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-225">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="6fb9c-226">你还了解了多个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建一个中心类，以及如何发送和从中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-226">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="6fb9c-227">有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[将 signalr 与在 Azure App Service Web Apps 配合](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-227">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="6fb9c-228">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="6fb9c-228">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="6fb9c-229">若要了解更多高级的 SignalR 最新开发进展概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="6fb9c-229">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="6fb9c-230">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="6fb9c-230">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="6fb9c-231">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="6fb9c-231">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="6fb9c-232">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="6fb9c-232">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
