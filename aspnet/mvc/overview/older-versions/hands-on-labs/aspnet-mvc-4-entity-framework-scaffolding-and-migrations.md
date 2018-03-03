---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: "ASP.NET MVC 4 实体框架基架和迁移 |Microsoft 文档"
author: rick-anderson
description: "如果你熟悉 ASP.NET MVC 4 控制器方法，或已完成&quot;帮助器、 窗体和验证&quot;动手实验中，你应注意..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 396859463446d95c58271c4b00fc950bcd0d539a
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="46300-103">ASP.NET MVC 4 实体框架基架和迁移</span><span class="sxs-lookup"><span data-stu-id="46300-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="46300-104">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="46300-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="46300-105">下载 Web 营地培训工具包</span><span class="sxs-lookup"><span data-stu-id="46300-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="46300-106">如果你熟悉 ASP.NET MVC 4 控制器方法，或已完成&quot;帮助器、 窗体和验证&quot;动手实验中，你应注意的逻辑来创建，许多更新、 列出和删除它重复任何数据实体在应用程序。</span><span class="sxs-lookup"><span data-stu-id="46300-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="46300-107">更不必说，如果你的模型具有多个类来处理，你将可能花费相当长的时间编写 POST 和 GET 操作方法的每个实体操作，以及每个视图。</span><span class="sxs-lookup"><span data-stu-id="46300-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="46300-108">在此实验将了解如何使用 ASP.NET MVC 4 基架来自动生成的应用程序的 CRUD （创建、 读取、 更新和删除） 的基线。</span><span class="sxs-lookup"><span data-stu-id="46300-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="46300-109">启动从一个简单的模型类，，和而无需编写一行代码，将创建一个控制器，将包含所有的 CRUD 操作，以及所有必要视图。</span><span class="sxs-lookup"><span data-stu-id="46300-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="46300-110">生成并运行简单的解决方案后, 您将拥有生成的 MVC 逻辑和数据操作的视图一起应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="46300-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="46300-111">此外，你将了解如何轻松地使用 Entity Framework 迁移来执行整个应用程序中的模型更新。</span><span class="sxs-lookup"><span data-stu-id="46300-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="46300-112">Entity Framework 迁移将让你修改你的数据库后的模型已更改简单的步骤。</span><span class="sxs-lookup"><span data-stu-id="46300-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="46300-113">与所有这些记住，将能够构建和维护 web 应用程序更有效地利用 ASP.NET MVC 4 的最新功能。</span><span class="sxs-lookup"><span data-stu-id="46300-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="46300-114">所有的示例代码和代码段都包含在 Web 营地培训工具包，可从在[Microsoft 的 Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="46300-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="46300-115">特定于此实验室项目位于[ASP.NET MVC 4 实体框架基架和迁移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)。</span><span class="sxs-lookup"><span data-stu-id="46300-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="46300-116">目标</span><span class="sxs-lookup"><span data-stu-id="46300-116">Objectives</span></span>

<span data-ttu-id="46300-117">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="46300-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="46300-118">使用 ASP.NET 基架的控制器中的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="46300-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="46300-119">更改使用 Entity Framework 迁移的数据库模型。</span><span class="sxs-lookup"><span data-stu-id="46300-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="46300-120">系统必备</span><span class="sxs-lookup"><span data-stu-id="46300-120">Prerequisites</span></span>

<span data-ttu-id="46300-121">你必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="46300-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="46300-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="46300-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="46300-123">安装</span><span class="sxs-lookup"><span data-stu-id="46300-123">Setup</span></span>

<span data-ttu-id="46300-124">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="46300-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="46300-125">为方便起见，你将沿此实验室管理大部分都是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="46300-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="46300-126">若要安装运行的代码段**.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="46300-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="46300-127">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 b： 使用代码段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="46300-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="46300-128">练习</span><span class="sxs-lookup"><span data-stu-id="46300-128">Exercises</span></span>

<span data-ttu-id="46300-129">下面的练习构成此动手实验：</span><span class="sxs-lookup"><span data-stu-id="46300-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="46300-130">ASP.NET MVC 4 基架使用 Entity Framework 迁移</span><span class="sxs-lookup"><span data-stu-id="46300-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="46300-131">本练习伴随**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="46300-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="46300-132">如果你需要通过练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="46300-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>


<span data-ttu-id="46300-133">估计时间来完成该实验： **30 分钟**</span><span class="sxs-lookup"><span data-stu-id="46300-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="46300-134">练习 1： 将 ASP.NET MVC 4 基架使用 Entity Framework 迁移</span><span class="sxs-lookup"><span data-stu-id="46300-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="46300-135">ASP.NET MVC 基架提供创建必要的逻辑，可让你的应用程序与数据库层进行交互的标准化方式中生成的 CRUD 操作的快速方法。</span><span class="sxs-lookup"><span data-stu-id="46300-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="46300-136">在本练习中，您将学习如何使用 ASP.NET MVC 4 基架代码首先创建 CRUD 方法。</span><span class="sxs-lookup"><span data-stu-id="46300-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="46300-137">然后，你将了解如何更新模型来使用 Entity Framework 迁移应用在数据库中的更改。</span><span class="sxs-lookup"><span data-stu-id="46300-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="46300-138">任务 1-创建新的 ASP.NET MVC 4 项目使用基架</span><span class="sxs-lookup"><span data-stu-id="46300-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="46300-139">如果尚未打开，启动**Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="46300-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="46300-140">选择**文件 |新项目**。</span><span class="sxs-lookup"><span data-stu-id="46300-140">Select **File | New Project**.</span></span> <span data-ttu-id="46300-141">在新建项目对话框中下, **Visual C# |Web**部分中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="46300-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="46300-142">命名项目**MVC4andEFMigrations**并将位置设置为**Source\Ex1 UsingMVC4ScaffoldingEFMigrations**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="46300-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="46300-143">设置**解决方案名称**到**开始**并确保**创建解决方案的目录**已选中。</span><span class="sxs-lookup"><span data-stu-id="46300-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="46300-144">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="46300-144">Click **OK**.</span></span>

    <span data-ttu-id="46300-145">![新的 ASP.NET MVC 4 项目对话框](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "新建 ASP.NET MVC 4 项目对话框")</span><span class="sxs-lookup"><span data-stu-id="46300-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="46300-146">*新的 ASP.NET MVC 4 项目对话框*</span><span class="sxs-lookup"><span data-stu-id="46300-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="46300-147">在**新建 ASP.NET MVC 4 项目**对话框框中，选择**Internet 应用程序**模板，并确保**Razor**是所选**视图引擎**.</span><span class="sxs-lookup"><span data-stu-id="46300-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="46300-148">单击**确定**以创建该项目。</span><span class="sxs-lookup"><span data-stu-id="46300-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="46300-149">![新的 ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新的 ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="46300-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="46300-150">*新的 ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="46300-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="46300-151">在解决方案资源管理器，右键单击**模型**和选择**添加 |类**创建简单的类人员 (POCO)。</span><span class="sxs-lookup"><span data-stu-id="46300-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="46300-152">将其命名为**人员**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="46300-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="46300-153">打开 Person 类并插入以下属性。</span><span class="sxs-lookup"><span data-stu-id="46300-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="46300-154">(代码段- *ASP.NET MVC 4 和 Entity Framework 迁移-Ex1 人员属性*)</span><span class="sxs-lookup"><span data-stu-id="46300-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="46300-155">单击**生成 |生成解决方案**以保存所做的更改并生成项目。</span><span class="sxs-lookup"><span data-stu-id="46300-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="46300-156">![生成应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "生成应用程序")</span><span class="sxs-lookup"><span data-stu-id="46300-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="46300-157">*生成应用程序*</span><span class="sxs-lookup"><span data-stu-id="46300-157">*Building the Application*</span></span>
7. <span data-ttu-id="46300-158">在解决方案资源管理器，右键单击 controllers 文件夹，然后选择**添加 |控制器**。</span><span class="sxs-lookup"><span data-stu-id="46300-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="46300-159">控制器*PersonController*并完成**基架选项**使用以下值。</span><span class="sxs-lookup"><span data-stu-id="46300-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

    1. <span data-ttu-id="46300-160">在**模板**下拉列表中，选择**具有读/写操作和视图使用 Entity Framework 的 MVC 控制器**选项。</span><span class="sxs-lookup"><span data-stu-id="46300-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
    2. <span data-ttu-id="46300-161">在**模型类**下拉列表中，选择**人员**类。</span><span class="sxs-lookup"><span data-stu-id="46300-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
    3. <span data-ttu-id="46300-162">在**数据上下文类**列表中，选择**&lt;新建数据上下文...&gt;**.</span><span class="sxs-lookup"><span data-stu-id="46300-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="46300-163">选择任何名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="46300-163">Choose any name and click **OK**.</span></span>
    4. <span data-ttu-id="46300-164">在**视图**下拉列表中，请确保**Razor**选择。</span><span class="sxs-lookup"><span data-stu-id="46300-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

    <span data-ttu-id="46300-165">![添加基架的人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "添加基架的人员控制器")</span><span class="sxs-lookup"><span data-stu-id="46300-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

    <span data-ttu-id="46300-166">*添加基架的人员控制器*</span><span class="sxs-lookup"><span data-stu-id="46300-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="46300-167">单击**添加**使用基架的个人创建新的控制器。</span><span class="sxs-lookup"><span data-stu-id="46300-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="46300-168">您现在已生成的控制器操作以及视图。</span><span class="sxs-lookup"><span data-stu-id="46300-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="46300-169">![之后使用基架创建人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "后使用基架创建人员控制器")</span><span class="sxs-lookup"><span data-stu-id="46300-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="46300-170">*之后使用基架创建人员控制器*</span><span class="sxs-lookup"><span data-stu-id="46300-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="46300-171">打开**PersonController**类。</span><span class="sxs-lookup"><span data-stu-id="46300-171">Open **PersonController** class.</span></span> <span data-ttu-id="46300-172">请注意自动生成完整的 CRUD 操作方法。</span><span class="sxs-lookup"><span data-stu-id="46300-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

    <span data-ttu-id="46300-173">![内部人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "内部人员控制器")</span><span class="sxs-lookup"><span data-stu-id="46300-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

    <span data-ttu-id="46300-174">*内部人员控制器*</span><span class="sxs-lookup"><span data-stu-id="46300-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="46300-175">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="46300-175">Task 2- Running the application</span></span>

<span data-ttu-id="46300-176">此时，将不创建数据库。</span><span class="sxs-lookup"><span data-stu-id="46300-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="46300-177">在此任务中，将运行的应用程序第一次，并测试的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="46300-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="46300-178">将使用 Code First 动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="46300-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="46300-179">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="46300-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="46300-180">在浏览器中，添加**/Person**到 URL 以打开人员页。</span><span class="sxs-lookup"><span data-stu-id="46300-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="46300-181">![首次运行的应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "首次运行的应用程序")</span><span class="sxs-lookup"><span data-stu-id="46300-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="46300-182">*首次运行应用程序：*</span><span class="sxs-lookup"><span data-stu-id="46300-182">*Application: first run*</span></span>
3. <span data-ttu-id="46300-183">现在，你将浏览人员页和测试的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="46300-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="46300-184">单击**新建**以添加新成员。</span><span class="sxs-lookup"><span data-stu-id="46300-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="46300-185">输入名字和姓氏，然后单击**创建**。</span><span class="sxs-lookup"><span data-stu-id="46300-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="46300-186">![添加新人员](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "添加新的用户")</span><span class="sxs-lookup"><span data-stu-id="46300-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="46300-187">*添加新的用户*</span><span class="sxs-lookup"><span data-stu-id="46300-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="46300-188">在用户的列表中，你可以删除、 编辑或添加项。</span><span class="sxs-lookup"><span data-stu-id="46300-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="46300-189">![用户列表](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "用户列表")</span><span class="sxs-lookup"><span data-stu-id="46300-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="46300-190">*用户列表*</span><span class="sxs-lookup"><span data-stu-id="46300-190">*Person list*</span></span>
    3. <span data-ttu-id="46300-191">单击**详细信息**以打开该人员的详细信息。</span><span class="sxs-lookup"><span data-stu-id="46300-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="46300-192">![人员的详细信息](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人员的详细信息")</span><span class="sxs-lookup"><span data-stu-id="46300-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="46300-193">*人员的详细信息*</span><span class="sxs-lookup"><span data-stu-id="46300-193">*Person's details*</span></span>
4. <span data-ttu-id="46300-194">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="46300-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="46300-195">请注意，你已创建了人员实体整个 CRUD 整个-从到视图模型的应用程序而无需编写一行代码 ！</span><span class="sxs-lookup"><span data-stu-id="46300-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="46300-196">任务 3-更新使用 Entity Framework 迁移的数据库</span><span class="sxs-lookup"><span data-stu-id="46300-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="46300-197">在此任务将更新使用 Entity Framework 迁移的数据库。</span><span class="sxs-lookup"><span data-stu-id="46300-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="46300-198">你会发现来更改模型和通过使用 Entity Framework 迁移功能反映数据库中的更改是多么容易。</span><span class="sxs-lookup"><span data-stu-id="46300-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="46300-199">打开程序包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="46300-199">Open the Package Manager Console.</span></span> <span data-ttu-id="46300-200">选择**工具 |库包管理器 |程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="46300-200">Select **Tools | Library Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="46300-201">在程序包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="46300-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="46300-202">PMC</span><span class="sxs-lookup"><span data-stu-id="46300-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="46300-203">![启用迁移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "启用迁移")</span><span class="sxs-lookup"><span data-stu-id="46300-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="46300-204">*启用迁移*</span><span class="sxs-lookup"><span data-stu-id="46300-204">*Enabling migrations*</span></span>

    <span data-ttu-id="46300-205">启用迁移命令创建**迁移**文件夹，其中包含用于初始化数据库的脚本。</span><span class="sxs-lookup"><span data-stu-id="46300-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="46300-206">![迁移文件夹](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations 文件夹")</span><span class="sxs-lookup"><span data-stu-id="46300-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="46300-207">*迁移文件夹*</span><span class="sxs-lookup"><span data-stu-id="46300-207">*Migrations folder*</span></span>
3. <span data-ttu-id="46300-208">打开**Configuration.cs** Migrations 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="46300-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="46300-209">找到的类构造函数并将更改**AutomaticMigrationsEnabled**值赋给*true*。</span><span class="sxs-lookup"><span data-stu-id="46300-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>


    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="46300-210">打开 Person 类并添加人员的中间名属性。</span><span class="sxs-lookup"><span data-stu-id="46300-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="46300-211">使用此新的属性，您在更改模型。</span><span class="sxs-lookup"><span data-stu-id="46300-211">With this new attribute, you are changing the model.</span></span>


    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="46300-212">选择**生成 |生成解决方案**上生成应用程序的菜单。</span><span class="sxs-lookup"><span data-stu-id="46300-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="46300-213">![生成应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "生成应用程序")</span><span class="sxs-lookup"><span data-stu-id="46300-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="46300-214">*生成应用程序*</span><span class="sxs-lookup"><span data-stu-id="46300-214">*Building the application*</span></span>
6. <span data-ttu-id="46300-215">在程序包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="46300-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="46300-216">PMC</span><span class="sxs-lookup"><span data-stu-id="46300-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="46300-217">此命令将会查找在对象的数据，更改，然后，它将添加必要的命令来相应地修改数据库。</span><span class="sxs-lookup"><span data-stu-id="46300-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="46300-218">![添加中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "添加中间名")</span><span class="sxs-lookup"><span data-stu-id="46300-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="46300-219">*添加中间名*</span><span class="sxs-lookup"><span data-stu-id="46300-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="46300-220">（可选）你可以运行以下命令以生成一个包含差异的更新的 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="46300-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="46300-221">这将允许你手动更新数据库 （在这种情况下它不需要），或应用中其他数据库的更改：</span><span class="sxs-lookup"><span data-stu-id="46300-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="46300-222">PMC</span><span class="sxs-lookup"><span data-stu-id="46300-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="46300-223">![生成 SQL 脚本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "生成 SQL 脚本")</span><span class="sxs-lookup"><span data-stu-id="46300-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="46300-224">*生成 SQL 脚本*</span><span class="sxs-lookup"><span data-stu-id="46300-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="46300-225">![SQL 脚本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 脚本更新")</span><span class="sxs-lookup"><span data-stu-id="46300-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="46300-226">*SQL 脚本更新*</span><span class="sxs-lookup"><span data-stu-id="46300-226">*SQL Script update*</span></span>
8. <span data-ttu-id="46300-227">在程序包管理器控制台中，输入以下命令以更新数据库：</span><span class="sxs-lookup"><span data-stu-id="46300-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="46300-228">PMC</span><span class="sxs-lookup"><span data-stu-id="46300-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="46300-229">![更新数据库](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新数据库")</span><span class="sxs-lookup"><span data-stu-id="46300-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="46300-230">*更新数据库*</span><span class="sxs-lookup"><span data-stu-id="46300-230">*Updating the Database*</span></span>

    <span data-ttu-id="46300-231">这将添加**MiddleName**中的列**人员**表以匹配的当前定义**人员**类。</span><span class="sxs-lookup"><span data-stu-id="46300-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="46300-232">更新数据库时，右键单击控制器文件夹，然后选择**添加 |控制器**人员将控制器添加再次 （具有相同值的完成）。</span><span class="sxs-lookup"><span data-stu-id="46300-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="46300-233">这将更新的现有方法和添加新属性的视图。</span><span class="sxs-lookup"><span data-stu-id="46300-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="46300-234">![添加控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "添加控制器更新")</span><span class="sxs-lookup"><span data-stu-id="46300-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="46300-235">*更新控制器*</span><span class="sxs-lookup"><span data-stu-id="46300-235">*Updating the controller*</span></span>
10. <span data-ttu-id="46300-236">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="46300-236">Click **Add**.</span></span> <span data-ttu-id="46300-237">然后，选择值**覆盖 PersonController.cs**和**覆盖关联视图**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="46300-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

    ![添加控制器覆盖](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

    <span data-ttu-id="46300-239">*更新控制器*</span><span class="sxs-lookup"><span data-stu-id="46300-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="46300-240">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="46300-240">Task4- Running the application</span></span>

1. <span data-ttu-id="46300-241">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="46300-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="46300-242">打开**/Person**。</span><span class="sxs-lookup"><span data-stu-id="46300-242">Open **/Person**.</span></span> <span data-ttu-id="46300-243">请注意已保留的数据时的中间名列已添加。</span><span class="sxs-lookup"><span data-stu-id="46300-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="46300-244">![添加的中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "添加的中间名")</span><span class="sxs-lookup"><span data-stu-id="46300-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="46300-245">*添加的中间名*</span><span class="sxs-lookup"><span data-stu-id="46300-245">*Middle Name added*</span></span>
3. <span data-ttu-id="46300-246">如果你单击**编辑**，你将能够将中间名添加到当前的人员。</span><span class="sxs-lookup"><span data-stu-id="46300-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="46300-247">![中间名版本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中间名版本")</span><span class="sxs-lookup"><span data-stu-id="46300-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="46300-248">摘要</span><span class="sxs-lookup"><span data-stu-id="46300-248">Summary</span></span>

<span data-ttu-id="46300-249">在此动手实验中，你学习了简单的步骤，使用 ASP.NET MVC 4 基架使用任何模型类创建 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="46300-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="46300-250">然后，你已学习如何使用 Entity Framework 迁移-从数据库到视图的应用程序中执行的端到端更新。</span><span class="sxs-lookup"><span data-stu-id="46300-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="46300-251">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="46300-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="46300-252">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="46300-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="46300-253">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="46300-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="46300-254">转到[ [https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="46300-254">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="46300-255">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; *Visual Studio Express 2012 for Web 的 Windows Azure SDK*&quot;。</span><span class="sxs-lookup"><span data-stu-id="46300-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="46300-256">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="46300-256">Click on **Install Now**.</span></span> <span data-ttu-id="46300-257">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="46300-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="46300-258">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="46300-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="46300-259">![安装 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="46300-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="46300-260">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="46300-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="46300-261">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="46300-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="46300-263">接受许可条款</span><span class="sxs-lookup"><span data-stu-id="46300-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="46300-264">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="46300-264">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="46300-266">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="46300-266">*Installation progress*</span></span>
6. <span data-ttu-id="46300-267">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="46300-267">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="46300-269">安装已完成</span><span class="sxs-lookup"><span data-stu-id="46300-269">*Installation completed*</span></span>
7. <span data-ttu-id="46300-270">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="46300-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="46300-271">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="46300-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="46300-273">Web 磁贴的 VS Express</span><span class="sxs-lookup"><span data-stu-id="46300-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="46300-274">附录 b： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="46300-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="46300-275">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="46300-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="46300-276">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="46300-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="46300-277">![使用 Visual Studio 代码段将代码插入到你的项目](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="46300-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="46300-278">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="46300-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="46300-279">***若要添加代码片段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="46300-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="46300-280">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="46300-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="46300-281">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="46300-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="46300-282">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="46300-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="46300-283">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="46300-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="46300-284">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="46300-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="46300-285">![开始键入代码段名称](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="46300-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="46300-286">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="46300-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="46300-287">![按 Tab 以选择突出显示代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="46300-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="46300-288">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="46300-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="46300-289">![再次按 Tab 和代码段将会扩展](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="46300-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="46300-290">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="46300-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="46300-291">***若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="46300-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="46300-292">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="46300-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="46300-293">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="46300-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="46300-294">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="46300-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="46300-295">![右键单击你想要插入代码段，并选择插入代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="46300-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="46300-296">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="46300-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="46300-297">![通过单击它选取列表中中的相关代码片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="46300-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="46300-298">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="46300-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
