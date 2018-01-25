---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: "ASP.NET MVC 4 帮助器、 窗体和验证 |Microsoft 文档"
author: rick-anderson
description: "在 ASP.NET MVC 4 模型和数据访问动手实验中，你已加载并显示从数据库的数据。 在本动手实验中，你将添加到..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 925d659f42496045089ba056e194ac977c37a8de
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="86413-104">ASP.NET MVC 4 帮助器、 窗体和验证</span><span class="sxs-lookup"><span data-stu-id="86413-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>
====================
<span data-ttu-id="86413-105">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="86413-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="86413-106">在**ASP.NET MVC 4 模型和数据访问**动手实验中，你已被加载和显示来自数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="86413-106">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="86413-107">在本动手实验中，你将添加到**音乐商店**应用程序编辑该数据的能力。</span><span class="sxs-lookup"><span data-stu-id="86413-107">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>
> 
> <span data-ttu-id="86413-108">与该目标，首先将创建将支持唱片集的创建、 读取、 更新和删除 (CRUD) 操作的控制器。</span><span class="sxs-lookup"><span data-stu-id="86413-108">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="86413-109">将生成利用 ASP.NET MVC 基架功能在 HTML 表中显示唱片集的属性的索引视图模板。</span><span class="sxs-lookup"><span data-stu-id="86413-109">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="86413-110">若要增强该视图，你将添加将截断长说明的自定义 HTML 帮助。</span><span class="sxs-lookup"><span data-stu-id="86413-110">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>
> 
> <span data-ttu-id="86413-111">然后，你将添加编辑和创建的视图，以便可以改变专辑在数据库中，如下拉列表的窗体元素的帮助。</span><span class="sxs-lookup"><span data-stu-id="86413-111">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>
> 
> <span data-ttu-id="86413-112">最后，您就可以让用户删除唱片集，也将从通过验证其输入来输入数据错误阻止它们。</span><span class="sxs-lookup"><span data-stu-id="86413-112">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="86413-113">此动手实验假定你具有的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="86413-113">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="86413-114">如果您未使用过**ASP.NET MVC**之前，我们建议你转到**ASP.NET MVC 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="86413-114">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>
> 
> 
> <span data-ttu-id="86413-115">此实验室将引导你完成的增强功能和前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用程序的新功能。</span><span class="sxs-lookup"><span data-stu-id="86413-115">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="86413-116">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843)。</span><span class="sxs-lookup"><span data-stu-id="86413-116">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="86413-117">目标</span><span class="sxs-lookup"><span data-stu-id="86413-117">Objectives</span></span>

<span data-ttu-id="86413-118">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="86413-118">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="86413-119">创建控制器以支持 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="86413-119">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="86413-120">生成索引视图以显示 HTML 表中的实体属性</span><span class="sxs-lookup"><span data-stu-id="86413-120">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="86413-121">添加自定义 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="86413-121">Add a custom HTML helper</span></span>
- <span data-ttu-id="86413-122">创建和自定义编辑视图</span><span class="sxs-lookup"><span data-stu-id="86413-122">Create and customize an Edit View</span></span>
- <span data-ttu-id="86413-123">区分响应 HTTP GET 或 HTTP POST 调用的操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-123">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="86413-124">添加和自定义创建视图</span><span class="sxs-lookup"><span data-stu-id="86413-124">Add and customize a Create View</span></span>
- <span data-ttu-id="86413-125">处理删除的实体</span><span class="sxs-lookup"><span data-stu-id="86413-125">Handle the deletion of an entity</span></span>
- <span data-ttu-id="86413-126">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="86413-126">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="86413-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="86413-127">Prerequisites</span></span>

<span data-ttu-id="86413-128">你必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="86413-128">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="86413-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="86413-129">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="86413-130">安装</span><span class="sxs-lookup"><span data-stu-id="86413-130">Setup</span></span>

<span data-ttu-id="86413-131">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="86413-131">**Installing Code Snippets**</span></span>

<span data-ttu-id="86413-132">为方便起见，你将沿此实验室管理大部分都是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="86413-132">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="86413-133">若要安装运行的代码段**.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="86413-133">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="86413-134">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 b： 使用代码段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="86413-134">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="86413-135">练习</span><span class="sxs-lookup"><span data-stu-id="86413-135">Exercises</span></span>

<span data-ttu-id="86413-136">在以下练习构成此动手实验：</span><span class="sxs-lookup"><span data-stu-id="86413-136">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="86413-137">创建存储管理器控制器和其索引视图</span><span class="sxs-lookup"><span data-stu-id="86413-137">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="86413-138">添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="86413-138">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="86413-139">创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="86413-139">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="86413-140">添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="86413-140">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="86413-141">处理删除</span><span class="sxs-lookup"><span data-stu-id="86413-141">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="86413-142">添加验证</span><span class="sxs-lookup"><span data-stu-id="86413-142">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="86413-143">在客户端使用非介入式 jQuery</span><span class="sxs-lookup"><span data-stu-id="86413-143">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="86413-144">每个练习均附带由**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="86413-145">如果你需要通过在练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="86413-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="86413-146">估计时间来完成该实验： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="86413-146">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="86413-147">练习 1： 创建存储管理器控制器和其索引视图</span><span class="sxs-lookup"><span data-stu-id="86413-147">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="86413-148">在本练习中，您将学习如何创建新的控制器以支持 CRUD 操作，自定义其索引操作方法，以从数据库和最后生成利用 ASP.NET MVC 基架的索引视图模板返回的唱片集列表若要在 HTML 表中显示唱片集的属性的功能。</span><span class="sxs-lookup"><span data-stu-id="86413-148">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="86413-149">任务 1-创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="86413-149">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="86413-150">在此任务中，你将创建新的控制器调用**StoreManagerController**以支持 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="86413-150">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="86413-151">打开**开始**解决方案位于**源/Ex1-CreatingTheStoreManagerController/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-151">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

    1. <span data-ttu-id="86413-152">你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-153">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-154">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-155">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-156">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-157">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-158">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-159">添加一个新的控制器。</span><span class="sxs-lookup"><span data-stu-id="86413-159">Add a new controller.</span></span> <span data-ttu-id="86413-160">要执行此操作，请右键单击**控制器**在解决方案资源管理器，选择文件夹**添加**然后**控制器**命令。</span><span class="sxs-lookup"><span data-stu-id="86413-160">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="86413-161">更改**控制器****名称**到**StoreManagerController**并确保选项**包含空读/写操作的MVC控制器**选择。</span><span class="sxs-lookup"><span data-stu-id="86413-161">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="86413-162">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="86413-162">Click **Add**.</span></span>

    <span data-ttu-id="86413-163">![添加控制器对话框](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "添加控制器对话框")</span><span class="sxs-lookup"><span data-stu-id="86413-163">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="86413-164">*添加控制器对话框*</span><span class="sxs-lookup"><span data-stu-id="86413-164">*Add Controller Dialog*</span></span>

    <span data-ttu-id="86413-165">生成新的控制器类。</span><span class="sxs-lookup"><span data-stu-id="86413-165">A new Controller class is generated.</span></span> <span data-ttu-id="86413-166">因为你要添加的读/写，对于那些，存根 （stub） 方法的操作来创建 TODO 注释填写，提示将应用程序特定逻辑包括常见 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="86413-166">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="86413-167">任务 2-自定义 StoreManager 索引</span><span class="sxs-lookup"><span data-stu-id="86413-167">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="86413-168">在此任务中，将自定义要从数据库返回具有唱片集的列表的视图的 StoreManager 索引操作方法。</span><span class="sxs-lookup"><span data-stu-id="86413-168">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="86413-169">在 StoreManagerController 类中，添加以下*使用*指令。</span><span class="sxs-lookup"><span data-stu-id="86413-169">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="86413-170">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex1 使用 MvcMusicStore*)</span><span class="sxs-lookup"><span data-stu-id="86413-170">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="86413-171">将字段添加到**StoreManagerController**来托管实例的**MusicStoreEntities。**</span><span class="sxs-lookup"><span data-stu-id="86413-171">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="86413-172">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="86413-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="86413-173">实现 StoreManagerController 索引操作返回与唱片集的列表视图。</span><span class="sxs-lookup"><span data-stu-id="86413-173">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="86413-174">控制器操作逻辑将非常类似于前面编写 StoreController 的索引操作。</span><span class="sxs-lookup"><span data-stu-id="86413-174">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="86413-175">使用 LINQ 检索所有专辑，包括的显示风格和艺术家信息。</span><span class="sxs-lookup"><span data-stu-id="86413-175">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="86413-176">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex1 StoreManagerController 索引*)</span><span class="sxs-lookup"><span data-stu-id="86413-176">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="86413-177">任务 3-创建索引视图</span><span class="sxs-lookup"><span data-stu-id="86413-177">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="86413-178">在此任务中，你将创建索引视图模板，以显示列表中返回的专辑**StoreManager**控制器。</span><span class="sxs-lookup"><span data-stu-id="86413-178">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="86413-179">在创建新的视图模板之前, 应生成项目，以便**添加视图对话框**就会了解有关**唱片集**要使用的类。</span><span class="sxs-lookup"><span data-stu-id="86413-179">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="86413-180">选择**生成 |生成 MvcMusicStore**以生成项目。</span><span class="sxs-lookup"><span data-stu-id="86413-180">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="86413-181">右键单击内部**索引**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="86413-181">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="86413-182">此时会弹出**添加视图**对话框。</span><span class="sxs-lookup"><span data-stu-id="86413-182">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="86413-183">![添加视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "添加视图")</span><span class="sxs-lookup"><span data-stu-id="86413-183">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="86413-184">*添加从索引方法内的某个视图*</span><span class="sxs-lookup"><span data-stu-id="86413-184">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="86413-185">在添加视图对话框中，验证是否视图名称**索引**。</span><span class="sxs-lookup"><span data-stu-id="86413-185">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="86413-186">选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)**从**模型类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-186">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="86413-187">选择**列表**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-187">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="86413-188">保留**视图引擎**到**Razor**和其他字段使用其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="86413-188">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="86413-189">![添加索引视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "添加索引视图")</span><span class="sxs-lookup"><span data-stu-id="86413-189">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="86413-190">*添加索引视图*</span><span class="sxs-lookup"><span data-stu-id="86413-190">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="86413-191">任务 4-自定义索引视图的基架</span><span class="sxs-lookup"><span data-stu-id="86413-191">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="86413-192">在此任务中，您将调整与 ASP.NET MVC 基架功能，以使它显示所需的字段创建的简单视图模板。</span><span class="sxs-lookup"><span data-stu-id="86413-192">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="86413-193">**基架**支持 ASP.NET MVC 中的生成一个简单的视图模板，其中列出了唱片集模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="86413-193">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="86413-194">**基架**快速地开始使用强类型化视图： 而不是无需手动编写查看模板，基架快速生成的默认模板，然后可以修改生成的代码。</span><span class="sxs-lookup"><span data-stu-id="86413-194">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>


1. <span data-ttu-id="86413-195">查看创建的代码。</span><span class="sxs-lookup"><span data-stu-id="86413-195">Review the code created.</span></span> <span data-ttu-id="86413-196">生成的字段列表将作为一部分的以下 HTML 表**基架**用于显示表格格式数据。</span><span class="sxs-lookup"><span data-stu-id="86413-196">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="86413-197">替换**&lt;表&gt;**代码替换为以下代码，以仅显示**流派**，**艺术家**，**唱片集标题**，和**价格**字段。</span><span class="sxs-lookup"><span data-stu-id="86413-197">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="86413-198">这将删除**AlbumId**和**唱片集艺术作品 URL**列。</span><span class="sxs-lookup"><span data-stu-id="86413-198">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="86413-199">此外，它将更改 GenreId 和 ArtistId 列以显示其链接的类属性**Artist.Name**和**Genre.Name**，并删除**详细信息**链接。</span><span class="sxs-lookup"><span data-stu-id="86413-199">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="86413-200">更改以下说明。</span><span class="sxs-lookup"><span data-stu-id="86413-200">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="86413-201">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-201">Task 5 - Running the Application</span></span>

<span data-ttu-id="86413-202">在此任务中，你将测试**StoreManager** **索引**视图模板显示根据前面的步骤的设计的唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="86413-202">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="86413-203">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-203">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-204">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-204">The project starts in the Home page.</span></span> <span data-ttu-id="86413-205">将 URL 更改为**/StoreManager**验证，显示的唱片集的列表，显示其**标题**，**艺术家**和**流派**。</span><span class="sxs-lookup"><span data-stu-id="86413-205">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="86413-206">![浏览的专辑列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "浏览唱片集的列表")</span><span class="sxs-lookup"><span data-stu-id="86413-206">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="86413-207">*浏览唱片集的列表*</span><span class="sxs-lookup"><span data-stu-id="86413-207">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="86413-208">练习 2： 添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="86413-208">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="86413-209">StoreManager 索引页都有一个潜在问题： 标题和艺术家名称属性都可以是足够长，以引发关闭表格的格式。</span><span class="sxs-lookup"><span data-stu-id="86413-209">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="86413-210">在本练习中你将了解如何添加自定义的 HTML 帮助器截断该文本。</span><span class="sxs-lookup"><span data-stu-id="86413-210">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="86413-211">在下图中，你可以看到如何格式时所使用的小型浏览器大小修改由于文本的长度。</span><span class="sxs-lookup"><span data-stu-id="86413-211">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="86413-212">![浏览与唱片集的列表不会被截断文本](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "浏览与唱片集的列表不截断的文本")</span><span class="sxs-lookup"><span data-stu-id="86413-212">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="86413-213">*浏览与唱片集的列表不截断的文本*</span><span class="sxs-lookup"><span data-stu-id="86413-213">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="86413-214">任务 1-扩展 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="86413-214">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="86413-215">在此任务中，你将添加一个新方法**Truncate**到**HTML**公开在 ASP.NET MVC 视图内的对象。</span><span class="sxs-lookup"><span data-stu-id="86413-215">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="86413-216">若要执行此操作，则将实现**扩展方法**到内置**System.Web.Mvc.HtmlHelper**类提供的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="86413-216">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="86413-217">若要阅读更多有关**扩展方法**，请访问此 msdn 文章。</span><span class="sxs-lookup"><span data-stu-id="86413-217">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="86413-218">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="86413-218">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>


1. <span data-ttu-id="86413-219">打开**开始**解决方案位于**源/Ex2-AddingAnHTMLHelper/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-219">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="86413-220">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-220">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-221">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-221">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-222">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-222">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-223">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-223">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-224">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-224">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-225">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-225">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-226">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-226">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-227">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-227">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-228">打开 StoreManager 的索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-228">Open StoreManager's Index View.</span></span> <span data-ttu-id="86413-229">若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，则**StoreManager**并打开**Index.cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="86413-229">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="86413-230">添加下面的代码下面 **@model** 指令来定义**Truncate**帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="86413-230">Add the following code below the **@model** directive to define the **Truncate** helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="86413-231">任务 2-在页中的截断文本</span><span class="sxs-lookup"><span data-stu-id="86413-231">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="86413-232">在此任务中，你将使用**Truncate**方法进行截断操作中查看模板的文本。</span><span class="sxs-lookup"><span data-stu-id="86413-232">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="86413-233">打开 StoreManager 的索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-233">Open StoreManager's Index View.</span></span> <span data-ttu-id="86413-234">若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，则**StoreManager**并打开**Index.cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="86413-234">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="86413-235">显示的行替换**艺术家名称**和唱片集的**标题**。</span><span class="sxs-lookup"><span data-stu-id="86413-235">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="86413-236">若要执行此操作，请将以下行。</span><span class="sxs-lookup"><span data-stu-id="86413-236">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="86413-237">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-237">Task 3 - Running the Application</span></span>

<span data-ttu-id="86413-238">在此任务中，你将测试**StoreManager** **索引**视图模板将截断唱片集的标题和艺术家名称。</span><span class="sxs-lookup"><span data-stu-id="86413-238">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="86413-239">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-239">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-240">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-240">The project starts in the Home page.</span></span> <span data-ttu-id="86413-241">将 URL 更改为**/StoreManager**以验证该 long 类型的值中的文本**标题**和**艺术家**列将被截断。</span><span class="sxs-lookup"><span data-stu-id="86413-241">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="86413-242">![截断标题和艺术家名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截断标题和艺术家名称")</span><span class="sxs-lookup"><span data-stu-id="86413-242">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="86413-243">*截断的标题和艺术家姓名*</span><span class="sxs-lookup"><span data-stu-id="86413-243">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="86413-244">练习 3： 创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="86413-244">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="86413-245">在本练习中，您将学习如何创建窗体，以允许存储管理器编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="86413-245">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="86413-246">用户将浏览**/StoreManager/Edit/id** URL (**id**正在编辑的唱片集的唯一 id)，从而使到服务器的 HTTP GET 调用。</span><span class="sxs-lookup"><span data-stu-id="86413-246">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="86413-247">控制器编辑操作方法将从数据库中检索相应唱片集，创建**StoreManagerViewModel**对象，用于封装 （以及专业人员和风格的列表），并将其传递给的视图模板向用户呈现的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="86413-247">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="86413-248">此页将包含**&lt;窗体&gt;**使用文本框和下拉列表编辑唱片集属性的元素。</span><span class="sxs-lookup"><span data-stu-id="86413-248">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="86413-249">用户更新唱片集窗体值并单击后**保存**按钮，所做的更改会提交通过 HTTP 发送回叫**/StoreManager/Edit/id**。虽然 URL 仍与最后一次调用中的相同，ASP.NET MVC 标识，此时它是 HTTP POST，并因此执行不同的编辑操作方法 (一个使用修饰**[HttpPost]**)。</span><span class="sxs-lookup"><span data-stu-id="86413-249">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="86413-250">任务 1-实现的 HTTP GET 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-250">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="86413-251">在此任务中，将实现来检索从数据库中的相应唱片集的编辑操作方法的 HTTP GET 版本以及所有风格和专业人员的列表。</span><span class="sxs-lookup"><span data-stu-id="86413-251">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="86413-252">它将此数据打包成**StoreManagerViewModel**最后一个步骤，然后将传递给要呈现具有的响应的视图模板中定义的对象。</span><span class="sxs-lookup"><span data-stu-id="86413-252">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="86413-253">打开**开始**解决方案位于**源/Ex3-CreatingTheEditView/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-253">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="86413-254">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-254">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-255">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-255">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-256">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-256">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-257">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-257">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-258">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-258">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-259">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-259">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-260">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-260">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-261">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-261">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-262">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="86413-262">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="86413-263">若要执行此操作，展开**控制器**文件夹并双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="86413-263">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="86413-264">替换**HTTP GET 编辑**替换为以下代码，以检索相应的操作方法**唱片集**以及**风格**和**艺术家**列出。</span><span class="sxs-lookup"><span data-stu-id="86413-264">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="86413-265">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex3 StoreManagerController HTTP GET 编辑操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-265">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="86413-266">你使用**System.Web.Mvc** **此时**专业人员和风格而不是为**System.Collections.Generic**列表。</span><span class="sxs-lookup"><span data-stu-id="86413-266">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="86413-267">**此时**是填充 HTML 下拉列表和管理等当前所选内容的更简洁方法。</span><span class="sxs-lookup"><span data-stu-id="86413-267">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="86413-268">实例化和更高版本设置中的控制器操作这些 ViewModel 对象将使编辑窗体方案清理器。</span><span class="sxs-lookup"><span data-stu-id="86413-268">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="86413-269">任务 2-创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="86413-269">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="86413-270">在此任务中，你将创建更高版本显示唱片集属性的编辑视图模板。</span><span class="sxs-lookup"><span data-stu-id="86413-270">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="86413-271">创建编辑视图。</span><span class="sxs-lookup"><span data-stu-id="86413-271">Create the Edit View.</span></span> <span data-ttu-id="86413-272">若要执行此操作，右键单击内**编辑**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="86413-272">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="86413-273">在添加视图对话框中，验证是否视图名称**编辑**。</span><span class="sxs-lookup"><span data-stu-id="86413-273">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="86413-274">检查**创建强类型化视图**复选框，然后选择**唱片集 (MvcMusicStore.Models)**从**查看数据类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-274">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="86413-275">选择**编辑**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-275">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="86413-276">将其他字段保留其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="86413-276">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="86413-277">![添加的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "添加的编辑视图")</span><span class="sxs-lookup"><span data-stu-id="86413-277">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="86413-278">*添加的编辑视图*</span><span class="sxs-lookup"><span data-stu-id="86413-278">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="86413-279">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-279">Task 3 - Running the Application</span></span>

<span data-ttu-id="86413-280">在此任务中，你将测试**StoreManager** **编辑**视图页中显示的唱片集作为参数传递的属性的值。</span><span class="sxs-lookup"><span data-stu-id="86413-280">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="86413-281">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-281">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-282">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-282">The project starts in the Home page.</span></span> <span data-ttu-id="86413-283">将 URL 更改为**/StoreManager/Edit/1**以验证显示是否传递唱片集的属性的值。</span><span class="sxs-lookup"><span data-stu-id="86413-283">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="86413-284">![浏览唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "浏览唱片集的编辑视图")</span><span class="sxs-lookup"><span data-stu-id="86413-284">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="86413-285">*浏览唱片集的编辑视图*</span><span class="sxs-lookup"><span data-stu-id="86413-285">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="86413-286">任务 4-在唱片集编辑器模板上实现下拉列表</span><span class="sxs-lookup"><span data-stu-id="86413-286">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="86413-287">在此任务中，你将添加下拉列表中的最后一个任务，创建的视图模板，以便用户可以选择从专业人员和风格的列表。</span><span class="sxs-lookup"><span data-stu-id="86413-287">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="86413-288">全部替换**唱片集**fieldset 代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="86413-288">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="86413-289">**Html.DropDownList**添加了帮助器以呈现下拉列表选择专业人员和风格。</span><span class="sxs-lookup"><span data-stu-id="86413-289">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="86413-290">参数传递给**Html.DropDownList**是：</span><span class="sxs-lookup"><span data-stu-id="86413-290">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="86413-291">窗体字段的名称 (**&quot;ArtistId&quot;**)。</span><span class="sxs-lookup"><span data-stu-id="86413-291">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="86413-292">**此时**的下拉列表的值。</span><span class="sxs-lookup"><span data-stu-id="86413-292">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="86413-293">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-293">Task 5 - Running the Application</span></span>

<span data-ttu-id="86413-294">在此任务中，你将测试**StoreManager** **编辑**视图页中显示而不是艺术家和风格 ID 文本字段的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-294">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="86413-295">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-295">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-296">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-296">The project starts in the Home page.</span></span> <span data-ttu-id="86413-297">将 URL 更改为**/StoreManager/Edit/1**以验证它显示而不是艺术家和风格 ID 文本字段的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-297">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="86413-298">![浏览唱片集的下拉列表编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "浏览唱片集的下拉列表编辑视图")</span><span class="sxs-lookup"><span data-stu-id="86413-298">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="86413-299">*浏览唱片集的编辑视图，这次它带有下拉列表*</span><span class="sxs-lookup"><span data-stu-id="86413-299">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="86413-300">任务 6-实现的 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-300">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="86413-301">现在，编辑视图显示按预期方式，你需要实现 HTTP POST 编辑操作方法，可保存到唱片集所做的更改。</span><span class="sxs-lookup"><span data-stu-id="86413-301">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="86413-302">关闭浏览器，如果需要可以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="86413-302">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="86413-303">打开**StoreManagerController**从**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-303">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="86413-304">替换**HTTP POST 编辑**操作方法代码替换为以下 （请注意，必须将其替换的方法接收两个参数的重载的版本）：</span><span class="sxs-lookup"><span data-stu-id="86413-304">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="86413-305">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex3 StoreManagerController HTTP POST 编辑操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-305">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="86413-306">将执行此方法，当用户单击**保存**视图的按钮，并执行 HTTP POST 的回发到服务器的窗体值将其保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="86413-306">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="86413-307">修饰**[HttpPost]**指示该方法应用于这些 HTTP POST 方案。</span><span class="sxs-lookup"><span data-stu-id="86413-307">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="86413-308">该方法采用**唱片集**对象。</span><span class="sxs-lookup"><span data-stu-id="86413-308">The method takes an **Album** object.</span></span> <span data-ttu-id="86413-309">ASP.NET MVC 将自动创建唱片集对象从已发布&lt;窗体&gt;值。</span><span class="sxs-lookup"><span data-stu-id="86413-309">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="86413-310">该方法将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="86413-310">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="86413-311">如果模型是有效的：</span><span class="sxs-lookup"><span data-stu-id="86413-311">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="86413-312">更新要将其标记为已修改对象的上下文中的唱片集条目。</span><span class="sxs-lookup"><span data-stu-id="86413-312">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="86413-313">保存所做的更改并将重定向到索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-313">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="86413-314">如果模型不是有效的它会使用填充与 ViewBag **GenreId**和**ArtistId**，则会返回该视图并且接收到的唱片集对象，以允许用户执行任何所需的更新。</span><span class="sxs-lookup"><span data-stu-id="86413-314">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="86413-315">任务 7-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-315">Task 7 - Running the Application</span></span>

<span data-ttu-id="86413-316">在此任务中，你将测试**StoreManager 编辑**视图页中实际将更新后的唱片集数据保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="86413-316">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="86413-317">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-317">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-318">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-318">The project starts in the Home page.</span></span> <span data-ttu-id="86413-319">将 URL 更改为**/StoreManager/Edit/1**。</span><span class="sxs-lookup"><span data-stu-id="86413-319">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="86413-320">将唱片集标题更改为**负载**，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="86413-320">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="86413-321">验证唱片集的列表中实际更改唱片集的标题。</span><span class="sxs-lookup"><span data-stu-id="86413-321">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="86413-322">![更新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新唱片集")</span><span class="sxs-lookup"><span data-stu-id="86413-322">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="86413-323">*更新唱片集*</span><span class="sxs-lookup"><span data-stu-id="86413-323">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="86413-324">练习 4： 添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="86413-324">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="86413-325">现在， **StoreManagerController**支持**编辑**功能，在此练习中你将了解如何添加 Create View 模板以便存储管理器将新唱片集添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-325">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="86413-326">如你具有编辑功能，您将实现使用两个不同方法中的创建方案**StoreManagerController**类：</span><span class="sxs-lookup"><span data-stu-id="86413-326">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="86413-327">在首次访问应用商店管理器时，一种操作方法将显示空窗体**/StoreManager/创建**URL。</span><span class="sxs-lookup"><span data-stu-id="86413-327">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="86413-328">第二个操作方法将处理该方案的存储管理器单击其中**保存**在窗体按钮和提交值回**/StoreManager/创建**URL 为 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="86413-328">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="86413-329">任务 1-实现的 HTTP GET 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-329">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="86413-330">在此任务中，你将实现若要检索的所有风格和艺术家列表，请打包到此数据的创建操作方法的 HTTP GET 版本**StoreManagerViewModel**对象，然后将传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="86413-330">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="86413-331">打开**开始**解决方案位于**源/Ex4-AddingACreateView/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-331">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="86413-332">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-332">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-333">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-333">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-334">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-334">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-335">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-335">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-336">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-336">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-337">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-337">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-338">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-338">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-339">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-339">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-340">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="86413-340">Open **StoreManagerController** class.</span></span> <span data-ttu-id="86413-341">若要执行此操作，展开**控制器**文件夹并双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="86413-341">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="86413-342">替换**创建**操作方法代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="86413-342">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="86413-343">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex4 StoreManagerController HTTP GET 创建操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-343">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="86413-344">任务 2-添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="86413-344">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="86413-345">在此任务中，你将添加 Create View 模板将显示新的 （空） 唱片集窗体。</span><span class="sxs-lookup"><span data-stu-id="86413-345">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="86413-346">右键单击内部**创建**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="86413-346">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="86413-347">这将显示添加视图对话框。</span><span class="sxs-lookup"><span data-stu-id="86413-347">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="86413-348">在添加视图对话框中，验证是否视图名称**创建**。</span><span class="sxs-lookup"><span data-stu-id="86413-348">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="86413-349">选择**创建强类型化视图**选项并选择**唱片集 (MvcMusicStore.Models)**从**模型类**下拉列表和**创建**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-349">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="86413-350">将其他字段保留其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="86413-350">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="86413-351">![添加 create 视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "添加-a-创建-view.png")</span><span class="sxs-lookup"><span data-stu-id="86413-351">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="86413-352">*添加 Create 视图*</span><span class="sxs-lookup"><span data-stu-id="86413-352">*Adding the Create View*</span></span>
3. <span data-ttu-id="86413-353">更新**GenreId**和**ArtistId**字段使用下拉列表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="86413-353">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="86413-354">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-354">Task 3 - Running the Application</span></span>

<span data-ttu-id="86413-355">在此任务中，你将测试**StoreManager** **创建**视图页中显示一个空的唱片集窗体。</span><span class="sxs-lookup"><span data-stu-id="86413-355">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="86413-356">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-356">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-357">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-357">The project starts in the Home page.</span></span> <span data-ttu-id="86413-358">将 URL 更改为**/StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="86413-358">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="86413-359">验证空窗体显示用于填充新唱片集属性。</span><span class="sxs-lookup"><span data-stu-id="86413-359">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="86413-360">![使用空的窗体中创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "创建空的窗体视图")</span><span class="sxs-lookup"><span data-stu-id="86413-360">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="86413-361">*使用空的窗体中创建视图*</span><span class="sxs-lookup"><span data-stu-id="86413-361">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="86413-362">任务 4-实现 HTTP POST 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-362">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="86413-363">在此任务中，你将实现将在用户单击时调用的创建操作方法的 HTTP POST 版本**保存**按钮。</span><span class="sxs-lookup"><span data-stu-id="86413-363">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="86413-364">该方法应将新唱片集保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="86413-364">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="86413-365">关闭浏览器，如果需要可以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="86413-365">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="86413-366">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="86413-366">Open **StoreManagerController** class.</span></span> <span data-ttu-id="86413-367">若要执行此操作，展开**控制器**文件夹并双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="86413-367">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="86413-368">替换**HTTP POST 创建**操作方法代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="86413-368">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="86413-369">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex4 StoreManagerController HTTP POST 创建操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-369">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="86413-370">创建操作非常类似于上一个编辑操作方法，但而不是将对象设置为已修改，它将被添加到上下文。</span><span class="sxs-lookup"><span data-stu-id="86413-370">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="86413-371">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-371">Task 5 - Running the Application</span></span>

<span data-ttu-id="86413-372">在此任务中，你将测试**StoreManager 创建**视图页中可以创建新唱片集，然后将重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-372">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="86413-373">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-373">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-374">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-374">The project starts in the Home page.</span></span> <span data-ttu-id="86413-375">将 URL 更改为**/StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="86413-375">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="86413-376">所有窗体字段用数据填充新唱片集，如下图中所示：</span><span class="sxs-lookup"><span data-stu-id="86413-376">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="86413-377">![创建唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "创建唱片集")</span><span class="sxs-lookup"><span data-stu-id="86413-377">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="86413-378">*创建唱片集*</span><span class="sxs-lookup"><span data-stu-id="86413-378">*Creating an Album*</span></span>
3. <span data-ttu-id="86413-379">验证你获取重定向到包含刚创建的新唱片集 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-379">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="86413-380">![创建新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "创建的新唱片集")</span><span class="sxs-lookup"><span data-stu-id="86413-380">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="86413-381">*创建新唱片集*</span><span class="sxs-lookup"><span data-stu-id="86413-381">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="86413-382">练习 5： 处理删除</span><span class="sxs-lookup"><span data-stu-id="86413-382">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="86413-383">若要删除唱片集的功能尚未实现。</span><span class="sxs-lookup"><span data-stu-id="86413-383">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="86413-384">这是本练习将哪些有关。</span><span class="sxs-lookup"><span data-stu-id="86413-384">This is what this exercise will be about.</span></span> <span data-ttu-id="86413-385">像之前，将实现使用两个不同方法中的删除方案**StoreManagerController**类：</span><span class="sxs-lookup"><span data-stu-id="86413-385">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="86413-386">一种操作方法将显示一个确认窗体</span><span class="sxs-lookup"><span data-stu-id="86413-386">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="86413-387">第二个操作方法将处理提交窗体</span><span class="sxs-lookup"><span data-stu-id="86413-387">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="86413-388">任务 1-实现 HTTP GET Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-388">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="86413-389">在此任务中，你将实现来检索唱片集的信息的删除操作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="86413-389">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="86413-390">打开**开始**解决方案位于**源/Ex5-HandlingDeletion/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-390">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="86413-391">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-391">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-392">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-392">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-393">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-393">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-394">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-394">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-395">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-395">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-396">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-396">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-397">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-397">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-398">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-398">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-399">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="86413-399">Open **StoreManagerController** class.</span></span> <span data-ttu-id="86413-400">若要执行此操作，展开**控制器**文件夹并双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="86413-400">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="86413-401">删除控制器操作正是之前存储详细信息控制器操作相同： 它会查询**唱片集**从数据库使用的对象**id** URL 和返回中提供适当**视图**。</span><span class="sxs-lookup"><span data-stu-id="86413-401">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="86413-402">若要执行此操作，将 HTTP GET**删除**操作方法代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="86413-402">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="86413-403">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex5 处理删除 HTTP GET Delete 操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-403">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="86413-404">右键单击内部**删除**操作方法，然后选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="86413-404">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="86413-405">这将显示添加视图对话框。</span><span class="sxs-lookup"><span data-stu-id="86413-405">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="86413-406">在添加视图对话框中，验证是否视图名称**删除**。</span><span class="sxs-lookup"><span data-stu-id="86413-406">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="86413-407">选择**创建强类型化视图**选项并选择**唱片集 (MvcMusicStore.Models)**从**模型类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-407">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="86413-408">选择**删除**从**基架模板**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="86413-408">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="86413-409">将其他字段保留其默认值，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="86413-409">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="86413-410">![添加删除视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "添加删除视图")</span><span class="sxs-lookup"><span data-stu-id="86413-410">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="86413-411">*添加删除视图*</span><span class="sxs-lookup"><span data-stu-id="86413-411">*Adding a Delete View*</span></span>
6. <span data-ttu-id="86413-412">删除模板显示模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="86413-412">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="86413-413">将显示仅唱片集的标题。</span><span class="sxs-lookup"><span data-stu-id="86413-413">You will show only the album's title.</span></span> <span data-ttu-id="86413-414">若要执行此操作，请将视图的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="86413-414">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="86413-415">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-415">Task 2 - Running the Application</span></span>

<span data-ttu-id="86413-416">在此任务中，你将测试**StoreManager** **删除**视图页中显示一个确认删除窗体。</span><span class="sxs-lookup"><span data-stu-id="86413-416">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="86413-417">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-417">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-418">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-418">The project starts in the Home page.</span></span> <span data-ttu-id="86413-419">将 URL 更改为**/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="86413-419">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="86413-420">选择要删除通过单击一个相册**删除**并验证是否已上载新视图。</span><span class="sxs-lookup"><span data-stu-id="86413-420">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="86413-421">![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "删除唱片集")</span><span class="sxs-lookup"><span data-stu-id="86413-421">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="86413-422">*删除唱片集*</span><span class="sxs-lookup"><span data-stu-id="86413-422">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="86413-423">任务 3-实现 HTTP POST Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-423">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="86413-424">在此任务中，你将实现将在用户单击时调用的删除操作方法的 HTTP POST 版本**删除**按钮。</span><span class="sxs-lookup"><span data-stu-id="86413-424">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="86413-425">该方法应删除数据库中的唱片集。</span><span class="sxs-lookup"><span data-stu-id="86413-425">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="86413-426">关闭浏览器，如果需要可以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="86413-426">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="86413-427">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="86413-427">Open **StoreManagerController** class.</span></span> <span data-ttu-id="86413-428">若要执行此操作，展开**控制器**文件夹并双击**StoreManagerController.cs**。</span><span class="sxs-lookup"><span data-stu-id="86413-428">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="86413-429">替换**HTTP POST 删除**操作方法代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="86413-429">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="86413-430">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex5 处理删除 HTTP POST 删除操作*)</span><span class="sxs-lookup"><span data-stu-id="86413-430">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="86413-431">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-431">Task 4 - Running the Application</span></span>

<span data-ttu-id="86413-432">在此任务中，你将测试**StoreManager 删除**视图页可让您删除唱片集，然后重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="86413-432">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="86413-433">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-433">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-434">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-434">The project starts in the Home page.</span></span> <span data-ttu-id="86413-435">将 URL 更改为**/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="86413-435">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="86413-436">选择要删除通过单击一个相册**删除。**</span><span class="sxs-lookup"><span data-stu-id="86413-436">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="86413-437">通过单击确认删除**删除**按钮：</span><span class="sxs-lookup"><span data-stu-id="86413-437">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="86413-438">![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "删除唱片集")</span><span class="sxs-lookup"><span data-stu-id="86413-438">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="86413-439">*删除唱片集*</span><span class="sxs-lookup"><span data-stu-id="86413-439">*Deleting an Album*</span></span>
3. <span data-ttu-id="86413-440">验证唱片集中已删除，因为它未出现在**索引**页。</span><span class="sxs-lookup"><span data-stu-id="86413-440">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="86413-441">练习 6： 添加验证</span><span class="sxs-lookup"><span data-stu-id="86413-441">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="86413-442">目前，创建和编辑窗体将不执行任何类型的验证。</span><span class="sxs-lookup"><span data-stu-id="86413-442">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="86413-443">如果用户离开在 price 字段中的必填的字段保留为空或类型字母，则会向您的第一个错误将从数据库中。</span><span class="sxs-lookup"><span data-stu-id="86413-443">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="86413-444">你可以通过将数据注释添加到您的模型类添加到应用程序的验证。</span><span class="sxs-lookup"><span data-stu-id="86413-444">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="86413-445">数据注释允许描述应用于您的模型属性，所需的规则和 ASP.NET MVC 将会负责的实施并向用户显示适当的消息。</span><span class="sxs-lookup"><span data-stu-id="86413-445">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="86413-446">任务 1-添加数据批注</span><span class="sxs-lookup"><span data-stu-id="86413-446">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="86413-447">在此任务中，你将添加到将使创建和编辑页唱片集模型的数据注释显示在适当的时候验证消息。</span><span class="sxs-lookup"><span data-stu-id="86413-447">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="86413-448">对于简单的模型类，添加数据批注仅处理通过添加**使用**语句**System.ComponentModel.DataAnnotation**，然后将放到**[必需]**上适当的属性的属性。</span><span class="sxs-lookup"><span data-stu-id="86413-448">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="86413-449">下面的示例会使**名称**属性视图中的必需字段。</span><span class="sxs-lookup"><span data-stu-id="86413-449">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="86413-450">这是在与此应用程序一样的情况下变得更加复杂实体数据模型生成的位置。</span><span class="sxs-lookup"><span data-stu-id="86413-450">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="86413-451">如果你直接向模型类添加数据注释，如果你从数据库更新模型它们将被覆盖。</span><span class="sxs-lookup"><span data-stu-id="86413-451">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="86413-452">相反，你可以使用元数据的分部类将是为了容纳批注，并且是与模型关联的类使用**[MetadataType]**属性。</span><span class="sxs-lookup"><span data-stu-id="86413-452">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="86413-453">打开**开始**解决方案位于**源/Ex6-AddingValidation/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-453">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="86413-454">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-454">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-455">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-455">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-456">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-456">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-457">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-457">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-458">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-458">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-459">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-459">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-460">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-460">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-461">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-461">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-462">打开**Album.cs**从**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-462">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="86413-463">替换**Album.cs**内容替换为突出显示的代码，以便其类似于下面所示：</span><span class="sxs-lookup"><span data-stu-id="86413-463">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-464">行**[DisplayFormat(ConvertEmptyStringToNull=false)]**指示在数据源中更新数据字段时，将不会从模型的空字符串转换为 null。</span><span class="sxs-lookup"><span data-stu-id="86413-464">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="86413-465">实体框架将 null 值分配给模型之前数据注释验证字段时，此设置将避免异常。</span><span class="sxs-lookup"><span data-stu-id="86413-465">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="86413-466">(代码段- *ASP.NET MVC 4 帮助器、 窗体和验证-Ex6 唱片集元数据分部类*)</span><span class="sxs-lookup"><span data-stu-id="86413-466">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="86413-467">这**唱片集**分部类具有**MetadataType**属性，用于指向**AlbumMetaData**对数据批注的类。</span><span class="sxs-lookup"><span data-stu-id="86413-467">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="86413-468">以下是一些你要用于批注唱片集模型的数据注释属性：</span><span class="sxs-lookup"><span data-stu-id="86413-468">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="86413-469">需要-指示该属性是必填的字段</span><span class="sxs-lookup"><span data-stu-id="86413-469">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="86413-470">DisplayName-定义要在窗体字段以及验证消息上使用的文本</span><span class="sxs-lookup"><span data-stu-id="86413-470">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="86413-471">DisplayFormat-指定显示和格式化数据字段的方式。</span><span class="sxs-lookup"><span data-stu-id="86413-471">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="86413-472">StringLength-定义字符串字段的最大长度</span><span class="sxs-lookup"><span data-stu-id="86413-472">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="86413-473">范围为-为数字字段提供最大和最小值</span><span class="sxs-lookup"><span data-stu-id="86413-473">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="86413-474">ScaffoldColumn-允许隐藏编辑器窗体中的字段</span><span class="sxs-lookup"><span data-stu-id="86413-474">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="86413-475">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="86413-475">Task 2 - Running the Application</span></span>

<span data-ttu-id="86413-476">在此任务中，你将测试的创建和编辑页验证字段，使用选择的最后一个任务中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="86413-476">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="86413-477">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-477">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="86413-478">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-478">The project starts in the Home page.</span></span> <span data-ttu-id="86413-479">将 URL 更改为**/StoreManager/创建**。</span><span class="sxs-lookup"><span data-stu-id="86413-479">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="86413-480">验证是否显示名称匹配的分部类中的 (如**唱片集艺术作品 URL**而不是**AlbumArtUrl**)</span><span class="sxs-lookup"><span data-stu-id="86413-480">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="86413-481">单击**创建**，而不填充窗体。</span><span class="sxs-lookup"><span data-stu-id="86413-481">Click **Create**, without filling the form.</span></span> <span data-ttu-id="86413-482">验证你获取相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="86413-482">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="86413-483">![验证创建页中的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "验证创建页中的字段")</span><span class="sxs-lookup"><span data-stu-id="86413-483">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="86413-484">*在创建页中的已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="86413-484">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="86413-485">你可以验证相同出现**编辑**页。</span><span class="sxs-lookup"><span data-stu-id="86413-485">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="86413-486">将 URL 更改为**/StoreManager/Edit/1**和验证的显示名称与在分部类中的匹配 (如**唱片集艺术作品 URL**而不是**AlbumArtUrl**)。</span><span class="sxs-lookup"><span data-stu-id="86413-486">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="86413-487">空**标题**和**价格**字段，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="86413-487">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="86413-488">验证你获取相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="86413-488">Verify that you get the corresponding validation messages.</span></span>

    ![在编辑页中的已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="86413-490">*在编辑页中的已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="86413-490">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="86413-491">练习 7： 在客户端使用非介入式 jQuery</span><span class="sxs-lookup"><span data-stu-id="86413-491">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="86413-492">在此练习中，你将了解如何启用在客户端的 MVC 4 非介入式 jQuery 验证。</span><span class="sxs-lookup"><span data-stu-id="86413-492">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="86413-493">非介入式 jQuery 使用数据 ajax 前缀 JavaScript 来调用在服务器而不是干扰的方式发出内联客户端脚本的操作方法。</span><span class="sxs-lookup"><span data-stu-id="86413-493">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="86413-494">任务 1-运行应用程序，然后启用非介入式 jQuery</span><span class="sxs-lookup"><span data-stu-id="86413-494">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="86413-495">在此任务中，你将运行应用程序，然后才能比较这两个验证模型包括 jQuery。</span><span class="sxs-lookup"><span data-stu-id="86413-495">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="86413-496">打开**开始**解决方案位于**源/Ex7-UnobtrusivejQueryValidation/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-496">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="86413-497">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="86413-497">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="86413-498">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="86413-498">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86413-499">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86413-499">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="86413-500">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="86413-500">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="86413-501">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86413-501">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86413-502">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="86413-502">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86413-503">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86413-503">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86413-504">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="86413-504">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86413-505">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-505">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="86413-506">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-506">The project starts in the Home page.</span></span> <span data-ttu-id="86413-507">浏览**/StoreManager/创建**单击**创建**而不填充此表单以验证你收到验证消息：</span><span class="sxs-lookup"><span data-stu-id="86413-507">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="86413-508">![禁用的客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "禁用客户端验证")</span><span class="sxs-lookup"><span data-stu-id="86413-508">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="86413-509">*禁用的客户端验证*</span><span class="sxs-lookup"><span data-stu-id="86413-509">*Client validation disabled*</span></span>
4. <span data-ttu-id="86413-510">在浏览器中打开的 HTML 源代码：</span><span class="sxs-lookup"><span data-stu-id="86413-510">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="86413-511">任务 2-启用非介入式客户端验证</span><span class="sxs-lookup"><span data-stu-id="86413-511">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="86413-512">在此任务中，将启用 jQuery**非介入式客户端验证**从**Web.config**文件，它是默认情况下设置为 false 在所有新的 ASP.NET MVC 4 项目中。</span><span class="sxs-lookup"><span data-stu-id="86413-512">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="86413-513">此外，你将添加所需的脚本引用，以使 jQuery 非介入式客户端验证工作。</span><span class="sxs-lookup"><span data-stu-id="86413-513">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="86413-514">打开**Web.Config**文件在项目根目录位置，并确保**ClientValidationEnabled**和**UnobtrusiveJavaScriptEnabled**密钥值设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="86413-514">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="86413-515">此外可以通过在 Global.asax.cs 以获得相同的结果代码来启用客户端验证：</span><span class="sxs-lookup"><span data-stu-id="86413-515">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="86413-516">**HtmlHelper.ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="86413-516">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="86413-517">此外，你可以插入任何控制器具有自定义行为分配 ClientValidationEnabled 特性。</span><span class="sxs-lookup"><span data-stu-id="86413-517">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="86413-518">打开**Create.cshtml**在**Views\StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="86413-518">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="86413-519">下面的脚本文件，请确保**jquery.validate**和**jquery.validate.unobtrusive**中视图按, 引用&quot; **~/bundles/jqueryval**&quot;捆绑包。</span><span class="sxs-lookup"><span data-stu-id="86413-519">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view throught the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="86413-520">所有这些 jQuery 库包含在 MVC 4 中的新项目。</span><span class="sxs-lookup"><span data-stu-id="86413-520">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="86413-521">你可以找到更多库中的**/脚本**你项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="86413-521">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="86413-522">为了使此验证的库工作，你需要添加对 jQuery framework 库的引用。</span><span class="sxs-lookup"><span data-stu-id="86413-522">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="86413-523">由于已在添加此引用 **\_Layout.cshtml**文件，则你不需要将其添加此特定的视图中。</span><span class="sxs-lookup"><span data-stu-id="86413-523">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="86413-524">任务 3-运行应用程序使用非介入式 jQuery 验证</span><span class="sxs-lookup"><span data-stu-id="86413-524">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="86413-525">在此任务中，你将测试**StoreManager**创建模板执行客户端验证使用 jQuery 库，当用户创建新唱片集的视图。</span><span class="sxs-lookup"><span data-stu-id="86413-525">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="86413-526">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="86413-526">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="86413-527">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="86413-527">The project starts in the Home page.</span></span> <span data-ttu-id="86413-528">浏览**/StoreManager/创建**单击**创建**而不填充此表单以验证你收到验证消息：</span><span class="sxs-lookup"><span data-stu-id="86413-528">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="86413-529">![使用 jQuery 启用的客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "使用 jQuery 启用的客户端验证")</span><span class="sxs-lookup"><span data-stu-id="86413-529">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="86413-530">*使用 jQuery 启用的客户端验证*</span><span class="sxs-lookup"><span data-stu-id="86413-530">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="86413-531">在浏览器中，打开创建视图的源代码:</span><span class="sxs-lookup"><span data-stu-id="86413-531">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

    > [!NOTE]
    > <span data-ttu-id="86413-532">对于每个客户端验证规则，非介入式 jQuery 添加具有数据的属性-val-*rulename*=&quot;*消息*&quot;。</span><span class="sxs-lookup"><span data-stu-id="86413-532">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="86413-533">下面是标记列表该 Unobtrusive jQuery 将插入到要执行客户端验证的 html 输入字段：</span><span class="sxs-lookup"><span data-stu-id="86413-533">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
    > 
    > - <span data-ttu-id="86413-534">数据 val</span><span class="sxs-lookup"><span data-stu-id="86413-534">Data-val</span></span>
    > - <span data-ttu-id="86413-535">Data-val-number</span><span class="sxs-lookup"><span data-stu-id="86413-535">Data-val-number</span></span>
    > - <span data-ttu-id="86413-536">数据 val 范围</span><span class="sxs-lookup"><span data-stu-id="86413-536">Data-val-range</span></span>
    > - <span data-ttu-id="86413-537">数据 val-范围最小/最大数据 val 范围</span><span class="sxs-lookup"><span data-stu-id="86413-537">Data-val-range-min / Data-val-range-max</span></span>
    > - <span data-ttu-id="86413-538">Data-val-required</span><span class="sxs-lookup"><span data-stu-id="86413-538">Data-val-required</span></span>
    > - <span data-ttu-id="86413-539">数据 val 长度</span><span class="sxs-lookup"><span data-stu-id="86413-539">Data-val-length</span></span>
    > - <span data-ttu-id="86413-540">数据 val-长度最大/最小数据 val 长度</span><span class="sxs-lookup"><span data-stu-id="86413-540">Data-val-length-max / Data-val-length-min</span></span>
    > 
    > <span data-ttu-id="86413-541">所有数据值将都填入模型**数据注释**。</span><span class="sxs-lookup"><span data-stu-id="86413-541">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="86413-542">然后，可以在客户端运行在服务器端工作的所有逻辑。</span><span class="sxs-lookup"><span data-stu-id="86413-542">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="86413-543">例如，价格特性具有以下数据注释在模型中：</span><span class="sxs-lookup"><span data-stu-id="86413-543">For example, Price attribute has the following data annotation in the model:</span></span>
    > 
    > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
    > 
    > <span data-ttu-id="86413-544">使用非介入式 jQuery 后, 生成的代码为：</span><span class="sxs-lookup"><span data-stu-id="86413-544">After using Unobtrusive jQuery, the generated code is:</span></span>
    >  
    > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="86413-545">摘要</span><span class="sxs-lookup"><span data-stu-id="86413-545">Summary</span></span>

<span data-ttu-id="86413-546">通过完成本动手实验中，你已了解如何使用户能够更改带有以下使用的数据库中存储的数据：</span><span class="sxs-lookup"><span data-stu-id="86413-546">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="86413-547">控制器操作如索引，创建、 编辑、 删除</span><span class="sxs-lookup"><span data-stu-id="86413-547">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="86413-548">ASP.NET MVC 基架功能用于 HTML 表中显示属性</span><span class="sxs-lookup"><span data-stu-id="86413-548">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="86413-549">自定义 HTML 帮助器以改进用户体验</span><span class="sxs-lookup"><span data-stu-id="86413-549">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="86413-550">响应 HTTP GET 或 HTTP POST 调用的操作方法</span><span class="sxs-lookup"><span data-stu-id="86413-550">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="86413-551">类似的视图模板，如创建和编辑共享的编辑器模板</span><span class="sxs-lookup"><span data-stu-id="86413-551">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="86413-552">窗体元素，如下拉列表</span><span class="sxs-lookup"><span data-stu-id="86413-552">Form elements like drop-downs</span></span>
- <span data-ttu-id="86413-553">模型验证的数据批注</span><span class="sxs-lookup"><span data-stu-id="86413-553">Data annotations for Model validation</span></span>
- <span data-ttu-id="86413-554">使用 jQuery 非介入式库的客户端验证</span><span class="sxs-lookup"><span data-stu-id="86413-554">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="86413-555">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="86413-555">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="86413-556">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="86413-556">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="86413-557">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="86413-557">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="86413-558">转到[ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="86413-558">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="86413-559">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; *Visual Studio Express 2012 for Web 的 Windows Azure SDK*&quot;。</span><span class="sxs-lookup"><span data-stu-id="86413-559">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="86413-560">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="86413-560">Click on **Install Now**.</span></span> <span data-ttu-id="86413-561">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="86413-561">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="86413-562">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="86413-562">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="86413-563">![安装 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="86413-563">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="86413-564">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="86413-564">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="86413-565">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="86413-565">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="86413-567">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="86413-567">*Accepting the license terms*</span></span>
5. <span data-ttu-id="86413-568">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="86413-568">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="86413-570">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="86413-570">*Installation progress*</span></span>
6. <span data-ttu-id="86413-571">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="86413-571">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="86413-573">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="86413-573">*Installation completed*</span></span>
7. <span data-ttu-id="86413-574">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="86413-574">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="86413-575">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="86413-575">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="86413-577">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="86413-577">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="86413-578">附录 b： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="86413-578">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="86413-579">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="86413-579">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="86413-580">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="86413-580">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="86413-581">![使用 Visual Studio 代码段将代码插入到你的项目](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="86413-581">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="86413-582">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="86413-582">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="86413-583">***若要添加代码片段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="86413-583">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="86413-584">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="86413-584">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="86413-585">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="86413-585">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="86413-586">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="86413-586">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="86413-587">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="86413-587">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="86413-588">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="86413-588">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="86413-589">![开始键入代码段名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="86413-589">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="86413-590">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="86413-590">*Start typing the snippet name*</span></span>

<span data-ttu-id="86413-591">![按 Tab 以选择突出显示代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="86413-591">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="86413-592">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="86413-592">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="86413-593">![再次按 Tab 和代码段将会扩展](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="86413-593">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="86413-594">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="86413-594">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="86413-595">***若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="86413-595">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="86413-596">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="86413-596">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="86413-597">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="86413-597">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="86413-598">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="86413-598">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="86413-599">![右键单击你想要插入代码段，并选择插入代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="86413-599">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="86413-600">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="86413-600">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="86413-601">![通过单击它选取列表中中的相关代码片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="86413-601">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="86413-602">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="86413-602">*Pick the relevant snippet from the list, by clicking on it*</span></span>
