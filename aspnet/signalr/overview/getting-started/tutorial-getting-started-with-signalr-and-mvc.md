---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: "教程： 开始使用 SignalR 2 和 MVC 5 |Microsoft 文档"
author: pfletcher
description: "本教程演示如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。 将 MVC 5 应用程序中添加 SignalR 和创建聊天视图..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.openlocfilehash: ca0471114da7363c5df9d459308708e7ab4f8b84
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="tutorial-getting-started-with-signalr-2-and-mvc-5"></a><span data-ttu-id="1bacd-104">教程： 开始使用 SignalR 2 和 MVC 5</span><span class="sxs-lookup"><span data-stu-id="1bacd-104">Tutorial: Getting Started with SignalR 2 and MVC 5</span></span>
====================
<span data-ttu-id="1bacd-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="1bacd-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[<span data-ttu-id="1bacd-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="1bacd-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

> <span data-ttu-id="1bacd-107">本教程演示如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-107">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="1bacd-108">你将添加到 MVC 5 应用程序的 SignalR 和创建聊天视图来发送和显示的消息。</span><span class="sxs-lookup"><span data-stu-id="1bacd-108">You will add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1bacd-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="1bacd-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="1bacd-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1bacd-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="1bacd-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1bacd-111">.NET 4.5</span></span>
> - <span data-ttu-id="1bacd-112">MVC 5</span><span class="sxs-lookup"><span data-stu-id="1bacd-112">MVC 5</span></span>
> - <span data-ttu-id="1bacd-113">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="1bacd-113">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="1bacd-114">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1bacd-114">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="1bacd-115">若要使用本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="1bacd-115">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="1bacd-116">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)的最新版本。</span><span class="sxs-lookup"><span data-stu-id="1bacd-116">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="1bacd-117">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bacd-117">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="1bacd-118">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web Tools for Visual Studio 2012 的 2013.1**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-118">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="1bacd-119">这将安装 SignalR 类的 Visual Studio 模板，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-119">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="1bacd-120">某些模板 (如**OWIN Startup 类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="1bacd-120">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="1bacd-121">教程版本</span><span class="sxs-lookup"><span data-stu-id="1bacd-121">Tutorial Versions</span></span>
> 
> <span data-ttu-id="1bacd-122">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="1bacd-122">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="1bacd-123">问题和意见</span><span class="sxs-lookup"><span data-stu-id="1bacd-123">Questions and comments</span></span>
> 
> <span data-ttu-id="1bacd-124">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="1bacd-124">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1bacd-125">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="1bacd-125">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="1bacd-126">概述</span><span class="sxs-lookup"><span data-stu-id="1bacd-126">Overview</span></span>

<span data-ttu-id="1bacd-127">本教程向你介绍使用 ASP.NET SignalR 2 和 ASP.NET MVC 5 的实时 web 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="1bacd-127">This tutorial introduces you to real-time web application development with ASP.NET SignalR 2 and ASP.NET MVC 5.</span></span> <span data-ttu-id="1bacd-128">本教程使用的相同聊天应用程序代码[SignalR 入门教程](tutorial-getting-started-with-signalr.md)，但演示如何将其添加到一个 MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-128">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 5 application.</span></span>

<span data-ttu-id="1bacd-129">本主题中，你将学习以下 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="1bacd-129">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="1bacd-130">将 SignalR 库添加到一个 MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-130">Adding the SignalR library to an MVC 5 application.</span></span>
- <span data-ttu-id="1bacd-131">创建中心和 OWIN 启动类，以将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="1bacd-131">Creating hub and OWIN startup classes to push content to clients.</span></span>
- <span data-ttu-id="1bacd-132">使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="1bacd-132">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="1bacd-133">下面的屏幕截图显示在浏览器中运行的已完成的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-133">The following screen shot shows the completed chat application running in a browser.</span></span>

![聊天实例](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

<span data-ttu-id="1bacd-135">各节：</span><span class="sxs-lookup"><span data-stu-id="1bacd-135">Sections:</span></span>

- [<span data-ttu-id="1bacd-136">将项目设置</span><span class="sxs-lookup"><span data-stu-id="1bacd-136">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="1bacd-137">运行示例</span><span class="sxs-lookup"><span data-stu-id="1bacd-137">Run the Sample</span></span>](#run)
- [<span data-ttu-id="1bacd-138">检查代码</span><span class="sxs-lookup"><span data-stu-id="1bacd-138">Examine the Code</span></span>](#code)
- [<span data-ttu-id="1bacd-139">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1bacd-139">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="1bacd-140">将项目设置</span><span class="sxs-lookup"><span data-stu-id="1bacd-140">Set up the Project</span></span>

<span data-ttu-id="1bacd-141">先决条件：</span><span class="sxs-lookup"><span data-stu-id="1bacd-141">Prerequisites:</span></span>

- <span data-ttu-id="1bacd-142">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1bacd-142">Visual Studio 2013.</span></span> <span data-ttu-id="1bacd-143">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="1bacd-143">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="1bacd-144">本部分演示如何创建一个 ASP.NET MVC 5 应用程序、 添加 SignalR 库，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-144">This section shows how to create an ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="1bacd-145">在 Visual Studio 中，创建面向.NET Framework 4.5 的 C# ASP.NET 应用程序，将其命名为 SignalRChat，，单击确定。</span><span class="sxs-lookup"><span data-stu-id="1bacd-145">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)
2. <span data-ttu-id="1bacd-147">在`New ASP.NET Project`对话框中，然后选择**MVC**，然后单击**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-147">In the `New ASP.NET Project` dialog, and select **MVC**, and click **Change Authentication**.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)
3. <span data-ttu-id="1bacd-149">选择**无身份验证**中**更改身份验证**对话框，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-149">Select **No Authentication** in the **Change Authentication** dialog, and click **OK**.</span></span>

    ![选择无身份验证](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="1bacd-151">如果你选择不同的身份验证提供程序用于你的应用程序，`Startup.cs`类将为你创建; 你不需要创建你自己`Startup.cs`下面的步骤 10 中的类。</span><span class="sxs-lookup"><span data-stu-id="1bacd-151">If you select a different authentication provider for your application, a `Startup.cs` class will be created for you; you will not need to create your own `Startup.cs` class in step 10 below.</span></span>
4. <span data-ttu-id="1bacd-152">单击**确定**中**新建 ASP.NET 项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="1bacd-152">Click **OK** in the **New ASP.NET Project** dialog.</span></span>
5. <span data-ttu-id="1bacd-153">打开**工具 |库包管理器 |程序包管理器控制台**并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="1bacd-153">Open the **Tools | Library Package Manager | Package Manager Console** and run the following command.</span></span> <span data-ttu-id="1bacd-154">此步骤将一组的脚本文件和启用 SignalR 功能的程序集引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="1bacd-154">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

    `install-package Microsoft.AspNet.SignalR`
6. <span data-ttu-id="1bacd-155">在**解决方案资源管理器**，展开脚本文件夹。</span><span class="sxs-lookup"><span data-stu-id="1bacd-155">In **Solution Explorer**, expand the Scripts folder.</span></span> <span data-ttu-id="1bacd-156">请注意，适用于 SignalR 的脚本库已添加到项目。</span><span class="sxs-lookup"><span data-stu-id="1bacd-156">Note that script libraries for SignalR have been added to the project.</span></span>

    ![脚本文件夹](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)
7. <span data-ttu-id="1bacd-158">在**解决方案资源管理器**，右键单击项目，选择**添加 |新文件夹**，并添加一个名为的新文件夹**中心**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-158">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
8. <span data-ttu-id="1bacd-159">右键单击**中心**文件夹中，单击**添加 |新项**，选择**Visual C# |Web |SignalR**中的节点**已安装**窗格中，选择**SignalR Hub Class (v2)**从中间窗格中，并创建名为的新集线器**ChatHub.cs**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-159">Right-click the **Hubs** folder, click **Add | New Item**, select the **Visual C# | Web | SignalR** node in the **Installed** pane, select **SignalR Hub Class (v2)** from the center pane, and create a new hub named **ChatHub.cs**.</span></span> <span data-ttu-id="1bacd-160">你将使用此类作为将消息发送到所有客户端的 SignalR 服务器集线器。</span><span class="sxs-lookup"><span data-stu-id="1bacd-160">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

    ![创建新的中心](tutorial-getting-started-with-signalr-and-mvc/_static/image6.png)
9. <span data-ttu-id="1bacd-162">中的代码替换**ChatHub**类替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="1bacd-162">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]
10. <span data-ttu-id="1bacd-163">创建一个名 Startup.cs 的新类。</span><span class="sxs-lookup"><span data-stu-id="1bacd-163">Create a new class called Startup.cs.</span></span> <span data-ttu-id="1bacd-164">更改为以下文件的内容。</span><span class="sxs-lookup"><span data-stu-id="1bacd-164">Change the contents of the file to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]
11. <span data-ttu-id="1bacd-165">编辑`HomeController`中找到该类**Controllers/HomeController.cs**并将以下方法添加到类。</span><span class="sxs-lookup"><span data-stu-id="1bacd-165">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="1bacd-166">此方法返回**聊天**将在稍后的步骤中创建的视图。</span><span class="sxs-lookup"><span data-stu-id="1bacd-166">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]
12. <span data-ttu-id="1bacd-167">右键单击**视图/主页**文件夹，并选择**添加.|视图**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-167">Right-click the **Views/Home** folder, and select **Add... | View**.</span></span>
13. <span data-ttu-id="1bacd-168">在**添加视图**对话框中，名称的新视图**聊天**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-168">In the **Add View** dialog, name the new view **Chat**.</span></span>

    ![添加视图](tutorial-getting-started-with-signalr-and-mvc/_static/image7.png)
14. <span data-ttu-id="1bacd-170">内容替换**Chat.cshtml**替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="1bacd-170">Replace the contents of **Chat.cshtml** with the following code.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1bacd-171">当你将 SignalR 和其他脚本库添加到 Visual Studio 项目中时，包管理器可能会安装本主题中显示的版本比更新 SignalR 脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="1bacd-171">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="1bacd-172">请确保你的代码中的脚本引用匹配在项目中安装的脚本库的版本。</span><span class="sxs-lookup"><span data-stu-id="1bacd-172">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]
15. <span data-ttu-id="1bacd-173">**保存所有**项目。</span><span class="sxs-lookup"><span data-stu-id="1bacd-173">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="1bacd-174">运行示例</span><span class="sxs-lookup"><span data-stu-id="1bacd-174">Run the Sample</span></span>

1. <span data-ttu-id="1bacd-175">按 F5 以在调试模式下运行该项目。</span><span class="sxs-lookup"><span data-stu-id="1bacd-175">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="1bacd-176">在浏览器地址行中，追加**/home/聊天**项目的默认页的 url。</span><span class="sxs-lookup"><span data-stu-id="1bacd-176">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="1bacd-177">聊天页面加载的浏览器实例并提示输入用户名。</span><span class="sxs-lookup"><span data-stu-id="1bacd-177">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc/_static/image8.png)
3. <span data-ttu-id="1bacd-179">输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="1bacd-179">Enter a user name.</span></span>
4. <span data-ttu-id="1bacd-180">从浏览器的地址行中复制 URL，并使用它来打开两个多个浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="1bacd-180">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="1bacd-181">在每个浏览器实例中，输入唯一的用户名。</span><span class="sxs-lookup"><span data-stu-id="1bacd-181">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="1bacd-182">在每个浏览器实例中，添加注释并单击**发送**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-182">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="1bacd-183">注释应该显示在所有浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="1bacd-183">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1bacd-184">此简单的聊天应用程序不维护服务器上的讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="1bacd-184">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="1bacd-185">中心广播到所有当前用户的注释。</span><span class="sxs-lookup"><span data-stu-id="1bacd-185">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="1bacd-186">加入这次聊天更高版本的用户将看到消息从时间添加加入。</span><span class="sxs-lookup"><span data-stu-id="1bacd-186">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="1bacd-187">下面的屏幕截图显示在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-187">The following screen shot shows the chat application running in a browser.</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr-and-mvc/_static/image9.png)
7. <span data-ttu-id="1bacd-189">在**解决方案资源管理器**，检查**脚本文档**运行的应用程序的节点。</span><span class="sxs-lookup"><span data-stu-id="1bacd-189">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="1bacd-190">如果你使用的 Internet Explorer 作为你的浏览器，此节点会显示在调试模式下。</span><span class="sxs-lookup"><span data-stu-id="1bacd-190">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="1bacd-191">没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。</span><span class="sxs-lookup"><span data-stu-id="1bacd-191">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="1bacd-192">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="1bacd-192">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="1bacd-193">如果你使用非 Internet Explorer 浏览器，你还可以访问动态**中心**通过浏览到它直接，例如 http://mywebsite/signalr/hubs 的文件。</span><span class="sxs-lookup"><span data-stu-id="1bacd-193">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="1bacd-194">检查代码</span><span class="sxs-lookup"><span data-stu-id="1bacd-194">Examine the Code</span></span>

<span data-ttu-id="1bacd-195">SignalR 聊天应用程序演示两个基本的 SignalR 开发任务： 与主协调对象在服务器上，创建一个中心并使用 SignalR jQuery 库来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="1bacd-195">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="1bacd-196">SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="1bacd-196">SignalR Hubs</span></span>

<span data-ttu-id="1bacd-197">中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。</span><span class="sxs-lookup"><span data-stu-id="1bacd-197">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="1bacd-198">派生自**中心**类是提供有用的方法来构建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-198">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="1bacd-199">你可以在你的中心类上创建公共方法，然后通过调用这些方法从 web 页中的脚本中访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="1bacd-199">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="1bacd-200">在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。</span><span class="sxs-lookup"><span data-stu-id="1bacd-200">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="1bacd-201">中心反过来将消息发送到所有客户端，通过调用**Clients.All.addNewMessageToPage**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-201">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="1bacd-202">**发送**方法演示了多个中心概念：</span><span class="sxs-lookup"><span data-stu-id="1bacd-202">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="1bacd-203">公共方法声明的中心，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="1bacd-203">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="1bacd-204">使用**Microsoft.AspNet.SignalR.Hub.Clients**属性来访问所有客户端连接到此集线器。</span><span class="sxs-lookup"><span data-stu-id="1bacd-204">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="1bacd-205">客户端上调用的函数 (如`addNewMessageToPage`函数) 来更新客户端。</span><span class="sxs-lookup"><span data-stu-id="1bacd-205">Call a function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="1bacd-206">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="1bacd-206">SignalR and jQuery</span></span>

<span data-ttu-id="1bacd-207">**Chat.cshtml**视图文件中的代码示例演示如何使用 SignalR jQuery 库与 SignalR hub 进行通信。</span><span class="sxs-lookup"><span data-stu-id="1bacd-207">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="1bacd-208">在代码中的基本任务创建时自动生成的代理的中心，声明该服务器可以将内容推送到客户端，调用的函数和启动连接将消息发送到中心的引用。</span><span class="sxs-lookup"><span data-stu-id="1bacd-208">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="1bacd-209">下面的代码声明对中心代理的引用。</span><span class="sxs-lookup"><span data-stu-id="1bacd-209">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="1bacd-210">在 JavaScript 到的服务器类及其成员的引用位于 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="1bacd-210">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="1bacd-211">引用的代码示例的 C# **ChatHub**类中作为**chatHub**。</span><span class="sxs-lookup"><span data-stu-id="1bacd-211">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span> <span data-ttu-id="1bacd-212">如果你想要引用`ChatHub`类在 jQuery 与传统 Pascal 大小写就像在 C# 中，编辑 ChatHub.cs 类文件。</span><span class="sxs-lookup"><span data-stu-id="1bacd-212">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="1bacd-213">添加`using`语句来引用`Microsoft.AspNet.SignalR.Hubs`命名空间。</span><span class="sxs-lookup"><span data-stu-id="1bacd-213">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="1bacd-214">然后添加`HubName`属性设为`ChatHub`类，例如`[HubName("ChatHub")]`。</span><span class="sxs-lookup"><span data-stu-id="1bacd-214">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="1bacd-215">最后，更新对你 jQuery 引用`ChatHub`类。</span><span class="sxs-lookup"><span data-stu-id="1bacd-215">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="1bacd-216">下面的代码演示如何在脚本中创建的回调函数。</span><span class="sxs-lookup"><span data-stu-id="1bacd-216">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="1bacd-217">在服务器上的中心类调用此函数可将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="1bacd-217">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="1bacd-218">可选调用`htmlEncode`函数显示了一个 html 的方式显示在页中，作为一种方法，以防止脚本注入前对进行编码的消息内容。</span><span class="sxs-lookup"><span data-stu-id="1bacd-218">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="1bacd-219">下面的代码演示如何使用中心打开连接。</span><span class="sxs-lookup"><span data-stu-id="1bacd-219">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="1bacd-220">代码启动连接，然后将它传递函数来处理 click 事件上**发送**聊天页中的按钮。</span><span class="sxs-lookup"><span data-stu-id="1bacd-220">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="1bacd-221">此方法确保事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="1bacd-221">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="1bacd-222">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1bacd-222">Next Steps</span></span>

<span data-ttu-id="1bacd-223">你已了解 SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1bacd-223">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="1bacd-224">你还了解了多个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建一个中心类，以及如何发送和从中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="1bacd-224">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="1bacd-225">有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[将 signalr 与在 Azure App Service Web Apps 配合](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="1bacd-225">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="1bacd-226">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="1bacd-226">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="1bacd-227">若要了解更多高级的 SignalR 最新开发进展概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="1bacd-227">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="1bacd-228">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="1bacd-228">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="1bacd-229">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="1bacd-229">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="1bacd-230">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="1bacd-230">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
