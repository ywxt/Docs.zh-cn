---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和数据访问 |Microsoft Docs
author: rick-anderson
description: 注意： 此动手实验假定你的 ASP.NET MVC 基础知识。 如果你未使用过 ASP.NET MVC 之前，我们建议你通过 ASP.NET MVC 4...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 26896e6ee3c02e8f939296ecbfb8b7d500940765
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825278"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="63bbe-104">ASP.NET MVC 4 模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="63bbe-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="63bbe-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="63bbe-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="63bbe-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="63bbe-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="63bbe-107">此动手实验假定你已了解的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="63bbe-108">如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 4 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="63bbe-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="63bbe-109">此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。</span><span class="sxs-lookup"><span data-stu-id="63bbe-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-110">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="63bbe-111">特定于此实验室项目位于[ASP.NET MVC 4 模型和数据访问](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="63bbe-112">在中**ASP.NET MVC 基础知识**动手实验中，您已经传递了硬编码数据从控制器到视图模板。</span><span class="sxs-lookup"><span data-stu-id="63bbe-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="63bbe-113">但是，若要生成实际的 Web 应用程序，你可能想要使用的实际数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="63bbe-114">此动手实验室将演示如何为使用数据库引擎，以便存储和检索音乐应用商店应用程序所需的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="63bbe-115">若要完成此操作，将启动使用现有的数据库并从中创建实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="63bbe-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="63bbe-116">在此实验中，将满足**Database First**方法并将**Code First**方法。</span><span class="sxs-lookup"><span data-stu-id="63bbe-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="63bbe-117">但是，还可以使用**Model First**方法，创建相同的模型使用的工具，然后从其生成数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="63bbe-118">![数据库第一个 vs。模型优先](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs。模型优先")</span><span class="sxs-lookup"><span data-stu-id="63bbe-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="63bbe-119">*数据库第一个 vs。模型优先*</span><span class="sxs-lookup"><span data-stu-id="63bbe-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="63bbe-120">生成模型之后, 将 StoreController 存储视图提供从数据库中，而不是使用硬编码数据中获取的数据中进行适当调整。</span><span class="sxs-lookup"><span data-stu-id="63bbe-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="63bbe-121">不需要对进行任何更改视图模板由于 StoreController 将返回相同的 Viewmodel 对视图模板中，尽管这一次的数据将来自该数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="63bbe-122">**代码第一种方法**</span><span class="sxs-lookup"><span data-stu-id="63bbe-122">**The Code First Approach**</span></span>

<span data-ttu-id="63bbe-123">代码第一种方法允许我们定义的代码模型而不会生成通常结合了框架的类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="63bbe-124">在代码中首先，模型对象定义 Poco，与&quot;Plain Old CLR Objects&quot;。</span><span class="sxs-lookup"><span data-stu-id="63bbe-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="63bbe-125">Poco 是简单的普通类不继承并不实现接口。</span><span class="sxs-lookup"><span data-stu-id="63bbe-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="63bbe-126">我们可以自动生成数据库，从它们，也可以使用现有数据库并从代码生成的类映射。</span><span class="sxs-lookup"><span data-stu-id="63bbe-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="63bbe-127">使用此方法的好处是模型仍独立于持久性框架 （在本例中为实体框架），与 Poco 类不结合映射框架。</span><span class="sxs-lookup"><span data-stu-id="63bbe-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-128">此实验室基于 ASP.NET MVC 4 和音乐应用商店示例应用程序的版本自定义和最小化以适合仅在此动手实验中所示的功能。</span><span class="sxs-lookup"><span data-stu-id="63bbe-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="63bbe-129">如果你想要浏览整个**音乐应用商店**教程应用程序可以找到它在[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="63bbe-130">系统必备</span><span class="sxs-lookup"><span data-stu-id="63bbe-130">Prerequisites</span></span>

<span data-ttu-id="63bbe-131">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="63bbe-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="63bbe-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="63bbe-133">安装</span><span class="sxs-lookup"><span data-stu-id="63bbe-133">Setup</span></span>

<span data-ttu-id="63bbe-134">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="63bbe-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="63bbe-135">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="63bbe-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="63bbe-136">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="63bbe-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="63bbe-137">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="63bbe-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="63bbe-138">练习</span><span class="sxs-lookup"><span data-stu-id="63bbe-138">Exercises</span></span>

<span data-ttu-id="63bbe-139">此动手实验包含由以下练习：</span><span class="sxs-lookup"><span data-stu-id="63bbe-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="63bbe-140">练习 1： 添加数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="63bbe-141">练习 2： 创建使用 Code First 数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="63bbe-142">练习 3： 查询具有参数的数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="63bbe-143">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="63bbe-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="63bbe-144">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="63bbe-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="63bbe-145">估计的时间才能完成此实验： **35 だ 牧**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="63bbe-146">练习 1： 添加数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="63bbe-147">在此练习中，您将学习如何添加具有 MusicStore 应用程序，向解决方案以便使用其数据的表的数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="63bbe-148">一旦使用该模型生成数据库并将其添加到解决方案中，将修改 StoreController 类，以查看模板提供从数据库中，而不是使用硬编码的值中获取的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="63bbe-149">任务 1-添加数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="63bbe-150">在本任务中，您将添加到解决方案 MusicStore 应用程序的主表已创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="63bbe-151">打开**开始**解决方案位于**源/Ex1-AddingADatabaseDBFirst/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="63bbe-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="63bbe-152">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="63bbe-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="63bbe-153">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="63bbe-154">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="63bbe-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="63bbe-155">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="63bbe-156">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="63bbe-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="63bbe-157">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="63bbe-158">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="63bbe-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="63bbe-159">添加**MvcMusicStore**数据库文件。</span><span class="sxs-lookup"><span data-stu-id="63bbe-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="63bbe-160">在本动手实验中，你将使用名为已创建的数据库**MvcMusicStore.mdf**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="63bbe-161">为此，请右键单击**应用程序\_数据**文件夹，指向**添加**，然后单击**现有项**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="63bbe-162">浏览到**\Source\Assets** ，然后选择**MvcMusicStore.mdf**文件。</span><span class="sxs-lookup"><span data-stu-id="63bbe-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="63bbe-163">![添加现有项目](aspnet-mvc-4-models-and-data-access/_static/image2.png "添加现有项目")</span><span class="sxs-lookup"><span data-stu-id="63bbe-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="63bbe-164">*添加现有项目*</span><span class="sxs-lookup"><span data-stu-id="63bbe-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="63bbe-165">![MvcMusicStore.mdf 数据库文件](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 数据库文件")</span><span class="sxs-lookup"><span data-stu-id="63bbe-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="63bbe-166">*MvcMusicStore.mdf 数据库文件*</span><span class="sxs-lookup"><span data-stu-id="63bbe-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="63bbe-167">数据库已添加到项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-167">The database has been added to the project.</span></span> <span data-ttu-id="63bbe-168">即使数据库所在的解决方案内，可以查询和更新它，因为它托管在不同的数据库服务器中。</span><span class="sxs-lookup"><span data-stu-id="63bbe-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="63bbe-169">![在解决方案资源管理器中的 MvcMusicStore 数据库](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore 数据库在解决方案资源管理器")</span><span class="sxs-lookup"><span data-stu-id="63bbe-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="63bbe-170">*在解决方案资源管理器中的 MvcMusicStore 数据库*</span><span class="sxs-lookup"><span data-stu-id="63bbe-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="63bbe-171">验证到数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="63bbe-171">Verify the connection to the database.</span></span> <span data-ttu-id="63bbe-172">若要执行此操作，请双击**MvcMusicStore.mdf**建立的连接。</span><span class="sxs-lookup"><span data-stu-id="63bbe-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="63bbe-173">![连接到 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "连接到 MvcMusicStore.mdf")</span><span class="sxs-lookup"><span data-stu-id="63bbe-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="63bbe-174">*连接到 MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="63bbe-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="63bbe-175">任务 2-创建数据模型</span><span class="sxs-lookup"><span data-stu-id="63bbe-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="63bbe-176">在本任务中，将创建数据模型与上一任务中添加的数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="63bbe-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="63bbe-177">创建将表示的数据库的数据模型。</span><span class="sxs-lookup"><span data-stu-id="63bbe-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="63bbe-178">为此，请在解决方案资源管理器中右击**模型**文件夹，指向**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="63bbe-179">在中**添加新项**对话框中，选择**数据**模板，然后**ADO.NET 实体数据模型**项。</span><span class="sxs-lookup"><span data-stu-id="63bbe-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="63bbe-180">将数据模型名称更改为**StoreDB.edmx**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="63bbe-181">![添加 StoreDB ADO.NET 实体数据模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "添加 StoreDB ADO.NET 实体数据模型")</span><span class="sxs-lookup"><span data-stu-id="63bbe-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="63bbe-182">*添加 StoreDB ADO.NET 实体数据模型*</span><span class="sxs-lookup"><span data-stu-id="63bbe-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="63bbe-183">**实体数据模型向导**将出现。</span><span class="sxs-lookup"><span data-stu-id="63bbe-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="63bbe-184">此向导将引导您完成创建模型层。</span><span class="sxs-lookup"><span data-stu-id="63bbe-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="63bbe-185">由于该模型应创建基于现有的数据库 recentyl 添加，因此选择**从数据库生成**然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-185">Since the model should be created based on the existing database recentyl added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="63bbe-186">![选择模型内容](aspnet-mvc-4-models-and-data-access/_static/image7.png "选择模型内容")</span><span class="sxs-lookup"><span data-stu-id="63bbe-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="63bbe-187">*选择模型内容*</span><span class="sxs-lookup"><span data-stu-id="63bbe-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="63bbe-188">由于您从数据库生成模型，需要指定要使用的连接。</span><span class="sxs-lookup"><span data-stu-id="63bbe-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="63bbe-189">单击**新的连接**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="63bbe-190">选择**Microsoft SQL Server 数据库文件**然后单击**继续**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="63bbe-191">![选择数据源](aspnet-mvc-4-models-and-data-access/_static/image8.png "选择数据源")</span><span class="sxs-lookup"><span data-stu-id="63bbe-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="63bbe-192">*选择数据源对话框*</span><span class="sxs-lookup"><span data-stu-id="63bbe-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="63bbe-193">单击**浏览**，然后选择数据库**MvcMusicStore.mdf**你在中找到**应用\_数据**文件夹，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="63bbe-194">![连接属性](aspnet-mvc-4-models-and-data-access/_static/image9.png "连接属性")</span><span class="sxs-lookup"><span data-stu-id="63bbe-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="63bbe-195">*连接属性*</span><span class="sxs-lookup"><span data-stu-id="63bbe-195">*Connection properties*</span></span>
6. <span data-ttu-id="63bbe-196">生成的类应该具有与实体连接字符串相同的名称，因此其名称更改为**MusicStoreEntities**然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="63bbe-197">![选择数据连接](aspnet-mvc-4-models-and-data-access/_static/image10.png "选择数据连接")</span><span class="sxs-lookup"><span data-stu-id="63bbe-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="63bbe-198">*选择数据连接*</span><span class="sxs-lookup"><span data-stu-id="63bbe-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="63bbe-199">选择要使用的数据库对象。</span><span class="sxs-lookup"><span data-stu-id="63bbe-199">Choose the database objects to use.</span></span> <span data-ttu-id="63bbe-200">因为实体模型将使用只是数据库的表，选择**表**选项，并确保选中**在模型中包含外键列**和**确定的单复数生成对象名**选项也将被选中。</span><span class="sxs-lookup"><span data-stu-id="63bbe-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="63bbe-201">更改到模型 Namespace **MvcMusicStore.Model**然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="63bbe-202">![选择数据库对象](aspnet-mvc-4-models-and-data-access/_static/image11.png "选择数据库对象")</span><span class="sxs-lookup"><span data-stu-id="63bbe-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="63bbe-203">*选择数据库对象*</span><span class="sxs-lookup"><span data-stu-id="63bbe-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-204">如果显示安全警告对话框，单击**确定**运行该模板并生成模型实体的类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="63bbe-205">用于数据库的实体关系图将显示，而将创建一个单独的类映射到数据库的每个表。</span><span class="sxs-lookup"><span data-stu-id="63bbe-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="63bbe-206">例如，**相册**表将由表示**唱片集**类，其中每个表中的列将映射到类属性。</span><span class="sxs-lookup"><span data-stu-id="63bbe-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="63bbe-207">这样，您可以查询和使用这些对象表示数据库中的行。</span><span class="sxs-lookup"><span data-stu-id="63bbe-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="63bbe-208">![实体关系图](aspnet-mvc-4-models-and-data-access/_static/image12.png "实体关系图")</span><span class="sxs-lookup"><span data-stu-id="63bbe-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="63bbe-209">*实体关系图*</span><span class="sxs-lookup"><span data-stu-id="63bbe-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-210">T4 模板 (.tt) 运行代码，以生成实体类，并将覆盖具有相同名称的现有类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="63bbe-211">在此示例中，类&quot;唱片集&quot;，&quot;流派&quot;并&quot;艺术家&quot;覆盖与生成的代码。</span><span class="sxs-lookup"><span data-stu-id="63bbe-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="63bbe-212">任务 3-生成应用程序</span><span class="sxs-lookup"><span data-stu-id="63bbe-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="63bbe-213">在本任务中，您将检查，尽管模型生成已删除**唱片集**，**流派**并**艺术家**模型类，成功生成项目通过使用新的数据模型类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="63bbe-214">通过选择生成项目**构建**菜单项，然后**生成 MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="63bbe-215">![生成项目](aspnet-mvc-4-models-and-data-access/_static/image13.png "生成项目")</span><span class="sxs-lookup"><span data-stu-id="63bbe-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="63bbe-216">*生成项目*</span><span class="sxs-lookup"><span data-stu-id="63bbe-216">*Building the project*</span></span>
2. <span data-ttu-id="63bbe-217">成功生成项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-217">The project builds successfully.</span></span> <span data-ttu-id="63bbe-218">为什么它仍工作？</span><span class="sxs-lookup"><span data-stu-id="63bbe-218">Why does it still work?</span></span> <span data-ttu-id="63bbe-219">它有效，因为数据库表具有已删除的类中包含已使用的属性字段**唱片集**并**流派**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="63bbe-220">![生成成功](aspnet-mvc-4-models-and-data-access/_static/image14.png "生成成功")</span><span class="sxs-lookup"><span data-stu-id="63bbe-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="63bbe-221">*生成成功*</span><span class="sxs-lookup"><span data-stu-id="63bbe-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="63bbe-222">尽管在设计器关系图格式显示实体，它们实际上是 C# 类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="63bbe-223">展开**StoreDB.edmx**在解决方案资源管理器中的节点，然后**StoreDB.tt**，你将看到新生成的实体。</span><span class="sxs-lookup"><span data-stu-id="63bbe-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="63bbe-224">![生成的文件](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成的文件")</span><span class="sxs-lookup"><span data-stu-id="63bbe-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="63bbe-225">*生成的文件*</span><span class="sxs-lookup"><span data-stu-id="63bbe-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="63bbe-226">任务 4-查询数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="63bbe-227">在此任务中，将更新 StoreController 类，以便不使用硬编码数据，它将查询数据库以检索信息。</span><span class="sxs-lookup"><span data-stu-id="63bbe-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="63bbe-228">打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**类，名为**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="63bbe-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="63bbe-229">(代码段-*模型和数据访问权限的 Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="63bbe-230">**MusicStoreEntities**类公开数据库中每个表的集合属性。</span><span class="sxs-lookup"><span data-stu-id="63bbe-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="63bbe-231">更新**浏览**操作方法来检索所有流派**相册**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="63bbe-232">(代码段-*模型和数据访问-Ex1 应用商店浏览*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="63bbe-233">使用.NET 调用的一项功能**LINQ** （语言集成查询） 来编写强类型化查询表达式对这些集合-将执行对数据库的代码并返回对象，您可以进行编程作用。</span><span class="sxs-lookup"><span data-stu-id="63bbe-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="63bbe-234">有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="63bbe-235">更新**索引**操作方法来检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="63bbe-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="63bbe-236">(代码段-*模型和数据访问-Ex1 存储索引*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="63bbe-237">更新**索引**操作方法来检索所有流派和转换列表的集合。</span><span class="sxs-lookup"><span data-stu-id="63bbe-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="63bbe-238">(代码段-*模型和数据访问-Ex1 存储 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="63bbe-239">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="63bbe-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="63bbe-240">在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的流派。</span><span class="sxs-lookup"><span data-stu-id="63bbe-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="63bbe-241">若要更改视图模板，因为无需**StoreController**返回相同的实体与之前一样，尽管这一次的数据将来自该数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="63bbe-242">重新生成解决方案并按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="63bbe-243">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-243">The project starts in the Home page.</span></span> <span data-ttu-id="63bbe-244">验证的菜单**流派**不再是硬编码列表，并直接从数据库检索的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="63bbe-246">*从数据库中浏览类型*</span><span class="sxs-lookup"><span data-stu-id="63bbe-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="63bbe-247">现在浏览到任何类型，并验证从数据库中填充唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="63bbe-248">![从数据库中浏览相册](aspnet-mvc-4-models-and-data-access/_static/image17.png "浏览数据库中的唱片集")</span><span class="sxs-lookup"><span data-stu-id="63bbe-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="63bbe-249">*从数据库中浏览唱片集*</span><span class="sxs-lookup"><span data-stu-id="63bbe-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="63bbe-250">练习 2： 创建使用 Code First 数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="63bbe-251">在此练习中，您将学习如何使用代码第一种方法来创建具有 MusicStore 应用程序的表的数据库以及如何访问其数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="63bbe-252">模型生成后，您将修改 StoreController 视图模板提供从数据库中，而不是使用硬编码值中获取的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-253">如果已完成练习 1 中，已处理过数据库第一种方法，将现在了解如何获取与不同的进程相同的结果。</span><span class="sxs-lookup"><span data-stu-id="63bbe-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="63bbe-254">已标记与练习 1 中相同的任务以方便您阅读。</span><span class="sxs-lookup"><span data-stu-id="63bbe-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="63bbe-255">如果尚未完成练习 1，但想要了解代码第一种方法，可以从本练习中启动，并获取该主题的完整的覆盖范围。</span><span class="sxs-lookup"><span data-stu-id="63bbe-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="63bbe-256">任务 1-填充示例数据</span><span class="sxs-lookup"><span data-stu-id="63bbe-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="63bbe-257">在此任务中，将开始创建使用代码优先时填充示例数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-257">In this task, you will populate the database with sample data when it is intially created using Code-First.</span></span>

1. <span data-ttu-id="63bbe-258">打开**开始**解决方案位于**源/Ex2-CreatingADatabaseCodeFirst/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="63bbe-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="63bbe-259">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="63bbe-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="63bbe-260">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="63bbe-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="63bbe-261">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="63bbe-262">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="63bbe-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="63bbe-263">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="63bbe-264">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="63bbe-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="63bbe-265">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="63bbe-266">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="63bbe-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="63bbe-267">添加**SampleData.cs**的文件**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="63bbe-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="63bbe-268">为此，请右键单击**模型**文件夹，指向**添加**，然后单击**现有项**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="63bbe-269">浏览到**\Source\Assets** ，然后选择**SampleData.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="63bbe-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="63bbe-270">![示例数据填充代码](aspnet-mvc-4-models-and-data-access/_static/image18.png "示例数据填充代码")</span><span class="sxs-lookup"><span data-stu-id="63bbe-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="63bbe-271">*示例数据填充代码*</span><span class="sxs-lookup"><span data-stu-id="63bbe-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="63bbe-272">打开**Global.asax.cs**文件，并添加以下*使用*语句。</span><span class="sxs-lookup"><span data-stu-id="63bbe-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="63bbe-273">(代码段-*模型和数据访问-Ex2 全局 Asax Using*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="63bbe-274">在中**应用程序\_start （)** 方法添加以下行以设置数据库初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="63bbe-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="63bbe-275">(代码段-*模型和数据访问-Ex2 全局 Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="63bbe-276">任务 2-配置数据库的连接</span><span class="sxs-lookup"><span data-stu-id="63bbe-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="63bbe-277">现在，已将数据库加入我们的项目，将在中编写**Web.config**文件的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="63bbe-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="63bbe-278">添加在连接字符串**Web.config**。为此，请打开**Web.config**在项目根和替换连接字符串中的此行与名为 DefaultConnection **&lt;connectionStrings&gt;** 部分：</span><span class="sxs-lookup"><span data-stu-id="63bbe-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="63bbe-279">![Web.config 文件位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 文件位置")</span><span class="sxs-lookup"><span data-stu-id="63bbe-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="63bbe-280">*Web.config 文件位置*</span><span class="sxs-lookup"><span data-stu-id="63bbe-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="63bbe-281">任务 3-使用的模型</span><span class="sxs-lookup"><span data-stu-id="63bbe-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="63bbe-282">现在，已配置数据库的连接，将链接的模型与数据库表。</span><span class="sxs-lookup"><span data-stu-id="63bbe-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="63bbe-283">在本任务中，将创建将链接到的数据库使用 Code First 的类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="63bbe-284">请记住，应修改的现有 POCO 模型类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-285">如果你完成练习 1 中，您会注意此步骤由一个向导。</span><span class="sxs-lookup"><span data-stu-id="63bbe-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="63bbe-286">通过执行 Code First，您将手动创建将链接到数据实体的类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="63bbe-287">打开 POCO 模型类**流派**从**模型**项目文件夹，并包含一个 id。</span><span class="sxs-lookup"><span data-stu-id="63bbe-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="63bbe-288">使用整型属性以名称**GenreId**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="63bbe-289">(代码段-*模型和数据访问-Ex2 代码的第一个流派*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="63bbe-290">若要使用 Code First 约定，类类型必须具有主键属性，将自动检测到。</span><span class="sxs-lookup"><span data-stu-id="63bbe-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="63bbe-291">你可以阅读更多有关在此代码优先约定[msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="63bbe-292">现在，打开 POCO 模型类**唱片集**从**模型**项目文件夹和包含外键，创建属性的名称**GenreId**和**ArtistId**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="63bbe-293">此类已有**GenreId**为主键。</span><span class="sxs-lookup"><span data-stu-id="63bbe-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="63bbe-294">(代码段-*模型和数据访问-Ex2 代码第一个唱片集*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="63bbe-295">打开 POCO 模型类**艺术家**和包含**ArtistId**属性。</span><span class="sxs-lookup"><span data-stu-id="63bbe-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="63bbe-296">(代码段-*模型和数据访问-Ex2 代码的第一个艺术家*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="63bbe-297">右键单击**模型**项目文件夹，然后选择**添加 |类**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="63bbe-298">将文件命名**MusicStoreEntities.cs**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="63bbe-299">然后，单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="63bbe-299">Then, click **Add.**</span></span>

    <span data-ttu-id="63bbe-300">![添加类](aspnet-mvc-4-models-and-data-access/_static/image20.png "添加类")</span><span class="sxs-lookup"><span data-stu-id="63bbe-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="63bbe-301">*添加新项*</span><span class="sxs-lookup"><span data-stu-id="63bbe-301">*Adding a new item*</span></span>

    <span data-ttu-id="63bbe-302">![添加 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "添加 class2")</span><span class="sxs-lookup"><span data-stu-id="63bbe-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="63bbe-303">*添加类*</span><span class="sxs-lookup"><span data-stu-id="63bbe-303">*Adding a class*</span></span>
5. <span data-ttu-id="63bbe-304">打开您刚创建的类**MusicStoreEntities.cs**，并包括命名空间**System.Data.Entity**并**System.Data.Entity.Infrastructure**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="63bbe-305">替换为要扩展的类声明**DbContext**类： 声明一个公共**DBSet**并重写**OnModelCreating**方法。</span><span class="sxs-lookup"><span data-stu-id="63bbe-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="63bbe-306">在此步骤后，你将收到您的模型使用实体框架将链接的域类。</span><span class="sxs-lookup"><span data-stu-id="63bbe-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="63bbe-307">为此，将为与以下的类代码：</span><span class="sxs-lookup"><span data-stu-id="63bbe-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="63bbe-308">(代码段-*模型和数据访问-Ex2 代码的第一个 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="63bbe-309">使用实体框架**DbContext**并**DBSet**可以查询 POCO 类流派。</span><span class="sxs-lookup"><span data-stu-id="63bbe-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="63bbe-310">通过扩展**OnModelCreating**中指定的方法，**代码**如何类型将映射到数据库表。</span><span class="sxs-lookup"><span data-stu-id="63bbe-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="63bbe-311">可以在此 msdn 文章中找到有关 DBContext 和 DBSet 的详细信息：[链接](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="63bbe-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="63bbe-312">任务 4-查询数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="63bbe-313">在此任务中，将更新 StoreController 类，以便不使用硬编码数据，它将其从数据库中检索。</span><span class="sxs-lookup"><span data-stu-id="63bbe-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-314">此任务是与练习 1 中相同。</span><span class="sxs-lookup"><span data-stu-id="63bbe-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="63bbe-315">如果你完成练习 1 中您将注意这些步骤都在这两种方法中相同的 (数据库优先或代码优先)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="63bbe-316">它们是不同中如何将数据链接模型，但对数据实体的访问权限是尚未从控制器透明的。</span><span class="sxs-lookup"><span data-stu-id="63bbe-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="63bbe-317">打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**类，名为**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="63bbe-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="63bbe-318">(代码段-*模型和数据访问权限的 Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="63bbe-319">**MusicStoreEntities**类公开数据库中每个表的集合属性。</span><span class="sxs-lookup"><span data-stu-id="63bbe-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="63bbe-320">更新**浏览**操作方法来检索所有流派**相册**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="63bbe-321">(代码段-*模型和数据访问-Ex2 应用商店浏览*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="63bbe-322">使用.NET 调用的一项功能**LINQ** （语言集成查询） 来编写强类型化查询表达式对这些集合-将执行对数据库的代码并返回对象，您可以进行编程作用。</span><span class="sxs-lookup"><span data-stu-id="63bbe-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="63bbe-323">有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="63bbe-324">更新**索引**操作方法来检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="63bbe-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="63bbe-325">(代码段-*模型和数据访问-Ex2 存储索引*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="63bbe-326">更新**索引**操作方法来检索所有流派和转换列表的集合。</span><span class="sxs-lookup"><span data-stu-id="63bbe-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="63bbe-327">(代码段-*模型和数据访问-Ex2 存储 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="63bbe-328">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="63bbe-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="63bbe-329">在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的流派。</span><span class="sxs-lookup"><span data-stu-id="63bbe-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="63bbe-330">若要更改视图模板，因为无需**StoreController**返回相同**StoreIndexViewModel**与之前一样，但这一次的数据将来自该数据库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="63bbe-331">重新生成解决方案并按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="63bbe-332">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-332">The project starts in the Home page.</span></span> <span data-ttu-id="63bbe-333">验证的菜单**流派**不再是硬编码列表，并直接从数据库检索的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="63bbe-335">*从数据库中浏览类型*</span><span class="sxs-lookup"><span data-stu-id="63bbe-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="63bbe-336">现在浏览到任何类型，并验证从数据库中填充唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="63bbe-337">![从数据库中浏览相册](aspnet-mvc-4-models-and-data-access/_static/image23.png "浏览数据库中的唱片集")</span><span class="sxs-lookup"><span data-stu-id="63bbe-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="63bbe-338">*从数据库中浏览唱片集*</span><span class="sxs-lookup"><span data-stu-id="63bbe-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="63bbe-339">练习 3： 查询具有参数的数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="63bbe-340">在此练习中，您将了解如何使用参数，在数据库中查询以及如何使用查询结果调整，一项功能，减少了数字数据库以更有效地访问中检索数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-341">查询结果调整的详细信息，请访问以下[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="63bbe-342">任务 1-修改 StoreController 从数据库检索相册</span><span class="sxs-lookup"><span data-stu-id="63bbe-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="63bbe-343">在本任务中，您将更改**StoreController**类来访问数据库以检索特定流派的唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="63bbe-344">打开**开始**解决方案位于**Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin**文件夹，如果想要使用代码优先方法或**Source\Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin**文件夹，如果想要使用数据库为先的方法。</span><span class="sxs-lookup"><span data-stu-id="63bbe-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="63bbe-345">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="63bbe-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="63bbe-346">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="63bbe-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="63bbe-347">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="63bbe-348">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="63bbe-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="63bbe-349">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="63bbe-350">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="63bbe-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="63bbe-351">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="63bbe-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="63bbe-352">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="63bbe-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="63bbe-353">打开**StoreController**类，以更改**浏览**操作方法。</span><span class="sxs-lookup"><span data-stu-id="63bbe-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="63bbe-354">若要执行此操作，在**解决方案资源管理器**，展开**控制器**文件夹，然后双击**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="63bbe-355">更改**浏览**操作方法来检索特定流派的唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="63bbe-356">若要执行此操作，将以下代码：</span><span class="sxs-lookup"><span data-stu-id="63bbe-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="63bbe-357">(代码段-*模型和数据访问-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="63bbe-358">若要填充的实体的集合，您需要使用**Include**方法，以指定你想要过检索相册。</span><span class="sxs-lookup"><span data-stu-id="63bbe-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="63bbe-359">可以使用。**Single （)** 中 LINQ 的扩展因为在这种情况下只有一个流派预期唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="63bbe-360">**Single （)** 方法采用 Lambda 表达式作为参数，在这种情况下指定单个流派对象，以便其名称不匹配定义的值。</span><span class="sxs-lookup"><span data-stu-id="63bbe-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="63bbe-361">将充分利用一项功能，可用于指示检索该类型对象时，你需要同时加载其他相关的实体。</span><span class="sxs-lookup"><span data-stu-id="63bbe-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="63bbe-362">此功能被称为**查询结果调整**，并使您可以减少访问数据库以检索信息所需的次数。</span><span class="sxs-lookup"><span data-stu-id="63bbe-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="63bbe-363">在此方案中，你将想要预提取检索的流派唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="63bbe-364">该查询包含**Genres.Include (&quot;相册&quot;)** 以指示要以及相关的唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="63bbe-365">这将导致更高效的应用程序，因为它会检索中的单个数据库请求流派和唱片集的数据。</span><span class="sxs-lookup"><span data-stu-id="63bbe-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="63bbe-366">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="63bbe-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="63bbe-367">在本任务中，将运行该应用程序，并从数据库中检索的特定流派的唱片集。</span><span class="sxs-lookup"><span data-stu-id="63bbe-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="63bbe-368">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="63bbe-369">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-369">The project starts in the Home page.</span></span> <span data-ttu-id="63bbe-370">将 URL 更改为 **/Store/浏览？ genre = Pop**以验证从数据库检索到结果。</span><span class="sxs-lookup"><span data-stu-id="63bbe-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="63bbe-371">![浏览按流派](aspnet-mvc-4-models-and-data-access/_static/image24.png "按流派浏览")</span><span class="sxs-lookup"><span data-stu-id="63bbe-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="63bbe-372">*浏览/Store/浏览？ genre = Pop*</span><span class="sxs-lookup"><span data-stu-id="63bbe-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="63bbe-373">任务 3-访问唱片集的 Id</span><span class="sxs-lookup"><span data-stu-id="63bbe-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="63bbe-374">在此任务中，将重复前面的过程，以获取唱片集由其 id。</span><span class="sxs-lookup"><span data-stu-id="63bbe-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="63bbe-375">关闭浏览器，如果需要可以返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="63bbe-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="63bbe-376">打开**StoreController**类，以更改**详细信息**操作方法。</span><span class="sxs-lookup"><span data-stu-id="63bbe-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="63bbe-377">若要执行此操作，在**解决方案资源管理器**，展开**控制器**文件夹，然后双击**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="63bbe-378">更改**详细信息**操作方法来检索相册详细信息，根据其**Id**。若要执行此操作，将以下代码：</span><span class="sxs-lookup"><span data-stu-id="63bbe-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="63bbe-379">(代码段-*模型和数据访问-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="63bbe-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="63bbe-380">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="63bbe-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="63bbe-381">在本任务中，将在 web 浏览器中运行应用程序并获取由其 id 的唱片集详细信息</span><span class="sxs-lookup"><span data-stu-id="63bbe-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="63bbe-382">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="63bbe-383">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="63bbe-383">The project starts in the Home page.</span></span> <span data-ttu-id="63bbe-384">将 URL 更改为 **/Store/Details/51**或浏览流派，并选择某个唱片集以验证从数据库检索到结果。</span><span class="sxs-lookup"><span data-stu-id="63bbe-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="63bbe-385">![浏览的详细信息](aspnet-mvc-4-models-and-data-access/_static/image25.png "浏览详细信息")</span><span class="sxs-lookup"><span data-stu-id="63bbe-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="63bbe-386">*浏览 /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="63bbe-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="63bbe-387">此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="63bbe-388">总结</span><span class="sxs-lookup"><span data-stu-id="63bbe-388">Summary</span></span>

<span data-ttu-id="63bbe-389">通过完成本动手实验介绍了 ASP.NET MVC 模型和数据访问的基础知识，请使用**Database First**方法并将**Code First**方法：</span><span class="sxs-lookup"><span data-stu-id="63bbe-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="63bbe-390">如何将数据库添加到解决方案，以便使用其数据</span><span class="sxs-lookup"><span data-stu-id="63bbe-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="63bbe-391">如何更新控制器，以提供从而不是硬编码一个数据库中获取的数据视图模板</span><span class="sxs-lookup"><span data-stu-id="63bbe-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="63bbe-392">如何使用参数在数据库中查询</span><span class="sxs-lookup"><span data-stu-id="63bbe-392">How to query the database using parameters</span></span>
- <span data-ttu-id="63bbe-393">如何使用查询结果调整，一项功能，用于减少数据库访问中更有效地检索数据</span><span class="sxs-lookup"><span data-stu-id="63bbe-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="63bbe-394">如何在 Microsoft Entity Framework 中使用数据库优先和代码优先方法，用于链接的模型数据库</span><span class="sxs-lookup"><span data-stu-id="63bbe-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="63bbe-395">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="63bbe-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="63bbe-396">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="63bbe-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="63bbe-397">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="63bbe-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="63bbe-398">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="63bbe-399">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="63bbe-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="63bbe-400">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-400">Click on **Install Now**.</span></span> <span data-ttu-id="63bbe-401">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="63bbe-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="63bbe-402">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="63bbe-403">![安装 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="63bbe-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="63bbe-404">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="63bbe-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="63bbe-405">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="63bbe-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="63bbe-407">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="63bbe-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="63bbe-408">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="63bbe-408">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="63bbe-410">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="63bbe-410">*Installation progress*</span></span>
6. <span data-ttu-id="63bbe-411">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-411">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="63bbe-413">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="63bbe-413">*Installation completed*</span></span>
7. <span data-ttu-id="63bbe-414">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="63bbe-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="63bbe-415">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="63bbe-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="63bbe-417">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="63bbe-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="63bbe-418">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="63bbe-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="63bbe-419">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="63bbe-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="63bbe-420">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="63bbe-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="63bbe-421">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="63bbe-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-422">使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="63bbe-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="63bbe-423">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-423">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="63bbe-424">![登录到 Windows Azure 门户](aspnet-mvc-4-models-and-data-access/_static/image31.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="63bbe-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="63bbe-425">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="63bbe-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="63bbe-426">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="63bbe-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="63bbe-427">![创建新的 Web 站点](aspnet-mvc-4-models-and-data-access/_static/image32.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="63bbe-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="63bbe-428">*创建新的 Web 站点*</span><span class="sxs-lookup"><span data-stu-id="63bbe-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="63bbe-429">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="63bbe-430">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="63bbe-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="63bbe-431">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-432">Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。</span><span class="sxs-lookup"><span data-stu-id="63bbe-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="63bbe-433">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。</span><span class="sxs-lookup"><span data-stu-id="63bbe-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="63bbe-434">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="63bbe-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="63bbe-435">![创建新的网站使用快速创建](aspnet-mvc-4-models-and-data-access/_static/image33.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="63bbe-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="63bbe-436">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="63bbe-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="63bbe-437">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="63bbe-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="63bbe-438">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="63bbe-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="63bbe-439">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="63bbe-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="63bbe-440">![浏览到新的 web 站点](aspnet-mvc-4-models-and-data-access/_static/image34.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="63bbe-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="63bbe-441">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="63bbe-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="63bbe-442">![正在运行的网站](aspnet-mvc-4-models-and-data-access/_static/image35.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="63bbe-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="63bbe-443">*正在运行的网站*</span><span class="sxs-lookup"><span data-stu-id="63bbe-443">*Web site running*</span></span>
6. <span data-ttu-id="63bbe-444">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="63bbe-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="63bbe-445">![打开网站管理页](aspnet-mvc-4-models-and-data-access/_static/image36.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="63bbe-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="63bbe-446">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="63bbe-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="63bbe-447">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="63bbe-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-448">*发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="63bbe-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="63bbe-449">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="63bbe-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="63bbe-450">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="63bbe-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="63bbe-451">![正在下载网站发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image37.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="63bbe-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="63bbe-452">*正在下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="63bbe-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="63bbe-453">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="63bbe-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="63bbe-454">进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。</span><span class="sxs-lookup"><span data-stu-id="63bbe-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="63bbe-455">![保存发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image38.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="63bbe-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="63bbe-456">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="63bbe-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="63bbe-457">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="63bbe-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="63bbe-458">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="63bbe-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="63bbe-459">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="63bbe-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="63bbe-460">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="63bbe-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="63bbe-461">可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="63bbe-462">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="63bbe-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="63bbe-463">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="63bbe-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="63bbe-464">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="63bbe-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="63bbe-465">![SQL 数据库服务器仪表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="63bbe-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="63bbe-466">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="63bbe-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="63bbe-467">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="63bbe-468">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="63bbe-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="63bbe-470">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="63bbe-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="63bbe-471">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="63bbe-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="63bbe-473">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="63bbe-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="63bbe-474">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="63bbe-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="63bbe-475">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="63bbe-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="63bbe-476">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="63bbe-477">![发布应用程序](aspnet-mvc-4-models-and-data-access/_static/image43.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="63bbe-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="63bbe-478">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="63bbe-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="63bbe-479">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="63bbe-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="63bbe-480">![导入发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image44.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="63bbe-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="63bbe-481">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="63bbe-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="63bbe-482">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-482">Click **Validate Connection**.</span></span> <span data-ttu-id="63bbe-483">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63bbe-484">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="63bbe-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="63bbe-485">![验证连接](aspnet-mvc-4-models-and-data-access/_static/image45.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="63bbe-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="63bbe-486">*验证连接*</span><span class="sxs-lookup"><span data-stu-id="63bbe-486">*Validating connection*</span></span>
4. <span data-ttu-id="63bbe-487">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="63bbe-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="63bbe-488">![Web 部署配置](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="63bbe-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="63bbe-489">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="63bbe-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="63bbe-490">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63bbe-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="63bbe-491">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="63bbe-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="63bbe-492">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="63bbe-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="63bbe-493">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="63bbe-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="63bbe-494">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="63bbe-494">Type a new database name.</span></span>

     <span data-ttu-id="63bbe-495">![配置目标连接字符串](aspnet-mvc-4-models-and-data-access/_static/image47.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="63bbe-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="63bbe-496">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="63bbe-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="63bbe-497">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="63bbe-497">Then click **OK**.</span></span> <span data-ttu-id="63bbe-498">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="63bbe-499">![创建数据库](aspnet-mvc-4-models-and-data-access/_static/image48.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="63bbe-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="63bbe-500">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="63bbe-500">*Creating the database*</span></span>
7. <span data-ttu-id="63bbe-501">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="63bbe-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="63bbe-502">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-502">Then click **Next**.</span></span>

    <span data-ttu-id="63bbe-503">![连接字符串指向 SQL 数据库](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="63bbe-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="63bbe-504">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="63bbe-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="63bbe-505">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="63bbe-506">![Web 应用程序发布](aspnet-mvc-4-models-and-data-access/_static/image50.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="63bbe-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="63bbe-507">*Web 应用程序发布*</span><span class="sxs-lookup"><span data-stu-id="63bbe-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="63bbe-508">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="63bbe-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="63bbe-509">附录 c： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="63bbe-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="63bbe-510">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="63bbe-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="63bbe-511">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="63bbe-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="63bbe-512">![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="63bbe-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="63bbe-513">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="63bbe-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="63bbe-514">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="63bbe-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="63bbe-515">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="63bbe-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="63bbe-516">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="63bbe-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="63bbe-517">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="63bbe-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="63bbe-518">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="63bbe-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="63bbe-519">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="63bbe-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="63bbe-520">![开始键入代码段名称](aspnet-mvc-4-models-and-data-access/_static/image52.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="63bbe-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="63bbe-521">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="63bbe-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="63bbe-522">![按 tab 键以选择突出显示代码段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="63bbe-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="63bbe-523">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="63bbe-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="63bbe-524">![再次按 Tab 和代码段将 expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="63bbe-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="63bbe-525">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="63bbe-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="63bbe-526">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="63bbe-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="63bbe-527">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="63bbe-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="63bbe-528">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="63bbe-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="63bbe-529">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="63bbe-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="63bbe-530">![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-models-and-data-access/_static/image55.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="63bbe-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="63bbe-531">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="63bbe-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="63bbe-532">![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-models-and-data-access/_static/image56.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="63bbe-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="63bbe-533">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="63bbe-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
