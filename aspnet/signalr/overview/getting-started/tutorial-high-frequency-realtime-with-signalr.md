---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 教程： 使用 signalr 2 实现高频率实时 |Microsoft Docs
author: pfletcher
description: 本教程演示如何创建使用 ASP.NET SignalR 来提供高频率消息传送功能的 web 应用程序。 高频率内消息传送...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e710980cecf9093ea9046b5790379befb5b61841
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834684"
---
<a name="tutorial-high-frequency-realtime-with-signalr-2"></a><span data-ttu-id="e7721-104">教程： 使用 signalr 2 实现高频率实时</span><span class="sxs-lookup"><span data-stu-id="e7721-104">Tutorial: High-Frequency Realtime with SignalR 2</span></span>
====================
<span data-ttu-id="e7721-105">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e7721-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="e7721-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="e7721-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

> <span data-ttu-id="e7721-107">本教程演示如何创建使用 ASP.NET SignalR 2 提供高频率的消息传送功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-107">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="e7721-108">在这种情况下消息传送高频率意味着费率是固定的; 在发送的更新对于此应用程序，最多 10 个消息的第二个。</span><span class="sxs-lookup"><span data-stu-id="e7721-108">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="e7721-109">将在本教程中创建的应用程序显示用户可以将一个形状。</span><span class="sxs-lookup"><span data-stu-id="e7721-109">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="e7721-110">在所有其他连接的浏览器中的形状位置然后将更新以匹配使用定时的更新拖动形状的位置。</span><span class="sxs-lookup"><span data-stu-id="e7721-110">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="e7721-111">本教程中介绍的概念有实时游戏中的应用程序和其他模拟应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-111">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e7721-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="e7721-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="e7721-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e7721-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="e7721-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e7721-114">.NET 4.5</span></span>
> - <span data-ttu-id="e7721-115">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="e7721-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="e7721-116">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e7721-116">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="e7721-117">若要学习本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e7721-117">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="e7721-118">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e7721-118">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="e7721-119">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7721-119">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="e7721-120">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="e7721-120">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="e7721-121">这将安装 Visual Studio 模板的 SignalR 类，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="e7721-121">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="e7721-122">某些模板 (如**OWIN 启动类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="e7721-122">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="e7721-123">教程版本</span><span class="sxs-lookup"><span data-stu-id="e7721-123">Tutorial Versions</span></span>
> 
> <span data-ttu-id="e7721-124">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e7721-124">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="e7721-125">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="e7721-125">Questions and comments</span></span>
> 
> <span data-ttu-id="e7721-126">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="e7721-126">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e7721-127">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="e7721-127">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="e7721-128">概述</span><span class="sxs-lookup"><span data-stu-id="e7721-128">Overview</span></span>

<span data-ttu-id="e7721-129">本教程演示如何创建应用程序与其他浏览器实时共享对象的状态。</span><span class="sxs-lookup"><span data-stu-id="e7721-129">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="e7721-130">我们将创建应用程序被称为 MoveShape。</span><span class="sxs-lookup"><span data-stu-id="e7721-130">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="e7721-131">MoveShape 页将显示的 HTML Div 元素，用户可拖动;当用户拖动该 Div，其新位置将发送到服务器，然后告知所有其他连接的客户端以更新要匹配的形状的位置。</span><span class="sxs-lookup"><span data-stu-id="e7721-131">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="e7721-133">在本教程中创建的应用程序基于 Damian edwards 提供演示。</span><span class="sxs-lookup"><span data-stu-id="e7721-133">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="e7721-134">可以看到其中包含此演示视频[此处](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)。</span><span class="sxs-lookup"><span data-stu-id="e7721-134">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="e7721-135">本教程将首先演示如何将 SignalR 消息发送时所触发该形状拖动每个事件。</span><span class="sxs-lookup"><span data-stu-id="e7721-135">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="e7721-136">每个连接的客户端然后将更新该形状的本地版本的位置每次收到一条消息。</span><span class="sxs-lookup"><span data-stu-id="e7721-136">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="e7721-137">虽然应用程序将正常使用此方法，这并不建议的编程模型，因为会有获取发送，因此客户端和服务器无法获取过重消息并将会降低性能的消息数没有上限.</span><span class="sxs-lookup"><span data-stu-id="e7721-137">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="e7721-138">在客户端上显示的动画也是不相互连接，每个方法会立即移动形状，而不是移动顺利地为每个新的位置。</span><span class="sxs-lookup"><span data-stu-id="e7721-138">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="e7721-139">本教程的后面部分将演示如何创建将由客户端或服务器，发送消息的最大速率限制的计时器函数以及如何位置之间顺利移动形状。</span><span class="sxs-lookup"><span data-stu-id="e7721-139">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="e7721-140">在本教程中创建的应用程序的最终版本可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)。</span><span class="sxs-lookup"><span data-stu-id="e7721-140">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a).</span></span>

<span data-ttu-id="e7721-141">本教程包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="e7721-141">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="e7721-142">先决条件</span><span class="sxs-lookup"><span data-stu-id="e7721-142">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="e7721-143">创建项目并添加 SignalR 和 JQuery.UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="e7721-143">Create the project and add the SignalR and JQuery.UI NuGet package</span></span>](#createtheproject2013)
- [<span data-ttu-id="e7721-144">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="e7721-144">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="e7721-145">在应用程序启动时启动中心</span><span class="sxs-lookup"><span data-stu-id="e7721-145">Starting the hub when the application starts</span></span>](#startup2013)
- [<span data-ttu-id="e7721-146">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="e7721-146">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="e7721-147">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="e7721-147">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="e7721-148">添加客户端上流畅的动画</span><span class="sxs-lookup"><span data-stu-id="e7721-148">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="e7721-149">执行进一步的步骤</span><span class="sxs-lookup"><span data-stu-id="e7721-149">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="e7721-150">系统必备</span><span class="sxs-lookup"><span data-stu-id="e7721-150">Prerequisites</span></span>

<span data-ttu-id="e7721-151">本教程需要 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="e7721-151">This tutorial requires Visual Studio 2013.</span></span>

<a id="createtheproject2013"></a>

## <a name="create-the-project-and-add-the-signalr-and-jqueryui-nuget-package"></a><span data-ttu-id="e7721-152">创建项目并添加 SignalR 和 JQuery.UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="e7721-152">Create the project and add the SignalR and JQuery.UI NuGet package</span></span>

<span data-ttu-id="e7721-153">在本部分中，我们将创建 Visual Studio 2013 中的项目。</span><span class="sxs-lookup"><span data-stu-id="e7721-153">In this section, we'll create the project in Visual Studio 2013.</span></span>

<span data-ttu-id="e7721-154">以下步骤使用 Visual Studio 2013 创建 ASP.NET 空 Web 应用程序并将添加的 SignalR 和 jQuery.UI 库：</span><span class="sxs-lookup"><span data-stu-id="e7721-154">The following steps use Visual Studio 2013 to create an ASP.NET Empty Web Application and add the SignalR and jQuery.UI libraries:</span></span>

1. <span data-ttu-id="e7721-155">在 Visual Studio 创建 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-155">In Visual Studio create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)
2. <span data-ttu-id="e7721-157">在中**新建 ASP.NET 项目**窗口中，保留**空**选中然后单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="e7721-157">In the **New ASP.NET Project** window, leave **Empty** selected and click **Create Project**.</span></span>

    ![创建空的 web](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
3. <span data-ttu-id="e7721-159">在中**解决方案资源管理器**，右键单击项目，选择**添加 |SignalR Hub 类 (v2)**。</span><span class="sxs-lookup"><span data-stu-id="e7721-159">In **Solution Explorer**, right-click the project, select **Add | SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="e7721-160">将类命名**MoveShapeHub.cs**并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="e7721-160">Name the class **MoveShapeHub.cs** and add it to the project.</span></span> <span data-ttu-id="e7721-161">此步骤将创建**MoveShapeHub**类，并将一组脚本文件和支持 SignalR 的程序集引用添加到项目。</span><span class="sxs-lookup"><span data-stu-id="e7721-161">This step creates the **MoveShapeHub** class and adds to the project a set of script files and assembly references that support SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e7721-162">您还可以将 SignalR 通过单击添加到项目**工具 |库包管理器 |包管理器控制台**并运行命令：</span><span class="sxs-lookup"><span data-stu-id="e7721-162">You can also add SignalR to a project by clicking **Tools | Library Package Manager | Package Manager Console** and running a command:</span></span>

    <span data-ttu-id="e7721-163">`install-package Microsoft.AspNet.SignalR`。</span><span class="sxs-lookup"><span data-stu-id="e7721-163">`install-package Microsoft.AspNet.SignalR`.</span></span> 

    <span data-ttu-id="e7721-164">如果使用控制台来添加 SignalR，SignalR hub 类作为单独的步骤后创建将 SignalR 添加。</span><span class="sxs-lookup"><span data-stu-id="e7721-164">If you use the console to add SignalR, create the SignalR hub class as a separate step after you add SignalR.</span></span>
4. <span data-ttu-id="e7721-165">单击**工具 |库包管理器 |包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="e7721-165">Click **Tools | Library Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="e7721-166">在包管理器窗口中，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e7721-166">In the package manager window, run the following command:</span></span>

    `Install-Package jQuery.UI.Combined`

    <span data-ttu-id="e7721-167">这将安装 jQuery UI 库，这将用于对形状进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="e7721-167">This installs the jQuery UI library, which you'll use to animate the shape.</span></span>
5. <span data-ttu-id="e7721-168">在中**解决方案资源管理器**展开脚本节点。</span><span class="sxs-lookup"><span data-stu-id="e7721-168">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="e7721-169">JQuery、 jQueryUI，和 SignalR 的脚本库将显示在该项目。</span><span class="sxs-lookup"><span data-stu-id="e7721-169">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

    ![脚本库引用](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="e7721-171">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="e7721-171">Create the base application</span></span>

<span data-ttu-id="e7721-172">在本部分中，我们将创建在每个鼠标移动事件向服务器发送形状的位置的浏览器应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-172">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="e7721-173">服务器然后会接收广播到所有其他连接的客户端此信息。</span><span class="sxs-lookup"><span data-stu-id="e7721-173">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="e7721-174">我们将在稍后的部分此应用程序上进行扩展。</span><span class="sxs-lookup"><span data-stu-id="e7721-174">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="e7721-175">如果尚未创建 MoveShapeHub.cs 类中**解决方案资源管理器**，右键单击该项目并选择**添加**，**类...**.将类命名**MoveShapeHub**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="e7721-175">If you haven't already created the MoveShapeHub.cs class, in **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="e7721-176">在新的代码替换为**MoveShapeHub**用下面的代码的类。</span><span class="sxs-lookup"><span data-stu-id="e7721-176">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="e7721-177">`MoveShapeHub`上面类是 SignalR 集线器的实现。</span><span class="sxs-lookup"><span data-stu-id="e7721-177">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="e7721-178">在中作为[SignalR 入门](tutorial-getting-started-with-signalr.md)教程中，中心都有客户端将直接调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e7721-178">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="e7721-179">在这种情况下，客户端将发送一个对象，包含新的服务器，然后获取将广播到所有其他连接的客户端到形状的 X 和 Y 坐标。</span><span class="sxs-lookup"><span data-stu-id="e7721-179">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="e7721-180">SignalR 将自动序列化此对象使用 JSON。</span><span class="sxs-lookup"><span data-stu-id="e7721-180">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="e7721-181">将发送到客户端的对象 (`ShapeModel`) 包含成员来存储该形状的位置。</span><span class="sxs-lookup"><span data-stu-id="e7721-181">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="e7721-182">在服务器上对象的版本还包含成员来跟踪哪些客户端的数据存储，以便指定客户端将不会发送自己的数据。</span><span class="sxs-lookup"><span data-stu-id="e7721-182">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="e7721-183">此成员使用`JsonIgnore`属性以防止进行序列化并发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="e7721-183">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>

<a id="startup2013"></a>
## <a name="starting-the-hub-when-the-application-starts"></a><span data-ttu-id="e7721-184">在应用程序启动时启动中心</span><span class="sxs-lookup"><span data-stu-id="e7721-184">Starting the hub when the application starts</span></span>

1. <span data-ttu-id="e7721-185">接下来，我们将设置到中心的映射，应用程序启动时。</span><span class="sxs-lookup"><span data-stu-id="e7721-185">Next, we'll set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="e7721-186">在 SignalR 2 中，这是通过添加 OWIN 启动类，后者会调用`MapSignalR`时启动类的`Configuration`OWIN 启动时执行方法。</span><span class="sxs-lookup"><span data-stu-id="e7721-186">In SignalR 2, this is done by adding an OWIN startup class, which will call `MapSignalR` when the startup class' `Configuration` method is executed when OWIN starts.</span></span> <span data-ttu-id="e7721-187">将类添加到 OWIN 的启动处理使用`OwinStartup`程序集属性。</span><span class="sxs-lookup"><span data-stu-id="e7721-187">The class is added to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

    <span data-ttu-id="e7721-188">在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |OWIN 启动类**。</span><span class="sxs-lookup"><span data-stu-id="e7721-188">In **Solution Explorer**, right-click the project, then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="e7721-189">将类命名*启动*然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="e7721-189">Name the class *Startup* and click **OK**.</span></span>
2. <span data-ttu-id="e7721-190">将 Startup.cs 的内容更改为以下：</span><span class="sxs-lookup"><span data-stu-id="e7721-190">Change the contents of Startup.cs to the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<a id="client"></a>
## <a name="adding-the-client"></a><span data-ttu-id="e7721-191">添加客户端</span><span class="sxs-lookup"><span data-stu-id="e7721-191">Adding the client</span></span>

1. <span data-ttu-id="e7721-192">接下来，我们将添加客户端。</span><span class="sxs-lookup"><span data-stu-id="e7721-192">Next, we'll add the client.</span></span> <span data-ttu-id="e7721-193">在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="e7721-193">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="e7721-194">在中**添加新项**对话框中，选择**Html 页**。</span><span class="sxs-lookup"><span data-stu-id="e7721-194">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="e7721-195">将该页命名为**Default.html**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="e7721-195">Name the page **Default.html** and click **Add**.</span></span>
2. <span data-ttu-id="e7721-196">在中**解决方案资源管理器**，右键单击刚创建的页，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="e7721-196">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
3. <span data-ttu-id="e7721-197">HTML 页中的默认代码替换为以下代码片段。</span><span class="sxs-lookup"><span data-stu-id="e7721-197">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e7721-198">验证该脚本引用以下匹配项添加到你的项目的 Scripts 文件夹中的包。</span><span class="sxs-lookup"><span data-stu-id="e7721-198">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html)]

    <span data-ttu-id="e7721-199">上面的 HTML 和 JavaScript 代码创建名为形状的红色 Div、 启用形状的拖放行为使用 jQuery 库，并使用形状的`drag`事件以向服务器发送形状的位置。</span><span class="sxs-lookup"><span data-stu-id="e7721-199">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
4. <span data-ttu-id="e7721-200">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-200">Start the application by pressing F5.</span></span> <span data-ttu-id="e7721-201">复制页面的 URL，并将其粘贴到第二个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="e7721-201">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="e7721-202">在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="e7721-202">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="e7721-204">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="e7721-204">Add the client loop</span></span>

<span data-ttu-id="e7721-205">由于发送的每个鼠标移动事件中的形状的位置将创建不必要数量的网络流量，从客户端的消息需要受到限制。</span><span class="sxs-lookup"><span data-stu-id="e7721-205">Since sending the location of the shape on every mouse move event will create an unneccesary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="e7721-206">我们将使用 javascript`setInterval`函数来设置一个循环，将新的位置信息发送到服务器以固定费率。</span><span class="sxs-lookup"><span data-stu-id="e7721-206">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="e7721-207">此循环是"游戏循环"，驱动器的所有功能的游戏或其他模拟重复调用函数的非常基本表示形式。</span><span class="sxs-lookup"><span data-stu-id="e7721-207">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="e7721-208">更新要匹配下面的代码段的 HTML 页面中的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="e7721-208">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html)]

    <span data-ttu-id="e7721-209">更高版本的更新添加了`updateServerModel`函数，它获取名为按固定的频率。</span><span class="sxs-lookup"><span data-stu-id="e7721-209">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="e7721-210">此函数将位置数据发送到服务器时`moved`标志指示是要发送的新位置数据。</span><span class="sxs-lookup"><span data-stu-id="e7721-210">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="e7721-211">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-211">Start the application by pressing F5.</span></span> <span data-ttu-id="e7721-212">复制页面的 URL，并将其粘贴到第二个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="e7721-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="e7721-213">在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="e7721-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="e7721-214">获取发送到服务器的消息数会受到限制，因为动画不会顺利地如前一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="e7721-214">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="e7721-216">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="e7721-216">Add the server loop</span></span>

<span data-ttu-id="e7721-217">在当前应用程序，从服务器发送到客户端的消息转通常它们被接收。</span><span class="sxs-lookup"><span data-stu-id="e7721-217">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="e7721-218">这会产生类似的问题，因为客户端; 上出现过通常需要它们，然后连接可能会变得来路因此可以将消息发送。</span><span class="sxs-lookup"><span data-stu-id="e7721-218">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="e7721-219">本部分介绍如何更新服务器以实现一个计时器，用于限制的传出消息的速率。</span><span class="sxs-lookup"><span data-stu-id="e7721-219">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="e7721-220">内容替换为`MoveShapeHub.cs`使用以下代码片段。</span><span class="sxs-lookup"><span data-stu-id="e7721-220">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="e7721-221">上面的代码中扩展客户端添加`Broadcaster`类，该类将限制传出消息使用`Timer`从.NET framework 类。</span><span class="sxs-lookup"><span data-stu-id="e7721-221">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="e7721-222">由于中心本身是暂时性 （创建每次在需要时），`Broadcaster`将创建为单一实例。</span><span class="sxs-lookup"><span data-stu-id="e7721-222">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="e7721-223">（在.NET 4 中引入） 的迟缓初始化用于将其创建推迟，直到有必要，确保计时器启动之前完全创建第一个集线器实例。</span><span class="sxs-lookup"><span data-stu-id="e7721-223">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="e7721-224">对客户端的调用`UpdateShape`函数然后移出该中心的`UpdateModel`方法，因此它不再接收传入消息时，立即调用。</span><span class="sxs-lookup"><span data-stu-id="e7721-224">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="e7721-225">而是发送到客户端的消息将发送的每秒 25 调用速率受`_broadcastLoop`中的计时器`Broadcaster`类。</span><span class="sxs-lookup"><span data-stu-id="e7721-225">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="e7721-226">最后，而不是调用客户端方法从中心直接`Broadcaster`类需要获取对当前正在运行的中心的引用 (`_hubContext`) 使用`GlobalHost`。</span><span class="sxs-lookup"><span data-stu-id="e7721-226">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="e7721-227">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-227">Start the application by pressing F5.</span></span> <span data-ttu-id="e7721-228">复制页面的 URL，并将其粘贴到第二个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="e7721-228">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="e7721-229">在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="e7721-229">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="e7721-230">不会在浏览器中从上一节中看到的差异，但将被发送到客户端的消息数。</span><span class="sxs-lookup"><span data-stu-id="e7721-230">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="e7721-232">添加客户端上流畅的动画</span><span class="sxs-lookup"><span data-stu-id="e7721-232">Add smooth animation on the client</span></span>

<span data-ttu-id="e7721-233">应用程序几乎已完成，但我们可以进行一更多项改进，在客户端上形状的动态移动以响应服务器消息。</span><span class="sxs-lookup"><span data-stu-id="e7721-233">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="e7721-234">而不是将该形状的位置设置为给定服务器的新位置，我们将使用 JQuery UI 库`animate`函数以其当前和新位置之间顺利移动形状。</span><span class="sxs-lookup"><span data-stu-id="e7721-234">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="e7721-235">更新客户端的`updateShape`方法看起来像下面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="e7721-235">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

    <span data-ttu-id="e7721-236">上面的代码将从旧位置形状移到新服务器 （在本例中为 100 毫秒） 的动画时间间隔内提供。</span><span class="sxs-lookup"><span data-stu-id="e7721-236">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="e7721-237">新动画开始之前清除该形状上运行任何前一个动画。</span><span class="sxs-lookup"><span data-stu-id="e7721-237">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="e7721-238">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7721-238">Start the application by pressing F5.</span></span> <span data-ttu-id="e7721-239">复制页面的 URL，并将其粘贴到第二个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="e7721-239">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="e7721-240">在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="e7721-240">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="e7721-241">在其他窗口中的形状的移动应显示较低即使如及其移动内插时间，而无需一次设置每个传入消息。</span><span class="sxs-lookup"><span data-stu-id="e7721-241">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image8.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="e7721-243">执行进一步的步骤</span><span class="sxs-lookup"><span data-stu-id="e7721-243">Further Steps</span></span>

<span data-ttu-id="e7721-244">在本教程中，已学习了如何发送客户端和服务器之间的高频率消息 SignalR 应用程序进行编程。</span><span class="sxs-lookup"><span data-stu-id="e7721-244">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="e7721-245">这种通信模式可用于开发联机游戏和其他模拟，如[ShootR 游戏使用 SignalR 创建](http://shootr.signalr.net)。</span><span class="sxs-lookup"><span data-stu-id="e7721-245">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="e7721-246">在本教程中创建的完整应用程序可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)。</span><span class="sxs-lookup"><span data-stu-id="e7721-246">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a).</span></span>

<span data-ttu-id="e7721-247">若要了解有关 SignalR 开发概念的详细信息，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="e7721-247">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="e7721-248">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="e7721-248">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="e7721-249">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="e7721-249">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="e7721-250">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="e7721-250">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

<span data-ttu-id="e7721-251">有关如何部署到 Azure 的 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="e7721-251">For a walkthrough on how to deploy a SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="e7721-252">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="e7721-252">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
