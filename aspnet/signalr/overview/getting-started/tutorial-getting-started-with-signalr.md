---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教程： SignalR 2 入门 |Microsoft Docs
author: pfletcher
description: 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序，并创建 HTML pa...
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 798838af099cceb12652b7c6c66633a03a73e538
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841837"
---
<a name="tutorial-getting-started-with-signalr-2"></a><span data-ttu-id="92390-104">教程： SignalR 2 入门</span><span class="sxs-lookup"><span data-stu-id="92390-104">Tutorial: Getting Started with SignalR 2</span></span>
====================
<span data-ttu-id="92390-105">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="92390-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="92390-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="92390-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

> <span data-ttu-id="92390-107">本教程介绍如何使用 SignalR 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-107">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="92390-108">将 SignalR 添加到空的 ASP.NET web 应用程序，并创建 HTML 页以发送和显示的消息。</span><span class="sxs-lookup"><span data-stu-id="92390-108">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="92390-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="92390-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="92390-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="92390-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="92390-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="92390-111">.NET 4.5</span></span>
> - <span data-ttu-id="92390-112">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="92390-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="92390-113">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="92390-113">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="92390-114">若要学习本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="92390-114">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="92390-115">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)到最新版本。</span><span class="sxs-lookup"><span data-stu-id="92390-115">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="92390-116">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92390-116">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="92390-117">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="92390-117">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="92390-118">这将安装 Visual Studio 模板的 SignalR 类，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="92390-118">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="92390-119">某些模板 (如**OWIN 启动类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="92390-119">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="92390-120">教程版本</span><span class="sxs-lookup"><span data-stu-id="92390-120">Tutorial versions</span></span>
> 
> <span data-ttu-id="92390-121">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="92390-121">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="92390-122">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="92390-122">Questions and comments</span></span>
> 
> <span data-ttu-id="92390-123">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="92390-123">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="92390-124">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="92390-124">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="92390-125">概述</span><span class="sxs-lookup"><span data-stu-id="92390-125">Overview</span></span>

<span data-ttu-id="92390-126">本教程介绍了通过演示如何生成简单的基于浏览器的聊天应用程序的 SignalR 开发。</span><span class="sxs-lookup"><span data-stu-id="92390-126">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="92390-127">将 SignalR 库添加到空的 ASP.NET web 应用程序，创建一个中心类，用于将消息发送到客户端，并创建使用户能够发送和接收聊天消息的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="92390-127">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="92390-128">有关演示如何在 MVC 5 中创建的聊天应用程序使用 MVC 视图的类似教程，请参阅[SignalR 2 和 MVC 5 入门](tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="92390-128">For a similar tutorial that shows how to create a chat application in MVC 5 using an MVC view, see [Getting Started with SignalR 2 and MVC 5](tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

> [!NOTE]
> <span data-ttu-id="92390-129">本教程演示如何创建版本 2 中的 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-129">This tutorial demonstrates how to create SignalR applications in version 2.</span></span> <span data-ttu-id="92390-130">有关 SignalR 之间的更改的详细信息 1.x 和 2，请参阅[升级 SignalR 1.x 项目](../releases/upgrading-signalr-1x-projects-to-20.md)并[Visual Studio 2013 发行说明](../../../visual-studio/overview/2013/release-notes.md#TOC13)。</span><span class="sxs-lookup"><span data-stu-id="92390-130">For details on changes between SignalR 1.x and 2, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md) and [Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md#TOC13).</span></span>

<span data-ttu-id="92390-131">SignalR 是构建 web 应用程序的需要实时用户交互或实时数据更新的开放源.NET 库。</span><span class="sxs-lookup"><span data-stu-id="92390-131">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="92390-132">示例包括社交应用程序、 多用户游戏、 业务协作和新闻、 天气或财务更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-132">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="92390-133">这些测试通常称为实时应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-133">These are often called real-time applications.</span></span>

<span data-ttu-id="92390-134">SignalR 简化了构建实时应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="92390-134">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="92390-135">它包括 ASP.NET 服务器库和 JavaScript 客户端库来轻松地管理客户端-服务器连接，并将内容更新推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="92390-135">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="92390-136">您可以将 SignalR 库添加到现有 ASP.NET 应用程序以获取实时功能。</span><span class="sxs-lookup"><span data-stu-id="92390-136">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="92390-137">本教程演示以下的 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="92390-137">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="92390-138">SignalR 库添加到 ASP.NET web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-138">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="92390-139">创建用于将内容推送到客户端的中心类。</span><span class="sxs-lookup"><span data-stu-id="92390-139">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="92390-140">创建配置应用程序的 OWIN 启动类。</span><span class="sxs-lookup"><span data-stu-id="92390-140">Creating an OWIN startup class to configure the application.</span></span>
- <span data-ttu-id="92390-141">使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="92390-141">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="92390-142">以下屏幕截图显示在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-142">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="92390-143">每个新用户可以发表评论，并查看用户加入聊天后已添加注释。</span><span class="sxs-lookup"><span data-stu-id="92390-143">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![聊天实例](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="92390-145">部分：</span><span class="sxs-lookup"><span data-stu-id="92390-145">Sections:</span></span>

- [<span data-ttu-id="92390-146">设置项目</span><span class="sxs-lookup"><span data-stu-id="92390-146">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="92390-147">运行示例</span><span class="sxs-lookup"><span data-stu-id="92390-147">Run the Sample</span></span>](#run)
- [<span data-ttu-id="92390-148">检查代码</span><span class="sxs-lookup"><span data-stu-id="92390-148">Examine the Code</span></span>](#code)
- [<span data-ttu-id="92390-149">后续步骤</span><span class="sxs-lookup"><span data-stu-id="92390-149">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="92390-150">设置项目</span><span class="sxs-lookup"><span data-stu-id="92390-150">Set up the Project</span></span>

<span data-ttu-id="92390-151">本部分演示如何使用 Visual Studio 2013 和 SignalR 版本 2 创建空的 ASP.NET web 应用程序，将 SignalR 中，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-151">This section shows how to use Visual Studio 2013 and SignalR version 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="92390-152">先决条件：</span><span class="sxs-lookup"><span data-stu-id="92390-152">Prerequisites:</span></span>

- <span data-ttu-id="92390-153">Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="92390-153">Visual Studio 2013.</span></span> <span data-ttu-id="92390-154">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="92390-154">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="92390-155">以下步骤使用 Visual Studio 2013 创建 ASP.NET 空 Web 应用程序并添加 SignalR 库：</span><span class="sxs-lookup"><span data-stu-id="92390-155">The following steps use Visual Studio 2013 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="92390-156">在 Visual Studio 中创建 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-156">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="92390-158">在中**新建 ASP.NET 项目**窗口中，保留**空**选中然后单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="92390-158">In the **New ASP.NET Project** window, leave **Empty** selected and click **Create Project**.</span></span>

    ![创建空的 web](tutorial-getting-started-with-signalr/_static/image3.png)
3. <span data-ttu-id="92390-160">在中**解决方案资源管理器**，右键单击项目，选择**添加 |SignalR Hub 类 (v2)**。</span><span class="sxs-lookup"><span data-stu-id="92390-160">In **Solution Explorer**, right-click the project, select **Add | SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="92390-161">将类命名**ChatHub.cs**并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="92390-161">Name the class **ChatHub.cs** and add it to the project.</span></span> <span data-ttu-id="92390-162">此步骤将创建**ChatHub**类，并将一组脚本文件和支持 SignalR 的程序集引用添加到项目。</span><span class="sxs-lookup"><span data-stu-id="92390-162">This step creates the **ChatHub** class and adds to the project a set of script files and assembly references that support SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92390-163">您还可以将 SignalR 通过打开添加到项目**工具 |库包管理器 |包管理器控制台**并运行命令：</span><span class="sxs-lookup"><span data-stu-id="92390-163">You can also add SignalR to a project by opening the **Tools | Library Package Manager | Package Manager Console** and running a command:</span></span>

    `install-package Microsoft.AspNet.SignalR`

    <span data-ttu-id="92390-164">如果使用控制台来添加 SignalR，SignalR hub 类作为单独的步骤后创建将 SignalR 添加。</span><span class="sxs-lookup"><span data-stu-id="92390-164">If you use the console to add SignalR, create the SignalR hub class as a separate step after you add SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92390-165">如果使用 Visual Studio 2012 中， **SignalR Hub 类 (v2)** 模板将不可用。</span><span class="sxs-lookup"><span data-stu-id="92390-165">If you are using Visual Studio 2012, the **SignalR Hub Class (v2)** template will not be available.</span></span> <span data-ttu-id="92390-166">您可以添加纯**类**调用`ChatHub`相反。</span><span class="sxs-lookup"><span data-stu-id="92390-166">You can add a plain **Class** called `ChatHub` instead.</span></span>
4. <span data-ttu-id="92390-167">在中**解决方案资源管理器**，展开脚本节点。</span><span class="sxs-lookup"><span data-stu-id="92390-167">In **Solution Explorer**, expand the Scripts node.</span></span> <span data-ttu-id="92390-168">适用于 jQuery 和 SignalR 的脚本库将显示在该项目。</span><span class="sxs-lookup"><span data-stu-id="92390-168">Script libraries for jQuery and SignalR are visible in the project.</span></span>
5. <span data-ttu-id="92390-169">在新的代码替换为**ChatHub**用下面的代码的类。</span><span class="sxs-lookup"><span data-stu-id="92390-169">Replace the code in the new **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="92390-170">在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |OWIN 启动类**。</span><span class="sxs-lookup"><span data-stu-id="92390-170">In **Solution Explorer**, right-click the project, then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="92390-171">新类命名为`Startup`并单击确定。</span><span class="sxs-lookup"><span data-stu-id="92390-171">Name the new class `Startup` and click OK.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92390-172">如果使用 Visual Studio 2012 中， **OWIN 启动类**模板将不可用。</span><span class="sxs-lookup"><span data-stu-id="92390-172">If you are using Visual Studio 2012, the **OWIN Startup Class** template will not be available.</span></span> <span data-ttu-id="92390-173">您可以添加纯**类**调用`Startup`相反。</span><span class="sxs-lookup"><span data-stu-id="92390-173">You can add a plain **Class** called `Startup` instead.</span></span>
7. <span data-ttu-id="92390-174">将新的启动类的内容更改为以下。</span><span class="sxs-lookup"><span data-stu-id="92390-174">Change the contents of the new Startup class to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="92390-175">在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |HTML 页**。</span><span class="sxs-lookup"><span data-stu-id="92390-175">In **Solution Explorer**, right-click the project, then click **Add | HTML Page**.</span></span> <span data-ttu-id="92390-176">命名新页面`index.html`。</span><span class="sxs-lookup"><span data-stu-id="92390-176">Name the new page `index.html`.</span></span>
    >[!NOTE]
    ><span data-ttu-id="92390-177">可能需要更改对 JQuery 和 SignalR 库的引用的版本号</span><span class="sxs-lookup"><span data-stu-id="92390-177">You might need to change the version numbers for the references to JQuery and SignalR libraries</span></span>
9. <span data-ttu-id="92390-178">在中**解决方案资源管理器**，右键单击刚创建的 HTML 页，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="92390-178">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
10. <span data-ttu-id="92390-179">HTML 页中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="92390-179">Replace the default code in the HTML page with the following code.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92390-180">可能通过程序包管理器安装 SignalR 脚本的更高版本。</span><span class="sxs-lookup"><span data-stu-id="92390-180">A later version of the SignalR scripts may be installed by the package manager.</span></span> <span data-ttu-id="92390-181">验证以下脚本参考对应于版本的脚本文件在项目中 （它们将与此不同如果添加了使用 NuGet，而不是添加 hub 的 SignalR。）</span><span class="sxs-lookup"><span data-stu-id="92390-181">Verify that the script references below correspond to the versions of the script files in the project (they will be different if you added SignalR using NuGet rather than adding a hub.)</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]
11. <span data-ttu-id="92390-182">**保存所有**项目。</span><span class="sxs-lookup"><span data-stu-id="92390-182">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="92390-183">运行示例</span><span class="sxs-lookup"><span data-stu-id="92390-183">Run the Sample</span></span>

1. <span data-ttu-id="92390-184">按 F5 以在调试模式下运行该项目。</span><span class="sxs-lookup"><span data-stu-id="92390-184">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="92390-185">中的浏览器实例并提示输入用户名称的 HTML 页面加载。</span><span class="sxs-lookup"><span data-stu-id="92390-185">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image4.png)
2. <span data-ttu-id="92390-187">输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="92390-187">Enter a user name.</span></span>
3. <span data-ttu-id="92390-188">从地址行中的浏览器复制 URL 并将其用于打开两个更多的浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="92390-188">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="92390-189">在每个浏览器实例中，输入唯一的用户名称。</span><span class="sxs-lookup"><span data-stu-id="92390-189">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="92390-190">在每个浏览器实例中，添加注释并单击**发送**。</span><span class="sxs-lookup"><span data-stu-id="92390-190">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="92390-191">注释应显示在浏览器的所有实例。</span><span class="sxs-lookup"><span data-stu-id="92390-191">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92390-192">此简单的聊天应用程序不维护服务器上的讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="92390-192">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="92390-193">在中心广播到所有当前用户的注释。</span><span class="sxs-lookup"><span data-stu-id="92390-193">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="92390-194">加入聊天更高版本的用户将看到消息从时添加它们加入。</span><span class="sxs-lookup"><span data-stu-id="92390-194">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="92390-195">下面的屏幕截图显示了在三个浏览器情况下，所有这些更新一个实例发送消息时运行的聊天应用程序：</span><span class="sxs-lookup"><span data-stu-id="92390-195">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr/_static/image5.png)
5. <span data-ttu-id="92390-197">在中**解决方案资源管理器**，检查**脚本文档**节点运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-197">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="92390-198">没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。</span><span class="sxs-lookup"><span data-stu-id="92390-198">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="92390-199">此文件管理的 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="92390-199">This file manages the communication between jQuery script and server-side code.</span></span>

    ![](tutorial-getting-started-with-signalr/_static/image6.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="92390-200">检查代码</span><span class="sxs-lookup"><span data-stu-id="92390-200">Examine the Code</span></span>

<span data-ttu-id="92390-201">SignalR 聊天应用程序演示了两个基本的 SignalR 开发任务： 在服务器上的主要协调对象为创建中心和使用 SignalR jQuery 库来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="92390-201">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="92390-202">SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="92390-202">SignalR Hubs</span></span>

<span data-ttu-id="92390-203">中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。</span><span class="sxs-lookup"><span data-stu-id="92390-203">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="92390-204">派生自**中心**类是一种有用的方式来构建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-204">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="92390-205">可以在中心类上创建的公共方法，然后通过调用从网页中的脚本中访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="92390-205">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="92390-206">在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。</span><span class="sxs-lookup"><span data-stu-id="92390-206">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="92390-207">在中心反过来将消息发送给所有客户端，通过调用**Clients.All.broadcastMessage**。</span><span class="sxs-lookup"><span data-stu-id="92390-207">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="92390-208">**发送**方法演示了多个中心概念：</span><span class="sxs-lookup"><span data-stu-id="92390-208">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="92390-209">集线器上声明的公共方法，以便客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="92390-209">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="92390-210">使用**Microsoft.AspNet.SignalR.Hub.Clients**动态属性来访问所有客户端连接到此中心。</span><span class="sxs-lookup"><span data-stu-id="92390-210">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="92390-211">在客户端上调用的函数 (如`broadcastMessage`函数) 来更新客户端。</span><span class="sxs-lookup"><span data-stu-id="92390-211">Call a function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="92390-212">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="92390-212">SignalR and jQuery</span></span>

<span data-ttu-id="92390-213">HTML 页中的代码示例演示如何使用 SignalR jQuery 库与 SignalR 中心进行通信。</span><span class="sxs-lookup"><span data-stu-id="92390-213">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="92390-214">在代码中的基本任务声明的代理服务器能够引用中心，声明服务器可以将内容推送到客户端，调用的函数和启动的连接将消息发送到中心。</span><span class="sxs-lookup"><span data-stu-id="92390-214">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="92390-215">下面的代码声明对集线器代理的引用。</span><span class="sxs-lookup"><span data-stu-id="92390-215">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="92390-216">在 JavaScript 中于服务器类及其成员的引用位于混合大小写。</span><span class="sxs-lookup"><span data-stu-id="92390-216">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="92390-217">代码示例将引用 C# **ChatHub**中作为 JavaScript 类**chatHub**。</span><span class="sxs-lookup"><span data-stu-id="92390-217">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span>


<span data-ttu-id="92390-218">下面的代码是如何在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="92390-218">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="92390-219">在服务器上的中心类会调用此函数可将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="92390-219">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="92390-220">HTML 显示前先编码内容的两行都是可选的并显示简单的方法来阻止脚本注入。</span><span class="sxs-lookup"><span data-stu-id="92390-220">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="92390-221">下面的代码演示如何在中心打开的连接。</span><span class="sxs-lookup"><span data-stu-id="92390-221">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="92390-222">代码启动连接，然后将其传递函数来处理单击事件上**发送**HTML 页中的按钮。</span><span class="sxs-lookup"><span data-stu-id="92390-222">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="92390-223">此方法可确保事件处理程序在执行之前建立的连接。</span><span class="sxs-lookup"><span data-stu-id="92390-223">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="92390-224">后续步骤</span><span class="sxs-lookup"><span data-stu-id="92390-224">Next Steps</span></span>

<span data-ttu-id="92390-225">您学习了 SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92390-225">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="92390-226">您还学习了几个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建 hub 类以及如何发送和接收来自中心的消息。</span><span class="sxs-lookup"><span data-stu-id="92390-226">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="92390-227">有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="92390-227">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="92390-228">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="92390-228">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="92390-229">若要了解更高级的 SignalR 开发概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="92390-229">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="92390-230">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="92390-230">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="92390-231">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="92390-231">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="92390-232">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="92390-232">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
