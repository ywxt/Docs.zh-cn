---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 动手实验： 使用 SignalR 实时 Web 应用程序 |Microsoft 文档
author: rick-anderson
description: 实时 Web 应用程序功能推送服务器端的情况下，实时连接的客户端到内容的能力。 对于 ASP.NET 开发人员，ASP...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 5a2bc120ded18ad2302fd6c5cde65a5323e86ca8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878043"
---
<a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="56879-104">使用 SignalR 的动手实验： 实时 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="56879-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>
====================
<span data-ttu-id="56879-105">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="56879-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="56879-106">下载 Web 营地培训工具包</span><span class="sxs-lookup"><span data-stu-id="56879-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="56879-107">实时 Web 应用程序功能推送服务器端的情况下，实时连接的客户端到内容的能力。</span><span class="sxs-lookup"><span data-stu-id="56879-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="56879-108">对于 ASP.NET 开发人员， **ASP.NET SignalR**是一个库将实时 web 功能添加到其应用程序。</span><span class="sxs-lookup"><span data-stu-id="56879-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="56879-109">它充分利用多个传输，自动选择客户端和服务器的最佳可用传输最佳的可用传输。</span><span class="sxs-lookup"><span data-stu-id="56879-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="56879-110">它利用**WebSocket**，HTML5 API，使浏览器和服务器之间的双向通信。</span><span class="sxs-lookup"><span data-stu-id="56879-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="56879-111">**SignalR**拍摄服务器到客户端 RPC 还提供简单、 高级别 API （在从服务器端.NET 代码的客户端的浏览器中调用 JavaScript 函数） 在 ASP.NET 应用程序，以及添加用于连接管理的有用挂钩如连接/断开事件、 分组连接和授权。</span><span class="sxs-lookup"><span data-stu-id="56879-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="56879-112">**SignalR**是上某些要求进行客户端和服务器之间的实时工作的传输的抽象。</span><span class="sxs-lookup"><span data-stu-id="56879-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="56879-113">A **SignalR**连接作为 HTTP，启动，并随后将提升到**WebSocket**如果可用的连接。</span><span class="sxs-lookup"><span data-stu-id="56879-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="56879-114">**WebSocket**是有关的理想传输**SignalR**，因为它使最有效的服务器内存使用具有最低的延迟，并且具有最基础的功能 (如客户端之间的全双工通信和服务器），但它也有最严格的要求： **WebSocket**要求服务器使用**Windows Server 2012**或**Windows 8**，以及 **.NET framework 4.5**。</span><span class="sxs-lookup"><span data-stu-id="56879-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="56879-115">如果不满足这些要求， **SignalR**将尝试使用其他传输，以使其连接 (如*Ajax 长轮询*)。</span><span class="sxs-lookup"><span data-stu-id="56879-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="56879-116">**SignalR** API 包含用于客户端和服务器之间进行通信的两个模型：**永久连接**和**中心**。</span><span class="sxs-lookup"><span data-stu-id="56879-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="56879-117">A**连接**代表一个简单的终结点发送单个接收方组合在一起，或将消息广播。</span><span class="sxs-lookup"><span data-stu-id="56879-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="56879-118">A**中心**是基于连接 API，从而使你的客户端和服务器相互直接调用方法的更多高级管道。</span><span class="sxs-lookup"><span data-stu-id="56879-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 体系结构](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="56879-120">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="56879-120">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="56879-121">概述</span><span class="sxs-lookup"><span data-stu-id="56879-121">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="56879-122">目标</span><span class="sxs-lookup"><span data-stu-id="56879-122">Objectives</span></span>

<span data-ttu-id="56879-123">在此动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="56879-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="56879-124">向使用 SignalR 客户端，从服务器发送通知。</span><span class="sxs-lookup"><span data-stu-id="56879-124">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="56879-125">横向扩展 SignalR 应用程序使用**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="56879-125">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="56879-126">系统必备</span><span class="sxs-lookup"><span data-stu-id="56879-126">Prerequisites</span></span>

<span data-ttu-id="56879-127">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="56879-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="56879-128">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="56879-128">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="56879-129">安装</span><span class="sxs-lookup"><span data-stu-id="56879-129">Setup</span></span>

<span data-ttu-id="56879-130">若要运行本动手实验中的练习，你将需要先设置你的环境。</span><span class="sxs-lookup"><span data-stu-id="56879-130">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="56879-131">打开 Windows 资源管理器窗口并浏览到本实验的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-131">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="56879-132">右键单击**Setup.cmd**和选择**以管理员身份运行**以启动安装过程将配置您的环境并安装本实验的 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="56879-132">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="56879-133">如果显示用户帐户控制对话框中，确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="56879-133">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="56879-134">请确保您已在运行安装程序之前检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="56879-134">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="56879-135">使用代码片段</span><span class="sxs-lookup"><span data-stu-id="56879-135">Using the Code Snippets</span></span>

<span data-ttu-id="56879-136">在整个实验文档中，你将指示要插入代码块。</span><span class="sxs-lookup"><span data-stu-id="56879-136">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="56879-137">为方便起见，大多数的此代码提供作为 Visual Studio 代码段，你可以从访问在 Visual Studio 2013，为了避免必须手动添加它。</span><span class="sxs-lookup"><span data-stu-id="56879-137">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="56879-138">每个练习均附带的开始解决方案位于**开始**本练习，您可以完成相互独立地每个练习的文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-138">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="56879-139">请注意在练习过程中添加的代码段缺少这些开始解决方案中，并且可能不工作，直到完成练习。</span><span class="sxs-lookup"><span data-stu-id="56879-139">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="56879-140">在练习的源代码，你将找到**结束**包含具有完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-140">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="56879-141">如果您在演练本动手实验需要其他帮助，你可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="56879-141">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="56879-142">练习</span><span class="sxs-lookup"><span data-stu-id="56879-142">Exercises</span></span>

<span data-ttu-id="56879-143">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="56879-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="56879-144">使用使用 SignalR 的实时数据</span><span class="sxs-lookup"><span data-stu-id="56879-144">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="56879-145">向外扩展使用的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="56879-145">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="56879-146">估计时间来完成该实验： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="56879-146">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="56879-147">当你首次启动 Visual Studio 时，你必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="56879-147">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="56879-148">每个预定义的集合用于匹配特定的开发风格和确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="56879-148">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="56879-149">在本实验中的过程描述完成给定的任务 Visual Studio 中使用时所需的操作**常规开发设置**集合。</span><span class="sxs-lookup"><span data-stu-id="56879-149">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="56879-150">如果您为开发环境选择不同的设置集合，则表明可能存在你应考虑到帐户的步骤中的差异。</span><span class="sxs-lookup"><span data-stu-id="56879-150">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="56879-151">练习 1： 使用使用 SignalR 的实时数据</span><span class="sxs-lookup"><span data-stu-id="56879-151">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="56879-152">尽管聊天经常使用作为示例，你可以执行整个许多内容与实时 Web 功能。</span><span class="sxs-lookup"><span data-stu-id="56879-152">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="56879-153">用户刷新网页可看到新数据或页实现 Ajax 长轮询要检索新数据，随时可以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="56879-153">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="56879-154">SignalR 支持**服务器推送**或**广播**功能; 它将自动处理的连接管理。</span><span class="sxs-lookup"><span data-stu-id="56879-154">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="56879-155">在经典 HTTP 连接中客户端服务器通信，为每个请求，重新建立连接时，但 SignalR 提供客户端和服务器之间的持续性连接。</span><span class="sxs-lookup"><span data-stu-id="56879-155">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="56879-156">在服务器代码调用到使用远程过程调用 (RPC) 的浏览器中的客户端代码的 SignalR，而不是请求-响应模型我们知道今天。</span><span class="sxs-lookup"><span data-stu-id="56879-156">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="56879-157">在本练习中，您将配置**专家 Quiz**应用程序以使用 SignalR 显示与而无需刷新整个页面的更新度量值统计信息仪表板。</span><span class="sxs-lookup"><span data-stu-id="56879-157">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="56879-158">任务 1 – 浏览专家测验统计信息页</span><span class="sxs-lookup"><span data-stu-id="56879-158">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="56879-159">在此任务中，你将通过应用程序并验证统计信息页的显示方式以及可以如何改进信息的方式更新。</span><span class="sxs-lookup"><span data-stu-id="56879-159">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="56879-160">打开**Visual Studio Express 2013 for Web**并打开**GeekQuiz.sln**解决方案位于**Source\Ex1 WorkingWithRealTimeData\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-160">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="56879-161">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="56879-161">Press **F5** to run the solution.</span></span> <span data-ttu-id="56879-162">**登录**页应出现在浏览器。</span><span class="sxs-lookup"><span data-stu-id="56879-162">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="56879-163">![运行解决方案](real-time-web-applications-with-signalr/_static/image2.png "运行解决方案")</span><span class="sxs-lookup"><span data-stu-id="56879-163">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="56879-164">*运行解决方案*</span><span class="sxs-lookup"><span data-stu-id="56879-164">*Running the solution*</span></span>
3. <span data-ttu-id="56879-165">单击**注册**右上角的页后，可以在应用程序中创建新用户。</span><span class="sxs-lookup"><span data-stu-id="56879-165">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="56879-166">![注册链接](real-time-web-applications-with-signalr/_static/image3.png "注册链接")</span><span class="sxs-lookup"><span data-stu-id="56879-166">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="56879-167">*注册链接*</span><span class="sxs-lookup"><span data-stu-id="56879-167">*Register link*</span></span>
4. <span data-ttu-id="56879-168">在**注册**页上，输入**用户名**和**密码**，然后单击**注册**。</span><span class="sxs-lookup"><span data-stu-id="56879-168">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="56879-169">![注册用户](real-time-web-applications-with-signalr/_static/image4.png "注册用户")</span><span class="sxs-lookup"><span data-stu-id="56879-169">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="56879-170">*注册用户*</span><span class="sxs-lookup"><span data-stu-id="56879-170">*Registering a user*</span></span>
5. <span data-ttu-id="56879-171">应用程序注册新帐户和用户经过身份验证和重定向回主页上显示的第一个测验问题。</span><span class="sxs-lookup"><span data-stu-id="56879-171">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="56879-172">打开**统计信息**页在新窗口中，并将放**主页**页和**统计信息**页上的并行。</span><span class="sxs-lookup"><span data-stu-id="56879-172">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="56879-173">![并排显示 windows](real-time-web-applications-with-signalr/_static/image5.png "并排端 windows")</span><span class="sxs-lookup"><span data-stu-id="56879-173">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="56879-174">*并排显示 windows*</span><span class="sxs-lookup"><span data-stu-id="56879-174">*Side-by-side windows*</span></span>
7. <span data-ttu-id="56879-175">在**主页**页上，通过单击某个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="56879-175">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="56879-176">![回答问题](real-time-web-applications-with-signalr/_static/image6.png "回答问题")</span><span class="sxs-lookup"><span data-stu-id="56879-176">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="56879-177">*回答问题*</span><span class="sxs-lookup"><span data-stu-id="56879-177">*Answering a question*</span></span>
8. <span data-ttu-id="56879-178">单击后的一个按钮，应显示答案。</span><span class="sxs-lookup"><span data-stu-id="56879-178">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="56879-179">![问题答案正确](real-time-web-applications-with-signalr/_static/image7.png "正确回答的问题")</span><span class="sxs-lookup"><span data-stu-id="56879-179">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="56879-180">*正确回答的问题*</span><span class="sxs-lookup"><span data-stu-id="56879-180">*Question answered correctly*</span></span>
9. <span data-ttu-id="56879-181">请注意的统计信息页中提供的信息已过时。</span><span class="sxs-lookup"><span data-stu-id="56879-181">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="56879-182">刷新该页才能看到更新后的结果。</span><span class="sxs-lookup"><span data-stu-id="56879-182">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="56879-183">![统计信息页](real-time-web-applications-with-signalr/_static/image8.png "统计信息页")</span><span class="sxs-lookup"><span data-stu-id="56879-183">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="56879-184">*统计信息页*</span><span class="sxs-lookup"><span data-stu-id="56879-184">*Statistics page*</span></span>
10. <span data-ttu-id="56879-185">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="56879-185">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="56879-186">任务 2 – 添加 SignalR 到奇测验，以显示联机图表</span><span class="sxs-lookup"><span data-stu-id="56879-186">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="56879-187">在此任务中，将向解决方案中添加 SignalR，并将更新发送到客户端自动在新的答案发送到服务器时。</span><span class="sxs-lookup"><span data-stu-id="56879-187">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="56879-188">从**工具**菜单在 Visual Studio 中，选择**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="56879-188">From the **Tools** menu in Visual Studio, select **Library Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="56879-189">在**程序包管理器控制台**窗口中，执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="56879-189">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="56879-190">![SignalR 包安装](real-time-web-applications-with-signalr/_static/image9.png "SignalR 包安装")</span><span class="sxs-lookup"><span data-stu-id="56879-190">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="56879-191">*SignalR 包安装*</span><span class="sxs-lookup"><span data-stu-id="56879-191">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="56879-192">在安装时**SignalR** NuGet 包版本 2.0.2 从全新的 MVC 5 应用程序，你将需要手动更新**OWIN**程序包更新到版本 2.0.1 （或更高版本） 安装 SignalR 前的准备。</span><span class="sxs-lookup"><span data-stu-id="56879-192">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="56879-193">若要执行此操作，你可以执行以下脚本中的**程序包管理器控制台**:</span><span class="sxs-lookup"><span data-stu-id="56879-193">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="56879-194">在 SignalR 将来版本中，将自动更新 OWIN 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="56879-194">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="56879-195">在**解决方案资源管理器**，展开**脚本**文件夹，请注意，SignalR *js*文件已添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="56879-195">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="56879-196">![SignalR JavaScript 引用](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 引用")</span><span class="sxs-lookup"><span data-stu-id="56879-196">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="56879-197">*SignalR JavaScript 引用*</span><span class="sxs-lookup"><span data-stu-id="56879-197">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="56879-198">在**解决方案资源管理器**，右键单击**GeekQuiz**项目，依次选择**添加** | **新文件夹**，并将其命名**中心**。</span><span class="sxs-lookup"><span data-stu-id="56879-198">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="56879-199">右键单击**中心**文件夹，然后选择**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="56879-199">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="56879-200">![添加新项](real-time-web-applications-with-signalr/_static/image11.png "添加新项")</span><span class="sxs-lookup"><span data-stu-id="56879-200">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="56879-201">*添加新项*</span><span class="sxs-lookup"><span data-stu-id="56879-201">*Add new item*</span></span>
6. <span data-ttu-id="56879-202">在**添加新项**对话框中，选择**Visual C# |Web |SignalR**的左窗格中，选择的节点**SignalR Hub Class (v2)** 从中间窗格中，命名该文件**StatisticsHub.cs**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="56879-202">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="56879-203">![添加新项对话框](real-time-web-applications-with-signalr/_static/image12.png "添加新项对话框")</span><span class="sxs-lookup"><span data-stu-id="56879-203">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="56879-204">*添加新项对话框*</span><span class="sxs-lookup"><span data-stu-id="56879-204">*Add new item dialog box*</span></span>
7. <span data-ttu-id="56879-205">中的代码替换**StatisticsHub**类替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="56879-205">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="56879-206">(代码段- *RealTimeSignalR-Ex1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="56879-206">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="56879-207">打开**Startup.cs**并在末尾添加以下行**配置**方法。</span><span class="sxs-lookup"><span data-stu-id="56879-207">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="56879-208">(代码段- *RealTimeSignalR-Ex1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="56879-208">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="56879-209">打开**StatisticsService.cs**页内**服务**文件夹并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="56879-209">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="56879-210">(代码段- *RealTimeSignalR-Ex1-UsingDirectives*)</span><span class="sxs-lookup"><span data-stu-id="56879-210">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="56879-211">若要通知连接的客户端的更新，请首先检索**上下文**当前连接的对象。</span><span class="sxs-lookup"><span data-stu-id="56879-211">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="56879-212">**中心**对象包含用于将消息发送到单个客户端或广播到所有连接的客户端的方法。</span><span class="sxs-lookup"><span data-stu-id="56879-212">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="56879-213">添加以下方法**StatisticsService**类广播的统计信息数据。</span><span class="sxs-lookup"><span data-stu-id="56879-213">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="56879-214">(代码段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="56879-214">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="56879-215">在上面的代码中，你使用的是任意的方法名称在客户端上调用的函数 (即： *updateStatistics*)。</span><span class="sxs-lookup"><span data-stu-id="56879-215">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="56879-216">你指定的方法名称被解释为动态对象，这意味着没有 IntelliSense 或它的编译时验证。</span><span class="sxs-lookup"><span data-stu-id="56879-216">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="56879-217">在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="56879-217">The expression is evaluated at run time.</span></span> <span data-ttu-id="56879-218">当方法调用执行时，SignalR 将方法名称和参数值发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="56879-218">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="56879-219">如果客户端有一个与名称匹配的方法，该方法调用和参数值传递给它。</span><span class="sxs-lookup"><span data-stu-id="56879-219">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="56879-220">如果客户端上不找到任何匹配方法，则不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="56879-220">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="56879-221">有关详细信息，请参阅[ASP.NET SignalR 中心 API 指南](../guide-to-the-api/hubs-api-guide-server.md)。</span><span class="sxs-lookup"><span data-stu-id="56879-221">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="56879-222">打开**TriviaController.cs**页内**控制器**文件夹并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="56879-222">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="56879-223">添加以下突出显示的代码**Post**操作方法。</span><span class="sxs-lookup"><span data-stu-id="56879-223">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="56879-224">(代码段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*)</span><span class="sxs-lookup"><span data-stu-id="56879-224">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="56879-225">打开**Statistics.cshtml**页内**视图 |主页**文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-225">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="56879-226">找到**脚本**部分，并在部分的开头添加以下脚本引用。</span><span class="sxs-lookup"><span data-stu-id="56879-226">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="56879-227">(代码段- *RealTimeSignalR-Ex1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="56879-227">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="56879-228">当你将 SignalR 和其他脚本库添加到 Visual Studio 项目中时，包管理器可能会安装本主题中显示的版本比更新 SignalR 脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="56879-228">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="56879-229">请确保你的代码中的脚本引用匹配在项目中安装的脚本库的版本。</span><span class="sxs-lookup"><span data-stu-id="56879-229">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="56879-230">添加以下突出显示的代码，以将客户端连接到 SignalR 集线器和更新统计信息数据，从中心接收新消息时。</span><span class="sxs-lookup"><span data-stu-id="56879-230">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="56879-231">(代码段- *RealTimeSignalR-Ex1-SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="56879-231">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="56879-232">在此代码中，所以在创建中心代理并注册事件处理程序以侦听的服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="56879-232">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="56879-233">在这种情况下，侦听消息通过发送*updateStatistics*方法。</span><span class="sxs-lookup"><span data-stu-id="56879-233">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="56879-234">任务 3 – 运行解决方案</span><span class="sxs-lookup"><span data-stu-id="56879-234">Task 3 – Running the Solution</span></span>

<span data-ttu-id="56879-235">在此任务中，你将运行该解决方案以验证使用在应答新问题后 SignalR 自动更新统计信息视图。</span><span class="sxs-lookup"><span data-stu-id="56879-235">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="56879-236">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="56879-236">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="56879-237">如果尚未登录到应用程序，使用在任务 1 中创建的用户登录。</span><span class="sxs-lookup"><span data-stu-id="56879-237">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="56879-238">打开**统计信息**页在新窗口中，并将放**主页**页和**统计信息**页上的并行，就像在任务 1 中。</span><span class="sxs-lookup"><span data-stu-id="56879-238">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="56879-239">在**主页**页上，通过单击某个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="56879-239">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="56879-240">![回答另一个问题](real-time-web-applications-with-signalr/_static/image13.png "回答另一个问题")</span><span class="sxs-lookup"><span data-stu-id="56879-240">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="56879-241">*回答另一个问题*</span><span class="sxs-lookup"><span data-stu-id="56879-241">*Answering another question*</span></span>
4. <span data-ttu-id="56879-242">单击后的一个按钮，应显示答案。</span><span class="sxs-lookup"><span data-stu-id="56879-242">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="56879-243">请注意，回答这个问题与更新的信息，而无需刷新整个页面后自动更新页上的统计信息。</span><span class="sxs-lookup"><span data-stu-id="56879-243">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="56879-244">![统计信息页面刷新后应答](real-time-web-applications-with-signalr/_static/image14.png "在应答后刷新统计信息页")</span><span class="sxs-lookup"><span data-stu-id="56879-244">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="56879-245">*刷新后应答的统计信息页*</span><span class="sxs-lookup"><span data-stu-id="56879-245">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="56879-246">练习 2： 向外扩展使用的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="56879-246">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="56879-247">当缩放 web 应用程序，你可以通常选择之间*向上扩展*和*向外扩展*选项。</span><span class="sxs-lookup"><span data-stu-id="56879-247">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="56879-248">*向上扩展*意味着更大的服务器，使用更多的资源 （CPU、 RAM 等） 时*向外扩展*意味着添加更多服务器以处理负载。</span><span class="sxs-lookup"><span data-stu-id="56879-248">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="56879-249">后者的问题是，可以获取客户端路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="56879-249">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="56879-250">连接到一台服务器的客户端不会收到从另一台服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="56879-250">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="56879-251">通过使用名为的组件来解决这些问题*底板*、 邮件服务器之间进行转发。</span><span class="sxs-lookup"><span data-stu-id="56879-251">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="56879-252">启用底板，每个应用程序实例将消息发送到底板，与底板将其转发给其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="56879-252">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="56879-253">目前，有三种类型的适用于 SignalR 的背板：</span><span class="sxs-lookup"><span data-stu-id="56879-253">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="56879-254">**Windows Azure Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="56879-254">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="56879-255">Service Bus 是允许组件发送松散耦合的消息的消息传递基础结构。</span><span class="sxs-lookup"><span data-stu-id="56879-255">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="56879-256">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="56879-256">**SQL Server**.</span></span> <span data-ttu-id="56879-257">SQL Server 底板将消息写入 SQL 表。</span><span class="sxs-lookup"><span data-stu-id="56879-257">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="56879-258">底板为有效的消息传递使用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="56879-258">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="56879-259">但是，它还适用如果未启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="56879-259">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="56879-260">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="56879-260">**Redis**.</span></span> <span data-ttu-id="56879-261">Redis 是一个内存中键 / 值存储。</span><span class="sxs-lookup"><span data-stu-id="56879-261">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="56879-262">Redis 支持发布/订阅 ("pub/sub") 模式，用于将消息发送。</span><span class="sxs-lookup"><span data-stu-id="56879-262">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="56879-263">通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="56879-263">Every message is sent through a message bus.</span></span> <span data-ttu-id="56879-264">消息总线实现[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，从而提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="56879-264">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="56879-265">通过替换默认的工作的底板**IMessageBus**含总线为该底板设计的。</span><span class="sxs-lookup"><span data-stu-id="56879-265">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="56879-266">每个服务器实例连接到通过总线底板。</span><span class="sxs-lookup"><span data-stu-id="56879-266">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="56879-267">发送一条消息，它将转到面板，并底板将其发送到每个服务器。</span><span class="sxs-lookup"><span data-stu-id="56879-267">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="56879-268">当服务器从底板收到一条消息时，它将在其本地缓存中存储消息。</span><span class="sxs-lookup"><span data-stu-id="56879-268">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="56879-269">服务器然后将从其本地缓存消息传送到客户端。</span><span class="sxs-lookup"><span data-stu-id="56879-269">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="56879-270">有关 SignalR 基架的工作原理，阅读此[文章](../performance/scaleout-in-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="56879-270">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="56879-271">有底板可能成为瓶颈的其中一些方案。</span><span class="sxs-lookup"><span data-stu-id="56879-271">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="56879-272">这里有一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="56879-272">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="56879-273">[服务器广播](tutorial-server-broadcast-with-signalr.md)（例如，股票行情）： 背板很适合此方案中，因为该服务器控制速率发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="56879-273">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="56879-274">[客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）： 在此方案中，底板可能成为瓶颈如果的消息数会随着客户端的数量; 也就是说，如果消息的速率增长按比例随着越来越多的客户端将加入。</span><span class="sxs-lookup"><span data-stu-id="56879-274">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="56879-275">[高频率实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）： 底板不建议用于此方案。</span><span class="sxs-lookup"><span data-stu-id="56879-275">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>


<span data-ttu-id="56879-276">在本练习中，你将使用**SQL Server**分发跨邮件**专家 Quiz**应用程序。</span><span class="sxs-lookup"><span data-stu-id="56879-276">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="56879-277">将单个测试计算机以了解如何设置配置，不过，若要获取完整的效果上运行这些任务，你将需要 SignalR 将应用部署到两个或多个服务器。</span><span class="sxs-lookup"><span data-stu-id="56879-277">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="56879-278">在一台服务器，或单独的专用服务器上，还必须安装 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="56879-278">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![横向扩展使用 SQL Server 关系图](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="56879-280">任务 1-了解方案</span><span class="sxs-lookup"><span data-stu-id="56879-280">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="56879-281">在此任务中，你将运行 2 个实例的**专家 Quiz**模拟多个 IIS 实例在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="56879-281">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="56879-282">在此方案，回答琐事问题上一个应用程序时，更新将不会收到第二个实例的统计信息页上。</span><span class="sxs-lookup"><span data-stu-id="56879-282">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="56879-283">此模拟类似于你的应用程序多个实例的部署的环境和使用负载平衡器与它们通信。</span><span class="sxs-lookup"><span data-stu-id="56879-283">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="56879-284">打开**Begin.sln**解决方案位于**源/Ex2-ScalingOutWithSQLServer/开始**文件夹。</span><span class="sxs-lookup"><span data-stu-id="56879-284">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="56879-285">加载后，您将会发现**服务器资源管理器**解决方案必须使用完全相同的两个项目结构但使用不同的名称。</span><span class="sxs-lookup"><span data-stu-id="56879-285">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="56879-286">这将模拟在本地计算机上运行同一应用程序的两个实例。</span><span class="sxs-lookup"><span data-stu-id="56879-286">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="56879-287">![开始解决方案模拟专家测验的 2 个实例](real-time-web-applications-with-signalr/_static/image16.png "开始模拟专家测验的 2 个实例的解决方案")</span><span class="sxs-lookup"><span data-stu-id="56879-287">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="56879-288">*开始解决方案模拟专家测验的 2 个实例*</span><span class="sxs-lookup"><span data-stu-id="56879-288">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="56879-289">打开解决方案的属性页上，右键单击解决方案节点并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="56879-289">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="56879-290">下**启动项目**，选择**多启动项目**和更改**操作**到这两个项目的值*启动*。</span><span class="sxs-lookup"><span data-stu-id="56879-290">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="56879-291">![启动多个项目](real-time-web-applications-with-signalr/_static/image17.png "启动多个项目")</span><span class="sxs-lookup"><span data-stu-id="56879-291">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="56879-292">*启动多个项目*</span><span class="sxs-lookup"><span data-stu-id="56879-292">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="56879-293">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="56879-293">Press **F5** to run the solution.</span></span> <span data-ttu-id="56879-294">应用程序将启动两个实例**专家 Quiz**在不同的端口，模拟的同一个应用程序的多个实例。</span><span class="sxs-lookup"><span data-stu-id="56879-294">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="56879-295">在左侧和右侧屏幕的其他固定浏览器之一。</span><span class="sxs-lookup"><span data-stu-id="56879-295">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="56879-296">使用你的凭据登录或注册一个新用户。</span><span class="sxs-lookup"><span data-stu-id="56879-296">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="56879-297">登录后，在左侧保留琐事页并转到**统计信息**浏览器中的右侧。</span><span class="sxs-lookup"><span data-stu-id="56879-297">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![专家测验并排显示](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="56879-299">*专家测验并排显示*</span><span class="sxs-lookup"><span data-stu-id="56879-299">*Geek Quiz Side by Side*</span></span>

    ![专家测验中不同的端口](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="56879-301">*专家测验中不同的端口*</span><span class="sxs-lookup"><span data-stu-id="56879-301">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="56879-302">左侧的浏览器中启动回答问题，你将注意到，**统计信息**右浏览器中没有进行更新。</span><span class="sxs-lookup"><span data-stu-id="56879-302">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="56879-303">这是因为**SignalR**使用本地缓存，可将消息分布跨其客户端和这种情况下模拟多个实例，因此它们之间不共享缓存。</span><span class="sxs-lookup"><span data-stu-id="56879-303">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="56879-304">你可以验证**SignalR**测试相同的步骤，但是使用的单个应用程序是否工作。</span><span class="sxs-lookup"><span data-stu-id="56879-304">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="56879-305">下面的任务中，你将配置底板在实例上复制消息。</span><span class="sxs-lookup"><span data-stu-id="56879-305">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="56879-306">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="56879-306">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="56879-307">任务 2 – 创建 SQL Server 底板</span><span class="sxs-lookup"><span data-stu-id="56879-307">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="56879-308">在此任务中，你将创建数据库将充当基架**专家 Quiz**应用程序。</span><span class="sxs-lookup"><span data-stu-id="56879-308">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="56879-309">你将使用**SQL Server 对象资源管理器**浏览你的服务器和初始化数据库。</span><span class="sxs-lookup"><span data-stu-id="56879-309">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="56879-310">此外，你将启用**Service Broker**。</span><span class="sxs-lookup"><span data-stu-id="56879-310">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="56879-311">在**Visual Studio**，打开菜单**视图**和选择**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="56879-311">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="56879-312">通过右键单击连接到 LocalDB 实例**SQL Server**节点并选择**添加 SQL Server...** 选项。</span><span class="sxs-lookup"><span data-stu-id="56879-312">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="56879-313">![添加 SQL Server 实例](real-time-web-applications-with-signalr/_static/image20.png "添加 SQL Server 实例")</span><span class="sxs-lookup"><span data-stu-id="56879-313">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="56879-314">*将 SQL Server 实例添加到 SQL Server 对象资源管理器*</span><span class="sxs-lookup"><span data-stu-id="56879-314">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="56879-315">设置**服务器名称**到 *(localdb) \v11.0*并使**Windows 身份验证**作为身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="56879-315">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="56879-316">单击**连接**以继续。</span><span class="sxs-lookup"><span data-stu-id="56879-316">Click **Connect** to continue.</span></span>

    <span data-ttu-id="56879-317">![连接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "连接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="56879-317">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="56879-318">*连接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="56879-318">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="56879-319">现在，你将连接到 LocalDB 实例，你将需要创建将表示 SQL Server 底板 SignalR 的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="56879-319">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="56879-320">要执行此操作，请右键单击**数据库**节点，然后选择**添加新数据库**。</span><span class="sxs-lookup"><span data-stu-id="56879-320">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="56879-321">![将新数据库添加](real-time-web-applications-with-signalr/_static/image22.png "添加新的数据库")</span><span class="sxs-lookup"><span data-stu-id="56879-321">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="56879-322">*添加新的数据库*</span><span class="sxs-lookup"><span data-stu-id="56879-322">*Adding a new database*</span></span>
5. <span data-ttu-id="56879-323">将数据库名称设置为*SignalR*单击**确定**来创建它。</span><span class="sxs-lookup"><span data-stu-id="56879-323">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="56879-324">![创建 SignalR 数据库](real-time-web-applications-with-signalr/_static/image23.png "创建 SignalR 数据库")</span><span class="sxs-lookup"><span data-stu-id="56879-324">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="56879-325">*创建 SignalR 数据库*</span><span class="sxs-lookup"><span data-stu-id="56879-325">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="56879-326">您可以选择数据库的任何名称。</span><span class="sxs-lookup"><span data-stu-id="56879-326">You can choose any name for the database.</span></span>
6. <span data-ttu-id="56879-327">若要从底板更有效地接收更新，建议为数据库启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="56879-327">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="56879-328">Service Broker 提供的消息和队列在 SQL Server 中的本机支持。</span><span class="sxs-lookup"><span data-stu-id="56879-328">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="56879-329">底板也适用于而无需 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="56879-329">The backplane also works without Service Broker.</span></span> <span data-ttu-id="56879-330">通过右键单击数据库并选择打开一个新查询**新查询**。</span><span class="sxs-lookup"><span data-stu-id="56879-330">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="56879-331">![打开新查询](real-time-web-applications-with-signalr/_static/image24.png "打开新查询")</span><span class="sxs-lookup"><span data-stu-id="56879-331">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="56879-332">*打开新查询*</span><span class="sxs-lookup"><span data-stu-id="56879-332">*Opening a New Query*</span></span>
7. <span data-ttu-id="56879-333">若要检查是否启用 Service Broker，请查询**是\_broker\_启用**中的列**sys.databases**目录视图。</span><span class="sxs-lookup"><span data-stu-id="56879-333">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="56879-334">在最近打开的查询窗口中执行以下脚本。</span><span class="sxs-lookup"><span data-stu-id="56879-334">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="56879-335">![查询服务 Broker 状态](real-time-web-applications-with-signalr/_static/image25.png "查询服务代理状态")</span><span class="sxs-lookup"><span data-stu-id="56879-335">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="56879-336">*查询服务代理状态*</span><span class="sxs-lookup"><span data-stu-id="56879-336">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="56879-337">如果值**是\_broker\_启用**数据库中的列是&quot;0&quot;，使用以下命令来启用它。</span><span class="sxs-lookup"><span data-stu-id="56879-337">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="56879-338">替换 **&lt;YOUR 数据库&gt;** 与创建数据库时设置的名称 (例如： SignalR)。</span><span class="sxs-lookup"><span data-stu-id="56879-338">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="56879-339">![启用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "启用 Service Broker")</span><span class="sxs-lookup"><span data-stu-id="56879-339">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="56879-340">*启用 Service Broker*</span><span class="sxs-lookup"><span data-stu-id="56879-340">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="56879-341">如果此查询出现死锁，请确保没有连接到的数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="56879-341">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="56879-342">任务 3 – 配置 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="56879-342">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="56879-343">在此任务中，您将配置**专家 Quiz**连接到 SQL Server 底板。</span><span class="sxs-lookup"><span data-stu-id="56879-343">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="56879-344">首先，你将添加**SignalR.SqlServer** NuGet 包并设置连接字符串以底板数据库。</span><span class="sxs-lookup"><span data-stu-id="56879-344">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="56879-345">打开**程序包管理器控制台**从**工具** | **库程序包管理器**。</span><span class="sxs-lookup"><span data-stu-id="56879-345">Open the **Package Manager Console** from **Tools** | **Library Package Manager**.</span></span> <span data-ttu-id="56879-346">请确保**GeekQuiz**中选择项目**默认项目**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="56879-346">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="56879-347">键入以下命令以安装**Microsoft.AspNet.SignalR.SqlServer** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="56879-347">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="56879-348">对项目重复上一步但这次**GeekQuiz2**。</span><span class="sxs-lookup"><span data-stu-id="56879-348">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="56879-349">若要配置 SQL Server 底板，打开**Startup.cs**文件**GeekQuiz**项目，并添加以下代码**配置**方法。</span><span class="sxs-lookup"><span data-stu-id="56879-349">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="56879-350">替换 **&lt;YOUR 数据库&gt;** 替换为你创建 SQL Server 底板时使用的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="56879-350">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="56879-351">重复此步骤**GeekQuiz2**项目。</span><span class="sxs-lookup"><span data-stu-id="56879-351">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="56879-352">(代码段- *RealTimeSignalR-Ex2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="56879-352">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="56879-353">现在，这两个项目配置为使用 SQL Server 底板，按**F5**同时运行它们。</span><span class="sxs-lookup"><span data-stu-id="56879-353">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="56879-354">同样， **Visual Studio**将启动两个实例**专家 Quiz**中不同的端口。</span><span class="sxs-lookup"><span data-stu-id="56879-354">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="56879-355">在左侧和右侧屏幕的其他固定一个浏览器并登录你的凭据。</span><span class="sxs-lookup"><span data-stu-id="56879-355">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="56879-356">在左侧保留琐事页并转到**统计信息**pagein 右浏览器。</span><span class="sxs-lookup"><span data-stu-id="56879-356">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="56879-357">启动回答问题在左侧的浏览器中。</span><span class="sxs-lookup"><span data-stu-id="56879-357">Start answering questions in the left browser.</span></span> <span data-ttu-id="56879-358">此时，**统计信息**页更新底板感谢。</span><span class="sxs-lookup"><span data-stu-id="56879-358">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="56879-359">应用程序之间切换 (**统计信息**现在位于左侧，和**琐事**位于右侧) 并重复执行测试来验证它正在为两个实例。</span><span class="sxs-lookup"><span data-stu-id="56879-359">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="56879-360">底板用作*共享缓存*消息的每个连接的服务器，且每个服务器将存储消息在其自己要分发到连接的客户端的本地缓存中。</span><span class="sxs-lookup"><span data-stu-id="56879-360">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="56879-361">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="56879-361">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="56879-362">SQL Server 底板组件会自动生成对指定的数据库所需的表。</span><span class="sxs-lookup"><span data-stu-id="56879-362">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="56879-363">在**SQL Server 对象资源管理器**面板中，打开你在底板中创建的数据库 (例如： SignalR) 并展开其表。</span><span class="sxs-lookup"><span data-stu-id="56879-363">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="56879-364">你应该会看到以下表：</span><span class="sxs-lookup"><span data-stu-id="56879-364">You should see the following tables:</span></span>

    ![底板生成表](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="56879-366">*底板生成表*</span><span class="sxs-lookup"><span data-stu-id="56879-366">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="56879-367">右键单击**SignalR.Messages\_0**表，然后选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="56879-367">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![视图 SignalR 基架消息表](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="56879-369">*视图 SignalR 基架消息表*</span><span class="sxs-lookup"><span data-stu-id="56879-369">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="56879-370">你可以看到不同的消息发送到**中心**时回答琐事问题。</span><span class="sxs-lookup"><span data-stu-id="56879-370">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="56879-371">底板将分发到任何连接实例这些消息。</span><span class="sxs-lookup"><span data-stu-id="56879-371">The backplane distributes these messages to any connected instance.</span></span>

    ![底板消息表](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="56879-373">*底板消息表*</span><span class="sxs-lookup"><span data-stu-id="56879-373">*Backplane Messages Table*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="56879-374">总结</span><span class="sxs-lookup"><span data-stu-id="56879-374">Summary</span></span>

<span data-ttu-id="56879-375">在此动手实验中，你学习了如何添加**SignalR**你应用程序和发送通知从服务器到你使用的连接的客户端**中心**。</span><span class="sxs-lookup"><span data-stu-id="56879-375">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="56879-376">此外，您学习了如何通过使用横向扩展你的应用程序*底板*组件时你的应用程序部署在多个 IIS 实例中。</span><span class="sxs-lookup"><span data-stu-id="56879-376">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
