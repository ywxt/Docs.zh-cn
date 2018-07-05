---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 帮助程序、 窗体和验证 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和数据访问的动手实验中，你已加载并显示数据库中的数据。 在本动手实验中，您将添加到...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: f2eb624e72d6f52d1694b5753ee2b1f8117c2851
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376732"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="89e0f-104">ASP.NET MVC 4 帮助程序、 窗体和验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="89e0f-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="89e0f-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="89e0f-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="89e0f-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="89e0f-107">在中**ASP.NET MVC 4 模型和数据访问**动手实验中，您已被加载和显示数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="89e0f-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="89e0f-108">在本动手实验中，您将添加到**音乐应用商店**应用程序编辑该数据的能力。</span><span class="sxs-lookup"><span data-stu-id="89e0f-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="89e0f-109">记住这一目标，将首先创建将支持唱片集的创建、 读取、 更新和删除 (CRUD) 操作的控制器。</span><span class="sxs-lookup"><span data-stu-id="89e0f-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="89e0f-110">将生成利用 ASP.NET MVC 基架功能，以显示 HTML 表中的唱片集的属性的索引视图模板。</span><span class="sxs-lookup"><span data-stu-id="89e0f-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="89e0f-111">若要增强该视图，您将添加的自定义 HTML 帮助程序将截断长说明。</span><span class="sxs-lookup"><span data-stu-id="89e0f-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="89e0f-112">然后，您将添加编辑和创建视图，你会更改在数据库中，从下拉列表等窗体元素的帮助唱片集。</span><span class="sxs-lookup"><span data-stu-id="89e0f-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="89e0f-113">最后，您就可以让用户删除唱片集，并还会从输入错误的数据通过验证其输入阻止它们。</span><span class="sxs-lookup"><span data-stu-id="89e0f-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="89e0f-114">此动手实验假定你已了解的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="89e0f-115">如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="89e0f-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="89e0f-116">此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。</span><span class="sxs-lookup"><span data-stu-id="89e0f-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="89e0f-117">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="89e0f-118">特定于此实验室项目位于[ASP.NET MVC 4 帮助器、 窗体和验证](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="89e0f-119">目标</span><span class="sxs-lookup"><span data-stu-id="89e0f-119">Objectives</span></span>

<span data-ttu-id="89e0f-120">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="89e0f-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="89e0f-121">创建控制器支持 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="89e0f-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="89e0f-122">生成的索引视图以显示 HTML 表中的实体属性</span><span class="sxs-lookup"><span data-stu-id="89e0f-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="89e0f-123">添加自定义 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="89e0f-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="89e0f-124">创建和自定义编辑视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="89e0f-125">区分响应 HTTP GET 或 HTTP POST 调用的操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="89e0f-126">添加和自定义创建视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-126">Add and customize a Create View</span></span>
- <span data-ttu-id="89e0f-127">处理实体的删除</span><span class="sxs-lookup"><span data-stu-id="89e0f-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="89e0f-128">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="89e0f-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="89e0f-129">系统必备</span><span class="sxs-lookup"><span data-stu-id="89e0f-129">Prerequisites</span></span>

<span data-ttu-id="89e0f-130">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="89e0f-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="89e0f-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="89e0f-132">安装</span><span class="sxs-lookup"><span data-stu-id="89e0f-132">Setup</span></span>

<span data-ttu-id="89e0f-133">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="89e0f-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="89e0f-134">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="89e0f-135">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="89e0f-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="89e0f-136">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 b： 使用代码片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="89e0f-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="89e0f-137">练习</span><span class="sxs-lookup"><span data-stu-id="89e0f-137">Exercises</span></span>

<span data-ttu-id="89e0f-138">以下练习构成本动手实验：</span><span class="sxs-lookup"><span data-stu-id="89e0f-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="89e0f-139">创建存储管理器控制器和其索引视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="89e0f-140">添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="89e0f-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="89e0f-141">创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="89e0f-142">添加创建视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="89e0f-143">处理删除</span><span class="sxs-lookup"><span data-stu-id="89e0f-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="89e0f-144">添加验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="89e0f-145">在客户端使用非介入式 jQuery</span><span class="sxs-lookup"><span data-stu-id="89e0f-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="89e0f-146">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="89e0f-147">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="89e0f-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="89e0f-148">估计的时间才能完成此实验： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="89e0f-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="89e0f-149">练习 1： 创建存储管理器控制器和其索引视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="89e0f-150">在此练习中，您将学习如何创建新的控制器，以支持 CRUD 操作，自定义其 Index 操作方法，以从数据库和最后生成利用 ASP.NET MVC 基架的索引视图模板返回的唱片集列表若要显示 HTML 表中的唱片集的属性的功能。</span><span class="sxs-lookup"><span data-stu-id="89e0f-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="89e0f-151">任务 1-创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="89e0f-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="89e0f-152">在本任务中，您将创建名为的新控制器**StoreManagerController**以支持 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="89e0f-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="89e0f-153">打开**开始**解决方案位于**源/Ex1-CreatingTheStoreManagerController/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="89e0f-154">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-155">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-156">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-157">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-158">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-159">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-160">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-161">添加新的控制器。</span><span class="sxs-lookup"><span data-stu-id="89e0f-161">Add a new controller.</span></span> <span data-ttu-id="89e0f-162">若要执行此操作，右键单击**控制器**在解决方案资源管理器，选择文件夹**添加**，然后**控制器**命令。</span><span class="sxs-lookup"><span data-stu-id="89e0f-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="89e0f-163">更改**控制器****名称**到**StoreManagerController** ，并确保选择**包含空读/写操作的MVC控制器**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="89e0f-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="89e0f-164">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-164">Click **Add**.</span></span>

    <span data-ttu-id="89e0f-165">![添加控制器对话框](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "添加控制器对话框")</span><span class="sxs-lookup"><span data-stu-id="89e0f-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="89e0f-166">*添加控制器对话框*</span><span class="sxs-lookup"><span data-stu-id="89e0f-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="89e0f-167">生成新的控制器类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-167">A new Controller class is generated.</span></span> <span data-ttu-id="89e0f-168">指示若要添加操作的读/写，存根 （stub） 方法，因为使用 TODO 注释填充，并提示您包括应用程序特定逻辑创建常见 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="89e0f-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="89e0f-169">任务 2-自定义 StoreManager 索引</span><span class="sxs-lookup"><span data-stu-id="89e0f-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="89e0f-170">在此任务中，将自定义 StoreManager Index 操作方法，以从数据库中返回的唱片集的列表视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="89e0f-171">在 StoreManagerController 类中，添加以下*使用*指令。</span><span class="sxs-lookup"><span data-stu-id="89e0f-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="89e0f-172">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 使用 MvcMusicStore*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="89e0f-173">将字段添加到**StoreManagerController**以保存的实例**MusicStoreEntities。**</span><span class="sxs-lookup"><span data-stu-id="89e0f-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="89e0f-174">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="89e0f-175">实现 StoreManagerController 索引操作可以返回的唱片集的列表视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="89e0f-176">控制器操作逻辑将非常类似于前面编写的 StoreController 的索引操作。</span><span class="sxs-lookup"><span data-stu-id="89e0f-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="89e0f-177">使用 LINQ 检索所有唱片集，包括流派和艺术家信息显示。</span><span class="sxs-lookup"><span data-stu-id="89e0f-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="89e0f-178">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 StoreManagerController 索引*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="89e0f-179">任务 3-创建索引视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="89e0f-180">在本任务中，您将创建索引视图模板要显示的唱片集返回的列表**StoreManager**控制器。</span><span class="sxs-lookup"><span data-stu-id="89e0f-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="89e0f-181">在创建新的视图模板之前, 应先生成项目，以便**添加视图对话框**知道**唱片集**类使用。</span><span class="sxs-lookup"><span data-stu-id="89e0f-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="89e0f-182">选择**生成 |生成 MvcMusicStore**以生成项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="89e0f-183">内右击**索引**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="89e0f-184">此时会弹出**添加视图**对话框。</span><span class="sxs-lookup"><span data-stu-id="89e0f-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="89e0f-185">![添加视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "添加视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="89e0f-186">*添加从索引方法中的视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="89e0f-187">在添加视图对话框中，验证是否视图名称是**索引**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="89e0f-188">选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="89e0f-189">选择**列表**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="89e0f-190">将保留**视图引擎**到**Razor**和其他字段具有其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="89e0f-191">![添加索引视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "添加索引视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="89e0f-192">*添加索引视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="89e0f-193">任务 4-自定义索引视图的基架</span><span class="sxs-lookup"><span data-stu-id="89e0f-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="89e0f-194">在此任务中，将调整与 ASP.NET MVC 基架功能，使其显示所需的字段创建的简单视图模板。</span><span class="sxs-lookup"><span data-stu-id="89e0f-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="89e0f-195">**基架**支持在 ASP.NET MVC 中的生成一个简单的视图模板，其中列出了唱片集模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="89e0f-196">**基架**，可以快速开始对强类型化视图： 而不是无需手动编写视图模板，快速基架生成的默认模板，然后，可以修改生成的代码。</span><span class="sxs-lookup"><span data-stu-id="89e0f-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>


1. <span data-ttu-id="89e0f-197">查看创建的代码。</span><span class="sxs-lookup"><span data-stu-id="89e0f-197">Review the code created.</span></span> <span data-ttu-id="89e0f-198">生成的字段列表将属于以下 HTML 表**基架**使用用于显示表格数据。</span><span class="sxs-lookup"><span data-stu-id="89e0f-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="89e0f-199">替换**&lt;表&gt;** 以下代码，以仅显示代码**流派**，**艺术家**，**唱片集标题**，并**价格**字段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="89e0f-200">这会删除**AlbumId**并**唱片集画面 URL**列。</span><span class="sxs-lookup"><span data-stu-id="89e0f-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="89e0f-201">此外，它更改 GenreId 和 ArtistId 要显示的及其链接的类属性的列**Artist.Name**并**Genre.Name**，并删除**详细信息**链接。</span><span class="sxs-lookup"><span data-stu-id="89e0f-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="89e0f-202">更改以下说明。</span><span class="sxs-lookup"><span data-stu-id="89e0f-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="89e0f-203">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="89e0f-204">在此任务中，将测试**StoreManager** **索引**视图模板显示根据前面的步骤的设计的唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="89e0f-205">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-206">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-206">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-207">将 URL 更改为 **/StoreManager**若要验证是否显示唱片集的列表，显示其**标题**，**艺术家**并**流派**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="89e0f-208">![浏览唱片集的列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "浏览唱片集的列表")</span><span class="sxs-lookup"><span data-stu-id="89e0f-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="89e0f-209">*浏览唱片集的列表*</span><span class="sxs-lookup"><span data-stu-id="89e0f-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="89e0f-210">练习 2： 添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="89e0f-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="89e0f-211">StoreManager 索引页都有一个潜在的问题： 标题和艺术家姓名属性可以同时为足够长，以引发关闭表格的格式。</span><span class="sxs-lookup"><span data-stu-id="89e0f-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="89e0f-212">在此练习中将了解如何添加自定义的 HTML 帮助器来截断该文本。</span><span class="sxs-lookup"><span data-stu-id="89e0f-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="89e0f-213">在下图中，可以看到如何格式时所使用的小型浏览器大小修改由于文本的长度。</span><span class="sxs-lookup"><span data-stu-id="89e0f-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="89e0f-214">![浏览与唱片集的列表不截断的文本](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "浏览与唱片集的列表不截断的文本")</span><span class="sxs-lookup"><span data-stu-id="89e0f-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="89e0f-215">*浏览与唱片集的列表不截断的文本*</span><span class="sxs-lookup"><span data-stu-id="89e0f-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="89e0f-216">任务 1-扩展的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="89e0f-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="89e0f-217">在本任务中，您将添加一个新方法**Truncate**到**HTML** ASP.NET MVC 视图中公开的对象。</span><span class="sxs-lookup"><span data-stu-id="89e0f-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="89e0f-218">若要执行此操作，将实现**扩展方法**到内置**System.Web.Mvc.HtmlHelper**类提供的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="89e0f-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="89e0f-219">若要详细了解**扩展方法**，请访问此 msdn 文章。</span><span class="sxs-lookup"><span data-stu-id="89e0f-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="89e0f-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>


1. <span data-ttu-id="89e0f-221">打开**开始**解决方案位于**源/Ex2-AddingAnHTMLHelper/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="89e0f-222">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-223">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-224">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-225">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-226">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-227">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-228">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-229">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-230">打开 StoreManager 的索引视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="89e0f-231">若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，然后**StoreManager** ，然后打开**Index.cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="89e0f-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="89e0f-232">添加以下代码<strong>@model</strong>指令来定义<strong>Truncate</strong>帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="89e0f-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="89e0f-233">任务 2-在页中截断的文本</span><span class="sxs-lookup"><span data-stu-id="89e0f-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="89e0f-234">在本任务中，您将使用**Truncate**方法来截断视图模板中的文本。</span><span class="sxs-lookup"><span data-stu-id="89e0f-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="89e0f-235">打开 StoreManager 的索引视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="89e0f-236">若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，然后**StoreManager** ，然后打开**Index.cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="89e0f-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="89e0f-237">替换显示的线条**艺术家姓名**和唱片集的**标题**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="89e0f-238">若要执行此操作，将以下行。</span><span class="sxs-lookup"><span data-stu-id="89e0f-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="89e0f-239">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="89e0f-240">在此任务中，将测试**StoreManager** **索引**视图模板将截断的唱片集标题和艺术家姓名。</span><span class="sxs-lookup"><span data-stu-id="89e0f-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="89e0f-241">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-242">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-242">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-243">将 URL 更改为 **/StoreManager**以验证该长时间中的文本**标题**并**艺术家**列将被截断。</span><span class="sxs-lookup"><span data-stu-id="89e0f-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="89e0f-244">![截断的标题和艺术家姓名](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截断标题和艺术家名称")</span><span class="sxs-lookup"><span data-stu-id="89e0f-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="89e0f-245">*截断的标题和艺术家姓名*</span><span class="sxs-lookup"><span data-stu-id="89e0f-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="89e0f-246">练习 3： 创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="89e0f-247">在此练习中，您将学习如何创建一个窗体以允许存储管理器编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="89e0f-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="89e0f-248">在将浏览 **/StoreManager/Edit/id** URL (**id**正在编辑的唱片集的唯一 id)，从而使对服务器的 HTTP GET 调用。</span><span class="sxs-lookup"><span data-stu-id="89e0f-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="89e0f-249">控制器编辑操作方法将从数据库中检索相应的唱片集，创建**StoreManagerViewModel**对象封装 （以及的艺术家和流派列表），然后将其传递给为视图模板向用户呈现的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="89e0f-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="89e0f-250">此页将包含**&lt;窗体&gt;** 使用文本框和下拉列表以进行编辑的唱片集属性的元素。</span><span class="sxs-lookup"><span data-stu-id="89e0f-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="89e0f-251">一旦用户更新唱片集的表单值并单击**保存**按钮，将更改提交通过 HTTP POST 回叫 **/StoreManager/Edit/id**。尽管 URL 将保留与最后一次调用中的相同，但 ASP.NET MVC 标识，这次它是 HTTP POST，因此执行不同的编辑操作方法 (一个使用修饰 **[HttpPost]**)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="89e0f-252">任务 1-实现 HTTP GET 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="89e0f-253">在此任务中，您将实现要检索从数据库中的相应唱片集的编辑操作方法的 HTTP GET 版本以及所有流派和艺术家的列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="89e0f-254">它将此数据打包成**StoreManagerViewModel**的最后一步，然后将传递到用于呈现具有响应的视图模板中定义的对象。</span><span class="sxs-lookup"><span data-stu-id="89e0f-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="89e0f-255">打开**开始**解决方案位于**源/Ex3-CreatingTheEditView/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="89e0f-256">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-257">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-258">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-259">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-260">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-261">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-262">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-263">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-264">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="89e0f-265">若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="89e0f-266">替换**HTTP GET 编辑**使用以下代码来检索相应的操作方法**唱片集**并将**流派**和**艺术家**列出了。</span><span class="sxs-lookup"><span data-stu-id="89e0f-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="89e0f-267">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex3 StoreManagerController HTTP GET 编辑操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-268">正在使用**System.Web.Mvc** **SelectList**艺术家和而不是流派**System.Collections.Generic**列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="89e0f-269">**SelectList**是更简洁的方式来填充 HTML 下拉列表和管理当前所选内容等内容。</span><span class="sxs-lookup"><span data-stu-id="89e0f-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="89e0f-270">实例化和更高版本设置中的控制器操作这些 ViewModel 对象将使编辑窗体方案更简洁。</span><span class="sxs-lookup"><span data-stu-id="89e0f-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="89e0f-271">任务 2-创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="89e0f-272">在本任务中，将创建更高版本将显示的唱片集属性的编辑视图模板。</span><span class="sxs-lookup"><span data-stu-id="89e0f-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="89e0f-273">创建编辑视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-273">Create the Edit View.</span></span> <span data-ttu-id="89e0f-274">若要执行此操作，右键单击内**编辑**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="89e0f-275">在添加视图对话框中，验证是否视图名称是**编辑**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="89e0f-276">检查**创建强类型化视图**复选框，然后选择**唱片集 (MvcMusicStore.Models)** 从**查看数据类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="89e0f-277">选择**编辑**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="89e0f-278">其他字段保留为其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="89e0f-279">![添加编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "添加 Edit 视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="89e0f-280">*添加 Edit 视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="89e0f-281">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="89e0f-282">在此任务中，将测试**StoreManager** **编辑**视图页会显示作为参数传递的唱片集的属性的值。</span><span class="sxs-lookup"><span data-stu-id="89e0f-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="89e0f-283">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-284">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-284">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-285">将 URL 更改为 **/StoreManager/Edit/1**以验证是否显示了传递的唱片集的属性的值。</span><span class="sxs-lookup"><span data-stu-id="89e0f-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="89e0f-286">![浏览唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "浏览唱片集的编辑视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="89e0f-287">*浏览唱片集的编辑视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="89e0f-288">任务 4-实现唱片集编辑器模板上的下拉列表</span><span class="sxs-lookup"><span data-stu-id="89e0f-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="89e0f-289">在此任务中，你将在最后一个任务中，创建视图模板添加下拉列表，以便用户可以选择从一系列艺术家和流派。</span><span class="sxs-lookup"><span data-stu-id="89e0f-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="89e0f-290">将替换所有**唱片集**fieldset 以下代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-291">**Html.DropDownList**已添加帮助器来呈现下拉列表选择艺术家和流派。</span><span class="sxs-lookup"><span data-stu-id="89e0f-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="89e0f-292">参数传递给**Html.DropDownList**是：</span><span class="sxs-lookup"><span data-stu-id="89e0f-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="89e0f-293">窗体字段的名称 (**&quot;ArtistId&quot;**)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="89e0f-294">**SelectList**的值的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="89e0f-295">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="89e0f-296">在此任务中，将测试**StoreManager** **编辑**视图页显示而不是艺术家和类型 ID 文本字段的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="89e0f-297">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-298">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-298">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-299">将 URL 更改为 **/StoreManager/Edit/1**以验证它显示而不是艺术家和类型 ID 文本字段的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="89e0f-300">![浏览具有下拉列表确定的唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "浏览唱片集的相应下拉列表编辑视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="89e0f-301">*浏览唱片集的编辑视图，这次使用下拉列表*</span><span class="sxs-lookup"><span data-stu-id="89e0f-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="89e0f-302">任务 6-实现 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="89e0f-303">现在，编辑视图显示按预期方式，您需要实现 HTTP POST 编辑操作方法以保存到相册所做的更改。</span><span class="sxs-lookup"><span data-stu-id="89e0f-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="89e0f-304">关闭浏览器，如果需要以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="89e0f-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="89e0f-305">打开**StoreManagerController**从**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="89e0f-306">替换**HTTP POST 编辑**操作方法与以下的代码 （请注意，必须将其替换的方法是接收两个参数的重载的版本）：</span><span class="sxs-lookup"><span data-stu-id="89e0f-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="89e0f-307">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex3 StoreManagerController HTTP POST 编辑操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-308">将执行此方法，当用户单击**保存**视图的按钮，并执行 HTTP POST 回发到服务器的表单值将其保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="89e0f-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="89e0f-309">修饰器 **[HttpPost]** 指示应这些 HTTP POST 方案使用的方法。</span><span class="sxs-lookup"><span data-stu-id="89e0f-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="89e0f-310">该方法采用**唱片集**对象。</span><span class="sxs-lookup"><span data-stu-id="89e0f-310">The method takes an **Album** object.</span></span> <span data-ttu-id="89e0f-311">ASP.NET MVC 将自动创建的唱片集对象从已发布&lt;窗体&gt;值。</span><span class="sxs-lookup"><span data-stu-id="89e0f-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="89e0f-312">该方法将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="89e0f-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="89e0f-313">如果模型是有效的：</span><span class="sxs-lookup"><span data-stu-id="89e0f-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="89e0f-314">更新要将其标记为已修改对象的上下文中的唱片集条目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="89e0f-315">保存所做的更改和重定向到索引视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="89e0f-316">如果模型不是有效的它将会填充使用 ViewBag **GenreId**并**ArtistId**，则会返回接收到的唱片集对象，以允许用户与视图执行任何所需的更新。</span><span class="sxs-lookup"><span data-stu-id="89e0f-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="89e0f-317">任务 7-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="89e0f-318">在此任务中，将测试**StoreManager 编辑**视图页实际上将更新后的唱片集数据保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="89e0f-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="89e0f-319">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-320">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-320">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-321">将 URL 更改为 **/StoreManager/Edit/1**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="89e0f-322">将唱片集标题改为**负载**，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="89e0f-323">验证在列表中的唱片集实际更改唱片集的标题。</span><span class="sxs-lookup"><span data-stu-id="89e0f-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="89e0f-324">![正在更新相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新唱片集")</span><span class="sxs-lookup"><span data-stu-id="89e0f-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="89e0f-325">*正在更新唱片集*</span><span class="sxs-lookup"><span data-stu-id="89e0f-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="89e0f-326">练习 4： 添加创建视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="89e0f-327">既然**StoreManagerController**支持**编辑**功能，在此练习中将了解如何添加创建视图模板，以便存储管理器将新的唱片集添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="89e0f-328">编辑功能与您处理，将实现使用中的两个不同方法的创建方案**StoreManagerController**类：</span><span class="sxs-lookup"><span data-stu-id="89e0f-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="89e0f-329">存储管理器第一次访问时，一种操作方法将显示一个空窗体 **/StoreManager/创建**URL。</span><span class="sxs-lookup"><span data-stu-id="89e0f-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="89e0f-330">第二个操作方法将处理方案当单击 store manager**保存**中的窗体按钮，然后提交值回 **/StoreManager/创建**作为 HTTP POST 的 URL。</span><span class="sxs-lookup"><span data-stu-id="89e0f-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="89e0f-331">任务 1-实现创建 HTTP GET 操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="89e0f-332">在此任务中，您将实现的 Create 操作方法来检索所有流派和艺术家的列表，此数据打包到 HTTP GET 版本**StoreManagerViewModel**对象，然后将传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="89e0f-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="89e0f-333">打开**开始**解决方案位于**源/Ex4-AddingACreateView/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="89e0f-334">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-335">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-336">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-337">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-338">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-339">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-340">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-341">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-342">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="89e0f-343">若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="89e0f-344">替换**创建**以下操作方法代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="89e0f-345">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex4 StoreManagerController HTTP GET 创建操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="89e0f-346">任务 2-添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="89e0f-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="89e0f-347">在本任务中，您将添加将显示一个新的 （空） 唱片集窗体创建视图模板。</span><span class="sxs-lookup"><span data-stu-id="89e0f-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="89e0f-348">内右击**创建**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="89e0f-349">这将显示添加视图对话框。</span><span class="sxs-lookup"><span data-stu-id="89e0f-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="89e0f-350">在添加视图对话框中，验证是否视图名称是**创建**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="89e0f-351">选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表和**创建**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="89e0f-352">其他字段保留为其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="89e0f-353">![添加 create 视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "添加-a-创建-view.png")</span><span class="sxs-lookup"><span data-stu-id="89e0f-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="89e0f-354">*添加 Create 视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="89e0f-355">更新**GenreId**并**ArtistId**字段使用下拉列表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="89e0f-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="89e0f-356">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="89e0f-357">在此任务中，将测试**StoreManager** **创建**视图页将显示一个空的唱片集窗体。</span><span class="sxs-lookup"><span data-stu-id="89e0f-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="89e0f-358">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-359">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-359">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-360">将 URL 更改为**StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="89e0f-361">验证用于填充新的唱片集属性显示一个空窗体。</span><span class="sxs-lookup"><span data-stu-id="89e0f-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="89e0f-362">![使用一个空窗体创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "创建一个空窗体视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="89e0f-363">*使用一个空窗体创建视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="89e0f-364">任务 4-实现 HTTP POST 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="89e0f-365">在此任务中，您将实现将在用户单击时调用的创建操作方法的 HTTP POST 版本**保存**按钮。</span><span class="sxs-lookup"><span data-stu-id="89e0f-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="89e0f-366">该方法应在数据库中保存新唱片集。</span><span class="sxs-lookup"><span data-stu-id="89e0f-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="89e0f-367">关闭浏览器，如果需要以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="89e0f-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="89e0f-368">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="89e0f-369">若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="89e0f-370">替换**HTTP POST 创建**以下操作方法代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="89e0f-371">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex4 StoreManagerController HTTP-POST 创建操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-372">创建操作非常类似于上一个编辑操作方法，但而不是将对象设置为已修改，它将被添加到上下文。</span><span class="sxs-lookup"><span data-stu-id="89e0f-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="89e0f-373">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="89e0f-374">在此任务中，将测试**StoreManager 创建**视图页，可以创建新的唱片集，然后重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="89e0f-375">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-376">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-376">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-377">将 URL 更改为**StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="89e0f-378">所有窗体字段用数据填充新的唱片集，如图所示：</span><span class="sxs-lookup"><span data-stu-id="89e0f-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="89e0f-379">![创建相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "创建相册")</span><span class="sxs-lookup"><span data-stu-id="89e0f-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="89e0f-380">*创建相册*</span><span class="sxs-lookup"><span data-stu-id="89e0f-380">*Creating an Album*</span></span>
3. <span data-ttu-id="89e0f-381">验证会重定向到 StoreManager 索引视图，其中包括刚刚创建的新唱片集。</span><span class="sxs-lookup"><span data-stu-id="89e0f-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="89e0f-382">![创建新相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "创建新相册")</span><span class="sxs-lookup"><span data-stu-id="89e0f-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="89e0f-383">*创建新相册*</span><span class="sxs-lookup"><span data-stu-id="89e0f-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="89e0f-384">练习 5： 处理删除</span><span class="sxs-lookup"><span data-stu-id="89e0f-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="89e0f-385">若要删除唱片集的功能尚未实现。</span><span class="sxs-lookup"><span data-stu-id="89e0f-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="89e0f-386">这是本练习中将对。</span><span class="sxs-lookup"><span data-stu-id="89e0f-386">This is what this exercise will be about.</span></span> <span data-ttu-id="89e0f-387">像之前那样将实现使用两个不同方法中的删除方案**StoreManagerController**类：</span><span class="sxs-lookup"><span data-stu-id="89e0f-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="89e0f-388">一种操作方法将显示确认窗体</span><span class="sxs-lookup"><span data-stu-id="89e0f-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="89e0f-389">第二个操作方法将处理窗体提交</span><span class="sxs-lookup"><span data-stu-id="89e0f-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="89e0f-390">任务 1-实现 HTTP GET Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="89e0f-391">在此任务中，您将实现要检索的唱片集信息的删除操作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="89e0f-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="89e0f-392">打开**开始**解决方案位于**源/Ex5-HandlingDeletion/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="89e0f-393">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-394">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-395">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-396">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-397">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-398">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-399">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-400">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-401">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="89e0f-402">若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="89e0f-403">删除控制器操作正是与上一存储详细信息控制器操作相同： 它会查询**唱片集**对象从数据库中使用**id**提供 URL，并返回适当**视图**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="89e0f-404">若要执行此操作，将为 HTTP GET**删除**以下操作方法代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="89e0f-405">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex5 处理删除 HTTP GET Delete 操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="89e0f-406">内右击**删除**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="89e0f-407">这将显示添加视图对话框。</span><span class="sxs-lookup"><span data-stu-id="89e0f-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="89e0f-408">在添加视图对话框中，验证是否视图名称是**删除**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="89e0f-409">选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="89e0f-410">选择**删除**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="89e0f-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="89e0f-411">其他字段保留为其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="89e0f-412">![添加 Delete 视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "添加 Delete 视图")</span><span class="sxs-lookup"><span data-stu-id="89e0f-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="89e0f-413">*添加 Delete 视图*</span><span class="sxs-lookup"><span data-stu-id="89e0f-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="89e0f-414">删除模板显示模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="89e0f-415">将显示仅唱片集的标题。</span><span class="sxs-lookup"><span data-stu-id="89e0f-415">You will show only the album's title.</span></span> <span data-ttu-id="89e0f-416">若要执行此操作，请将视图的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="89e0f-417">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="89e0f-418">在此任务中，将测试**StoreManager** **删除**视图页显示确认删除窗体。</span><span class="sxs-lookup"><span data-stu-id="89e0f-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="89e0f-419">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-420">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-420">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-421">将 URL 更改为 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="89e0f-422">选择要删除通过单击一个相册**删除**并验证是否已上载新视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="89e0f-423">![删除 Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "删除 Album")</span><span class="sxs-lookup"><span data-stu-id="89e0f-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="89e0f-424">*删除 Album*</span><span class="sxs-lookup"><span data-stu-id="89e0f-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="89e0f-425">任务 3-实现 HTTP POST Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="89e0f-426">在此任务中，您将实现将在用户单击时调用的 Delete 操作方法的 HTTP POST 版本**删除**按钮。</span><span class="sxs-lookup"><span data-stu-id="89e0f-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="89e0f-427">该方法应在删除数据库中的唱片集。</span><span class="sxs-lookup"><span data-stu-id="89e0f-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="89e0f-428">关闭浏览器，如果需要以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="89e0f-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="89e0f-429">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="89e0f-430">若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="89e0f-431">替换**HTTP POST Delete**以下操作方法代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="89e0f-432">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex5 处理删除 HTTP POST Delete 操作*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="89e0f-433">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="89e0f-434">在此任务中，将测试**StoreManager 删除**视图页可让您删除唱片集，然后重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="89e0f-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="89e0f-435">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-436">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-436">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-437">将 URL 更改为 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="89e0f-438">选择要删除通过单击一个相册**删除。**</span><span class="sxs-lookup"><span data-stu-id="89e0f-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="89e0f-439">通过单击确认删除**删除**按钮：</span><span class="sxs-lookup"><span data-stu-id="89e0f-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="89e0f-440">![删除 Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "删除 Album")</span><span class="sxs-lookup"><span data-stu-id="89e0f-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="89e0f-441">*删除 Album*</span><span class="sxs-lookup"><span data-stu-id="89e0f-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="89e0f-442">验证是否删除唱片集，因为它不会出现在**索引**页。</span><span class="sxs-lookup"><span data-stu-id="89e0f-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="89e0f-443">练习 6： 添加验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="89e0f-444">目前，您所具有的创建和编辑窗体不执行任何类型的验证。</span><span class="sxs-lookup"><span data-stu-id="89e0f-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="89e0f-445">如果用户离开价格字段中的所需的字段留空或键入字母，会向您的第一个错误将从数据库中。</span><span class="sxs-lookup"><span data-stu-id="89e0f-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="89e0f-446">通过将数据批注添加到 model 类，可以向应用程序添加验证。</span><span class="sxs-lookup"><span data-stu-id="89e0f-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="89e0f-447">描述所需的规则应用于您的模型属性，可以利用数据批注和 ASP.NET MVC 将负责强制执行和向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="89e0f-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="89e0f-448">任务 1-添加数据批注</span><span class="sxs-lookup"><span data-stu-id="89e0f-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="89e0f-449">在此任务中，您将添加到将使创建和编辑页面的唱片集模型的数据注释显示验证消息在适当的时候。</span><span class="sxs-lookup"><span data-stu-id="89e0f-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="89e0f-450">对于简单的模型类，添加数据批注只需添加处理**使用**语句**System.ComponentModel.DataAnnotation**，然后将放到 **[必需]** 上相应的属性的属性。</span><span class="sxs-lookup"><span data-stu-id="89e0f-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="89e0f-451">下面的示例将使**名称**属性在视图中的必填字段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="89e0f-452">这是稍微复杂一些类似于此应用程序的情况下在其中生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="89e0f-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="89e0f-453">如果你的数据批注直接添加到模型类，它们将被覆盖如果从数据库对模型进行更新。</span><span class="sxs-lookup"><span data-stu-id="89e0f-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="89e0f-454">相反，您可使用元数据部分类将是为了容纳批注并与模型相关联的类使用 **[MetadataType]** 属性。</span><span class="sxs-lookup"><span data-stu-id="89e0f-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="89e0f-455">打开**开始**解决方案位于**源/Ex6-AddingValidation/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="89e0f-456">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-457">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-458">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-459">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-460">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-461">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-462">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-463">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-464">打开**Album.cs**从**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="89e0f-465">替换**Album.cs**内容与突出显示的代码，以便它看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="89e0f-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="89e0f-466">在行 **[DisplayFormat(ConvertEmptyStringToNull=false)]** 指示数据源中更新数据字段时，将不会从模型的空字符串转换为 null。</span><span class="sxs-lookup"><span data-stu-id="89e0f-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="89e0f-467">实体框架将 null 值分配给该模型之前数据批注验证字段时，此设置会避免异常。</span><span class="sxs-lookup"><span data-stu-id="89e0f-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="89e0f-468">(代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex6 唱片集的元数据部分类*)</span><span class="sxs-lookup"><span data-stu-id="89e0f-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-469">这**唱片集**分部类具有**MetadataType**属性，用于指向**AlbumMetaData**数据批注的类。</span><span class="sxs-lookup"><span data-stu-id="89e0f-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="89e0f-470">以下是一些用于批注的唱片集模型的数据批注属性：</span><span class="sxs-lookup"><span data-stu-id="89e0f-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="89e0f-471">需要-指示该属性是必填的字段</span><span class="sxs-lookup"><span data-stu-id="89e0f-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="89e0f-472">DisplayName-定义要使用窗体字段并验证消息的文本</span><span class="sxs-lookup"><span data-stu-id="89e0f-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="89e0f-473">DisplayFormat-指定如何显示和格式化数据字段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="89e0f-474">StringLength-定义字符串字段的最大长度</span><span class="sxs-lookup"><span data-stu-id="89e0f-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="89e0f-475">范围-最大和最小值为数值字段</span><span class="sxs-lookup"><span data-stu-id="89e0f-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="89e0f-476">ScaffoldColumn-允许隐藏编辑器窗体中的字段</span><span class="sxs-lookup"><span data-stu-id="89e0f-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="89e0f-477">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="89e0f-478">在本任务中，您将测试创建和编辑页面验证字段，使用上一个任务中选择的显示名称。</span><span class="sxs-lookup"><span data-stu-id="89e0f-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="89e0f-479">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="89e0f-480">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-480">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-481">将 URL 更改为**StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="89e0f-482">验证是否显示名称匹配的分部类中的 (如**唱片集画面 URL**而不是**AlbumArtUrl**)</span><span class="sxs-lookup"><span data-stu-id="89e0f-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="89e0f-483">单击**创建**，而不填充窗体。</span><span class="sxs-lookup"><span data-stu-id="89e0f-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="89e0f-484">验证获取相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="89e0f-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="89e0f-485">![验证创建页中的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "验证创建页中的字段")</span><span class="sxs-lookup"><span data-stu-id="89e0f-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="89e0f-486">*在创建页中的已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="89e0f-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="89e0f-487">你可以验证相同出现**编辑**页。</span><span class="sxs-lookup"><span data-stu-id="89e0f-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="89e0f-488">将 URL 更改为 **/StoreManager/Edit/1**并验证是否显示名称与在分部类中的匹配 (如**唱片集画面 URL**而不是**AlbumArtUrl**)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="89e0f-489">空**标题**并**价格**字段，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="89e0f-490">验证获取相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="89e0f-490">Verify that you get the corresponding validation messages.</span></span>

    ![在编辑页中的已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="89e0f-492">*在编辑页中的已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="89e0f-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="89e0f-493">练习 7： 在客户端使用非介入式 jQuery</span><span class="sxs-lookup"><span data-stu-id="89e0f-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="89e0f-494">在此练习中，您将学习如何启用客户端的 MVC 4 非介入式 jQuery 验证。</span><span class="sxs-lookup"><span data-stu-id="89e0f-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="89e0f-495">非介入式 jQuery 使用数据 ajax 前缀 JavaScript 来调用操作方法在服务器而不是干扰的方式发出的内联客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="89e0f-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="89e0f-496">任务 1-运行之前启用非介入式 jQuery 在应用程序</span><span class="sxs-lookup"><span data-stu-id="89e0f-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="89e0f-497">在本任务中，将运行之前要比较这两种验证模型包括 jQuery 在应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="89e0f-498">打开**开始**解决方案位于**源/Ex7-UnobtrusivejQueryValidation/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="89e0f-499">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="89e0f-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="89e0f-500">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="89e0f-501">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="89e0f-502">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="89e0f-503">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="89e0f-504">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="89e0f-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="89e0f-505">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="89e0f-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="89e0f-506">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="89e0f-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="89e0f-507">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="89e0f-508">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-508">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-509">浏览 **/StoreManager/创建**然后单击**创建**而不填充该窗体以验证你收到验证消息：</span><span class="sxs-lookup"><span data-stu-id="89e0f-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="89e0f-510">![客户端验证已禁用](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "禁用客户端验证")</span><span class="sxs-lookup"><span data-stu-id="89e0f-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="89e0f-511">*禁用客户端验证*</span><span class="sxs-lookup"><span data-stu-id="89e0f-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="89e0f-512">在浏览器中打开的 HTML 源代码：</span><span class="sxs-lookup"><span data-stu-id="89e0f-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="89e0f-513">任务 2-启用非介入式客户端验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="89e0f-514">在本任务中，将启用 jQuery**非介入式客户端验证**从**Web.config**文件，它是默认情况下所有新的 ASP.NET MVC 4 项目中设置为 false。</span><span class="sxs-lookup"><span data-stu-id="89e0f-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="89e0f-515">此外，您将添加所需的脚本引用，以使 jQuery 非介入式客户端验证工作。</span><span class="sxs-lookup"><span data-stu-id="89e0f-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="89e0f-516">打开**Web.Config**文件在项目根目录位置，并确保选中**ClientValidationEnabled**并**UnobtrusiveJavaScriptEnabled**密钥值设置为 **，则返回 true**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-517">此外可以通过在 Global.asax.cs 以获得相同的结果的代码来启用客户端验证：</span><span class="sxs-lookup"><span data-stu-id="89e0f-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="89e0f-518">**HtmlHelper.ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="89e0f-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="89e0f-519">此外，可以将 ClientValidationEnabled 属性分配到任何控制器具有自定义行为。</span><span class="sxs-lookup"><span data-stu-id="89e0f-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="89e0f-520">打开**Create.cshtml**处**Views\StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="89e0f-521">以下脚本文件，请确保**jquery.validate**并**jquery.validate.unobtrusive**，查看站点中引用&quot; **~/bundles/jqueryval**&quot;捆绑包。</span><span class="sxs-lookup"><span data-stu-id="89e0f-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view throught the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="89e0f-522">所有这些 jQuery 库包含在新的 MVC 4 项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="89e0f-523">您可以找到更多库中的 **/脚本**您项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="89e0f-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="89e0f-524">为了使此验证库的工作原理，您需要添加对 jQuery 框架库的引用。</span><span class="sxs-lookup"><span data-stu-id="89e0f-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="89e0f-525">由于已在添加此引用 **\_Layout.cshtml**文件，您不需要在此特定视图中添加它。</span><span class="sxs-lookup"><span data-stu-id="89e0f-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="89e0f-526">任务 3-运行应用程序使用非介入式 jQuery 验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="89e0f-527">在此任务中，将测试**StoreManager**创建视图模板执行用户创建新的唱片集时使用 jQuery 库的客户端验证。</span><span class="sxs-lookup"><span data-stu-id="89e0f-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="89e0f-528">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="89e0f-529">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="89e0f-529">The project starts in the Home page.</span></span> <span data-ttu-id="89e0f-530">浏览 **/StoreManager/创建**然后单击**创建**而不填充该窗体以验证你收到验证消息：</span><span class="sxs-lookup"><span data-stu-id="89e0f-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="89e0f-531">![使用 jQuery 启用客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "使用 jQuery 启用客户端验证")</span><span class="sxs-lookup"><span data-stu-id="89e0f-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="89e0f-532">*使用 jQuery 启用客户端验证*</span><span class="sxs-lookup"><span data-stu-id="89e0f-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="89e0f-533">在浏览器中，打开创建视图的源代码:</span><span class="sxs-lookup"><span data-stu-id="89e0f-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="89e0f-534">对于每个客户端验证规则，非介入式 jQuery 将添加一个特性，其数据-val-*rulename*=&quot;*消息*&quot;。</span><span class="sxs-lookup"><span data-stu-id="89e0f-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="89e0f-535">下面是一系列标记该 Unobtrusive jQuery 插入 html 输入字段来执行客户端验证：</span><span class="sxs-lookup"><span data-stu-id="89e0f-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="89e0f-536">数据值</span><span class="sxs-lookup"><span data-stu-id="89e0f-536">Data-val</span></span>
   > - <span data-ttu-id="89e0f-537">数据 val 编号</span><span class="sxs-lookup"><span data-stu-id="89e0f-537">Data-val-number</span></span>
   > - <span data-ttu-id="89e0f-538">数据值范围</span><span class="sxs-lookup"><span data-stu-id="89e0f-538">Data-val-range</span></span>
   > - <span data-ttu-id="89e0f-539">数据值的范围最小/最大数据值范围</span><span class="sxs-lookup"><span data-stu-id="89e0f-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="89e0f-540">-Val 的所需的数据</span><span class="sxs-lookup"><span data-stu-id="89e0f-540">Data-val-required</span></span>
   > - <span data-ttu-id="89e0f-541">数据值长度</span><span class="sxs-lookup"><span data-stu-id="89e0f-541">Data-val-length</span></span>
   > - <span data-ttu-id="89e0f-542">数据值的长度最大/最小数据 val 长度</span><span class="sxs-lookup"><span data-stu-id="89e0f-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="89e0f-543">所有数据值将都填入模型**数据批注**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="89e0f-544">然后，可以在客户端运行在服务器端工作的所有逻辑。</span><span class="sxs-lookup"><span data-stu-id="89e0f-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="89e0f-545">例如，价格属性具有以下数据注释在模型中：</span><span class="sxs-lookup"><span data-stu-id="89e0f-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="89e0f-546">在使用非介入式 jQuery 后, 生成的代码是：</span><span class="sxs-lookup"><span data-stu-id="89e0f-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="89e0f-547">总结</span><span class="sxs-lookup"><span data-stu-id="89e0f-547">Summary</span></span>

<span data-ttu-id="89e0f-548">通过完成本动手实验介绍了如何使用户能够更改与使用以下数据库中存储的数据：</span><span class="sxs-lookup"><span data-stu-id="89e0f-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="89e0f-549">控制器的操作，例如索引、 创建、 编辑、 删除</span><span class="sxs-lookup"><span data-stu-id="89e0f-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="89e0f-550">ASP.NET MVC 基架功能用于 HTML 表中显示属性</span><span class="sxs-lookup"><span data-stu-id="89e0f-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="89e0f-551">自定义 HTML 帮助程序来提高用户体验</span><span class="sxs-lookup"><span data-stu-id="89e0f-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="89e0f-552">对 HTTP GET 或 HTTP POST 调用做出响应的操作方法</span><span class="sxs-lookup"><span data-stu-id="89e0f-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="89e0f-553">有关类似视图模板，如创建和编辑共享的编辑器模板</span><span class="sxs-lookup"><span data-stu-id="89e0f-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="89e0f-554">窗体元素，如下拉列表</span><span class="sxs-lookup"><span data-stu-id="89e0f-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="89e0f-555">数据注释进行模型验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="89e0f-556">使用 jQuery 非介入式库的客户端验证</span><span class="sxs-lookup"><span data-stu-id="89e0f-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="89e0f-557">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="89e0f-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="89e0f-558">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="89e0f-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="89e0f-559">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="89e0f-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="89e0f-560">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="89e0f-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="89e0f-561">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="89e0f-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="89e0f-562">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-562">Click on **Install Now**.</span></span> <span data-ttu-id="89e0f-563">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="89e0f-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="89e0f-564">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="89e0f-565">![安装 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="89e0f-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="89e0f-566">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="89e0f-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="89e0f-567">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="89e0f-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="89e0f-569">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="89e0f-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="89e0f-570">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="89e0f-570">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="89e0f-572">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="89e0f-572">*Installation progress*</span></span>
6. <span data-ttu-id="89e0f-573">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-573">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="89e0f-575">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="89e0f-575">*Installation completed*</span></span>
7. <span data-ttu-id="89e0f-576">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="89e0f-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="89e0f-577">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="89e0f-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="89e0f-579">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="89e0f-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="89e0f-580">附录 b： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="89e0f-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="89e0f-581">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="89e0f-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="89e0f-582">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="89e0f-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="89e0f-583">![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="89e0f-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="89e0f-584">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="89e0f-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="89e0f-585">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="89e0f-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="89e0f-586">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="89e0f-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="89e0f-587">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="89e0f-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="89e0f-588">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="89e0f-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="89e0f-589">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="89e0f-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="89e0f-590">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="89e0f-591">![开始键入代码段名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="89e0f-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="89e0f-592">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="89e0f-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="89e0f-593">![按 tab 键以选择突出显示代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="89e0f-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="89e0f-594">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="89e0f-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="89e0f-595">![再次按 Tab 和代码段将 expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="89e0f-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="89e0f-596">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="89e0f-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="89e0f-597">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="89e0f-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="89e0f-598">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="89e0f-599">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="89e0f-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="89e0f-600">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="89e0f-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="89e0f-601">![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="89e0f-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="89e0f-602">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="89e0f-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="89e0f-603">![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="89e0f-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="89e0f-604">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="89e0f-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
