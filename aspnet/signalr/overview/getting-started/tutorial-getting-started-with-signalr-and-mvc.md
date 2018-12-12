---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 教程：使用 SignalR 2 和 MVC 5 入门 |Microsoft Docs
author: pfletcher
description: 本教程演示如何使用 ASP.NET SignalR 2 来创建实时聊天应用程序。 将 SignalR 添加到 MVC 5 应用程序并创建一个聊天视图...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.openlocfilehash: 568f82daa67f33736c2bf7a45a3e1339f265c487
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287504"
---
<a name="tutorial-getting-started-with-signalr-2-and-mvc-5"></a><span data-ttu-id="9fb82-104">教程：使用 SignalR 2 和 MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="9fb82-104">Tutorial: Getting Started with SignalR 2 and MVC 5</span></span>
====================
<span data-ttu-id="9fb82-105">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="9fb82-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="9fb82-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="9fb82-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

> <span data-ttu-id="9fb82-107">本教程演示如何使用 ASP.NET SignalR 2 来创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-107">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="9fb82-108">将将 SignalR 添加到 MVC 5 应用程序，并创建要发送，并显示消息的聊天视图。</span><span class="sxs-lookup"><span data-stu-id="9fb82-108">You will add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9fb82-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="9fb82-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="9fb82-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9fb82-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="9fb82-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9fb82-111">.NET 4.5</span></span>
> - <span data-ttu-id="9fb82-112">MVC 5</span><span class="sxs-lookup"><span data-stu-id="9fb82-112">MVC 5</span></span>
> - <span data-ttu-id="9fb82-113">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="9fb82-113">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="9fb82-114">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9fb82-114">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="9fb82-115">若要学习本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9fb82-115">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="9fb82-116">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)到最新版本。</span><span class="sxs-lookup"><span data-stu-id="9fb82-116">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="9fb82-117">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9fb82-117">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="9fb82-118">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-118">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="9fb82-119">这将安装 Visual Studio 模板的 SignalR 类，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-119">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="9fb82-120">某些模板 (如**OWIN 启动类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="9fb82-120">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="9fb82-121">教程版本</span><span class="sxs-lookup"><span data-stu-id="9fb82-121">Tutorial Versions</span></span>
>
> <span data-ttu-id="9fb82-122">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="9fb82-122">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="9fb82-123">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="9fb82-123">Questions and comments</span></span>
>
> <span data-ttu-id="9fb82-124">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="9fb82-124">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="9fb82-125">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="9fb82-125">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="9fb82-126">概述</span><span class="sxs-lookup"><span data-stu-id="9fb82-126">Overview</span></span>

<span data-ttu-id="9fb82-127">本教程向您介绍使用 ASP.NET SignalR 2 和 ASP.NET MVC 5 开发的实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-127">This tutorial introduces you to real-time web application development with ASP.NET SignalR 2 and ASP.NET MVC 5.</span></span> <span data-ttu-id="9fb82-128">本教程使用相同的聊天应用程序代码作为[SignalR 入门教程](tutorial-getting-started-with-signalr.md)，但显示了如何将其添加到 MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-128">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 5 application.</span></span>

<span data-ttu-id="9fb82-129">在本主题中，您将学习以下的 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="9fb82-129">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="9fb82-130">SignalR 库添加到 MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-130">Adding the SignalR library to an MVC 5 application.</span></span>
- <span data-ttu-id="9fb82-131">创建中心和 OWIN 启动类，可将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="9fb82-131">Creating hub and OWIN startup classes to push content to clients.</span></span>
- <span data-ttu-id="9fb82-132">使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。</span><span class="sxs-lookup"><span data-stu-id="9fb82-132">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="9fb82-133">以下屏幕截图显示在浏览器中运行的已完成的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-133">The following screen shot shows the completed chat application running in a browser.</span></span>

![聊天实例](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

<span data-ttu-id="9fb82-135">部分：</span><span class="sxs-lookup"><span data-stu-id="9fb82-135">Sections:</span></span>

- [<span data-ttu-id="9fb82-136">设置项目</span><span class="sxs-lookup"><span data-stu-id="9fb82-136">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="9fb82-137">运行示例</span><span class="sxs-lookup"><span data-stu-id="9fb82-137">Run the Sample</span></span>](#run)
- [<span data-ttu-id="9fb82-138">检查代码</span><span class="sxs-lookup"><span data-stu-id="9fb82-138">Examine the Code</span></span>](#code)
- [<span data-ttu-id="9fb82-139">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9fb82-139">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="9fb82-140">设置项目</span><span class="sxs-lookup"><span data-stu-id="9fb82-140">Set up the Project</span></span>

<span data-ttu-id="9fb82-141">先决条件：</span><span class="sxs-lookup"><span data-stu-id="9fb82-141">Prerequisites:</span></span>

- <span data-ttu-id="9fb82-142">Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="9fb82-142">Visual Studio 2013.</span></span> <span data-ttu-id="9fb82-143">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="9fb82-143">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="9fb82-144">本部分演示如何创建一个 ASP.NET MVC 5 应用程序、 添加 SignalR 库，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-144">This section shows how to create an ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="9fb82-145">在 Visual Studio 中，创建面向.NET Framework 4.5 的 C# ASP.NET 应用程序、 其命名为 SignalRChat，并单击确定。</span><span class="sxs-lookup"><span data-stu-id="9fb82-145">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)
2. <span data-ttu-id="9fb82-147">在中`New ASP.NET Project`对话框中，然后选择**MVC**，然后单击**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-147">In the `New ASP.NET Project` dialog, and select **MVC**, and click **Change Authentication**.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)
3. <span data-ttu-id="9fb82-149">选择**无身份验证**中**更改身份验证**对话框中，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-149">Select **No Authentication** in the **Change Authentication** dialog, and click **OK**.</span></span>

    ![选择无身份验证](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="9fb82-151">如果为应用程序中，选择不同的身份验证提供程序`Startup.cs`将为您创建类; 不需要创建您自己`Startup.cs`下面的步骤 10 中的类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-151">If you select a different authentication provider for your application, a `Startup.cs` class will be created for you; you will not need to create your own `Startup.cs` class in step 10 below.</span></span>
4. <span data-ttu-id="9fb82-152">单击**确定**中**新建 ASP.NET 项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="9fb82-152">Click **OK** in the **New ASP.NET Project** dialog.</span></span>
5. <span data-ttu-id="9fb82-153">打开**工具 > NuGet 包管理器 > 程序包管理器控制台**并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9fb82-153">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="9fb82-154">此步骤将一组脚本文件和启用 SignalR 功能的程序集引用添加到项目。</span><span class="sxs-lookup"><span data-stu-id="9fb82-154">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

    `install-package Microsoft.AspNet.SignalR`
6. <span data-ttu-id="9fb82-155">在中**解决方案资源管理器**，展开脚本文件夹。</span><span class="sxs-lookup"><span data-stu-id="9fb82-155">In **Solution Explorer**, expand the Scripts folder.</span></span> <span data-ttu-id="9fb82-156">请注意有关 SignalR 的脚本库已添加到项目。</span><span class="sxs-lookup"><span data-stu-id="9fb82-156">Note that script libraries for SignalR have been added to the project.</span></span>

    ![脚本文件夹](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)
7. <span data-ttu-id="9fb82-158">在中**解决方案资源管理器**，右键单击项目，选择**添加 |新的文件夹**，并添加名为的新文件夹**中心**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-158">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
8. <span data-ttu-id="9fb82-159">右键单击**中心**文件夹中，单击**添加 |新项**，选择**Visual C# |Web |SignalR**中的节点**已安装**窗格中，选择**SignalR Hub 类 (v2)** 在中心窗格中，并创建一个名为的新中心**ChatHub.cs**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-159">Right-click the **Hubs** folder, click **Add | New Item**, select the **Visual C# | Web | SignalR** node in the **Installed** pane, select **SignalR Hub Class (v2)** from the center pane, and create a new hub named **ChatHub.cs**.</span></span> <span data-ttu-id="9fb82-160">将此类用作 SignalR 服务器集线器将消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="9fb82-160">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

    ![创建新的中心](tutorial-getting-started-with-signalr-and-mvc/_static/image6.png)
9. <span data-ttu-id="9fb82-162">中的代码替换**ChatHub**用下面的代码的类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-162">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]
10. <span data-ttu-id="9fb82-163">创建一个名为 Startup.cs 的新类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-163">Create a new class called Startup.cs.</span></span> <span data-ttu-id="9fb82-164">更改为以下文件的内容。</span><span class="sxs-lookup"><span data-stu-id="9fb82-164">Change the contents of the file to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]
11. <span data-ttu-id="9fb82-165">编辑`HomeController`类中找到**controllers/Homecontroller.cs**并将以下方法添加到类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-165">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="9fb82-166">此方法返回**聊天**将在稍后的步骤中创建的视图。</span><span class="sxs-lookup"><span data-stu-id="9fb82-166">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]
12. <span data-ttu-id="9fb82-167">右键单击**Views/Home**文件夹，然后选择**添加...|视图**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-167">Right-click the **Views/Home** folder, and select **Add... | View**.</span></span>
13. <span data-ttu-id="9fb82-168">在中**添加视图**对话框中，命名新视图**聊天**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-168">In the **Add View** dialog, name the new view **Chat**.</span></span>

    ![添加视图](tutorial-getting-started-with-signalr-and-mvc/_static/image7.png)
14. <span data-ttu-id="9fb82-170">内容替换为**Chat.cshtml**用下面的代码。</span><span class="sxs-lookup"><span data-stu-id="9fb82-170">Replace the contents of **Chat.cshtml** with the following code.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9fb82-171">当您将 SignalR 和其他脚本库添加到你的 Visual Studio 项目中时，包管理器可能会安装比本主题中所示的版本更新的 SignalR 脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="9fb82-171">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="9fb82-172">请确保在代码中的脚本引用与脚本库在项目中安装的版本匹配。</span><span class="sxs-lookup"><span data-stu-id="9fb82-172">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]
15. <span data-ttu-id="9fb82-173">**保存所有**项目。</span><span class="sxs-lookup"><span data-stu-id="9fb82-173">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="9fb82-174">运行示例</span><span class="sxs-lookup"><span data-stu-id="9fb82-174">Run the Sample</span></span>

1. <span data-ttu-id="9fb82-175">按 F5 以在调试模式下运行该项目。</span><span class="sxs-lookup"><span data-stu-id="9fb82-175">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="9fb82-176">在浏览器地址行中，追加 **/home/聊天**到项目的默认页的 URL。</span><span class="sxs-lookup"><span data-stu-id="9fb82-176">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="9fb82-177">聊天页面加载中的浏览器实例并提示输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="9fb82-177">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc/_static/image8.png)
3. <span data-ttu-id="9fb82-179">输入用户名称。</span><span class="sxs-lookup"><span data-stu-id="9fb82-179">Enter a user name.</span></span>
4. <span data-ttu-id="9fb82-180">从地址行中的浏览器复制 URL 并将其用于打开两个更多的浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="9fb82-180">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="9fb82-181">在每个浏览器实例中，输入唯一的用户名称。</span><span class="sxs-lookup"><span data-stu-id="9fb82-181">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="9fb82-182">在每个浏览器实例中，添加注释并单击**发送**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-182">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="9fb82-183">注释应显示在浏览器的所有实例。</span><span class="sxs-lookup"><span data-stu-id="9fb82-183">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9fb82-184">此简单的聊天应用程序不维护服务器上的讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="9fb82-184">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="9fb82-185">在中心广播到所有当前用户的注释。</span><span class="sxs-lookup"><span data-stu-id="9fb82-185">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="9fb82-186">加入聊天更高版本的用户将看到消息从时添加它们加入。</span><span class="sxs-lookup"><span data-stu-id="9fb82-186">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="9fb82-187">以下屏幕截图显示在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-187">The following screen shot shows the chat application running in a browser.</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr-and-mvc/_static/image9.png)
7. <span data-ttu-id="9fb82-189">在中**解决方案资源管理器**，检查**脚本文档**节点运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-189">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="9fb82-190">如果使用 Internet Explorer 作为你的浏览器，此节点会显示在调试模式下。</span><span class="sxs-lookup"><span data-stu-id="9fb82-190">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="9fb82-191">没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。</span><span class="sxs-lookup"><span data-stu-id="9fb82-191">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="9fb82-192">此文件管理的 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="9fb82-192">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="9fb82-193">如果使用 Internet Explorer 以外的浏览器，您还可以访问动态**中心**通过浏览到它直接，例如文件 http://mywebsite/signalr/hubs 。</span><span class="sxs-lookup"><span data-stu-id="9fb82-193">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="9fb82-194">检查代码</span><span class="sxs-lookup"><span data-stu-id="9fb82-194">Examine the Code</span></span>

<span data-ttu-id="9fb82-195">SignalR 聊天应用程序演示了两个基本的 SignalR 开发任务： 在服务器上的主要协调对象为创建中心和使用 SignalR jQuery 库来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="9fb82-195">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="9fb82-196">SignalR 集线器</span><span class="sxs-lookup"><span data-stu-id="9fb82-196">SignalR Hubs</span></span>

<span data-ttu-id="9fb82-197">中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-197">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="9fb82-198">派生自**中心**类是一种有用的方式来构建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-198">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="9fb82-199">可以在中心类上创建的公共方法，然后通过调用从网页中的脚本中访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="9fb82-199">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="9fb82-200">在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。</span><span class="sxs-lookup"><span data-stu-id="9fb82-200">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="9fb82-201">在中心反过来将消息发送给所有客户端，通过调用**Clients.All.addNewMessageToPage**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-201">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="9fb82-202">**发送**方法演示了多个中心概念：</span><span class="sxs-lookup"><span data-stu-id="9fb82-202">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="9fb82-203">集线器上声明的公共方法，以便客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="9fb82-203">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="9fb82-204">使用**Microsoft.AspNet.SignalR.Hub.Clients**属性来访问所有客户端连接到此中心。</span><span class="sxs-lookup"><span data-stu-id="9fb82-204">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="9fb82-205">在客户端上调用的函数 (如`addNewMessageToPage`函数) 来更新客户端。</span><span class="sxs-lookup"><span data-stu-id="9fb82-205">Call a function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="9fb82-206">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="9fb82-206">SignalR and jQuery</span></span>

<span data-ttu-id="9fb82-207">**Chat.cshtml**视图文件中的代码示例演示如何使用 SignalR jQuery 库与 SignalR 中心进行通信。</span><span class="sxs-lookup"><span data-stu-id="9fb82-207">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="9fb82-208">在代码中的基本任务创建对自动生成的代理为中心，声明函数的服务器可以调用内容推送到客户端，并启动连接来将消息发送到中心的引用。</span><span class="sxs-lookup"><span data-stu-id="9fb82-208">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="9fb82-209">下面的代码声明对集线器代理的引用。</span><span class="sxs-lookup"><span data-stu-id="9fb82-209">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="9fb82-210">在 JavaScript 中于服务器类及其成员的引用位于混合大小写。</span><span class="sxs-lookup"><span data-stu-id="9fb82-210">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="9fb82-211">代码示例将引用 C# **ChatHub**中作为 JavaScript 类**chatHub**。</span><span class="sxs-lookup"><span data-stu-id="9fb82-211">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span> <span data-ttu-id="9fb82-212">如果你想要引用`ChatHub`类在 jQuery 中使用传统的 Pascal 大小写，就像在 C# 中，编辑 ChatHub.cs 类文件。</span><span class="sxs-lookup"><span data-stu-id="9fb82-212">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="9fb82-213">添加`using`语句来引用`Microsoft.AspNet.SignalR.Hubs`命名空间。</span><span class="sxs-lookup"><span data-stu-id="9fb82-213">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="9fb82-214">然后添加`HubName`归于`ChatHub`类，例如`[HubName("ChatHub")]`。</span><span class="sxs-lookup"><span data-stu-id="9fb82-214">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="9fb82-215">最后，更新到你的 jQuery 引用`ChatHub`类。</span><span class="sxs-lookup"><span data-stu-id="9fb82-215">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="9fb82-216">下面的代码演示如何在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="9fb82-216">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="9fb82-217">在服务器上的中心类会调用此函数可将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="9fb82-217">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="9fb82-218">可选调用`htmlEncode`函数将显示一种方式，以 html 格式显示在页中，作为一种方法，以防止脚本注入之前编码消息内容。</span><span class="sxs-lookup"><span data-stu-id="9fb82-218">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="9fb82-219">下面的代码演示如何在中心打开的连接。</span><span class="sxs-lookup"><span data-stu-id="9fb82-219">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="9fb82-220">代码启动连接，然后将其传递函数来处理单击事件上**发送**聊天页中的按钮。</span><span class="sxs-lookup"><span data-stu-id="9fb82-220">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="9fb82-221">此方法可确保事件处理程序在执行之前建立的连接。</span><span class="sxs-lookup"><span data-stu-id="9fb82-221">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="9fb82-222">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9fb82-222">Next Steps</span></span>

<span data-ttu-id="9fb82-223">您学习了 SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fb82-223">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="9fb82-224">您还学习了几个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建 hub 类以及如何发送和接收来自中心的消息。</span><span class="sxs-lookup"><span data-stu-id="9fb82-224">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="9fb82-225">有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="9fb82-225">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="9fb82-226">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="9fb82-226">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="9fb82-227">若要了解更高级的 SignalR 开发概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="9fb82-227">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="9fb82-228">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="9fb82-228">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="9fb82-229">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="9fb82-229">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="9fb82-230">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="9fb82-230">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
