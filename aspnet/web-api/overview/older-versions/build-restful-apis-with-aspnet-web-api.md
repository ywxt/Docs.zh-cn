---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 生成与 ASP.NET Web API RESTful Api |Microsoft 文档
author: rick-anderson
description: 最近几年，它已变得明确 HTTP 并不只是为了提供 HTML 页面。 它也是一个功能强大的平台，用于生成 Web Api，使用几 o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 320409cd395384a608a07307a56d18105d45de14
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="797aa-104">生成与 ASP.NET Web API RESTful Api</span><span class="sxs-lookup"><span data-stu-id="797aa-104">Build RESTful APIs with ASP.NET Web API</span></span>
====================
<span data-ttu-id="797aa-105">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="797aa-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="797aa-106">最近几年，它已变得明确 HTTP 并不只是为了提供 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="797aa-106">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="797aa-107">它也是一个功能强大的平台，用于生成 Web Api，使用少量的谓词 （GET、 POST 和等） 以及几个简单的概念类似于*Uri*和*标头*。</span><span class="sxs-lookup"><span data-stu-id="797aa-107">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="797aa-108">ASP.NET Web API 是一组组件，用于简化 HTTP 编程。</span><span class="sxs-lookup"><span data-stu-id="797aa-108">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="797aa-109">由于它构建基于 ASP.NET MVC 运行时，Web API 将自动处理 HTTP 低级别的传输详细的信息。</span><span class="sxs-lookup"><span data-stu-id="797aa-109">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="797aa-110">同时，Web API 自然公开 HTTP 编程模型。</span><span class="sxs-lookup"><span data-stu-id="797aa-110">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="797aa-111">事实上，Web api 的一个目标是为*不*抽象化 HTTP 的现实。</span><span class="sxs-lookup"><span data-stu-id="797aa-111">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="797aa-112">因此，Web API 是灵活且易于扩展。</span><span class="sxs-lookup"><span data-stu-id="797aa-112">As a result, Web API is both flexible and easy to extend.</span></span> <span data-ttu-id="797aa-113">在此动手实验中，你将使用 Web API 构建一个简单的 REST API 为联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-113">In this hands-on lab, you will use Web API to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="797aa-114">你还将建立客户端使用该 API。</span><span class="sxs-lookup"><span data-stu-id="797aa-114">You will also build a client to consume the API.</span></span> <span data-ttu-id="797aa-115">REST 体系结构样式已被证明是一种利用 HTTP 的有效方法，尽管它肯定不是唯一有效的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="797aa-115">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="797aa-116">联系人管理器将公开用于列出、 添加和删除联系人，以及其他基于 Rest。</span><span class="sxs-lookup"><span data-stu-id="797aa-116">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> <span data-ttu-id="797aa-117">本实验需要基本了解 HTTP，其余部分，并且假定你已基本了解 HTML、 JavaScript 和 jQuery。</span><span class="sxs-lookup"><span data-stu-id="797aa-117">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="797aa-118">ASP.NET Web 站点有专用于在 ASP.NET Web API 框架的区域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="797aa-118">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="797aa-119">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它经常检查如果你想要深入探讨创建可用于几乎任何设备或开发框架自定义 Web Api 的技巧。</span><span class="sxs-lookup"><span data-stu-id="797aa-119">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="797aa-120">ASP.NET Web API，类似于 ASP.NET MVC 4，具有很大的灵活性，以将服务层与允许你同时使用多个可用的依赖关系注入框架变得相当容易控制器分开。</span><span class="sxs-lookup"><span data-stu-id="797aa-120">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="797aa-121">没有很好的示例演示如何使用你可以下载它从 ASP.NET Web API 项目中的依赖关系注入 Ninject 的 MSDN 中[此处](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)。</span><span class="sxs-lookup"><span data-stu-id="797aa-121">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="797aa-122">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="797aa-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="797aa-123">目标</span><span class="sxs-lookup"><span data-stu-id="797aa-123">Objectives</span></span>

<span data-ttu-id="797aa-124">在此动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="797aa-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="797aa-125">实现 rest 样式 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-125">Implement a RESTful Web API</span></span>
- <span data-ttu-id="797aa-126">从 HTML 客户端调用 API</span><span class="sxs-lookup"><span data-stu-id="797aa-126">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="797aa-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="797aa-127">Prerequisites</span></span>

<span data-ttu-id="797aa-128">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="797aa-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="797aa-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="797aa-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="797aa-130">安装</span><span class="sxs-lookup"><span data-stu-id="797aa-130">Setup</span></span>

<span data-ttu-id="797aa-131">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="797aa-131">**Installing Code Snippets**</span></span>

<span data-ttu-id="797aa-132">为方便起见，你将沿此实验室管理大部分都是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="797aa-132">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="797aa-133">若要安装运行的代码段**.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-133">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="797aa-134">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 a： 使用代码段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="797aa-134">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="797aa-135">练习</span><span class="sxs-lookup"><span data-stu-id="797aa-135">Exercises</span></span>

<span data-ttu-id="797aa-136">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="797aa-136">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="797aa-137">练习 1： 创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-137">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="797aa-138">练习 2： 创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-138">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="797aa-139">练习 3： 使用 HTML 客户端从 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-139">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="797aa-140">每个练习均附带由**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="797aa-140">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="797aa-141">如果你需要通过在练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="797aa-141">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="797aa-142">估计时间来完成该实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="797aa-142">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="797aa-143">练习 1： 创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-143">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="797aa-144">在此练习中，将为联系人管理器实现只读的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="797aa-144">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="797aa-145">任务 1-创建 API 项目</span><span class="sxs-lookup"><span data-stu-id="797aa-145">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="797aa-146">在此任务中，你将使用新的 ASP.NET web 项目模板创建 Web API 的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-146">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="797aa-147">运行**Visual Studio 2012 Express for Web**，为此请转到**启动**和类型**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="797aa-147">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="797aa-148">从**文件**菜单上，选择**新项目**。</span><span class="sxs-lookup"><span data-stu-id="797aa-148">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="797aa-149">选择**Visual C# |Web**项目类型从项目类型树视图，然后选择**ASP.NET MVC 4 Web 应用程序**项目类型。</span><span class="sxs-lookup"><span data-stu-id="797aa-149">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="797aa-150">设置项目的**名称**到*ContactManager*和**解决方案名称**到*开始*，然后单击**确定**.</span><span class="sxs-lookup"><span data-stu-id="797aa-150">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="797aa-151">![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")</span><span class="sxs-lookup"><span data-stu-id="797aa-151">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="797aa-152">*创建新的 ASP.NET MVC 4.0 Web 应用程序项目*</span><span class="sxs-lookup"><span data-stu-id="797aa-152">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="797aa-153">在 ASP.NET MVC 4 项目的类型对话框中，选择**Web API**项目类型。</span><span class="sxs-lookup"><span data-stu-id="797aa-153">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="797aa-154">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="797aa-154">Click **OK**.</span></span>

    <span data-ttu-id="797aa-155">![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")</span><span class="sxs-lookup"><span data-stu-id="797aa-155">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="797aa-156">*指定 Web API 项目类型*</span><span class="sxs-lookup"><span data-stu-id="797aa-156">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="797aa-157">任务 2-创建联系人管理器 API 控制器</span><span class="sxs-lookup"><span data-stu-id="797aa-157">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="797aa-158">在此任务中，你将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="797aa-158">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="797aa-159">删除名为的文件**ValuesController.cs**内**控制器**从项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="797aa-159">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="797aa-160">右键单击**控制器**文件夹中该项目并选择**添加 |控制器**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="797aa-160">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="797aa-161">![向项目添加新的控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新控制器")</span><span class="sxs-lookup"><span data-stu-id="797aa-161">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="797aa-162">*向项目添加新控制器*</span><span class="sxs-lookup"><span data-stu-id="797aa-162">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="797aa-163">在**添加控制器**对话框中，选择**空 API 控制器**的模板菜单中。</span><span class="sxs-lookup"><span data-stu-id="797aa-163">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="797aa-164">将控制器类**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="797aa-164">Name the controller class **ContactController**.</span></span> <span data-ttu-id="797aa-165">然后，单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="797aa-165">Then, click **Add.**</span></span>

    <span data-ttu-id="797aa-166">![使用添加控制器对话框创建一个新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用添加控制器对话框创建一个新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="797aa-166">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="797aa-167">*使用添加控制器对话框创建一个新的 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="797aa-167">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="797aa-168">以下代码添加到**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="797aa-168">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="797aa-169">(代码段- *Web API 实验-Ex01-Get API 方法*)</span><span class="sxs-lookup"><span data-stu-id="797aa-169">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="797aa-170">按**F5**调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-170">Press **F5** to debug the application.</span></span> <span data-ttu-id="797aa-171">Web API 项目的默认主页应显示。</span><span class="sxs-lookup"><span data-stu-id="797aa-171">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="797aa-172">![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")</span><span class="sxs-lookup"><span data-stu-id="797aa-172">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="797aa-173">*ASP.NET Web API 应用程序的默认主页*</span><span class="sxs-lookup"><span data-stu-id="797aa-173">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="797aa-174">在 Internet Explorer 窗口中，按**F12**键以打开**开发人员工具**窗口。</span><span class="sxs-lookup"><span data-stu-id="797aa-174">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="797aa-175">单击**网络**选项卡上，并依次**启动捕获**按钮以开始到窗口中捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="797aa-175">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="797aa-176">![打开网络选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开网络选项卡并启动网络捕获")</span><span class="sxs-lookup"><span data-stu-id="797aa-176">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="797aa-177">*打开网络选项卡并启动网络捕获*</span><span class="sxs-lookup"><span data-stu-id="797aa-177">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="797aa-178">追加与浏览器的地址栏中的 URL **/api/联系人**，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="797aa-178">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="797aa-179">传输详细信息会在网络捕获窗口中显示。</span><span class="sxs-lookup"><span data-stu-id="797aa-179">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="797aa-180">请注意，响应的 MIME 类型是**应用程序/json**。</span><span class="sxs-lookup"><span data-stu-id="797aa-180">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="797aa-181">此示例演示如何将默认输出格式为 JSON。</span><span class="sxs-lookup"><span data-stu-id="797aa-181">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="797aa-182">![在网络视图中查看 Web API 请求的输出中](build-restful-apis-with-aspnet-web-api/_static/image7.png "在网络视图中查看的 Web API 请求的输出")</span><span class="sxs-lookup"><span data-stu-id="797aa-182">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="797aa-183">*在网络视图中查看的 Web API 请求的输出*</span><span class="sxs-lookup"><span data-stu-id="797aa-183">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-184">Internet Explorer 10 的默认行为在这将会询问如果用户想要保存或打开的 Web API 调用导致的流。</span><span class="sxs-lookup"><span data-stu-id="797aa-184">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="797aa-185">输出将包含 Web API URL 调用的 JSON 结果的文本文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-185">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="797aa-186">若要观看通过开发人员工具窗口的响应的内容无法取消对话框。</span><span class="sxs-lookup"><span data-stu-id="797aa-186">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="797aa-187">单击**转到详细视图**按钮以查看有关此 API 调用的响应的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="797aa-187">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="797aa-188">![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")</span><span class="sxs-lookup"><span data-stu-id="797aa-188">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="797aa-189">*切换到详细视图*</span><span class="sxs-lookup"><span data-stu-id="797aa-189">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="797aa-190">单击**响应正文**选项卡以查看实际的 JSON 响应文本。</span><span class="sxs-lookup"><span data-stu-id="797aa-190">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="797aa-191">![查看 JSON 输出中网络监视器文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看 JSON 输出中网络监视器的文本")</span><span class="sxs-lookup"><span data-stu-id="797aa-191">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="797aa-192">*在网络监视器中查看的 JSON 输出文本*</span><span class="sxs-lookup"><span data-stu-id="797aa-192">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="797aa-193">任务 3-创建联系人模型和补充联系人控制器</span><span class="sxs-lookup"><span data-stu-id="797aa-193">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="797aa-194">在此任务中，你将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="797aa-194">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="797aa-195">右键单击**模型**文件夹，然后选择**添加 |类...**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="797aa-195">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="797aa-196">![将新的模型添加到 web 应用程序](build-restful-apis-with-aspnet-web-api/_static/image10.png "将新的模型添加到 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="797aa-196">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="797aa-197">*将新的模型添加到 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="797aa-197">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="797aa-198">在**添加新项**对话框中，将新文件**Contact.cs**单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="797aa-198">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="797aa-199">![创建新的联系人类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的联系人类文件")</span><span class="sxs-lookup"><span data-stu-id="797aa-199">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="797aa-200">*创建新的联系人类文件*</span><span class="sxs-lookup"><span data-stu-id="797aa-200">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="797aa-201">添加以下突出显示的代码**联系人**类。</span><span class="sxs-lookup"><span data-stu-id="797aa-201">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="797aa-202">(代码段- *Web API 实验-Ex01-联系人类*)</span><span class="sxs-lookup"><span data-stu-id="797aa-202">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>


~~~
[!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
~~~
4. <span data-ttu-id="797aa-203">在**ContactController**类中，选择 word**字符串**方法定义中**获取**方法和类型单词*联系人*。</span><span class="sxs-lookup"><span data-stu-id="797aa-203">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="797aa-204">中键入的单词后, 一个指示器将出现在单词的开头**联系人**。</span><span class="sxs-lookup"><span data-stu-id="797aa-204">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="797aa-205">可以按住**Ctrl**键和按句点 （.） 键或单击使用鼠标以打开代码编辑器中，以自动填充中的帮助对话框图标**使用**指令的模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="797aa-205">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![对于命名空间声明中使用 Intellisense 帮助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="797aa-207">*对于命名空间声明中使用 Intellisense 帮助*</span><span class="sxs-lookup"><span data-stu-id="797aa-207">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="797aa-208">修改的代码**获取**方法，以便它返回的联系人模型实例数组。</span><span class="sxs-lookup"><span data-stu-id="797aa-208">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="797aa-209">(代码段-*返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="797aa-209">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="797aa-210">按**F5**调试 web 应用程序在浏览器中的。</span><span class="sxs-lookup"><span data-stu-id="797aa-210">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="797aa-211">若要查看到 API 的响应输出所做的更改，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="797aa-211">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="797aa-212">浏览器打开后，按**F12**如果开发人员工具还不打开。</span><span class="sxs-lookup"><span data-stu-id="797aa-212">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="797aa-213">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="797aa-213">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="797aa-214">按**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-214">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="797aa-215">添加 URL 后缀**/api/联系人**到地址栏，然后按 URL **Enter**密钥。</span><span class="sxs-lookup"><span data-stu-id="797aa-215">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="797aa-216">按**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-216">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="797aa-217">选择**响应正文**选项卡。你应看到表示联系人实例的数组的序列化的格式的 JSON 字符串。</span><span class="sxs-lookup"><span data-stu-id="797aa-217">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="797aa-218">![JSON 序列化复杂的 Web API 方法调用的输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 序列化复杂的 Web API 方法调用的输出")</span><span class="sxs-lookup"><span data-stu-id="797aa-218">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="797aa-219">*复杂的 Web API 方法调用的序列化的 JSON 输出*</span><span class="sxs-lookup"><span data-stu-id="797aa-219">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="797aa-220">任务 4-解压功能集成到服务层</span><span class="sxs-lookup"><span data-stu-id="797aa-220">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="797aa-221">此任务将演示如何提取到服务层，以便可以方便开发人员能够从控制器层，从而允许的实际完成工作的服务的可重用性分隔其服务功能的功能。</span><span class="sxs-lookup"><span data-stu-id="797aa-221">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="797aa-222">在解决方案根目录中创建一个新文件夹并将其命名**服务**。</span><span class="sxs-lookup"><span data-stu-id="797aa-222">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="797aa-223">要执行此操作，请右键单击**ContactManager**项目，依次选择**添加** | **新文件夹**，将其命名为*服务*。</span><span class="sxs-lookup"><span data-stu-id="797aa-223">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="797aa-224">![创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "创建服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="797aa-224">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="797aa-225">*创建服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="797aa-225">*Creating Services folder*</span></span>
2. <span data-ttu-id="797aa-226">右键单击**服务**文件夹，然后选择**添加 |类...**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="797aa-226">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="797aa-227">![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="797aa-227">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="797aa-228">*将新类添加到服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="797aa-228">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="797aa-229">当**添加新项**对话框出现时，将新类**ContactRepository**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="797aa-229">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="797aa-230">![创建要包含联系人存储库服务层的代码的类文件](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")</span><span class="sxs-lookup"><span data-stu-id="797aa-230">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="797aa-231">*创建一个类文件以包含联系人存储库服务层的代码*</span><span class="sxs-lookup"><span data-stu-id="797aa-231">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="797aa-232">添加一条 using 指令至**ContactRepository.cs**文件以包括模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="797aa-232">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>


~~~
[!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
~~~
5. <span data-ttu-id="797aa-233">添加以下突出显示的代码**ContactRepository.cs**文件实现 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="797aa-233">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="797aa-234">(代码段- *Web API 实验-Ex01-联系存储库*)</span><span class="sxs-lookup"><span data-stu-id="797aa-234">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="797aa-235">打开**ContactController.cs**如果尚未打开文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-235">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="797aa-236">将以下代码添加到该文件的命名空间声明部分使用语句。</span><span class="sxs-lookup"><span data-stu-id="797aa-236">Add the following using statement to the namespace declaration section of the file.</span></span>


~~~
[!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
~~~
8. <span data-ttu-id="797aa-237">添加以下突出显示的代码**ContactController.cs**类添加一个私有字段来表示实例存储库，以便成员可以产生的类的其余部分使用的服务实现。</span><span class="sxs-lookup"><span data-stu-id="797aa-237">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="797aa-238">(代码段-*的 Web API 实验-Ex01-联系控制器*)</span><span class="sxs-lookup"><span data-stu-id="797aa-238">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="797aa-239">更改**获取**方法，以便它可以使用的联系人的存储库服务。</span><span class="sxs-lookup"><span data-stu-id="797aa-239">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="797aa-240">(代码段-*通过存储库中返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="797aa-240">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="797aa-241">放置一个断点**ContactController**的**获取**方法定义。</span><span class="sxs-lookup"><span data-stu-id="797aa-241">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="797aa-242">![将断点添加到联系人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "将断点添加到联系人控制器")</span><span class="sxs-lookup"><span data-stu-id="797aa-242">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="797aa-243">*将断点添加到联系人控制器*</span><span class="sxs-lookup"><span data-stu-id="797aa-243">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="797aa-244">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-244">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="797aa-245">当浏览器打开后时，按**F12**打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="797aa-245">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="797aa-246">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="797aa-246">Click the **Network** tab.</span></span>
14. <span data-ttu-id="797aa-247">单击**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-247">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="797aa-248">追加后缀的地址栏中的 URL **/api/联系人**按**Enter**加载 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="797aa-248">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="797aa-249">Visual Studio 2012 应会一次中断**获取**方法开始执行。</span><span class="sxs-lookup"><span data-stu-id="797aa-249">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="797aa-250">![Get 方法中的重大](build-restful-apis-with-aspnet-web-api/_static/image18.png "重大内 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="797aa-250">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="797aa-251">*Get 方法中的重大*</span><span class="sxs-lookup"><span data-stu-id="797aa-251">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="797aa-252">按 F5 继续。</span><span class="sxs-lookup"><span data-stu-id="797aa-252">Press **F5** to continue.</span></span>
18. <span data-ttu-id="797aa-253">返回到 Internet Explorer 如果尚不具有焦点。</span><span class="sxs-lookup"><span data-stu-id="797aa-253">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="797aa-254">请注意网络捕获窗口。</span><span class="sxs-lookup"><span data-stu-id="797aa-254">Note the network capture window.</span></span>

    <span data-ttu-id="797aa-255">![网络中显示的 Web API 调用的结果的 Internet 资源管理器视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "网络中显示的 Web API 调用的结果的 Internet 资源管理器视图")</span><span class="sxs-lookup"><span data-stu-id="797aa-255">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="797aa-256">*在 Internet Explorer 中显示的 Web API 调用的结果的网络视图*</span><span class="sxs-lookup"><span data-stu-id="797aa-256">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="797aa-257">单击**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-257">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="797aa-258">单击**响应正文**选项卡。请注意 API 调用中，和它如何表示检索的服务层的两个联系人的 JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="797aa-258">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="797aa-259">![在开发人员工具窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "在开发人员工具窗口中查看 Web API 的 JSON 输出")</span><span class="sxs-lookup"><span data-stu-id="797aa-259">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="797aa-260">*在开发人员工具窗口中查看 Web API 的 JSON 输出*</span><span class="sxs-lookup"><span data-stu-id="797aa-260">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="797aa-261">练习 2： 创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-261">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="797aa-262">在本练习中，你将实现 POST 和 PUT 方法联系人管理器中，若要使用数据编辑功能启用它。</span><span class="sxs-lookup"><span data-stu-id="797aa-262">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="797aa-263">任务 1-打开 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="797aa-263">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="797aa-264">在此任务中，你将准备增强，以便它可以接受用户输入在练习 1 中创建的 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="797aa-264">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="797aa-265">运行**Visual Studio 2012 Express for Web**，为此请转到**启动**和类型**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="797aa-265">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="797aa-266">打开**开始**解决方案位于**源/Ex02-ReadWriteWebAPI/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="797aa-266">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="797aa-267">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="797aa-267">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="797aa-268">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="797aa-268">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="797aa-269">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="797aa-269">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="797aa-270">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="797aa-270">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="797aa-271">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="797aa-271">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="797aa-272">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="797aa-272">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="797aa-273">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="797aa-273">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="797aa-274">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="797aa-274">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="797aa-275">打开**Services/ContactRepository.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-275">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="797aa-276">任务 2-添加的联系人的存储库实现的数据暂留功能</span><span class="sxs-lookup"><span data-stu-id="797aa-276">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="797aa-277">在此任务中，将增加，以便它可以保留并接受用户输入和新的联系人实例在练习 1 中创建的 Web API 项目 ContactRepository 类。</span><span class="sxs-lookup"><span data-stu-id="797aa-277">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="797aa-278">添加以下常量为**ContactRepository**类来表示 web 服务器缓存项键名称的更高版本在本练习中的名称。</span><span class="sxs-lookup"><span data-stu-id="797aa-278">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="797aa-279">添加到一个构造函数**ContactRepository**包含下面的代码。</span><span class="sxs-lookup"><span data-stu-id="797aa-279">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="797aa-280">(代码段- *Web API 实验-Ex02 的联系人的存储库构造函数*)</span><span class="sxs-lookup"><span data-stu-id="797aa-280">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="797aa-281">修改的代码**GetAllContacts**方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="797aa-281">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="797aa-282">(代码段- *Web API 实验-Ex02-获取所有联系人*)</span><span class="sxs-lookup"><span data-stu-id="797aa-282">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="797aa-283">此示例出于演示目的，并将使用 web 服务器的缓存作为存储媒体，以便值将可供多个客户端同时，而不使用会话存储机制或请求存储生存期。</span><span class="sxs-lookup"><span data-stu-id="797aa-283">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="797aa-284">可以使用实体框架、 XML 存储或任何其他各种代替 web 服务器缓存。</span><span class="sxs-lookup"><span data-stu-id="797aa-284">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="797aa-285">实现一个名为的新方法**SaveContact**到**ContactRepository**类来执行将联系人保存的工作。</span><span class="sxs-lookup"><span data-stu-id="797aa-285">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="797aa-286">**SaveContact**方法应采用单个**联系人**参数和返回一个布尔值，该值指示成功或失败。</span><span class="sxs-lookup"><span data-stu-id="797aa-286">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="797aa-287">(代码段- *Web API 实验-Ex02-实现 SaveContact 方法*)</span><span class="sxs-lookup"><span data-stu-id="797aa-287">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="797aa-288">练习 3： 使用 HTML 客户端从 Web API</span><span class="sxs-lookup"><span data-stu-id="797aa-288">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="797aa-289">在此练习中，你将创建 HTML 客户端调用 Web API。</span><span class="sxs-lookup"><span data-stu-id="797aa-289">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="797aa-290">此客户端将使用 Web API 使用 JavaScript 方便数据交换，并将在 web 浏览器使用 HTML 标记中显示结果。</span><span class="sxs-lookup"><span data-stu-id="797aa-290">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="797aa-291">任务 1-修改该索引视图，以提供用于显示联系人的 GUI</span><span class="sxs-lookup"><span data-stu-id="797aa-291">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="797aa-292">在此任务中，你将要修改默认索引视图的 web 应用程序以支持在 HTML 浏览器中显示现有联系人的列表的要求。</span><span class="sxs-lookup"><span data-stu-id="797aa-292">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="797aa-293">打开**Visual Studio 2012 Express for Web**如果尚未打开。</span><span class="sxs-lookup"><span data-stu-id="797aa-293">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="797aa-294">打开**开始**解决方案位于**源/Ex03-ConsumingWebAPI/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="797aa-294">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="797aa-295">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="797aa-295">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="797aa-296">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="797aa-296">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="797aa-297">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="797aa-297">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="797aa-298">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="797aa-298">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="797aa-299">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="797aa-299">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="797aa-300">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="797aa-300">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="797aa-301">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="797aa-301">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="797aa-302">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="797aa-302">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="797aa-303">打开**Index.cshtml**文件位于**视图/主页**文件夹。</span><span class="sxs-lookup"><span data-stu-id="797aa-303">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="797aa-304">在 div 元素的 HTML 代码替换 id**正文**以便其类似下列代码所示。</span><span class="sxs-lookup"><span data-stu-id="797aa-304">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>


~~~
[!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
~~~
5. <span data-ttu-id="797aa-305">在执行对 Web API 的 HTTP 请求的文件的底部添加以下 Javascript 代码。</span><span class="sxs-lookup"><span data-stu-id="797aa-305">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>


~~~
[!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
~~~
6. <span data-ttu-id="797aa-306">打开**ContactController.cs**如果尚未打开文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-306">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="797aa-307">上放置一个断点**获取**方法**ContactController**类。</span><span class="sxs-lookup"><span data-stu-id="797aa-307">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="797aa-308">![将断点放置在 API 控制器的 Get 方法](build-restful-apis-with-aspnet-web-api/_static/image21.png "将断点放置在 API 控制器的 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="797aa-308">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="797aa-309">*将断点放置在 API 控制器的 Get 方法*</span><span class="sxs-lookup"><span data-stu-id="797aa-309">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="797aa-310">按**F5**以运行该项目。</span><span class="sxs-lookup"><span data-stu-id="797aa-310">Press **F5** to run the project.</span></span> <span data-ttu-id="797aa-311">浏览器将加载 HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="797aa-311">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-312">确保您在浏览到你的应用程序的根 URL。</span><span class="sxs-lookup"><span data-stu-id="797aa-312">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="797aa-313">加载页面并 JavaScript 执行，将会命中断点，并执行代码将暂停在控制器中。</span><span class="sxs-lookup"><span data-stu-id="797aa-313">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="797aa-314">![调试使用适用于 Web VS Express 的 Web API 调用到](build-restful-apis-with-aspnet-web-api/_static/image22.png "调试到使用适用于 Web VS Express 的 Web API 调用")</span><span class="sxs-lookup"><span data-stu-id="797aa-314">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="797aa-315">*使用适用于 Web Visual Studio 2012 Express 的 Web API 调用调试*</span><span class="sxs-lookup"><span data-stu-id="797aa-315">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="797aa-316">删除断点和按**F5**或调试工具栏**继续**按钮以继续加载浏览器中的视图。</span><span class="sxs-lookup"><span data-stu-id="797aa-316">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="797aa-317">Web API 调用完成后，你应看到在浏览器中调用显示为列表项从 Web API 返回的联系人。</span><span class="sxs-lookup"><span data-stu-id="797aa-317">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="797aa-318">![在浏览器中显示为列表项的 API 调用的结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "在浏览器中显示为列表项的 API 调用的结果")</span><span class="sxs-lookup"><span data-stu-id="797aa-318">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="797aa-319">*在浏览器中显示为列表项的 API 调用的结果*</span><span class="sxs-lookup"><span data-stu-id="797aa-319">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="797aa-320">停止调试。</span><span class="sxs-lookup"><span data-stu-id="797aa-320">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="797aa-321">任务 2-修改该索引视图，以提供用于创建联系人的 GUI</span><span class="sxs-lookup"><span data-stu-id="797aa-321">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="797aa-322">在此任务中，你将继续修改索引视图的 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-322">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="797aa-323">窗体将添加到将捕获用户输入并将其发送到 Web API 来创建一个新的联系人的 HTML 页，并将创建一个新的 Web API 控制器方法来从 GUI 收集日期。</span><span class="sxs-lookup"><span data-stu-id="797aa-323">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="797aa-324">打开**ContactController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-324">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="797aa-325">将新方法添加到名为的控制器类**Post**中下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="797aa-325">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="797aa-326">(代码段- *Web API 实验室-Ex03-Post 方法*)</span><span class="sxs-lookup"><span data-stu-id="797aa-326">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>


~~~
[!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
~~~
3. <span data-ttu-id="797aa-327">打开**Index.cshtml**文件在 Visual Studio 中，如果未打开。</span><span class="sxs-lookup"><span data-stu-id="797aa-327">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="797aa-328">将以下 HTML 代码之后添加在上一任务中的无序列表添加到文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-328">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>


~~~
[!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
~~~
5. <span data-ttu-id="797aa-329">在底部的文档的脚本元素中，添加以下突出显示的代码，以处理按钮单击事件，将将数据发布到 Web API 使用的 HTTP POST 调用。</span><span class="sxs-lookup"><span data-stu-id="797aa-329">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="797aa-330">在**ContactController.cs**上, 放置一个断点**Post**方法。</span><span class="sxs-lookup"><span data-stu-id="797aa-330">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="797aa-331">按**F5**浏览器中运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-331">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="797aa-332">一旦加载页面时浏览器中，键入新的联系人姓名和 Id，然后单击**保存**按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-332">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="797aa-333">![客户端 HTML 文档加载到浏览器](build-restful-apis-with-aspnet-web-api/_static/image24.png "客户端 HTML 文档加载到浏览器")</span><span class="sxs-lookup"><span data-stu-id="797aa-333">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="797aa-334">*客户端 HTML 文档加载到浏览器*</span><span class="sxs-lookup"><span data-stu-id="797aa-334">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="797aa-335">调试器窗口的中断时**Post**方法，是看一下的属性**联系**参数。</span><span class="sxs-lookup"><span data-stu-id="797aa-335">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="797aa-336">值应匹配窗体中输入的数据。</span><span class="sxs-lookup"><span data-stu-id="797aa-336">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="797aa-337">![从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "从客户端发送到 Web API 的联系人对象")</span><span class="sxs-lookup"><span data-stu-id="797aa-337">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="797aa-338">*正在从客户端发送到 Web API 的联系人对象*</span><span class="sxs-lookup"><span data-stu-id="797aa-338">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="797aa-339">单步执行在调试器中直到方法**响应**创建变量。</span><span class="sxs-lookup"><span data-stu-id="797aa-339">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="797aa-340">在中检查**局部变量**在调试器中的窗口中，你将看到已设置了所有属性。</span><span class="sxs-lookup"><span data-stu-id="797aa-340">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="797aa-341">![以下在调试器中的创建的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "响应后在调试器中的创建")</span><span class="sxs-lookup"><span data-stu-id="797aa-341">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="797aa-342">*响应后在调试器中的创建*</span><span class="sxs-lookup"><span data-stu-id="797aa-342">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="797aa-343">如果按**F5**或单击**继续**请求将在调试器中完成。</span><span class="sxs-lookup"><span data-stu-id="797aa-343">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="797aa-344">新的联系人后切换回浏览器时，已添加到存储的联系人列表**ContactRepository**实现。</span><span class="sxs-lookup"><span data-stu-id="797aa-344">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="797aa-345">![浏览器反映成功创建新的联系人实例](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映成功创建新的联系人实例")</span><span class="sxs-lookup"><span data-stu-id="797aa-345">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="797aa-346">*浏览器反映成功创建新的联系人实例*</span><span class="sxs-lookup"><span data-stu-id="797aa-346">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="797aa-347">此外，你可以部署此应用程序对 Azure 以下[附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web Deploy](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="797aa-347">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>


* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="797aa-348">总结</span><span class="sxs-lookup"><span data-stu-id="797aa-348">Summary</span></span>

<span data-ttu-id="797aa-349">此实验室中已引入到新的 ASP.NET Web API 框架和使用框架的 RESTful Web Api 的实现。</span><span class="sxs-lookup"><span data-stu-id="797aa-349">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="797aa-350">从这里，你可以创建新的存储库，它方便了数据持久性使用任意数量的机制，并连接该服务而不是作为示例在本实验中提供的简单一个。</span><span class="sxs-lookup"><span data-stu-id="797aa-350">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="797aa-351">Web API 支持大量的其他功能，如启用从任何支持 HTTP 和 JSON 或 XML 的语言中编写的非 HTML 客户端的通信。</span><span class="sxs-lookup"><span data-stu-id="797aa-351">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="797aa-352">承载 Web API 典型 web 应用程序之外的能力也是有可能，以及是创建您自己的序列化格式的功能。</span><span class="sxs-lookup"><span data-stu-id="797aa-352">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="797aa-353">ASP.NET Web 站点有专用于在 ASP.NET Web API 框架的区域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="797aa-353">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="797aa-354">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它经常检查如果你想要深入探讨创建可用于几乎任何设备或开发框架自定义 Web Api 的技巧。</span><span class="sxs-lookup"><span data-stu-id="797aa-354">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="797aa-355">附录 a： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="797aa-355">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="797aa-356">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="797aa-356">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="797aa-357">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="797aa-357">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="797aa-358">![使用 Visual Studio 代码段将代码插入到你的项目](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="797aa-358">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="797aa-359">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="797aa-359">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="797aa-360">若要添加代码片段使用键盘 (仅限 C#)</span><span class="sxs-lookup"><span data-stu-id="797aa-360">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="797aa-361">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="797aa-361">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="797aa-362">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="797aa-362">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="797aa-363">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="797aa-363">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="797aa-364">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="797aa-364">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="797aa-365">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="797aa-365">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="797aa-366">![开始键入代码段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="797aa-366">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="797aa-367">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="797aa-367">*Start typing the snippet name*</span></span>

    <span data-ttu-id="797aa-368">![按 Tab 以选择突出显示代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="797aa-368">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="797aa-369">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="797aa-369">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="797aa-370">![再次按 Tab 和代码段将会扩展](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="797aa-370">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="797aa-371">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="797aa-371">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="797aa-372">若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）</span><span class="sxs-lookup"><span data-stu-id="797aa-372">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="797aa-373">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="797aa-373">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="797aa-374">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="797aa-374">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="797aa-375">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="797aa-375">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="797aa-376">![右键单击你想要插入代码段，并选择插入代码段](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="797aa-376">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="797aa-377">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="797aa-377">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="797aa-378">![通过单击它选取列表中中的相关代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="797aa-378">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="797aa-379">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="797aa-379">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="797aa-380">附录 b： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="797aa-380">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="797aa-381">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="797aa-381">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="797aa-382">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="797aa-382">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="797aa-383">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="797aa-383">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="797aa-384">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="797aa-384">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="797aa-385">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="797aa-385">Click on **Install Now**.</span></span> <span data-ttu-id="797aa-386">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="797aa-386">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="797aa-387">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-387">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="797aa-388">![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="797aa-388">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="797aa-389">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="797aa-389">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="797aa-390">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="797aa-390">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="797aa-392">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="797aa-392">*Accepting the license terms*</span></span>
5. <span data-ttu-id="797aa-393">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="797aa-393">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="797aa-395">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="797aa-395">*Installation progress*</span></span>
6. <span data-ttu-id="797aa-396">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="797aa-396">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="797aa-398">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="797aa-398">*Installation completed*</span></span>
7. <span data-ttu-id="797aa-399">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-399">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="797aa-400">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="797aa-400">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="797aa-402">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="797aa-402">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="797aa-403">附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="797aa-403">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="797aa-404">本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="797aa-404">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="797aa-405">任务 1-从 Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="797aa-405">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="797aa-406">转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="797aa-406">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-407">使用 Azure 可以免费承载 10 个 ASP.NET 网站，然后随着流量增长而扩展。</span><span class="sxs-lookup"><span data-stu-id="797aa-407">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="797aa-408">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="797aa-408">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="797aa-409">![登录到 Windows Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="797aa-409">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="797aa-410">*登录到门户*</span><span class="sxs-lookup"><span data-stu-id="797aa-410">*Log on to Portal*</span></span>
2. <span data-ttu-id="797aa-411">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="797aa-411">Click **New** on the command bar.</span></span>

    <span data-ttu-id="797aa-412">![创建新网站](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="797aa-412">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="797aa-413">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="797aa-413">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="797aa-414">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="797aa-414">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="797aa-415">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="797aa-415">Then select **Quick Create** option.</span></span> <span data-ttu-id="797aa-416">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="797aa-416">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-417">Azure 是运行在云中，你可以控制和管理 web 应用程序的宿主。</span><span class="sxs-lookup"><span data-stu-id="797aa-417">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="797aa-418">快速创建选项，可部署到从 Azure 门户外部的已完成的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="797aa-418">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="797aa-419">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="797aa-419">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="797aa-420">![创建新的网站使用快速创建](build-restful-apis-with-aspnet-web-api/_static/image41.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="797aa-420">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="797aa-421">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="797aa-421">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="797aa-422">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="797aa-422">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="797aa-423">创建网站后单击下的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="797aa-423">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="797aa-424">检查新的 Web 站点工作。</span><span class="sxs-lookup"><span data-stu-id="797aa-424">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="797aa-425">![浏览到新的 web 站点](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="797aa-425">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="797aa-426">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="797aa-426">*Browsing to the new web site*</span></span>

    <span data-ttu-id="797aa-427">![运行网站](build-restful-apis-with-aspnet-web-api/_static/image43.png "运行的网站")</span><span class="sxs-lookup"><span data-stu-id="797aa-427">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="797aa-428">*运行的网站*</span><span class="sxs-lookup"><span data-stu-id="797aa-428">*Web site running*</span></span>
6. <span data-ttu-id="797aa-429">返回到门户并单击在网站的名称**名称**列以显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="797aa-429">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="797aa-430">![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="797aa-430">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="797aa-431">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="797aa-431">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="797aa-432">在**仪表板**页上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="797aa-432">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-433">*发布配置文件*包含所有发布到 Azure，以便每个启用的发布方法的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="797aa-433">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="797aa-434">发布配置文件包含的 Url、 用户凭据和连接到并针对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="797aa-434">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="797aa-435">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件以自动执行的这些程序，以便配置web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="797aa-435">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="797aa-436">![下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="797aa-436">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="797aa-437">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="797aa-437">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="797aa-438">到一个已知位置下载发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="797aa-438">Download the publish profile file to a known location.</span></span> <span data-ttu-id="797aa-439">进一步在本练习中，你将了解如何使用此文件发布到 Azure web 应用程序从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="797aa-439">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="797aa-440">![保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="797aa-440">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="797aa-441">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="797aa-441">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="797aa-442">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="797aa-442">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="797aa-443">如果你的应用程序将使用 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="797aa-443">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="797aa-444">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="797aa-444">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="797aa-445">需要将用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="797aa-445">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="797aa-446">你可以从你的订阅在 Azure 管理门户中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**.</span><span class="sxs-lookup"><span data-stu-id="797aa-446">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="797aa-447">如果你没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-447">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="797aa-448">请记下的**服务器名称和 URL、 管理员登录名和密码**，如你将在接下来的任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="797aa-448">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="797aa-449">不创建数据库，它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="797aa-449">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="797aa-450">![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="797aa-450">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="797aa-451">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="797aa-451">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="797aa-452">在下一个任务将测试从 Visual Studio 中，数据库连接，因此你需要在的服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="797aa-452">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="797aa-453">若要做到这一点，请单击**配置**，选择的 IP 地址从**当前客户端 IP 地址**并将其粘贴在**起始 IP 地址**和**结束 IP 地址**文本框和单击![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="797aa-453">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="797aa-455">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="797aa-455">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="797aa-456">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="797aa-456">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认做的更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="797aa-458">*确认做的更改*</span><span class="sxs-lookup"><span data-stu-id="797aa-458">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="797aa-459">任务 3-发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="797aa-459">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="797aa-460">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="797aa-460">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="797aa-461">在**解决方案资源管理器**，右键单击网站项目，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="797aa-461">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="797aa-462">![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="797aa-462">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="797aa-463">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="797aa-463">*Publishing the web site*</span></span>
2. <span data-ttu-id="797aa-464">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="797aa-464">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="797aa-465">![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="797aa-465">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="797aa-466">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="797aa-466">*Importing publish profile*</span></span>
3. <span data-ttu-id="797aa-467">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="797aa-467">Click **Validate Connection**.</span></span> <span data-ttu-id="797aa-468">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="797aa-468">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797aa-469">请参阅验证连接按钮旁边将显示绿色的复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="797aa-469">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="797aa-470">![正在验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="797aa-470">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="797aa-471">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="797aa-471">*Validating connection*</span></span>
4. <span data-ttu-id="797aa-472">在**设置**页上，在**数据库**部分中，单击你的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="797aa-472">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="797aa-473">![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="797aa-473">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="797aa-474">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="797aa-474">*Web deploy configuration*</span></span>
5. <span data-ttu-id="797aa-475">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="797aa-475">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="797aa-476">在**服务器名称**类型 SQL 数据库服务器 URL 使用*tcp:*前缀。</span><span class="sxs-lookup"><span data-stu-id="797aa-476">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="797aa-477">在**用户名**键入您的服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="797aa-477">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="797aa-478">在**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="797aa-478">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="797aa-479">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="797aa-479">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="797aa-480">![配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="797aa-480">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="797aa-481">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="797aa-481">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="797aa-482">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="797aa-482">Then click **OK**.</span></span> <span data-ttu-id="797aa-483">当系统提示创建数据库单击**是**。</span><span class="sxs-lookup"><span data-stu-id="797aa-483">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="797aa-484">![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="797aa-484">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="797aa-485">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="797aa-485">*Creating the database*</span></span>
7. <span data-ttu-id="797aa-486">在默认连接文本框中显示了将用于连接到 Windows Azure 中的 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="797aa-486">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="797aa-487">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="797aa-487">Then click **Next**.</span></span>

    <span data-ttu-id="797aa-488">![连接字符串指向 SQL 数据库](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="797aa-488">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="797aa-489">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="797aa-489">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="797aa-490">在**预览**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="797aa-490">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="797aa-491">![Web 应用程序发布](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="797aa-491">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="797aa-492">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="797aa-492">*Publishing the web application*</span></span>
9. <span data-ttu-id="797aa-493">完成发布过程后，默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="797aa-493">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="797aa-494">![应用程序发布到 Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="797aa-494">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="797aa-495">*应用程序发布到 Azure*</span><span class="sxs-lookup"><span data-stu-id="797aa-495">*Application published to Azure*</span></span>
