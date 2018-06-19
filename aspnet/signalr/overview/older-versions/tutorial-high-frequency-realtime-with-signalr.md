---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: 高频率实时使用 SignalR 1.x |Microsoft 文档
author: pfletcher
description: 本教程演示如何创建的 web 应用程序使用 ASP.NET SignalR 来提供高频率的消息传递功能。 高频率在消息传递...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/16/2013
ms.topic: article
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0c680a7d8b911b2734647948b683d5ff6e47aec4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26505836"
---
<a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="1c3ec-104">高频率实时使用 SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="1c3ec-104">High-Frequency Realtime with SignalR 1.x</span></span>
====================
<span data-ttu-id="1c3ec-105">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="1c3ec-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="1c3ec-106">本教程演示如何创建的 web 应用程序使用 ASP.NET SignalR 来提供高频率的消息传递功能。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="1c3ec-107">在这种情况下消息传送高频率意味着发送，按固定费率; 的更新如果此应用程序，最多 10 条消息，第二个。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="1c3ec-108">你将在本教程中创建应用程序将显示用户可以拖动的形状。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="1c3ec-109">在所有其他连接的浏览器中的形状位置然后将更新以匹配使用定时的更新拖动形状的位置。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="1c3ec-110">在本教程中引入的概念具有实时游戏中的应用程序和其他模拟应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="1c3ec-111">在本教程的注释是欢迎。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="1c3ec-112">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>


## <a name="overview"></a><span data-ttu-id="1c3ec-113">概述</span><span class="sxs-lookup"><span data-stu-id="1c3ec-113">Overview</span></span>

<span data-ttu-id="1c3ec-114">本教程演示如何创建的应用程序与其他实时浏览共享对象的状态。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="1c3ec-115">我们将创建应用程序称为 MoveShape。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="1c3ec-116">MoveShape 页将显示用户可拖动; HTML Div 元素当用户拖动 Div，则其新位置将发送到服务器，然后通知所有其他连接的客户端以更新该形状的位置，以匹配。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="1c3ec-118">在本教程中创建的应用程序基于 Damian Edwards 一个演示。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="1c3ec-119">包含此演示视频，可以查看[此处](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="1c3ec-120">本教程将演示如何从每个事件而激发该形状拖动发送 SignalR 消息启动。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="1c3ec-121">每个连接的客户端然后将更新该形状的本地版本的位置每次收到一条消息。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="1c3ec-122">虽然应用程序将使用此方法起作用，这不是建议的编程模型，因为将获取发送，因此在客户端和服务器无法获取压倒消息和性能将会降低的消息数没有上限.</span><span class="sxs-lookup"><span data-stu-id="1c3ec-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="1c3ec-123">客户端上显示的动画也将不相互连接，因为每个方法中，将立即移动形状，而不是移动顺利到每个新的位置。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="1c3ec-124">本教程的后面部分将演示如何创建限制由客户端或服务器，发送消息的最大速率的计时器函数以及如何位置之间平稳移动形状。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="1c3ec-125">在本教程中创建的应用程序的最终版本可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="1c3ec-126">本教程包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="1c3ec-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="1c3ec-127">先决条件</span><span class="sxs-lookup"><span data-stu-id="1c3ec-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="1c3ec-128">创建项目</span><span class="sxs-lookup"><span data-stu-id="1c3ec-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="1c3ec-129">添加 ASP.NET SignalR 和 JQuery.UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="1c3ec-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="1c3ec-130">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="1c3ec-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="1c3ec-131">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="1c3ec-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="1c3ec-132">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="1c3ec-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="1c3ec-133">客户端上添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="1c3ec-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="1c3ec-134">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1c3ec-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="1c3ec-135">先决条件</span><span class="sxs-lookup"><span data-stu-id="1c3ec-135">Prerequisites</span></span>

<span data-ttu-id="1c3ec-136">本教程需要 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1c3ec-137">如果使用 Visual Studio 2010，则该项目将使用.NET Framework 4 而不是.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="1c3ec-138">如果你正在使用 Visual Studio 2012，建议你安装[ASP.NET 和 Web Tools 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="1c3ec-139">此更新包含新功能，如发布、 新功能的增强功能和新模板。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="1c3ec-140">如果你有 Visual Studio 2010，请确保[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)安装。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="1c3ec-141">创建项目</span><span class="sxs-lookup"><span data-stu-id="1c3ec-141">Create the project</span></span>

<span data-ttu-id="1c3ec-142">在此部分中，我们将创建 Visual Studio 中的项目。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="1c3ec-143">从**文件**菜单上，单击**新项目**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="1c3ec-144">在**新项目**对话框框中，展开**C#** 下**模板**和选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="1c3ec-145">选择**ASP.NET 空 Web 应用程序**模板，将项目*MoveShapeDemo*，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![创建新项目](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="1c3ec-147">添加 SignalR 和 JQuery.UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="1c3ec-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="1c3ec-148">你可以通过安装 NuGet 包添加到项目的 SignalR 功能。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="1c3ec-149">本教程还将使用 JQuery.UI 包允许该形状以拖放，进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="1c3ec-150">单击**工具 |库包管理器 |程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-150">Click **Tools | Library Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="1c3ec-151">在程序包管理器中输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="1c3ec-152">SignalR 包安装大量其他 NuGet 包依赖关系。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="1c3ec-153">完成安装后你将具有所有 ASP.NET 应用程序中使用 SignalR 所需的服务器和客户端组件。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="1c3ec-154">在包管理器控制台，若要安装的 JQuery 和 JQuery.UI 包输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="1c3ec-155">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="1c3ec-155">Create the base application</span></span>

<span data-ttu-id="1c3ec-156">在此部分中，我们将创建的浏览器应用程序在每个鼠标移动事件向服务器发送的形状的位置。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="1c3ec-157">接收到它时，服务器然后广播到所有其他连接的客户端此信息。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="1c3ec-158">我们将在后面的部分中的此应用程序上展开。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="1c3ec-159">在**解决方案资源管理器**，右键单击该项目并选择**添加**，**类...**.将类**MoveShapeHub**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="1c3ec-160">将在新代码**MoveShapeHub**类替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="1c3ec-161">`MoveShapeHub`上面类是 SignalR hub 的实现。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="1c3ec-162">作为 in [Getting Started with SignalR](index.md)教程中，中心有一个客户端将直接调用的方法。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="1c3ec-163">在这种情况下，客户端将发送一个对象，包含新的到服务器，然后获取已将广播到所有其他连接的客户端的形状的 X 和 Y 坐标。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="1c3ec-164">SignalR 将自动进行此对象使用 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="1c3ec-165">将发送到客户端的对象 (`ShapeModel`) 包含成员来存储形状的位置。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="1c3ec-166">在服务器上对象的版本还包含成员来跟踪正在存储哪种客户端的数据，以便给定客户端将不会发送自己的数据。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="1c3ec-167">此成员使用`JsonIgnore`属性以防止其进行序列化并发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="1c3ec-168">接下来，我们将设置中心应用程序启动时。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="1c3ec-169">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |全局应用程序类**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="1c3ec-170">接受默认名称的*全局*单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![添加全局应用程序类](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="1c3ec-172">添加以下`using`后提供语句**使用**Global.asax.cs 类中的语句。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="1c3ec-173">添加以下行中的代码`Application_Start`全局类，以便为 SignalR 注册默认路由的方法。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="1c3ec-174">Global.asax 文件应如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c3ec-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="1c3ec-175">接下来，我们将添加客户端。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-175">Next, we'll add the client.</span></span> <span data-ttu-id="1c3ec-176">在**解决方案资源管理器**，右键单击项目，然后单击**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="1c3ec-177">在**添加新项**对话框中，选择**Html 页**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="1c3ec-178">为页面提供一个适当的名称 (如**Default.html**)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="1c3ec-179">在**解决方案资源管理器**，右键单击你刚刚创建的页面，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="1c3ec-180">在 HTML 页中的默认代码替换为下面的代码段。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c3ec-181">验证脚本引用匹配下面添加到你项目的脚本文件夹中的包。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="1c3ec-182">在 Visual Studio 2010 中，JQuery 和 SignalR 添加到项目的版本可能与下面的版本编号不匹配。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="1c3ec-183">上面的 HTML 和 JavaScript 代码创建红色 Div 调用形状、 启用形状的拖动行为使用 jQuery 库，并使用形状的`drag`事件，以向服务器发送该形状的位置。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="1c3ec-184">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-184">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ec-185">复制页面的 URL，并将其粘贴到另一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ec-186">在浏览器窗口中; 之一中拖动形状在其他浏览器窗口中的形状应将移动。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="1c3ec-188">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="1c3ec-188">Add the client loop</span></span>

<span data-ttu-id="1c3ec-189">由于发送的每个鼠标移动事件上的形状的位置将创建不必要大量网络流量，从客户端的消息需要被阻止。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-189">Since sending the location of the shape on every mouse move event will create an unneccesary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="1c3ec-190">我们将使用 javascript`setInterval`函数设置向按固定费率服务器发送新的位置信息的循环。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="1c3ec-191">此循环是非常基本的表示形式"游戏循环"，驱动器的所有功能的游戏或其他模拟被反复调用函数。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="1c3ec-192">更新要匹配下面的代码段的 HTML 页面中的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="1c3ec-193">上面的更新将添加`updateServerModel`函数，该固定频率会被调用函数。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="1c3ec-194">此函数将位置数据发送到服务器时`moved`标志指示没有要发送的新位置数据。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="1c3ec-195">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-195">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ec-196">复制页面的 URL，并将其粘贴到另一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ec-197">在浏览器窗口中; 之一中拖动形状在其他浏览器窗口中的形状应将移动。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ec-198">获取发送到服务器的消息数将被阻止，因为动画将不会出现顺利如前一节中所示。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="1c3ec-200">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="1c3ec-200">Add the server loop</span></span>

<span data-ttu-id="1c3ec-201">在当前应用程序，从服务器到客户端发送的消息转通常它们被接收。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="1c3ec-202">这显示类似的问题，如客户端; 上发现通常比它们必需的和连接可能会变得溢满因此可以将消息发送。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="1c3ec-203">本部分介绍如何更新服务器以实现的计时器，限制的传出消息的速率。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="1c3ec-204">内容替换`MoveShapeHub.cs`替换为以下代码片段。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="1c3ec-205">上面的代码中扩展客户端添加`Broadcaster`类，该类限制传出消息使用`Timer`从.NET framework 的类。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="1c3ec-206">由于集线器本身是暂时性 （它在每次创建需要它），`Broadcaster`将被创建为单一实例。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="1c3ec-207">（在.NET 4 中引入） 的延迟初始化用于其创建的延迟，直到它需要时，确保计时器启动之前完全创建第一个中心实例。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="1c3ec-208">客户端的调用`UpdateShape`函数然后移出中心的`UpdateModel`方法，因此它不再称为立即每当接收传入消息。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="1c3ec-209">相反，将每秒，25 调用的速率发送到客户端的消息由`_broadcastLoop`中的计时器`Broadcaster`类。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="1c3ec-210">最后，而不是调用客户端方法从中心直接，`Broadcaster`类需要获取对当前正在运行的中心的引用 (`_hubContext`) 使用`GlobalHost`。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="1c3ec-211">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-211">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ec-212">复制页面的 URL，并将其粘贴到另一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ec-213">在浏览器窗口中; 之一中拖动形状在其他浏览器窗口中的形状应将移动。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ec-214">不会在浏览器中从上一节中明显的差异，但将被阻止到客户端发送的消息数。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="1c3ec-216">客户端上添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="1c3ec-216">Add smooth animation on the client</span></span>

<span data-ttu-id="1c3ec-217">应用程序即将完成，但我们无法使一个详细改善，客户端上的形状的动态移动以响应服务器消息。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="1c3ec-218">而不是将形状的位置设置为给定服务器的新位置，我们将使用 JQuery UI 库`animate`函数用于顺利翻其当前和新位置的形状。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="1c3ec-219">更新客户端的`updateShape`方法看起来像下面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="1c3ec-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="1c3ec-220">上面的代码将从旧位置形状移到新服务器获得的高于动画间隔 （以这种情况下，100 毫秒） 的过程。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="1c3ec-221">此新动画在开始之前清除在形状上运行任何前一动画。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="1c3ec-222">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-222">Start the application by pressing F5.</span></span> <span data-ttu-id="1c3ec-223">复制页面的 URL，并将其粘贴到另一个浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="1c3ec-224">在浏览器窗口中; 之一中拖动形状在其他浏览器窗口中的形状应将移动。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="1c3ec-225">在其他窗口中的形状的移动应显示为其移动插值通过时间，而不是每个传入消息一次设置不太平稳。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="1c3ec-227">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1c3ec-227">Further Steps</span></span>

<span data-ttu-id="1c3ec-228">在本教程中，你已了解如何发送客户端和服务器之间的高频率消息 SignalR 应用程序进行编程。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="1c3ec-229">此通信范例可用于开发联机游戏和其他模拟，如[ShootR 游戏使用 SignalR 创建](http://shootr.signalr.net)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="1c3ec-230">在本教程中创建的完整应用程序可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)。</span><span class="sxs-lookup"><span data-stu-id="1c3ec-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="1c3ec-231">若要了解有关 SignalR 开发概念的详细信息，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="1c3ec-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="1c3ec-232">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="1c3ec-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="1c3ec-233">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="1c3ec-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="1c3ec-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="1c3ec-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
