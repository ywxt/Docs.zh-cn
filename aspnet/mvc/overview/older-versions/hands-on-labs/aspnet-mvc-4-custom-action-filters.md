---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: "ASP.NET MVC 4 自定义操作筛选器 |Microsoft 文档"
author: rick-anderson
description: "ASP.NET MVC 提供用于执行筛选逻辑之前或之后，则操作方法调用的操作筛选器。 操作筛选器是自定义特性 tha..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: 103cd68c576463d87d0077cc149f9b89c6e028e8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="43326-104">ASP.NET MVC 4 自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-104">ASP.NET MVC 4 Custom Action Filters</span></span>
====================
<span data-ttu-id="43326-105">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="43326-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="43326-106">ASP.NET MVC 提供用于执行筛选逻辑之前或之后，则操作方法调用的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-106">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="43326-107">操作筛选器是提供声明性方式，将预操作和后操作行为添加到控制器的操作方法的自定义属性。</span><span class="sxs-lookup"><span data-stu-id="43326-107">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>
> 
> <span data-ttu-id="43326-108">在此动手实验将到 MvcMusicStore 解决方案，以捕获控制器的请求和记录插入数据库表的站点的活动来创建自定义操作筛选器属性。</span><span class="sxs-lookup"><span data-stu-id="43326-108">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="43326-109">你将能够通过注入的日志记录筛选器添加到任何控制器或操作。</span><span class="sxs-lookup"><span data-stu-id="43326-109">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="43326-110">最后，你将看到显示的访问者的列表的日志视图。</span><span class="sxs-lookup"><span data-stu-id="43326-110">Finally, you will see the log view that shows the list of visitors.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="43326-111">此动手实验假定你具有的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="43326-111">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="43326-112">如果您未使用过**ASP.NET MVC**之前，我们建议你转到**ASP.NET MVC 4 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="43326-112">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="43326-113">目标</span><span class="sxs-lookup"><span data-stu-id="43326-113">Objectives</span></span>

<span data-ttu-id="43326-114">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="43326-114">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="43326-115">创建要扩展的筛选功能的自定义操作筛选器属性</span><span class="sxs-lookup"><span data-stu-id="43326-115">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="43326-116">通过为特定级别的注入应用自定义的筛选器属性</span><span class="sxs-lookup"><span data-stu-id="43326-116">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="43326-117">全局注册自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-117">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="43326-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="43326-118">Prerequisites</span></span>

<span data-ttu-id="43326-119">你必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="43326-119">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="43326-120">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="43326-120">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="43326-121">安装</span><span class="sxs-lookup"><span data-stu-id="43326-121">Setup</span></span>

<span data-ttu-id="43326-122">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="43326-122">**Installing Code Snippets**</span></span>

<span data-ttu-id="43326-123">为方便起见，你将沿此实验室管理大部分都是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="43326-123">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="43326-124">若要安装运行的代码段**.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="43326-124">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="43326-125">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 c： 使用代码段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="43326-125">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="43326-126">练习</span><span class="sxs-lookup"><span data-stu-id="43326-126">Exercises</span></span>

<span data-ttu-id="43326-127">此动手实验包含通过在以下练习：</span><span class="sxs-lookup"><span data-stu-id="43326-127">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="43326-128">练习 1： 日志记录操作</span><span class="sxs-lookup"><span data-stu-id="43326-128">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="43326-129">练习 2： 管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-129">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="43326-130">估计时间来完成该实验： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="43326-130">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="43326-131">每个练习均附带由**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="43326-131">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="43326-132">如果你需要通过在练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="43326-132">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="43326-133">练习 1： 日志记录操作</span><span class="sxs-lookup"><span data-stu-id="43326-133">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="43326-134">在本练习中，你将学习如何使用 ASP.NET MVC 4 筛选器提供程序创建自定义操作日志筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-134">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="43326-135">为该目的将到将在所选的控制器中记录所有活动的 MusicStore 站点应用日志记录筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-135">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="43326-136">筛选器将扩展**ActionFilterAttributeClass** ，并重写**OnActionExecuting**方法来捕获每个请求，然后执行日志记录操作。</span><span class="sxs-lookup"><span data-stu-id="43326-136">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="43326-137">有关 HTTP 请求的上下文信息，执行方法、 结果和参数将会予以提供 ASP.NET MVC **ActionExecutingContext**类**。**</span><span class="sxs-lookup"><span data-stu-id="43326-137">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="43326-138">ASP.NET MVC 4 还具有默认筛选器提供程序可以使用而无需创建自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-138">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="43326-139">ASP.NET MVC 4 提供以下类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="43326-139">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="43326-140">**授权**筛选，这使得安全决策是否要执行的操作方法，如执行身份验证或验证的请求属性。</span><span class="sxs-lookup"><span data-stu-id="43326-140">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="43326-141">**操作**筛选器，用于包装操作方法的执行。</span><span class="sxs-lookup"><span data-stu-id="43326-141">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="43326-142">此筛选器可以执行其他处理，如提供到操作方法的额外数据、 检查返回的值，或取消执行的操作方法</span><span class="sxs-lookup"><span data-stu-id="43326-142">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="43326-143">**结果**筛选器，用于包装 ActionResult 对象执行。</span><span class="sxs-lookup"><span data-stu-id="43326-143">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="43326-144">此筛选器可以执行结果，例如修改 HTTP 响应的其他的处理。</span><span class="sxs-lookup"><span data-stu-id="43326-144">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="43326-145">**异常**筛选器，用于执行如果没有在操作方法中，开始授权筛选器，以与结果执行的某个位置引发未处理的异常。</span><span class="sxs-lookup"><span data-stu-id="43326-145">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="43326-146">异常筛选器可以用于任务，例如日志记录或显示错误页。</span><span class="sxs-lookup"><span data-stu-id="43326-146">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="43326-147">有关筛选器提供程序的详细信息，请访问此 MSDN 链接: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx))。</span><span class="sxs-lookup"><span data-stu-id="43326-147">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="43326-148">有关 MVC 音乐应用商店应用程序日志记录功能</span><span class="sxs-lookup"><span data-stu-id="43326-148">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="43326-149">此音乐商店解决方案具有站点日志记录的新数据模型表**ActionLog**，使用以下字段： 接收请求，调用操作，客户端 IP 和时间戳的控制器名称。</span><span class="sxs-lookup"><span data-stu-id="43326-149">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="43326-150">![数据模型。ActionLog 表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "数据模型。ActionLog 表。")</span><span class="sxs-lookup"><span data-stu-id="43326-150">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="43326-151">*数据模型的 ActionLog 表*</span><span class="sxs-lookup"><span data-stu-id="43326-151">*Data model - ActionLog table*</span></span>

<span data-ttu-id="43326-152">解决方案提供的操作日志中找不到在 ASP.NET MVC 视图**MvcMusicStores/视图/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="43326-152">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="43326-153">![操作日志视图](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作日志视图")</span><span class="sxs-lookup"><span data-stu-id="43326-153">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="43326-154">*操作日志视图*</span><span class="sxs-lookup"><span data-stu-id="43326-154">*Action Log view*</span></span>

<span data-ttu-id="43326-155">与此提供结构，情况下，所有工作将都侧重于中断控制器的请求和使用自定义筛选执行日志记录中。</span><span class="sxs-lookup"><span data-stu-id="43326-155">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="43326-156">任务 1-创建一个自定义的筛选器，以捕获控制器的请求</span><span class="sxs-lookup"><span data-stu-id="43326-156">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="43326-157">在此任务将创建一个将包含的日志记录逻辑的自定义筛选器属性类。</span><span class="sxs-lookup"><span data-stu-id="43326-157">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="43326-158">为实现此目的，你将扩展 ASP.NET MVC **ActionFilterAttribute**类和实现接口**IActionFilter**。</span><span class="sxs-lookup"><span data-stu-id="43326-158">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="43326-159">**ActionFilterAttribute**是属性的所有筛选器的基类。</span><span class="sxs-lookup"><span data-stu-id="43326-159">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="43326-160">它提供以下方法之后和控制器操作执行之前执行特定的逻辑：</span><span class="sxs-lookup"><span data-stu-id="43326-160">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="43326-161">**OnActionExecuting**(ActionExecutingContext filterContext): 恰好在操作之前调用方法。</span><span class="sxs-lookup"><span data-stu-id="43326-161">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="43326-162">**OnActionExecuted**(ActionExecutedContext filterContext): 操作方法调用之后之前 （前视图呈现） 执行的结果。</span><span class="sxs-lookup"><span data-stu-id="43326-162">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="43326-163">**OnResultExecuting**(ResultExecutingContext filterContext): 刚好在 （在之前视图呈现） 执行的结果之前。</span><span class="sxs-lookup"><span data-stu-id="43326-163">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="43326-164">**OnResultExecuted**(ResultExecutedContext filterContext): （后呈现视图） 执行的结果后。</span><span class="sxs-lookup"><span data-stu-id="43326-164">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="43326-165">通过重下列任一方法写到的派生类中，你可以执行筛选代码。</span><span class="sxs-lookup"><span data-stu-id="43326-165">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>


1. <span data-ttu-id="43326-166">打开**开始**解决方案位于**\Source\Ex01-LoggingActions\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="43326-166">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

    1. <span data-ttu-id="43326-167">你将需要下载一些缺少的 NuGet 程序包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="43326-167">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="43326-168">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="43326-168">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="43326-169">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="43326-169">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="43326-170">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="43326-170">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-171">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="43326-171">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="43326-172">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="43326-172">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="43326-173">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="43326-173">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
    > 
    > <span data-ttu-id="43326-174">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="43326-174">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="43326-175">添加一个新 C# 类到**筛选器**文件夹并将其命名*CustomActionFilter.cs*。</span><span class="sxs-lookup"><span data-stu-id="43326-175">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="43326-176">此文件夹将存储所有自定义的筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-176">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="43326-177">打开**CustomActionFilter.cs**并添加对引用**System.Web.Mvc**和**MvcMusicStore.Models**命名空间：</span><span class="sxs-lookup"><span data-stu-id="43326-177">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="43326-178">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="43326-178">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="43326-179">继承**CustomActionFilter**类**ActionFilterAttribute**然后进行**CustomActionFilter**类实现**IActionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="43326-179">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="43326-180">请**CustomActionFilter**类重写方法**OnActionExecuting**并添加必要的逻辑来筛选器的执行操作记录。</span><span class="sxs-lookup"><span data-stu-id="43326-180">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="43326-181">若要执行此操作，将添加以下突出显示的代码中**CustomActionFilter**类。</span><span class="sxs-lookup"><span data-stu-id="43326-181">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="43326-182">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="43326-182">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="43326-183">**OnActionExecuting**方法就使用**实体框架**添加新的 ActionLog 注册。</span><span class="sxs-lookup"><span data-stu-id="43326-183">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="43326-184">它会创建并填充新的实体实例的上下文信息从**filterContext**。</span><span class="sxs-lookup"><span data-stu-id="43326-184">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="43326-185">你可以阅读更多有关**ControllerContext**类在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43326-185">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="43326-186">任务 2-将代码拦截器注入到存储控制器类</span><span class="sxs-lookup"><span data-stu-id="43326-186">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="43326-187">在此任务将通过注入到所有控制器类和将记录的控制器操作添加自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-187">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="43326-188">本练习中，为了存储控制器类将具有一个日志。</span><span class="sxs-lookup"><span data-stu-id="43326-188">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="43326-189">该方法**OnActionExecuting**从**ActionLogFilterAttribute**在调用插入的元素时，将运行自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-189">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="43326-190">还有可能截获特定控制器方法。</span><span class="sxs-lookup"><span data-stu-id="43326-190">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="43326-191">打开**StoreController**在**MvcMusicStore\Controllers**并添加对引用**筛选器**命名空间：</span><span class="sxs-lookup"><span data-stu-id="43326-191">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="43326-192">插入自定义筛选器**CustomActionFilter**到**StoreController**类通过添加**[CustomActionFilter]**之前类声明的属性。</span><span class="sxs-lookup"><span data-stu-id="43326-192">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

    > [!NOTE]
    > <span data-ttu-id="43326-193">当筛选器注入到控制器类时，是还将插入的所有操作。</span><span class="sxs-lookup"><span data-stu-id="43326-193">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="43326-194">如果你想要应用筛选器仅针对一组操作，你将不得不注入**[CustomActionFilter]**到每个：</span><span class="sxs-lookup"><span data-stu-id="43326-194">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
    > 
    > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="43326-195">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="43326-195">Task 3 - Running the Application</span></span>

<span data-ttu-id="43326-196">在此任务中，将测试的日志记录筛选器正常工作。</span><span class="sxs-lookup"><span data-stu-id="43326-196">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="43326-197">将启动应用程序，请访问应用商店，，然后你将检查记录的活动。</span><span class="sxs-lookup"><span data-stu-id="43326-197">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="43326-198">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="43326-198">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="43326-199">浏览到**/ActionLog**若要查看日志视图初始状态：</span><span class="sxs-lookup"><span data-stu-id="43326-199">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="43326-200">![登录页的活动发生之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image3.png "登录页的活动发生之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="43326-200">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="43326-201">*页上的活动发生之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="43326-201">*Log tracker status before page activity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-202">默认情况下，它将始终显示检索菜单现有风格时生成的一个项。</span><span class="sxs-lookup"><span data-stu-id="43326-202">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
    > 
    > <span data-ttu-id="43326-203">为了简单起见我们正在清理**ActionLog**表每次应用程序运行时，因此它将仅显示每个特定任务的验证的日志。</span><span class="sxs-lookup"><span data-stu-id="43326-203">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
    > 
    > <span data-ttu-id="43326-204">你可能需要删除以下代码从**会话\_启动**方法 (在**Global.asax**类)，以便保存对在存储区中执行的所有操作的历史日志控制器。</span><span class="sxs-lookup"><span data-stu-id="43326-204">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
    > 
    > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="43326-205">单击其中一个**风格**从菜单并执行某些操作，如浏览可用唱片集。</span><span class="sxs-lookup"><span data-stu-id="43326-205">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="43326-206">浏览到**/ActionLog**和如果日志已空按**F5**刷新该页面。</span><span class="sxs-lookup"><span data-stu-id="43326-206">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="43326-207">请检查跟踪，您的访问：</span><span class="sxs-lookup"><span data-stu-id="43326-207">Check that your visits were tracked:</span></span>

    <span data-ttu-id="43326-208">![与活动记录的操作日志](aspnet-mvc-4-custom-action-filters/_static/image4.png "与活动记录的操作日志")</span><span class="sxs-lookup"><span data-stu-id="43326-208">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="43326-209">*与活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="43326-209">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="43326-210">练习 2： 管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-210">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="43326-211">在本练习将将第二个自定义操作筛选器添加到 StoreController 类，并定义将在其中执行两个筛选器的特定顺序。</span><span class="sxs-lookup"><span data-stu-id="43326-211">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="43326-212">然后将更新全局注册的筛选器的代码。</span><span class="sxs-lookup"><span data-stu-id="43326-212">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="43326-213">有定义的筛选器的执行顺序时，需要考虑的不同选项。</span><span class="sxs-lookup"><span data-stu-id="43326-213">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="43326-214">例如，Order 属性和筛选器的作用域:</span><span class="sxs-lookup"><span data-stu-id="43326-214">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="43326-215">你可以定义**作用域**对于每个筛选器，例如，你无法确定作用域的所有操作筛选器中运行**控制器都范围**，和所有授权筛选器中运行**全局作用都域**.</span><span class="sxs-lookup"><span data-stu-id="43326-215">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="43326-216">作用域具有定义的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="43326-216">The scopes have a defined execution order.</span></span>

<span data-ttu-id="43326-217">此外，每个操作筛选器具有顺序属性用于确定筛选器的作用域中的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="43326-217">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="43326-218">有关自定义操作筛选器执行顺序的详细信息，请访问此 MSDN 文章: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))。</span><span class="sxs-lookup"><span data-stu-id="43326-218">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="43326-219">任务 1： 创建新的自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-219">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="43326-220">在此任务中，你将创建新的自定义操作筛选器将插入 StoreController 类中，学习如何管理筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="43326-220">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="43326-221">打开**开始**解决方案位于**\Source\Ex02-ManagingMultipleActionFilters\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="43326-221">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="43326-222">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="43326-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="43326-223">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="43326-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="43326-224">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="43326-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="43326-225">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="43326-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="43326-226">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="43326-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="43326-227">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="43326-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="43326-228">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="43326-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="43326-229">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="43326-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="43326-230">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="43326-230">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="43326-231">添加一个新 C# 类到**筛选器**文件夹并将其命名*MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="43326-231">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="43326-232">打开**MyNewCustomActionFilter.cs**并添加对引用**System.Web.Mvc**和**MvcMusicStore.Models**命名空间：</span><span class="sxs-lookup"><span data-stu-id="43326-232">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="43326-233">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2 MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="43326-233">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="43326-234">默认类声明替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="43326-234">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="43326-235">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2 MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="43326-235">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="43326-236">此自定义操作筛选器是与你在上一练习中创建几乎相同的。</span><span class="sxs-lookup"><span data-stu-id="43326-236">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="43326-237">主要区别是它有*&quot;记录通过&quot;*更新与此新类的名称以标识 wich 筛选器属性注册日志。</span><span class="sxs-lookup"><span data-stu-id="43326-237">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify wich filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="43326-238">任务 2： 将新的代码拦截器注入到 StoreController 类</span><span class="sxs-lookup"><span data-stu-id="43326-238">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="43326-239">在此任务中，将将新的自定义筛选器添加到 StoreController 类，并运行解决方案，以验证如何两个筛选器协同工作。</span><span class="sxs-lookup"><span data-stu-id="43326-239">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="43326-240">打开**StoreController**类位于**MvcMusicStore\Controllers**和插入新的自定义筛选器**MyNewCustomActionFilter**到**StoreController**类，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="43326-240">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="43326-241">现在，运行应用程序，以便了解这些两个自定义操作筛选器的工作。</span><span class="sxs-lookup"><span data-stu-id="43326-241">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="43326-242">若要执行此操作，请按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="43326-242">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="43326-243">浏览到**/ActionLog**若要查看日志视图初始状态。</span><span class="sxs-lookup"><span data-stu-id="43326-243">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="43326-244">![登录页的活动发生之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image5.png "登录页的活动发生之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="43326-244">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="43326-245">*页上的活动发生之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="43326-245">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="43326-246">单击其中一个**风格**从菜单并执行某些操作，如浏览可用唱片集。</span><span class="sxs-lookup"><span data-stu-id="43326-246">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="43326-247">检查此时间;两次跟踪，您的访问： 后中添加自定义操作筛选器的每个**StorageController**类。</span><span class="sxs-lookup"><span data-stu-id="43326-247">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="43326-248">![与活动记录的操作日志](aspnet-mvc-4-custom-action-filters/_static/image6.png "与活动记录的操作日志")</span><span class="sxs-lookup"><span data-stu-id="43326-248">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="43326-249">*与活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="43326-249">*Action log with activity logged*</span></span>
6. <span data-ttu-id="43326-250">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="43326-250">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="43326-251">任务 3： 管理筛选器排序</span><span class="sxs-lookup"><span data-stu-id="43326-251">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="43326-252">在此任务中，你将了解如何通过顺序属性进行管理的筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="43326-252">In this task, you will learn how to manage the filters' execution order by using the Order propery.</span></span>

1. <span data-ttu-id="43326-253">打开**StoreController**类位于**MvcMusicStore\Controllers**并指定**顺序**中两个筛选器属性如下面所示。</span><span class="sxs-lookup"><span data-stu-id="43326-253">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="43326-254">现在，验证如何根据其顺序属性的值执行的筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-254">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="43326-255">您会发现具有最小的顺序值的筛选器 (**CustomActionFilter**) 是执行的第一个。</span><span class="sxs-lookup"><span data-stu-id="43326-255">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="43326-256">按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="43326-256">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="43326-257">浏览到**/ActionLog**若要查看日志视图初始状态。</span><span class="sxs-lookup"><span data-stu-id="43326-257">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="43326-258">![登录页的活动发生之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image7.png "登录页的活动发生之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="43326-258">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="43326-259">*页上的活动发生之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="43326-259">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="43326-260">单击其中一个**风格**从菜单并执行某些操作，如浏览可用唱片集。</span><span class="sxs-lookup"><span data-stu-id="43326-260">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="43326-261">检查此期间，您的访问中跟踪按筛选器的顺序值进行排序： **CustomActionFilter**日志的第一个。</span><span class="sxs-lookup"><span data-stu-id="43326-261">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="43326-262">![与活动记录的操作日志](aspnet-mvc-4-custom-action-filters/_static/image8.png "与活动记录的操作日志")</span><span class="sxs-lookup"><span data-stu-id="43326-262">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="43326-263">*与活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="43326-263">*Action log with activity logged*</span></span>
6. <span data-ttu-id="43326-264">现在，你将更新的筛选器的顺序值，并验证日志记录顺序将如何变化。</span><span class="sxs-lookup"><span data-stu-id="43326-264">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="43326-265">在**StoreController**类中，更新的筛选器的顺序值，如下面所示。</span><span class="sxs-lookup"><span data-stu-id="43326-265">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="43326-266">再次运行该应用程序，通过按**F5**。</span><span class="sxs-lookup"><span data-stu-id="43326-266">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="43326-267">单击其中一个**风格**从菜单并执行某些操作，如浏览可用唱片集。</span><span class="sxs-lookup"><span data-stu-id="43326-267">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="43326-268">检查此期间，日志是否创建通过**MyNewCustomActionFilter**筛选器显示在最前面。</span><span class="sxs-lookup"><span data-stu-id="43326-268">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="43326-269">![与活动记录的操作日志](aspnet-mvc-4-custom-action-filters/_static/image9.png "与活动记录的操作日志")</span><span class="sxs-lookup"><span data-stu-id="43326-269">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="43326-270">*与活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="43326-270">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="43326-271">任务 4： 注册全局筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-271">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="43326-272">在此任务中，你将更新解决方案以注册新的筛选器 (**MyNewCustomActionFilter**) 作为全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-272">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="43326-273">通过执行此操作，将会触发的所有操作执行应用程序中并不只在如下所示的上一任务 StoreController 的。</span><span class="sxs-lookup"><span data-stu-id="43326-273">By doing this, it will be triggered by all the actions perfomed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="43326-274">在**StoreController**类中，删除**[MyNewCustomActionFilter]**属性和顺序属性从**[CustomActionFilter]**。</span><span class="sxs-lookup"><span data-stu-id="43326-274">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="43326-275">其外观应如下所示：</span><span class="sxs-lookup"><span data-stu-id="43326-275">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="43326-276">打开**Global.asax**文件并找到**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="43326-276">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="43326-277">请注意，每个 thime 应用程序启动时它正在注册全局筛选器，通过调用**RegisterGlobalFilters**方法内的**FilterConfig**类。</span><span class="sxs-lookup"><span data-stu-id="43326-277">Notice that each thime the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="43326-278">![在 Global.asax 中注册全局筛选器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 Global.asax 中注册全局筛选器")</span><span class="sxs-lookup"><span data-stu-id="43326-278">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="43326-279">*在 Global.asax 中注册全局筛选器*</span><span class="sxs-lookup"><span data-stu-id="43326-279">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="43326-280">打开**FilterConfig.cs**文件内**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="43326-280">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="43326-281">添加对使用 System.Web.Mvc; 的引用使用 MvcMusicStore.Filters;命名空间。</span><span class="sxs-lookup"><span data-stu-id="43326-281">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="43326-282">更新**RegisterGlobalFilters**添加自定义的筛选器的方法。</span><span class="sxs-lookup"><span data-stu-id="43326-282">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="43326-283">若要执行此操作，添加突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="43326-283">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="43326-284">通过按运行该应用程序**F5**。</span><span class="sxs-lookup"><span data-stu-id="43326-284">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="43326-285">单击其中一个**风格**从菜单并执行某些操作，如浏览可用唱片集。</span><span class="sxs-lookup"><span data-stu-id="43326-285">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="43326-286">检查该现在**[MyNewCustomActionFilter]**被注入到 HomeController 和 ActionLogController 过。</span><span class="sxs-lookup"><span data-stu-id="43326-286">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="43326-287">![与活动记录的操作日志](aspnet-mvc-4-custom-action-filters/_static/image11.png "与活动记录的操作日志")</span><span class="sxs-lookup"><span data-stu-id="43326-287">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="43326-288">*具有全局活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="43326-288">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="43326-289">此外，你可以部署此应用程序对 Windows Azure 网站以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web Deploy](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="43326-289">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="43326-290">摘要</span><span class="sxs-lookup"><span data-stu-id="43326-290">Summary</span></span>

<span data-ttu-id="43326-291">通过完成本动手实验中，你已学习如何扩展操作筛选器以执行自定义操作。</span><span class="sxs-lookup"><span data-stu-id="43326-291">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="43326-292">你已学习如何插入到页控制器的任何筛选器。</span><span class="sxs-lookup"><span data-stu-id="43326-292">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="43326-293">使用以下概念：</span><span class="sxs-lookup"><span data-stu-id="43326-293">The following concepts were used:</span></span>

- <span data-ttu-id="43326-294">如何使用 ASP.NET MVC ActionFilterAttribute 类创建自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-294">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="43326-295">如何将筛选器注入到 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="43326-295">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="43326-296">如何管理筛选器排序使用的顺序属性</span><span class="sxs-lookup"><span data-stu-id="43326-296">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="43326-297">如何注册全局筛选器</span><span class="sxs-lookup"><span data-stu-id="43326-297">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="43326-298">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="43326-298">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="43326-299">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="43326-299">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="43326-300">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="43326-300">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="43326-301">转到[ [https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="43326-301">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="43326-302">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; *Visual Studio Express 2012 for Web 的 Windows Azure SDK*&quot;。</span><span class="sxs-lookup"><span data-stu-id="43326-302">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="43326-303">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="43326-303">Click on **Install Now**.</span></span> <span data-ttu-id="43326-304">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="43326-304">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="43326-305">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="43326-305">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="43326-306">![安装 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="43326-306">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="43326-307">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="43326-307">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="43326-308">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="43326-308">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="43326-310">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="43326-310">*Accepting the license terms*</span></span>
5. <span data-ttu-id="43326-311">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="43326-311">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="43326-313">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="43326-313">*Installation progress*</span></span>
6. <span data-ttu-id="43326-314">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="43326-314">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="43326-316">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="43326-316">*Installation completed*</span></span>
7. <span data-ttu-id="43326-317">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="43326-317">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="43326-318">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="43326-318">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="43326-320">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="43326-320">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="43326-321">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="43326-321">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="43326-322">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="43326-322">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="43326-323">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="43326-323">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="43326-324">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="43326-324">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-325">使用 Windows Azure 可以免费承载 10 个 ASP.NET 网站，然后随着流量增长而扩展。</span><span class="sxs-lookup"><span data-stu-id="43326-325">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="43326-326">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="43326-326">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="43326-327">![登录到 Windows Azure 门户](aspnet-mvc-4-custom-action-filters/_static/image17.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="43326-327">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="43326-328">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="43326-328">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="43326-329">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="43326-329">Click **New** on the command bar.</span></span>

    <span data-ttu-id="43326-330">![创建新网站](aspnet-mvc-4-custom-action-filters/_static/image18.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="43326-330">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="43326-331">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="43326-331">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="43326-332">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="43326-332">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="43326-333">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="43326-333">Then select **Quick Create** option.</span></span> <span data-ttu-id="43326-334">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="43326-334">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-335">Windows Azure 网站是在云中，你可以控制和管理运行的 web 应用程序的宿主。</span><span class="sxs-lookup"><span data-stu-id="43326-335">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="43326-336">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从在门户外部部署。</span><span class="sxs-lookup"><span data-stu-id="43326-336">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="43326-337">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="43326-337">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="43326-338">![创建新的网站使用快速创建](aspnet-mvc-4-custom-action-filters/_static/image19.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="43326-338">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="43326-339">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="43326-339">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="43326-340">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="43326-340">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="43326-341">创建网站后单击下的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="43326-341">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="43326-342">检查新的 Web 站点工作。</span><span class="sxs-lookup"><span data-stu-id="43326-342">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="43326-343">![浏览到新的 web 站点](aspnet-mvc-4-custom-action-filters/_static/image20.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="43326-343">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="43326-344">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="43326-344">*Browsing to the new web site*</span></span>

    <span data-ttu-id="43326-345">![运行网站](aspnet-mvc-4-custom-action-filters/_static/image21.png "运行的网站")</span><span class="sxs-lookup"><span data-stu-id="43326-345">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="43326-346">*运行的网站*</span><span class="sxs-lookup"><span data-stu-id="43326-346">*Web site running*</span></span>
6. <span data-ttu-id="43326-347">返回到门户并单击在网站的名称**名称**列以显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="43326-347">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="43326-348">![打开网站管理页](aspnet-mvc-4-custom-action-filters/_static/image22.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="43326-348">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="43326-349">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="43326-349">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="43326-350">在**仪表板**页上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="43326-350">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-351">*发布配置文件*包含所有 web 应用程序发布到 Windows Azure 网站中的每个启用的发布方法所需的信息。</span><span class="sxs-lookup"><span data-stu-id="43326-351">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="43326-352">发布配置文件包含的 Url、 用户凭据和连接到并针对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="43326-352">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="43326-353">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件以自动执行的这些程序，以便配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="43326-353">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="43326-354">![下载网站发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image23.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="43326-354">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="43326-355">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="43326-355">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="43326-356">到一个已知位置下载发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="43326-356">Download the publish profile file to a known location.</span></span> <span data-ttu-id="43326-357">进一步在本练习中您将了解如何使用此文件来发布 Visual Studio 中的 web 应用程序到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="43326-357">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="43326-358">![保存发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image24.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="43326-358">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="43326-359">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="43326-359">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="43326-360">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="43326-360">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="43326-361">如果你的应用程序将使用 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="43326-361">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="43326-362">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="43326-362">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="43326-363">需要将用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="43326-363">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="43326-364">你可以从你的订阅在 Windows Azure 管理门户中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="43326-364">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="43326-365">如果你没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="43326-365">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="43326-366">请记下的**服务器名称和 URL、 管理员登录名和密码**，如你将在接下来的任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="43326-366">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="43326-367">不创建数据库，它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="43326-367">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="43326-368">![SQL 数据库服务器仪表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="43326-368">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="43326-369">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="43326-369">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="43326-370">在下一个任务将测试从 Visual Studio 中，数据库连接，因此你需要在的服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="43326-370">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="43326-371">若要做到这一点，请单击**配置**，选择的 IP 地址从**当前客户端 IP 地址**并将其粘贴在**起始 IP 地址**和**结束 IP 地址**文本框和单击![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="43326-371">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="43326-373">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="43326-373">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="43326-374">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="43326-374">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认做的更改](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="43326-376">*确认做的更改*</span><span class="sxs-lookup"><span data-stu-id="43326-376">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="43326-377">任务 3-发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="43326-377">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="43326-378">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="43326-378">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="43326-379">在**解决方案资源管理器**，右键单击网站项目，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="43326-379">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="43326-380">![发布应用程序](aspnet-mvc-4-custom-action-filters/_static/image29.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="43326-380">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="43326-381">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="43326-381">*Publishing the web site*</span></span>
2. <span data-ttu-id="43326-382">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="43326-382">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="43326-383">![导入发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image30.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="43326-383">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="43326-384">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="43326-384">*Importing publish profile*</span></span>
3. <span data-ttu-id="43326-385">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="43326-385">Click **Validate Connection**.</span></span> <span data-ttu-id="43326-386">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="43326-386">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43326-387">请参阅验证连接按钮旁边将显示绿色的复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="43326-387">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="43326-388">![正在验证连接](aspnet-mvc-4-custom-action-filters/_static/image31.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="43326-388">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="43326-389">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="43326-389">*Validating connection*</span></span>
4. <span data-ttu-id="43326-390">在**设置**页上，在**数据库**部分中，单击你的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="43326-390">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="43326-391">![Web 部署配置](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="43326-391">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="43326-392">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="43326-392">*Web deploy configuration*</span></span>
5. <span data-ttu-id="43326-393">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="43326-393">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="43326-394">在**服务器名称**类型 SQL 数据库服务器 URL 使用*tcp:*前缀。</span><span class="sxs-lookup"><span data-stu-id="43326-394">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="43326-395">在**用户名**键入您的服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="43326-395">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="43326-396">在**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="43326-396">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="43326-397">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="43326-397">Type a new database name.</span></span>

    <span data-ttu-id="43326-398">![配置目标连接字符串](aspnet-mvc-4-custom-action-filters/_static/image33.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="43326-398">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="43326-399">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="43326-399">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="43326-400">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="43326-400">Then click **OK**.</span></span> <span data-ttu-id="43326-401">当系统提示创建数据库单击**是**。</span><span class="sxs-lookup"><span data-stu-id="43326-401">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="43326-402">![创建数据库](aspnet-mvc-4-custom-action-filters/_static/image34.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="43326-402">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="43326-403">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="43326-403">*Creating the database*</span></span>
7. <span data-ttu-id="43326-404">在默认连接文本框中显示了将用于连接到 Windows Azure 中的 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="43326-404">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="43326-405">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="43326-405">Then click **Next**.</span></span>

    <span data-ttu-id="43326-406">![连接字符串指向 SQL 数据库](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="43326-406">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="43326-407">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="43326-407">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="43326-408">在**预览**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="43326-408">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="43326-409">![Web 应用程序发布](aspnet-mvc-4-custom-action-filters/_static/image36.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="43326-409">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="43326-410">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="43326-410">*Publishing the web application*</span></span>
9. <span data-ttu-id="43326-411">完成发布过程后，默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="43326-411">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="43326-412">附录 c： 使用代码段</span><span class="sxs-lookup"><span data-stu-id="43326-412">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="43326-413">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="43326-413">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="43326-414">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="43326-414">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="43326-415">![使用 Visual Studio 代码段将代码插入到你的项目](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="43326-415">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="43326-416">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="43326-416">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="43326-417">***若要添加代码片段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="43326-417">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="43326-418">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="43326-418">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="43326-419">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="43326-419">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="43326-420">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="43326-420">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="43326-421">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="43326-421">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="43326-422">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="43326-422">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="43326-423">![开始键入代码段名称](aspnet-mvc-4-custom-action-filters/_static/image38.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="43326-423">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="43326-424">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="43326-424">*Start typing the snippet name*</span></span>

<span data-ttu-id="43326-425">![按 Tab 以选择突出显示代码段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="43326-425">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="43326-426">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="43326-426">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="43326-427">![再次按 Tab 和代码段将会扩展](aspnet-mvc-4-custom-action-filters/_static/image40.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="43326-427">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="43326-428">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="43326-428">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="43326-429">***若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="43326-429">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="43326-430">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="43326-430">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="43326-431">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="43326-431">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="43326-432">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="43326-432">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="43326-433">![右键单击你想要插入代码段，并选择插入代码段](aspnet-mvc-4-custom-action-filters/_static/image41.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="43326-433">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="43326-434">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="43326-434">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="43326-435">![通过单击它选取列表中中的相关代码片段](aspnet-mvc-4-custom-action-filters/_static/image42.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="43326-435">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="43326-436">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="43326-436">*Pick the relevant snippet from the list, by clicking on it*</span></span>
