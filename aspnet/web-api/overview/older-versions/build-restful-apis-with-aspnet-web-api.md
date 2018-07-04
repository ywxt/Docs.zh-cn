---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 生成使用 ASP.NET Web API 的 RESTful Api |Microsoft Docs
author: rick-anderson
description: 近年来，它已成为清除 HTTP 不再仅仅用于提供 HTML 页面。 它也是一个强大的平台，用于构建 Web Api，使用一些 o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 88ac5102a1cf14050412abc336e7a8260a9fa80d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363515"
---
<a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="69666-104">生成使用 ASP.NET Web API 的 RESTful Api</span><span class="sxs-lookup"><span data-stu-id="69666-104">Build RESTful APIs with ASP.NET Web API</span></span>
====================
<span data-ttu-id="69666-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="69666-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="69666-106">近年来，它已成为清除 HTTP 不再仅仅用于提供 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="69666-106">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="69666-107">它也是一个强大的平台，用于构建 Web Api，使用少数几个动词 （GET、 POST 等） 以及几个简单的概念类似于*Uri*并*标头*。</span><span class="sxs-lookup"><span data-stu-id="69666-107">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="69666-108">ASP.NET Web API 是一组简化 HTTP 编程的组件。</span><span class="sxs-lookup"><span data-stu-id="69666-108">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="69666-109">因为它基于 ASP.NET MVC 运行时，Web API 将自动处理 HTTP 的低级别传输详细信息。</span><span class="sxs-lookup"><span data-stu-id="69666-109">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="69666-110">同时，Web API 自然会公开 HTTP 编程模型。</span><span class="sxs-lookup"><span data-stu-id="69666-110">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="69666-111">实际上，Web API 的一个目标是向*不*抽象出 HTTP 的现实。</span><span class="sxs-lookup"><span data-stu-id="69666-111">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="69666-112">因此，Web API 是灵活且易于扩展。</span><span class="sxs-lookup"><span data-stu-id="69666-112">As a result, Web API is both flexible and easy to extend.</span></span> <span data-ttu-id="69666-113">在本动手实验中，将使用 Web API 来构建一个简单的 REST API 为联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-113">In this hands-on lab, you will use Web API to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="69666-114">您还将生成客户端以使用 API。</span><span class="sxs-lookup"><span data-stu-id="69666-114">You will also build a client to consume the API.</span></span> <span data-ttu-id="69666-115">REST 体系结构风格已被证明是利用 HTTP-的有效方法，尽管它并不是 HTTP 的唯一有效方法。</span><span class="sxs-lookup"><span data-stu-id="69666-115">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="69666-116">联系人管理器将公开用于列出、 添加和删除联系人，以及其他基于 Rest。</span><span class="sxs-lookup"><span data-stu-id="69666-116">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> <span data-ttu-id="69666-117">本实验需要基本了解 HTTP，其余部分，并假定你已基本了解 HTML、 JavaScript 和 jQuery。</span><span class="sxs-lookup"><span data-stu-id="69666-117">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="69666-118">ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ https://asp.net/web-api ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="69666-118">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="69666-119">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。</span><span class="sxs-lookup"><span data-stu-id="69666-119">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="69666-120">ASP.NET Web API，类似于 ASP.NET MVC 4 中，有很大的灵活性方面将服务层与允许您使用多个可用的依赖关系注入框架变得相当容易的控制器分离开来。</span><span class="sxs-lookup"><span data-stu-id="69666-120">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="69666-121">演示如何使用依赖关系注入在 ASP.NET Web API 项目中，你可以下载它从 Ninject 的 MSDN 中没有一个好的示例[此处](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)。</span><span class="sxs-lookup"><span data-stu-id="69666-121">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="69666-122">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="69666-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="69666-123">目标</span><span class="sxs-lookup"><span data-stu-id="69666-123">Objectives</span></span>

<span data-ttu-id="69666-124">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="69666-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="69666-125">实现 rest 样式 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-125">Implement a RESTful Web API</span></span>
- <span data-ttu-id="69666-126">从 HTML 客户端调用 API</span><span class="sxs-lookup"><span data-stu-id="69666-126">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="69666-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="69666-127">Prerequisites</span></span>

<span data-ttu-id="69666-128">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="69666-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="69666-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="69666-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="69666-130">安装</span><span class="sxs-lookup"><span data-stu-id="69666-130">Setup</span></span>

<span data-ttu-id="69666-131">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="69666-131">**Installing Code Snippets**</span></span>

<span data-ttu-id="69666-132">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="69666-132">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="69666-133">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="69666-133">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="69666-134">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 a： 使用代码片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="69666-134">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="69666-135">练习</span><span class="sxs-lookup"><span data-stu-id="69666-135">Exercises</span></span>

<span data-ttu-id="69666-136">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="69666-136">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="69666-137">练习 1： 创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-137">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="69666-138">练习 2： 创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-138">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="69666-139">练习 3： 使用从 HTML 客户端 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-139">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="69666-140">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="69666-140">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="69666-141">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="69666-141">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="69666-142">估计的时间才能完成此实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="69666-142">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="69666-143">练习 1： 创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-143">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="69666-144">在此练习中，将为联系人管理器实现只读的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="69666-144">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="69666-145">任务 1-创建 API 项目</span><span class="sxs-lookup"><span data-stu-id="69666-145">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="69666-146">在本任务中，您将使用新的 ASP.NET web 项目模板创建 Web API web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-146">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="69666-147">运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="69666-147">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="69666-148">从**文件**菜单中，选择**新项目**。</span><span class="sxs-lookup"><span data-stu-id="69666-148">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="69666-149">选择**Visual C# |Web**项目类型从项目类型树视图，然后选择**ASP.NET MVC 4 Web 应用程序**项目类型。</span><span class="sxs-lookup"><span data-stu-id="69666-149">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="69666-150">将项目的**名称**到*ContactManager*并**解决方案名称**到*开始*，然后单击**确定**.</span><span class="sxs-lookup"><span data-stu-id="69666-150">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="69666-151">![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")</span><span class="sxs-lookup"><span data-stu-id="69666-151">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="69666-152">*创建新的 ASP.NET MVC 4.0 Web 应用程序项目*</span><span class="sxs-lookup"><span data-stu-id="69666-152">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="69666-153">在 ASP.NET MVC 4 项目类型对话框中，选择**Web API**项目类型。</span><span class="sxs-lookup"><span data-stu-id="69666-153">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="69666-154">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="69666-154">Click **OK**.</span></span>

    <span data-ttu-id="69666-155">![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")</span><span class="sxs-lookup"><span data-stu-id="69666-155">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="69666-156">*指定 Web API 项目类型*</span><span class="sxs-lookup"><span data-stu-id="69666-156">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="69666-157">任务 2-创建联系人管理器 API 控制器</span><span class="sxs-lookup"><span data-stu-id="69666-157">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="69666-158">在本任务中，将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="69666-158">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="69666-159">删除名为的文件**ValuesController.cs**内**控制器**从项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="69666-159">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="69666-160">右键单击**控制器**文件夹中该项目并选择**添加 |控制器**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="69666-160">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="69666-161">![向项目添加新的控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新的控制器")</span><span class="sxs-lookup"><span data-stu-id="69666-161">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="69666-162">*向项目添加新的控制器*</span><span class="sxs-lookup"><span data-stu-id="69666-162">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="69666-163">在中**添加控制器**对话框中，选择**空 API 控制器**的模板菜单中。</span><span class="sxs-lookup"><span data-stu-id="69666-163">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="69666-164">控制器类命名**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="69666-164">Name the controller class **ContactController**.</span></span> <span data-ttu-id="69666-165">然后，单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="69666-165">Then, click **Add.**</span></span>

    <span data-ttu-id="69666-166">![使用添加控制器对话框创建新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用添加控制器对话框创建新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="69666-166">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="69666-167">*使用添加控制器对话框创建新的 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="69666-167">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="69666-168">将以下代码添加到**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="69666-168">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="69666-169">(代码段- *Web API 实验-Ex01-获取 API 方法*)</span><span class="sxs-lookup"><span data-stu-id="69666-169">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="69666-170">按**F5**调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-170">Press **F5** to debug the application.</span></span> <span data-ttu-id="69666-171">Web API 项目的默认主页应显示。</span><span class="sxs-lookup"><span data-stu-id="69666-171">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="69666-172">![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")</span><span class="sxs-lookup"><span data-stu-id="69666-172">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="69666-173">*ASP.NET Web API 应用程序的默认主页*</span><span class="sxs-lookup"><span data-stu-id="69666-173">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="69666-174">在 Internet Explorer 窗口中，按**F12**键以打开**开发人员工具**窗口。</span><span class="sxs-lookup"><span data-stu-id="69666-174">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="69666-175">单击**网络**选项卡，然后依次**启动捕获**按钮开始到窗口中捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="69666-175">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="69666-176">![打开网络选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开网络选项卡并启动网络捕获")</span><span class="sxs-lookup"><span data-stu-id="69666-176">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="69666-177">*打开网络选项卡并启动网络捕获*</span><span class="sxs-lookup"><span data-stu-id="69666-177">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="69666-178">追加与浏览器的地址栏中的 URL **/api/contact** ，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="69666-178">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="69666-179">传输的详细信息会在网络捕获窗口中显示。</span><span class="sxs-lookup"><span data-stu-id="69666-179">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="69666-180">请注意，响应的 MIME 类型是**应用程序 /json**。</span><span class="sxs-lookup"><span data-stu-id="69666-180">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="69666-181">此示例演示默认输出格式的 JSON 的方式。</span><span class="sxs-lookup"><span data-stu-id="69666-181">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="69666-182">![在网络视图中查看 Web API 请求的输出](build-restful-apis-with-aspnet-web-api/_static/image7.png "网络视图中查看 Web API 请求的输出")</span><span class="sxs-lookup"><span data-stu-id="69666-182">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="69666-183">*在网络视图中查看 Web API 请求的输出*</span><span class="sxs-lookup"><span data-stu-id="69666-183">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-184">Internet Explorer 10 的默认行为现在将询问如果用户想要保存或打开生成的 Web API 调用的流。</span><span class="sxs-lookup"><span data-stu-id="69666-184">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="69666-185">输出将包含 Web API URL 调用的 JSON 结果的文本文件。</span><span class="sxs-lookup"><span data-stu-id="69666-185">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="69666-186">若要查看通过开发人员工具窗口的响应的内容将不取消对话框。</span><span class="sxs-lookup"><span data-stu-id="69666-186">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="69666-187">单击**转到详细视图**按钮以查看有关此 API 调用的响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="69666-187">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="69666-188">![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")</span><span class="sxs-lookup"><span data-stu-id="69666-188">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="69666-189">*切换到详细视图*</span><span class="sxs-lookup"><span data-stu-id="69666-189">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="69666-190">单击**响应正文**选项卡以查看实际的 JSON 响应文本。</span><span class="sxs-lookup"><span data-stu-id="69666-190">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="69666-191">![查看 JSON 输出网络监视器中的文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看 JSON 输出网络监视器中的文本")</span><span class="sxs-lookup"><span data-stu-id="69666-191">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="69666-192">*在网络监视器中查看 JSON 输出文本*</span><span class="sxs-lookup"><span data-stu-id="69666-192">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="69666-193">任务 3-创建联系人的模型和增加为 Contact Controller</span><span class="sxs-lookup"><span data-stu-id="69666-193">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="69666-194">在本任务中，将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="69666-194">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="69666-195">右键单击**模型**文件夹，然后选择**添加 |类...** 从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="69666-195">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="69666-196">![向 web 应用程序中添加新模型](build-restful-apis-with-aspnet-web-api/_static/image10.png "向 web 应用程序中添加新模型")</span><span class="sxs-lookup"><span data-stu-id="69666-196">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="69666-197">*向 web 应用程序中添加新模型*</span><span class="sxs-lookup"><span data-stu-id="69666-197">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="69666-198">在中**添加新项**对话框中，将新文件命名**Contact.cs**单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="69666-198">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="69666-199">![创建新的联系人类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的联系人类文件")</span><span class="sxs-lookup"><span data-stu-id="69666-199">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="69666-200">*创建新的联系人类文件*</span><span class="sxs-lookup"><span data-stu-id="69666-200">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="69666-201">将以下突出显示的代码添加到**联系人**类。</span><span class="sxs-lookup"><span data-stu-id="69666-201">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="69666-202">(代码段- *Web API 实验-Ex01-Contact 类*)</span><span class="sxs-lookup"><span data-stu-id="69666-202">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="69666-203">在**ContactController**类中，选择 word**字符串**中的方法定义**获取**方法，并键入单词*联系人*。</span><span class="sxs-lookup"><span data-stu-id="69666-203">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="69666-204">在键入的单词后, 指示器将出现在单词的开头**联系人**。</span><span class="sxs-lookup"><span data-stu-id="69666-204">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="69666-205">可以按住**Ctrl**键和按句点 （.） 键或单击使用鼠标打开在代码编辑器中，以自动填充帮助对话框图标**使用**指令的模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="69666-205">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![对于命名空间声明中使用 Intellisense 协助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="69666-207">*对于命名空间声明中使用 Intellisense 协助*</span><span class="sxs-lookup"><span data-stu-id="69666-207">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="69666-208">修改的代码**获取**方法，以便它返回联系人模型实例的数组。</span><span class="sxs-lookup"><span data-stu-id="69666-208">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="69666-209">(代码段-*返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="69666-209">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="69666-210">按**F5**调试 web 应用程序在浏览器中的。</span><span class="sxs-lookup"><span data-stu-id="69666-210">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="69666-211">若要查看 API 的响应输出所做的更改，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="69666-211">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="69666-212">在浏览器打开后，按**F12**如果开发人员工具还不打开。</span><span class="sxs-lookup"><span data-stu-id="69666-212">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="69666-213">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="69666-213">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="69666-214">按**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-214">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="69666-215">添加 URL 后缀 **/api/contact**到的 URL 地址栏，然后按**Enter**密钥。</span><span class="sxs-lookup"><span data-stu-id="69666-215">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="69666-216">按**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-216">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="69666-217">选择**响应正文**选项卡。应会看到表示联系人实例的数组的序列化的形式的 JSON 字符串。</span><span class="sxs-lookup"><span data-stu-id="69666-217">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="69666-218">![JSON 序列化复杂的 Web API 方法调用的输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 序列化复杂的 Web API 方法调用的输出")</span><span class="sxs-lookup"><span data-stu-id="69666-218">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="69666-219">*复杂的 Web API 方法调用的序列化的 JSON 输出*</span><span class="sxs-lookup"><span data-stu-id="69666-219">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="69666-220">任务 4-解压缩功能集成到服务层</span><span class="sxs-lookup"><span data-stu-id="69666-220">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="69666-221">此任务将演示如何功能提取到服务层，以方便开发人员可以将其服务的功能与控制器层，从而允许实际完成工作的服务的可重用性。</span><span class="sxs-lookup"><span data-stu-id="69666-221">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="69666-222">在解决方案根目录中创建一个新文件夹并将其命名**Services**。</span><span class="sxs-lookup"><span data-stu-id="69666-222">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="69666-223">若要执行此操作，右键单击**ContactManager**项目，选择**添加** | **新文件夹**，其命名为*服务*。</span><span class="sxs-lookup"><span data-stu-id="69666-223">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="69666-224">![创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "创建服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="69666-224">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="69666-225">*正在创建服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="69666-225">*Creating Services folder*</span></span>
2. <span data-ttu-id="69666-226">右键单击**Services**文件夹，然后选择**添加 |类...** 从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="69666-226">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="69666-227">![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="69666-227">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="69666-228">*将新类添加到服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="69666-228">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="69666-229">当**添加新项**对话框出现时，将新类命名**ContactRepository**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="69666-229">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="69666-230">![创建一个类文件以包含联系人存储库服务层的代码](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")</span><span class="sxs-lookup"><span data-stu-id="69666-230">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="69666-231">*创建一个类文件以包含联系人存储库服务层的代码*</span><span class="sxs-lookup"><span data-stu-id="69666-231">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="69666-232">添加 using 指令**ContactRepository.cs**文件以包括模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="69666-232">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="69666-233">将以下突出显示的代码添加到**ContactRepository.cs**文件以实现 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="69666-233">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="69666-234">(代码段- *Web API 实验-Ex01-联系人存储库*)</span><span class="sxs-lookup"><span data-stu-id="69666-234">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="69666-235">打开**ContactController.cs**文件如果已打开。</span><span class="sxs-lookup"><span data-stu-id="69666-235">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="69666-236">将以下代码添加到该文件的命名空间声明部分使用语句。</span><span class="sxs-lookup"><span data-stu-id="69666-236">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="69666-237">将以下突出显示的代码添加到**ContactController.cs**类添加一个私有字段来表示存储库的实例，以便成员可以产生的类的其余部分使用的服务实现。</span><span class="sxs-lookup"><span data-stu-id="69666-237">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="69666-238">(代码段-*的 Web API 实验-Ex01-联系人控制器*)</span><span class="sxs-lookup"><span data-stu-id="69666-238">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="69666-239">更改**获取**方法，以便它可以使用联系人存储库服务。</span><span class="sxs-lookup"><span data-stu-id="69666-239">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="69666-240">(代码段-*通过存储库返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="69666-240">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="69666-241">放置一个断点**ContactController**的**获取**方法定义。</span><span class="sxs-lookup"><span data-stu-id="69666-241">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="69666-242">![将断点添加到联系人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "将断点添加到联系人控制器")</span><span class="sxs-lookup"><span data-stu-id="69666-242">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="69666-243">*将断点添加到联系人控制器*</span><span class="sxs-lookup"><span data-stu-id="69666-243">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="69666-244">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-244">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="69666-245">在浏览器打开后，按**F12**打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="69666-245">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="69666-246">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="69666-246">Click the **Network** tab.</span></span>
14. <span data-ttu-id="69666-247">单击**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-247">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="69666-248">追加后缀的地址栏中的 URL **/api/contact**然后按**Enter**加载 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="69666-248">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="69666-249">Visual Studio 2012 应中断一次**获取**方法开始执行。</span><span class="sxs-lookup"><span data-stu-id="69666-249">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="69666-250">![Get 方法中的重大](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 方法中的重大")</span><span class="sxs-lookup"><span data-stu-id="69666-250">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="69666-251">*Get 方法中的重大*</span><span class="sxs-lookup"><span data-stu-id="69666-251">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="69666-252">按 F5 继续。</span><span class="sxs-lookup"><span data-stu-id="69666-252">Press **F5** to continue.</span></span>
18. <span data-ttu-id="69666-253">返回到 Internet Explorer 如果它尚未处于焦点模式。</span><span class="sxs-lookup"><span data-stu-id="69666-253">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="69666-254">请注意网络捕获窗口。</span><span class="sxs-lookup"><span data-stu-id="69666-254">Note the network capture window.</span></span>

    <span data-ttu-id="69666-255">![网络中显示的 Web API 调用结果的 Internet 资源管理器视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "网络中显示的 Web API 调用结果的 Internet 资源管理器视图")</span><span class="sxs-lookup"><span data-stu-id="69666-255">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="69666-256">*在 Internet Explorer 中显示的 Web API 调用的结果的网络视图*</span><span class="sxs-lookup"><span data-stu-id="69666-256">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="69666-257">单击**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-257">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="69666-258">单击**响应正文**选项卡。请注意 JSON 输出的 API 调用，以及它如何表示两个服务层来检索的联系人。</span><span class="sxs-lookup"><span data-stu-id="69666-258">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="69666-259">![在开发人员工具窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "开发人员工具窗口中查看 Web API 的 JSON 输出")</span><span class="sxs-lookup"><span data-stu-id="69666-259">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="69666-260">*在开发人员工具窗口中查看 Web API 的 JSON 输出*</span><span class="sxs-lookup"><span data-stu-id="69666-260">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="69666-261">练习 2： 创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-261">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="69666-262">在此练习中，将实现 POST 和 PUT 方法的联系人管理器中，若要启用与数据编辑功能。</span><span class="sxs-lookup"><span data-stu-id="69666-262">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="69666-263">任务 1-打开 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="69666-263">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="69666-264">在本任务中，你将准备以增强，以便它可以接受用户输入在练习 1 中创建的 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="69666-264">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="69666-265">运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="69666-265">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="69666-266">打开**开始**解决方案位于**源/Ex02-ReadWriteWebAPI/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="69666-266">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="69666-267">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="69666-267">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="69666-268">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="69666-268">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="69666-269">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="69666-269">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="69666-270">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="69666-270">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="69666-271">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="69666-271">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="69666-272">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="69666-272">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="69666-273">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="69666-273">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="69666-274">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="69666-274">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="69666-275">打开**Services/ContactRepository.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="69666-275">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="69666-276">任务 2-将数据暂留功能添加到联系人存储库实现</span><span class="sxs-lookup"><span data-stu-id="69666-276">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="69666-277">在此任务中，您将扩展，以便它可以保存并接受用户输入和新联系人实例在练习 1 中创建的 Web API 项目的 ContactRepository 类。</span><span class="sxs-lookup"><span data-stu-id="69666-277">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="69666-278">添加到下面的常量**ContactRepository**类来表示 web 服务器缓存项密钥名称的更高版本在此练习中的名称。</span><span class="sxs-lookup"><span data-stu-id="69666-278">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="69666-279">添加到构造函数**ContactRepository**包含下面的代码。</span><span class="sxs-lookup"><span data-stu-id="69666-279">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="69666-280">(代码段- *Web API 实验-Ex02-联系人存储库构造函数*)</span><span class="sxs-lookup"><span data-stu-id="69666-280">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="69666-281">修改的代码**GetAllContacts**方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="69666-281">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="69666-282">(代码段- *Web API 实验-Ex02-获取所有联系人*)</span><span class="sxs-lookup"><span data-stu-id="69666-282">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="69666-283">此示例用于演示目的，并将使用 web 服务器的缓存作为存储介质，以便这些值将可供多个客户端同时，而不使用会话存储机制或请求存储生存期。</span><span class="sxs-lookup"><span data-stu-id="69666-283">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="69666-284">一个可以使用实体框架、 XML 存储或任何其他一种替代 web 服务器缓存。</span><span class="sxs-lookup"><span data-stu-id="69666-284">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="69666-285">实现一个名为的新方法**SaveContact**到**ContactRepository**类执行的将联系人保存工作。</span><span class="sxs-lookup"><span data-stu-id="69666-285">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="69666-286">**SaveContact**方法应采用单个**联系人**参数和返回一个布尔值，该值指示成功或失败。</span><span class="sxs-lookup"><span data-stu-id="69666-286">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="69666-287">(代码段- *Web API 实验-Ex02-实现 SaveContact 方法*)</span><span class="sxs-lookup"><span data-stu-id="69666-287">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="69666-288">练习 3： 使用从 HTML 客户端 Web API</span><span class="sxs-lookup"><span data-stu-id="69666-288">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="69666-289">在此练习中，您将创建 HTML 客户端调用 Web API。</span><span class="sxs-lookup"><span data-stu-id="69666-289">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="69666-290">此客户端将使用 Web API 通过 JavaScript 促进数据交换，并将使用 HTML 标记的 web 浏览器中显示的结果。</span><span class="sxs-lookup"><span data-stu-id="69666-290">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="69666-291">任务 1-修改索引视图用于显示联系人提供 GUI</span><span class="sxs-lookup"><span data-stu-id="69666-291">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="69666-292">在本任务中，将修改 web 应用程序以支持在 HTML 浏览器中显示的现有联系人列表的要求的默认索引视图。</span><span class="sxs-lookup"><span data-stu-id="69666-292">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="69666-293">打开**Visual Studio 2012 Express for Web**如果已打开。</span><span class="sxs-lookup"><span data-stu-id="69666-293">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="69666-294">打开**开始**解决方案位于**源/Ex03-ConsumingWebAPI/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="69666-294">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="69666-295">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="69666-295">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="69666-296">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="69666-296">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="69666-297">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="69666-297">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="69666-298">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="69666-298">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="69666-299">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="69666-299">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="69666-300">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="69666-300">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="69666-301">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="69666-301">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="69666-302">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="69666-302">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="69666-303">打开**Index.cshtml**文件位于**Views/Home**文件夹。</span><span class="sxs-lookup"><span data-stu-id="69666-303">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="69666-304">Div 元素中的 HTML 代码替换 id**正文**，以便它看起来像下面的代码。</span><span class="sxs-lookup"><span data-stu-id="69666-304">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="69666-305">要执行对 Web API 的 HTTP 请求的文件的底部添加以下 Javascript 代码。</span><span class="sxs-lookup"><span data-stu-id="69666-305">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="69666-306">打开**ContactController.cs**文件如果已打开。</span><span class="sxs-lookup"><span data-stu-id="69666-306">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="69666-307">上放置一个断点**获取**方法**ContactController**类。</span><span class="sxs-lookup"><span data-stu-id="69666-307">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="69666-308">![将断点放置在 API 控制器的 Get 方法](build-restful-apis-with-aspnet-web-api/_static/image21.png "将断点放置在 API 控制器的 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="69666-308">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="69666-309">*将断点放置在 API 控制器的 Get 方法*</span><span class="sxs-lookup"><span data-stu-id="69666-309">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="69666-310">按**F5**以运行该项目。</span><span class="sxs-lookup"><span data-stu-id="69666-310">Press **F5** to run the project.</span></span> <span data-ttu-id="69666-311">在浏览器将加载 HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="69666-311">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-312">请确保您浏览到你的应用程序的根 URL。</span><span class="sxs-lookup"><span data-stu-id="69666-312">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="69666-313">在页面加载并执行 JavaScript，将命中断点和执行代码将暂停控制器中。</span><span class="sxs-lookup"><span data-stu-id="69666-313">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="69666-314">![使用 VS Express for Web 的 Web API 调用到调试](build-restful-apis-with-aspnet-web-api/_static/image22.png "调试到使用 VS Express for Web 的 Web API 调用")</span><span class="sxs-lookup"><span data-stu-id="69666-314">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="69666-315">*使用 Visual Studio 2012 Express for Web 的 Web API 调用调试*</span><span class="sxs-lookup"><span data-stu-id="69666-315">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="69666-316">删除该断点并按**F5**或调试工具栏上的**继续**按钮以继续加载在浏览器中的视图。</span><span class="sxs-lookup"><span data-stu-id="69666-316">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="69666-317">Web API 调用完成后应会看到从 Web API 返回在浏览器中调用显示为列表项的联系人。</span><span class="sxs-lookup"><span data-stu-id="69666-317">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="69666-318">![在浏览器中显示为列表项的 API 调用的结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "API 调用在浏览器中显示为列表项的结果")</span><span class="sxs-lookup"><span data-stu-id="69666-318">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="69666-319">*在浏览器中显示为列表项的 API 调用的结果*</span><span class="sxs-lookup"><span data-stu-id="69666-319">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="69666-320">停止调试。</span><span class="sxs-lookup"><span data-stu-id="69666-320">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="69666-321">任务 2-修改索引视图创建联系人提供 GUI</span><span class="sxs-lookup"><span data-stu-id="69666-321">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="69666-322">在此任务中，将继续修改索引视图的 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-322">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="69666-323">窗体将添加到 HTML 页面，将捕获用户输入并将其发送到 Web API 以创建新的联系人，并将创建新的 Web API 控制器方法以从图形用户界面收集日期。</span><span class="sxs-lookup"><span data-stu-id="69666-323">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="69666-324">打开**ContactController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="69666-324">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="69666-325">将新方法添加到名为的控制器类**Post**如下面的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="69666-325">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="69666-326">(代码段- *Web API 实验室-Ex03-Post 方法*)</span><span class="sxs-lookup"><span data-stu-id="69666-326">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="69666-327">打开**Index.cshtml**文件在 Visual Studio 中，如果已打开。</span><span class="sxs-lookup"><span data-stu-id="69666-327">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="69666-328">将以下 HTML 代码之后添加上一任务中的未排序列表添加到该文件。</span><span class="sxs-lookup"><span data-stu-id="69666-328">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="69666-329">在文档底部的脚本元素中，添加以下突出显示的代码以处理按钮单击事件，会将数据发布到 Web API 使用的 HTTP POST 调用。</span><span class="sxs-lookup"><span data-stu-id="69666-329">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="69666-330">在中**ContactController.cs**上, 放置一个断点**Post**方法。</span><span class="sxs-lookup"><span data-stu-id="69666-330">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="69666-331">按**F5**在浏览器中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-331">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="69666-332">页面加载后在浏览器中，键入新的联系人名称和 Id，然后单击**保存**按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-332">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="69666-333">![在浏览器中加载客户端 HTML 文档](build-restful-apis-with-aspnet-web-api/_static/image24.png "在浏览器中加载客户端 HTML 文档")</span><span class="sxs-lookup"><span data-stu-id="69666-333">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="69666-334">*在浏览器中加载客户端 HTML 文档*</span><span class="sxs-lookup"><span data-stu-id="69666-334">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="69666-335">当在调试器窗口的分页符**Post**方法，请查阅的属性**联系**参数。</span><span class="sxs-lookup"><span data-stu-id="69666-335">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="69666-336">值应匹配窗体中输入的数据。</span><span class="sxs-lookup"><span data-stu-id="69666-336">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="69666-337">![从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "联系人对象从客户端发送到 Web API")</span><span class="sxs-lookup"><span data-stu-id="69666-337">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="69666-338">*正在从客户端发送到 Web API 的联系人对象*</span><span class="sxs-lookup"><span data-stu-id="69666-338">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="69666-339">单步执行之前在调试器中的方法**响应**创建变量。</span><span class="sxs-lookup"><span data-stu-id="69666-339">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="69666-340">在观察**局部变量**在调试器窗口中的，您将看到已设置的所有属性。</span><span class="sxs-lookup"><span data-stu-id="69666-340">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="69666-341">![在调试器中的创建之后的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "在调试器中的创建之后的响应")</span><span class="sxs-lookup"><span data-stu-id="69666-341">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="69666-342">*在调试器中的创建之后响应*</span><span class="sxs-lookup"><span data-stu-id="69666-342">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="69666-343">如果按下**F5**或单击**继续**请求将在调试器中完成。</span><span class="sxs-lookup"><span data-stu-id="69666-343">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="69666-344">新联系人后切换回浏览器时，已添加到联系人存储的列表**ContactRepository**实现。</span><span class="sxs-lookup"><span data-stu-id="69666-344">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="69666-345">![在浏览器反映成功创建新的联系人实例](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映成功创建新的连接实例")</span><span class="sxs-lookup"><span data-stu-id="69666-345">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="69666-346">*在浏览器反映成功创建新的连接实例*</span><span class="sxs-lookup"><span data-stu-id="69666-346">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="69666-347">此外，您可以此应用程序部署到 Azure 的以下[附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="69666-347">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>


* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="69666-348">总结</span><span class="sxs-lookup"><span data-stu-id="69666-348">Summary</span></span>

<span data-ttu-id="69666-349">此实验介绍了可以使用新的 ASP.NET Web API 框架和使用框架的 RESTful Web Api 的实现。</span><span class="sxs-lookup"><span data-stu-id="69666-349">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="69666-350">在这里，您可以创建新的存储库可帮助数据暂留使用任意数量的机制并连接该服务而不是作为示例，请参见此体验中提供的简单一个。</span><span class="sxs-lookup"><span data-stu-id="69666-350">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="69666-351">Web API 支持很多其他功能，例如启用以支持 HTTP 和 JSON 或 XML 的任何语言编写的非 HTML 客户端的通信。</span><span class="sxs-lookup"><span data-stu-id="69666-351">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="69666-352">承载 Web API 是典型的 web 应用程序外部的能力也是可能的以及是创建您自己的序列化格式的功能。</span><span class="sxs-lookup"><span data-stu-id="69666-352">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="69666-353">ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="69666-353">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="69666-354">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。</span><span class="sxs-lookup"><span data-stu-id="69666-354">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="69666-355">附录 a： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="69666-355">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="69666-356">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="69666-356">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="69666-357">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="69666-357">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="69666-358">![使用 Visual Studio 代码段代码插入到你的项目](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="69666-358">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="69666-359">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="69666-359">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="69666-360">若要添加代码段使用键盘 (仅限 C#)</span><span class="sxs-lookup"><span data-stu-id="69666-360">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="69666-361">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="69666-361">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="69666-362">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="69666-362">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="69666-363">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="69666-363">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="69666-364">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="69666-364">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="69666-365">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="69666-365">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="69666-366">![开始键入代码段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="69666-366">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="69666-367">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="69666-367">*Start typing the snippet name*</span></span>

    <span data-ttu-id="69666-368">![按 tab 键以选择突出显示代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="69666-368">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="69666-369">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="69666-369">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="69666-370">![再次按 Tab 和代码段将 expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="69666-370">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="69666-371">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="69666-371">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="69666-372">若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）</span><span class="sxs-lookup"><span data-stu-id="69666-372">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="69666-373">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="69666-373">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="69666-374">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="69666-374">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="69666-375">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="69666-375">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="69666-376">![右键单击你想要插入代码段和选择插入代码段](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="69666-376">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="69666-377">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="69666-377">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="69666-378">![通过单击选择列表中中的相关代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="69666-378">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="69666-379">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="69666-379">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="69666-380">附录 b： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="69666-380">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="69666-381">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="69666-381">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="69666-382">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="69666-382">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="69666-383">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="69666-383">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="69666-384">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="69666-384">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="69666-385">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="69666-385">Click on **Install Now**.</span></span> <span data-ttu-id="69666-386">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="69666-386">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="69666-387">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="69666-387">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="69666-388">![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="69666-388">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="69666-389">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="69666-389">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="69666-390">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="69666-390">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="69666-392">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="69666-392">*Accepting the license terms*</span></span>
5. <span data-ttu-id="69666-393">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="69666-393">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="69666-395">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="69666-395">*Installation progress*</span></span>
6. <span data-ttu-id="69666-396">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="69666-396">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="69666-398">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="69666-398">*Installation completed*</span></span>
7. <span data-ttu-id="69666-399">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="69666-399">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="69666-400">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="69666-400">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="69666-402">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="69666-402">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="69666-403">附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="69666-403">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="69666-404">本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="69666-404">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="69666-405">任务 1-从 Azure 门户创建新的 Web 站点</span><span class="sxs-lookup"><span data-stu-id="69666-405">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="69666-406">转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="69666-406">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-407">借助 Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="69666-407">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="69666-408">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="69666-408">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="69666-409">![登录到 Windows Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="69666-409">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="69666-410">*登录到门户*</span><span class="sxs-lookup"><span data-stu-id="69666-410">*Log on to Portal*</span></span>
2. <span data-ttu-id="69666-411">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="69666-411">Click **New** on the command bar.</span></span>

    <span data-ttu-id="69666-412">![创建新的 Web 站点](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="69666-412">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="69666-413">*创建新的 Web 站点*</span><span class="sxs-lookup"><span data-stu-id="69666-413">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="69666-414">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="69666-414">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="69666-415">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="69666-415">Then select **Quick Create** option.</span></span> <span data-ttu-id="69666-416">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="69666-416">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-417">Azure 是可以控制和管理在云中运行的 web 应用程序的主机。</span><span class="sxs-lookup"><span data-stu-id="69666-417">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="69666-418">快速创建选项，可部署到 Azure 门户外部的已完成的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="69666-418">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="69666-419">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="69666-419">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="69666-420">![创建新的网站使用快速创建](build-restful-apis-with-aspnet-web-api/_static/image41.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="69666-420">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="69666-421">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="69666-421">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="69666-422">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="69666-422">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="69666-423">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="69666-423">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="69666-424">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="69666-424">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="69666-425">![浏览到新的 web 站点](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="69666-425">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="69666-426">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="69666-426">*Browsing to the new web site*</span></span>

    <span data-ttu-id="69666-427">![正在运行的网站](build-restful-apis-with-aspnet-web-api/_static/image43.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="69666-427">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="69666-428">*正在运行的网站*</span><span class="sxs-lookup"><span data-stu-id="69666-428">*Web site running*</span></span>
6. <span data-ttu-id="69666-429">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="69666-429">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="69666-430">![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="69666-430">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="69666-431">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="69666-431">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="69666-432">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="69666-432">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-433">*发布配置文件*包含所有发布到 Azure 的每个启用的发布方法的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="69666-433">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="69666-434">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="69666-434">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="69666-435">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="69666-435">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="69666-436">![正在下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="69666-436">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="69666-437">*正在下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="69666-437">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="69666-438">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="69666-438">Download the publish profile file to a known location.</span></span> <span data-ttu-id="69666-439">进一步在此练习中将了解如何使用此文件发布到 Azure 的 web 应用程序从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="69666-439">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="69666-440">![保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="69666-440">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="69666-441">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="69666-441">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="69666-442">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="69666-442">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="69666-443">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="69666-443">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="69666-444">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="69666-444">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="69666-445">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="69666-445">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="69666-446">可以从在 Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**.</span><span class="sxs-lookup"><span data-stu-id="69666-446">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="69666-447">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-447">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="69666-448">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="69666-448">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="69666-449">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="69666-449">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="69666-450">![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="69666-450">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="69666-451">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="69666-451">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="69666-452">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="69666-452">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="69666-453">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="69666-453">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="69666-455">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="69666-455">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="69666-456">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="69666-456">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="69666-458">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="69666-458">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="69666-459">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="69666-459">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="69666-460">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="69666-460">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="69666-461">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="69666-461">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="69666-462">![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="69666-462">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="69666-463">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="69666-463">*Publishing the web site*</span></span>
2. <span data-ttu-id="69666-464">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="69666-464">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="69666-465">![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="69666-465">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="69666-466">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="69666-466">*Importing publish profile*</span></span>
3. <span data-ttu-id="69666-467">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="69666-467">Click **Validate Connection**.</span></span> <span data-ttu-id="69666-468">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="69666-468">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69666-469">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="69666-469">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="69666-470">![验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="69666-470">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="69666-471">*验证连接*</span><span class="sxs-lookup"><span data-stu-id="69666-471">*Validating connection*</span></span>
4. <span data-ttu-id="69666-472">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="69666-472">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="69666-473">![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="69666-473">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="69666-474">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="69666-474">*Web deploy configuration*</span></span>
5. <span data-ttu-id="69666-475">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="69666-475">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="69666-476">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="69666-476">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="69666-477">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="69666-477">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="69666-478">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="69666-478">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="69666-479">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="69666-479">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="69666-480">![配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="69666-480">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="69666-481">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="69666-481">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="69666-482">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="69666-482">Then click **OK**.</span></span> <span data-ttu-id="69666-483">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="69666-483">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="69666-484">![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="69666-484">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="69666-485">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="69666-485">*Creating the database*</span></span>
7. <span data-ttu-id="69666-486">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="69666-486">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="69666-487">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="69666-487">Then click **Next**.</span></span>

    <span data-ttu-id="69666-488">![连接字符串指向 SQL 数据库](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="69666-488">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="69666-489">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="69666-489">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="69666-490">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="69666-490">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="69666-491">![Web 应用程序发布](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="69666-491">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="69666-492">*Web 应用程序发布*</span><span class="sxs-lookup"><span data-stu-id="69666-492">*Publishing the web application*</span></span>
9. <span data-ttu-id="69666-493">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="69666-493">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="69666-494">![应用程序发布到 Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="69666-494">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="69666-495">*应用程序发布到 Azure*</span><span class="sxs-lookup"><span data-stu-id="69666-495">*Application published to Azure*</span></span>
