---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自定义操作筛选器 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 提供了用于执行筛选逻辑之前或之后调用操作方法的操作筛选器。 操作筛选器是自定义特性 tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: 0170fda6849c1dfb53b44908ea55ba2cad0dd067
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832936"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="bd631-104">ASP.NET MVC 4 自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="bd631-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="bd631-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="bd631-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="bd631-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="bd631-107">ASP.NET MVC 提供了用于执行筛选逻辑之前或之后调用操作方法的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="bd631-108">操作筛选器是提供声明性方法将操作前和操作后行为添加到控制器的操作方法的自定义属性。</span><span class="sxs-lookup"><span data-stu-id="bd631-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="bd631-109">在本动手实验将到 MvcMusicStore 解决方案来捕获控制器的请求并记录到数据库表的站点的活动创建自定义操作筛选器属性。</span><span class="sxs-lookup"><span data-stu-id="bd631-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="bd631-110">你将能够通过注入的日志记录筛选器添加到任何控制器或操作。</span><span class="sxs-lookup"><span data-stu-id="bd631-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="bd631-111">最后，您将看到显示的访问者的列表在日志视图。</span><span class="sxs-lookup"><span data-stu-id="bd631-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="bd631-112">此动手实验假定你已了解的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="bd631-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="bd631-113">如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 4 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="bd631-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="bd631-114">在 Web 训练营培训工具包中，在可从包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="bd631-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="bd631-115">特定于此实验室项目位于[ASP.NET MVC 4 自定义操作筛选器](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)。</span><span class="sxs-lookup"><span data-stu-id="bd631-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="bd631-116">目标</span><span class="sxs-lookup"><span data-stu-id="bd631-116">Objectives</span></span>

<span data-ttu-id="bd631-117">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="bd631-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="bd631-118">创建要扩展的筛选功能的自定义操作筛选器属性</span><span class="sxs-lookup"><span data-stu-id="bd631-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="bd631-119">通过为特定级别的注入应用自定义筛选器属性</span><span class="sxs-lookup"><span data-stu-id="bd631-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="bd631-120">全局注册自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="bd631-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="bd631-121">Prerequisites</span></span>

<span data-ttu-id="bd631-122">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="bd631-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="bd631-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="bd631-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="bd631-124">安装</span><span class="sxs-lookup"><span data-stu-id="bd631-124">Setup</span></span>

<span data-ttu-id="bd631-125">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="bd631-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="bd631-126">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="bd631-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="bd631-127">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="bd631-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="bd631-128">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="bd631-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="bd631-129">练习</span><span class="sxs-lookup"><span data-stu-id="bd631-129">Exercises</span></span>

<span data-ttu-id="bd631-130">此动手实验包含由以下练习：</span><span class="sxs-lookup"><span data-stu-id="bd631-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="bd631-131">练习 1： 日志记录操作</span><span class="sxs-lookup"><span data-stu-id="bd631-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="bd631-132">练习 2： 管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="bd631-133">估计的时间才能完成此实验： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="bd631-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="bd631-134">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd631-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="bd631-135">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="bd631-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="bd631-136">练习 1： 日志记录操作</span><span class="sxs-lookup"><span data-stu-id="bd631-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="bd631-137">在此练习中，您将学习如何使用 ASP.NET MVC 4 筛选器提供程序创建自定义操作日志筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="bd631-138">为此您将应用于 MusicStore 站点，以将所选的控制器中记录所有活动日志记录筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="bd631-139">将筛选器，从而扩大**ActionFilterAttributeClass**并重写**OnActionExecuting**方法来捕获每个请求，然后执行日志记录操作。</span><span class="sxs-lookup"><span data-stu-id="bd631-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="bd631-140">有关 HTTP 请求的上下文信息，执行方法、 结果和参数将由 ASP.NET MVC 提供**ActionExecutingContext**类 **。**</span><span class="sxs-lookup"><span data-stu-id="bd631-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="bd631-141">ASP.NET MVC 4 也有默认筛选器提供程序可以使用而无需创建自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="bd631-142">ASP.NET MVC 4 提供了以下类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="bd631-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="bd631-143">**授权**筛选，从而安全决定是否要执行的操作方法，如执行身份验证或验证请求的属性。</span><span class="sxs-lookup"><span data-stu-id="bd631-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="bd631-144">**操作**筛选器，用于包装操作方法执行。</span><span class="sxs-lookup"><span data-stu-id="bd631-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="bd631-145">此筛选器可以执行其他处理，如提供给操作方法的额外数据、 检查返回值，或取消执行的操作方法</span><span class="sxs-lookup"><span data-stu-id="bd631-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="bd631-146">**结果**筛选器，用于包装的 ActionResult 对象执行。</span><span class="sxs-lookup"><span data-stu-id="bd631-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="bd631-147">此筛选器可以执行其他处理的结果，如修改 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="bd631-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="bd631-148">**异常**筛选器，如果没有在操作方法中，使用授权筛选器开始和结束与结果执行的某个位置引发未处理的异常，则执行。</span><span class="sxs-lookup"><span data-stu-id="bd631-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="bd631-149">异常筛选器可用于任务，例如日志记录或显示错误页。</span><span class="sxs-lookup"><span data-stu-id="bd631-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="bd631-150">有关筛选器提供程序的详细信息，请访问此 MSDN 链接: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx))。</span><span class="sxs-lookup"><span data-stu-id="bd631-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="bd631-151">有关 MVC 音乐应用商店应用程序日志记录功能</span><span class="sxs-lookup"><span data-stu-id="bd631-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="bd631-152">此音乐应用商店解决方案具有站点日志记录的新数据模型表**ActionLog**，包含以下字段： 接收请求，调用操作、 客户端 IP 和时间戳的控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="bd631-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="bd631-153">![数据模型。ActionLog 表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "数据模型。ActionLog 表。")</span><span class="sxs-lookup"><span data-stu-id="bd631-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="bd631-154">*数据模型-ActionLog 表*</span><span class="sxs-lookup"><span data-stu-id="bd631-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="bd631-155">该解决方案提供了 ASP.NET MVC 视图，为操作日志，请参阅**MvcMusicStores/视图/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="bd631-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="bd631-156">![操作日志视图](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作日志视图")</span><span class="sxs-lookup"><span data-stu-id="bd631-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="bd631-157">*操作日志视图*</span><span class="sxs-lookup"><span data-stu-id="bd631-157">*Action Log view*</span></span>

<span data-ttu-id="bd631-158">与此假设结构，将中断控制器的请求和执行日志记录通过使用自定义筛选集中的所有工作。</span><span class="sxs-lookup"><span data-stu-id="bd631-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="bd631-159">任务 1-创建自定义筛选器来捕获控制器的请求</span><span class="sxs-lookup"><span data-stu-id="bd631-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="bd631-160">在此任务将创建一个将包含日志记录逻辑的自定义筛选器属性类。</span><span class="sxs-lookup"><span data-stu-id="bd631-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="bd631-161">为此，您将扩展 ASP.NET MVC **ActionFilterAttribute**类和实现该接口**IActionFilter**。</span><span class="sxs-lookup"><span data-stu-id="bd631-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="bd631-162">**ActionFilterAttribute**是所有属性筛选器的基类。</span><span class="sxs-lookup"><span data-stu-id="bd631-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="bd631-163">它提供了以下方法后且在执行控制器操作之前执行特定的逻辑：</span><span class="sxs-lookup"><span data-stu-id="bd631-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="bd631-164">**OnActionExecuting**(ActionExecutingContext filterContext): 操作之前，只需调用方法。</span><span class="sxs-lookup"><span data-stu-id="bd631-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="bd631-165">**OnActionExecuted**(ActionExecutedContext filterContext): 调用操作方法之后之前 （在之前视图呈现） 执行的结果。</span><span class="sxs-lookup"><span data-stu-id="bd631-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="bd631-166">**OnResultExecuting**(ResultExecutingContext filterContext): 只需之前 （在之前视图呈现） 执行的结果。</span><span class="sxs-lookup"><span data-stu-id="bd631-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="bd631-167">**OnResultExecuted**(ResultExecutedContext filterContext): （在呈现视图时） 后执行的结果后。</span><span class="sxs-lookup"><span data-stu-id="bd631-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="bd631-168">通过到派生类中替代任何一种方法，可以执行筛选的代码。</span><span class="sxs-lookup"><span data-stu-id="bd631-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>


1. <span data-ttu-id="bd631-169">打开 **开始** 解决方案位于 **\Source\Ex01-LoggingActions\Begin** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd631-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="bd631-170">你将需要下载某些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="bd631-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="bd631-171">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="bd631-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="bd631-172">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="bd631-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="bd631-173">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="bd631-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bd631-174">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="bd631-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bd631-175">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="bd631-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bd631-176">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="bd631-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="bd631-177">有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="bd631-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="bd631-178">添加一个新 C# 类到**筛选器**文件夹并将其命名*CustomActionFilter.cs*。</span><span class="sxs-lookup"><span data-stu-id="bd631-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="bd631-179">此文件夹将存储的自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="bd631-180">打开**CustomActionFilter.cs**并添加对引用**System.Web.Mvc**并**MvcMusicStore.Models**命名空间：</span><span class="sxs-lookup"><span data-stu-id="bd631-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="bd631-181">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="bd631-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="bd631-182">继承**CustomActionFilter**类派生**ActionFilterAttribute** ，然后进行**CustomActionFilter**类实现**是 IActionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="bd631-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="bd631-183">请**CustomActionFilter**类重写方法**OnActionExecuting**并添加必要的逻辑来记录筛选器的执行。</span><span class="sxs-lookup"><span data-stu-id="bd631-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="bd631-184">若要执行此操作，添加以下突出显示的代码内**CustomActionFilter**类。</span><span class="sxs-lookup"><span data-stu-id="bd631-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="bd631-185">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="bd631-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="bd631-186">**OnActionExecuting**的方法使用**Entity Framework**添加新的 ActionLog 注册。</span><span class="sxs-lookup"><span data-stu-id="bd631-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="bd631-187">它会创建并填充新的实体实例的上下文信息**filterContext**。</span><span class="sxs-lookup"><span data-stu-id="bd631-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="bd631-188">可以阅读更多有关**ControllerContext**类在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bd631-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="bd631-189">任务 2-将代码拦截器注入到应用商店控制器类</span><span class="sxs-lookup"><span data-stu-id="bd631-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="bd631-190">在此任务将通过将其注入到所有控制器类并将记录的控制器操作添加自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="bd631-191">本练习的目的存储控制器类将具有一个日志。</span><span class="sxs-lookup"><span data-stu-id="bd631-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="bd631-192">该方法**OnActionExecuting**从**ActionLogFilterAttribute**调用插入的元素时，在运行自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="bd631-193">还有可能以截获特定控制器方法。</span><span class="sxs-lookup"><span data-stu-id="bd631-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="bd631-194">打开**StoreController**处**MvcMusicStore\Controllers**并添加对引用**筛选器**命名空间：</span><span class="sxs-lookup"><span data-stu-id="bd631-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="bd631-195">注入自定义筛选器**CustomActionFilter**成**StoreController**类通过添加 **[CustomActionFilter]** 属性的类声明之前。</span><span class="sxs-lookup"><span data-stu-id="bd631-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="bd631-196">当筛选器注入到控制器类时，所有操作也都注入。</span><span class="sxs-lookup"><span data-stu-id="bd631-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="bd631-197">如果你想要应用筛选器仅对一组操作，必须将注入 **[CustomActionFilter]** 到每个之一：</span><span class="sxs-lookup"><span data-stu-id="bd631-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="bd631-198">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bd631-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="bd631-199">在本任务中，您将测试的日志记录筛选器正常工作。</span><span class="sxs-lookup"><span data-stu-id="bd631-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="bd631-200">将启动应用程序并访问应用商店，，然后您将检查记录的活动。</span><span class="sxs-lookup"><span data-stu-id="bd631-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="bd631-201">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd631-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="bd631-202">浏览到 **/ActionLog**若要查看日志视图初始状态：</span><span class="sxs-lookup"><span data-stu-id="bd631-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="bd631-203">![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image3.png "记录页活动之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bd631-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bd631-204">*页活动之前的日志跟踪程序状态*</span><span class="sxs-lookup"><span data-stu-id="bd631-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd631-205">默认情况下，它将始终显示检索现有流派菜单时，将生成的一项。</span><span class="sxs-lookup"><span data-stu-id="bd631-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="bd631-206">为简单起见我们正在清理**ActionLog**表每次应用程序运行时以便只显示每个特定任务的验证的日志。</span><span class="sxs-lookup"><span data-stu-id="bd631-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="bd631-207">可能需要删除中的以下代码**会话\_启动**方法 (在**Global.asax**类)，以便保存在存储区中执行的所有操作的历史日志控制器。</span><span class="sxs-lookup"><span data-stu-id="bd631-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="bd631-208">单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bd631-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="bd631-209">浏览到 **/ActionLog**且日志为空按**F5**刷新页面。</span><span class="sxs-lookup"><span data-stu-id="bd631-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="bd631-210">检查未跟踪您的访问：</span><span class="sxs-lookup"><span data-stu-id="bd631-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="bd631-211">![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image4.png "活动记录具有操作日志")</span><span class="sxs-lookup"><span data-stu-id="bd631-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bd631-212">*使用活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bd631-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="bd631-213">练习 2： 管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="bd631-214">在此练习中将将第二个自定义操作筛选器添加到 StoreController 类并定义将在其中执行两个筛选器的特定顺序。</span><span class="sxs-lookup"><span data-stu-id="bd631-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="bd631-215">然后将更新代码以注册全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="bd631-216">有不同的方法定义的筛选器的执行顺序时需要考虑。</span><span class="sxs-lookup"><span data-stu-id="bd631-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="bd631-217">例如，Order 属性和筛选器的作用域：</span><span class="sxs-lookup"><span data-stu-id="bd631-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="bd631-218">您可以定义**作用域**对于每个筛选器，例如，可将范围限定的所有操作筛选器中运行**控制器都范围**，和所有授权筛选器中运行**全局作用都域**.</span><span class="sxs-lookup"><span data-stu-id="bd631-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="bd631-219">作用域具有定义的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bd631-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="bd631-220">此外，每个操作筛选器有一个顺序属性，用于确定筛选器的作用域中的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bd631-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="bd631-221">有关自定义操作筛选器执行顺序的详细信息，请访问此 MSDN 文章: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))。</span><span class="sxs-lookup"><span data-stu-id="bd631-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="bd631-222">任务 1： 创建新的自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="bd631-223">在此任务中，您将创建新的自定义操作筛选器可将注入到 StoreController 类中，学习如何管理筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bd631-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="bd631-224">打开**开始** 解决方案位于 **\Source\Ex02-ManagingMultipleActionFilters\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd631-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="bd631-225">否则，可能会继续使用 **最终** 解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="bd631-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="bd631-226">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="bd631-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bd631-227">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="bd631-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="bd631-228">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="bd631-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="bd631-229">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="bd631-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bd631-230">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="bd631-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bd631-231">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="bd631-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bd631-232">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="bd631-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="bd631-233">有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="bd631-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="bd631-234">添加一个新 C# 类到**筛选器**文件夹并将其命名*MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="bd631-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="bd631-235">打开**MyNewCustomActionFilter.cs**并添加对引用**System.Web.Mvc**并**MvcMusicStore.Models**命名空间：</span><span class="sxs-lookup"><span data-stu-id="bd631-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="bd631-236">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2-MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="bd631-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="bd631-237">默认类声明替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="bd631-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="bd631-238">(代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2-MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="bd631-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="bd631-239">此自定义操作筛选器是几乎比你在上一练习中创建相同的。</span><span class="sxs-lookup"><span data-stu-id="bd631-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="bd631-240">主要区别是，它有 *&quot;记录由&quot;* 更新与此新类的名称以标识针对筛选器属性已注册的日志。</span><span class="sxs-lookup"><span data-stu-id="bd631-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify wich filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="bd631-241">任务 2： 将新代码拦截器注入到 StoreController 类</span><span class="sxs-lookup"><span data-stu-id="bd631-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="bd631-242">在此任务中，会将新的自定义筛选器添加到 StoreController 类，并运行解决方案，以验证这两种筛选器协同工作。</span><span class="sxs-lookup"><span data-stu-id="bd631-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="bd631-243">打开**StoreController**类位于**MvcMusicStore\Controllers** ，并插入新的自定义筛选器**MyNewCustomActionFilter**到**StoreController**类，如下所示的以下代码。</span><span class="sxs-lookup"><span data-stu-id="bd631-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="bd631-244">现在，运行应用程序，以便了解这些两个自定义操作筛选器的工作方式。</span><span class="sxs-lookup"><span data-stu-id="bd631-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="bd631-245">若要执行此操作，按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="bd631-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="bd631-246">浏览到 **/ActionLog**若要查看日志视图初始状态。</span><span class="sxs-lookup"><span data-stu-id="bd631-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="bd631-247">![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image5.png "记录页活动之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bd631-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bd631-248">*页活动之前的日志跟踪程序状态*</span><span class="sxs-lookup"><span data-stu-id="bd631-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="bd631-249">单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bd631-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="bd631-250">检查这一次;两次跟踪您的访问： 你在为每个自定义操作筛选器的添加后**StorageController**类。</span><span class="sxs-lookup"><span data-stu-id="bd631-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="bd631-251">![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image6.png "活动记录具有操作日志")</span><span class="sxs-lookup"><span data-stu-id="bd631-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bd631-252">*使用活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bd631-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="bd631-253">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="bd631-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="bd631-254">任务 3： 管理筛选器排序</span><span class="sxs-lookup"><span data-stu-id="bd631-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="bd631-255">在本任务中，您将学习如何使用顺序属性设置管理筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bd631-255">In this task, you will learn how to manage the filters' execution order by using the Order propery.</span></span>

1. <span data-ttu-id="bd631-256">打开**StoreController**类位于**MvcMusicStore\Controllers**并指定**顺序**喜欢这两个筛选器中的属性如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd631-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="bd631-257">现在，验证根据其顺序属性的值执行筛选器的方式。</span><span class="sxs-lookup"><span data-stu-id="bd631-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="bd631-258">您会发现具有最小的顺序值的筛选器 (**CustomActionFilter**) 是执行的第一个。</span><span class="sxs-lookup"><span data-stu-id="bd631-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="bd631-259">按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="bd631-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="bd631-260">浏览到 **/ActionLog**若要查看日志视图初始状态。</span><span class="sxs-lookup"><span data-stu-id="bd631-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="bd631-261">![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image7.png "记录页活动之前的跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bd631-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bd631-262">*页活动之前的日志跟踪程序状态*</span><span class="sxs-lookup"><span data-stu-id="bd631-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="bd631-263">单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bd631-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="bd631-264">检查这一次，您的访问未跟踪的筛选器的顺序值按排序： **CustomActionFilter**日志的第一个。</span><span class="sxs-lookup"><span data-stu-id="bd631-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="bd631-265">![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image8.png "活动记录具有操作日志")</span><span class="sxs-lookup"><span data-stu-id="bd631-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bd631-266">*使用活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bd631-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="bd631-267">现在，将更新的筛选器的顺序值，并验证日志记录顺序如何变化。</span><span class="sxs-lookup"><span data-stu-id="bd631-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="bd631-268">在中**StoreController**类中，更新类似的筛选器的顺序值如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd631-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="bd631-269">再次运行该应用程序，通过按**F5**。</span><span class="sxs-lookup"><span data-stu-id="bd631-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="bd631-270">单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bd631-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="bd631-271">检查这一次，日志是否创建由**MyNewCustomActionFilter**筛选器显示在最前面。</span><span class="sxs-lookup"><span data-stu-id="bd631-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="bd631-272">![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image9.png "活动记录具有操作日志")</span><span class="sxs-lookup"><span data-stu-id="bd631-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bd631-273">*使用活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bd631-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="bd631-274">任务 4： 注册全局筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="bd631-275">在此任务中，将更新解决方案，以注册新的筛选器 (**MyNewCustomActionFilter**) 作为全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="bd631-276">通过执行此操作，将会触发的所有操作执行应用程序中，而不仅限 StoreController 的如在上一任务中所示。</span><span class="sxs-lookup"><span data-stu-id="bd631-276">By doing this, it will be triggered by all the actions perfomed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="bd631-277">在中**StoreController**类中，删除 **[MyNewCustomActionFilter]** 属性和 order 属性从 **[CustomActionFilter]**。</span><span class="sxs-lookup"><span data-stu-id="bd631-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="bd631-278">其外观应如下所示：</span><span class="sxs-lookup"><span data-stu-id="bd631-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="bd631-279">打开**Global.asax**文件，找到**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="bd631-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="bd631-280">请注意，每次应用程序启动时它正在注册全局筛选器，通过调用**RegisterGlobalFilters**方法内的**FilterConfig**类。</span><span class="sxs-lookup"><span data-stu-id="bd631-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="bd631-281">![在 Global.asax 中注册全局筛选器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 Global.asax 中注册全局筛选器")</span><span class="sxs-lookup"><span data-stu-id="bd631-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="bd631-282">*在 Global.asax 中注册全局筛选器*</span><span class="sxs-lookup"><span data-stu-id="bd631-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="bd631-283">打开**FilterConfig.cs**文件内**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd631-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="bd631-284">添加对使用 System.Web.Mvc; 的引用使用 MvcMusicStore.Filters;命名空间。</span><span class="sxs-lookup"><span data-stu-id="bd631-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="bd631-285">更新**RegisterGlobalFilters**方法添加自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="bd631-286">若要执行此操作，添加突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="bd631-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="bd631-287">运行应用程序通过按**F5**。</span><span class="sxs-lookup"><span data-stu-id="bd631-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="bd631-288">单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bd631-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="bd631-289">检查现在 **[MyNewCustomActionFilter]** 太 HomeController 和 ActionLogController 中注入。</span><span class="sxs-lookup"><span data-stu-id="bd631-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="bd631-290">![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image11.png "活动记录具有操作日志")</span><span class="sxs-lookup"><span data-stu-id="bd631-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bd631-291">*使用全局活动记录的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bd631-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="bd631-292">此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="bd631-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="bd631-293">总结</span><span class="sxs-lookup"><span data-stu-id="bd631-293">Summary</span></span>

<span data-ttu-id="bd631-294">通过完成本动手实验介绍了如何扩展操作筛选器来执行自定义操作。</span><span class="sxs-lookup"><span data-stu-id="bd631-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="bd631-295">您还学习了如何将注入到页面控制器的任何筛选器。</span><span class="sxs-lookup"><span data-stu-id="bd631-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="bd631-296">使用以下概念：</span><span class="sxs-lookup"><span data-stu-id="bd631-296">The following concepts were used:</span></span>

- <span data-ttu-id="bd631-297">如何使用 ASP.NET MVC ActionFilterAttribute 类创建自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="bd631-298">如何将筛选器注入到 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="bd631-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="bd631-299">如何管理使用 Order 属性筛选器排序</span><span class="sxs-lookup"><span data-stu-id="bd631-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="bd631-300">如何注册全局筛选器</span><span class="sxs-lookup"><span data-stu-id="bd631-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="bd631-301">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="bd631-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="bd631-302">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="bd631-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="bd631-303">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="bd631-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="bd631-304">转到[ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="bd631-304">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="bd631-305">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="bd631-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="bd631-306">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="bd631-306">Click on **Install Now**.</span></span> <span data-ttu-id="bd631-307">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="bd631-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="bd631-308">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="bd631-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="bd631-309">![安装 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="bd631-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="bd631-310">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="bd631-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="bd631-311">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="bd631-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="bd631-313">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="bd631-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="bd631-314">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="bd631-314">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="bd631-316">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="bd631-316">*Installation progress*</span></span>
6. <span data-ttu-id="bd631-317">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="bd631-317">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="bd631-319">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="bd631-319">*Installation completed*</span></span>
7. <span data-ttu-id="bd631-320">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="bd631-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="bd631-321">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="bd631-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="bd631-323">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="bd631-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bd631-324">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="bd631-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="bd631-325">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="bd631-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="bd631-326">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="bd631-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="bd631-327">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="bd631-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd631-328">使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="bd631-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="bd631-329">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="bd631-329">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="bd631-330">![登录到 Windows Azure 门户](aspnet-mvc-4-custom-action-filters/_static/image17.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="bd631-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="bd631-331">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="bd631-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="bd631-332">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="bd631-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="bd631-333">![创建新的 Web 站点](aspnet-mvc-4-custom-action-filters/_static/image18.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="bd631-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="bd631-334">*创建新的 Web 站点*</span><span class="sxs-lookup"><span data-stu-id="bd631-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="bd631-335">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="bd631-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="bd631-336">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="bd631-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="bd631-337">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="bd631-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd631-338">Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。</span><span class="sxs-lookup"><span data-stu-id="bd631-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="bd631-339">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。</span><span class="sxs-lookup"><span data-stu-id="bd631-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="bd631-340">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="bd631-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="bd631-341">![创建新的网站使用快速创建](aspnet-mvc-4-custom-action-filters/_static/image19.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="bd631-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="bd631-342">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="bd631-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="bd631-343">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="bd631-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="bd631-344">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="bd631-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="bd631-345">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="bd631-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="bd631-346">![浏览到新的 web 站点](aspnet-mvc-4-custom-action-filters/_static/image20.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="bd631-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="bd631-347">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="bd631-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="bd631-348">![正在运行的网站](aspnet-mvc-4-custom-action-filters/_static/image21.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="bd631-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="bd631-349">*正在运行的网站*</span><span class="sxs-lookup"><span data-stu-id="bd631-349">*Web site running*</span></span>
6. <span data-ttu-id="bd631-350">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="bd631-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="bd631-351">![打开网站管理页](aspnet-mvc-4-custom-action-filters/_static/image22.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="bd631-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="bd631-352">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="bd631-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="bd631-353">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="bd631-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd631-354">*发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="bd631-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="bd631-355">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="bd631-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="bd631-356">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bd631-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="bd631-357">![正在下载网站发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image23.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bd631-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="bd631-358">*正在下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bd631-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="bd631-359">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="bd631-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="bd631-360">进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。</span><span class="sxs-lookup"><span data-stu-id="bd631-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="bd631-361">![保存发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image24.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bd631-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="bd631-362">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bd631-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="bd631-363">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="bd631-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="bd631-364">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bd631-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="bd631-365">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="bd631-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="bd631-366">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bd631-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="bd631-367">可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="bd631-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="bd631-368">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="bd631-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="bd631-369">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="bd631-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="bd631-370">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="bd631-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="bd631-371">![SQL 数据库服务器仪表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="bd631-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="bd631-372">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="bd631-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="bd631-373">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="bd631-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="bd631-374">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="bd631-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="bd631-376">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="bd631-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="bd631-377">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="bd631-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="bd631-379">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="bd631-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bd631-380">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="bd631-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="bd631-381">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="bd631-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="bd631-382">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="bd631-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="bd631-383">![发布应用程序](aspnet-mvc-4-custom-action-filters/_static/image29.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="bd631-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="bd631-384">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="bd631-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="bd631-385">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="bd631-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="bd631-386">![导入发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image30.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bd631-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="bd631-387">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bd631-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="bd631-388">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="bd631-388">Click **Validate Connection**.</span></span> <span data-ttu-id="bd631-389">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bd631-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd631-390">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="bd631-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="bd631-391">![验证连接](aspnet-mvc-4-custom-action-filters/_static/image31.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="bd631-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="bd631-392">*验证连接*</span><span class="sxs-lookup"><span data-stu-id="bd631-392">*Validating connection*</span></span>
4. <span data-ttu-id="bd631-393">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="bd631-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="bd631-394">![Web 部署配置](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="bd631-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="bd631-395">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="bd631-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="bd631-396">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bd631-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="bd631-397">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="bd631-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="bd631-398">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="bd631-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="bd631-399">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="bd631-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="bd631-400">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="bd631-400">Type a new database name.</span></span>

     <span data-ttu-id="bd631-401">![配置目标连接字符串](aspnet-mvc-4-custom-action-filters/_static/image33.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bd631-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="bd631-402">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="bd631-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="bd631-403">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="bd631-403">Then click **OK**.</span></span> <span data-ttu-id="bd631-404">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="bd631-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="bd631-405">![创建数据库](aspnet-mvc-4-custom-action-filters/_static/image34.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="bd631-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="bd631-406">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="bd631-406">*Creating the database*</span></span>
7. <span data-ttu-id="bd631-407">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="bd631-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="bd631-408">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="bd631-408">Then click **Next**.</span></span>

    <span data-ttu-id="bd631-409">![连接字符串指向 SQL 数据库](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bd631-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="bd631-410">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="bd631-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="bd631-411">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="bd631-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="bd631-412">![Web 应用程序发布](aspnet-mvc-4-custom-action-filters/_static/image36.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="bd631-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="bd631-413">*Web 应用程序发布*</span><span class="sxs-lookup"><span data-stu-id="bd631-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="bd631-414">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="bd631-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="bd631-415">附录 c： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="bd631-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="bd631-416">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="bd631-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="bd631-417">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="bd631-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="bd631-418">![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="bd631-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="bd631-419">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="bd631-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="bd631-420">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="bd631-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="bd631-421">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="bd631-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="bd631-422">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="bd631-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="bd631-423">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="bd631-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="bd631-424">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="bd631-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="bd631-425">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="bd631-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="bd631-426">![开始键入代码段名称](aspnet-mvc-4-custom-action-filters/_static/image38.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="bd631-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="bd631-427">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="bd631-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="bd631-428">![按 tab 键以选择突出显示代码段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="bd631-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="bd631-429">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="bd631-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="bd631-430">![再次按 Tab 和代码段将 expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="bd631-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="bd631-431">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="bd631-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="bd631-432">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="bd631-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="bd631-433">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="bd631-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="bd631-434">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="bd631-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="bd631-435">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="bd631-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="bd631-436">![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-custom-action-filters/_static/image41.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="bd631-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="bd631-437">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="bd631-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="bd631-438">![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-custom-action-filters/_static/image42.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="bd631-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="bd631-439">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="bd631-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
