---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: "ASP.NET MVC 4 模型和数据访问 |Microsoft 文档"
author: rick-anderson
description: "注意： 此动手实验假定你具有的 ASP.NET MVC 的基本知识。 如果你不使用 ASP.NET MVC 之前，我们建议你通过 ASP.NET MVC 4..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 076fa87eff140a3e7ff6855e4876abac40419c57
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="bcdd7-104">ASP.NET MVC 4 模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="bcdd7-104">ASP.NET MVC 4 Models and Data Access</span></span>
====================
<span data-ttu-id="bcdd7-105">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-106">此动手实验假定你具有的基础知识**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-106">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="bcdd7-107">如果您未使用过**ASP.NET MVC**之前，我们建议你转到**ASP.NET MVC 4 基础知识**动手实验。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-107">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>
> 
> <span data-ttu-id="bcdd7-108">此实验室将引导你完成的增强功能和前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用程序的新功能。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-108">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="bcdd7-109">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-109">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843).</span></span>


<span data-ttu-id="bcdd7-110">在**ASP.NET MVC 基础知识**动手实验中，你已经传递了硬编码数据从控制器到查看模板。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-110">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="bcdd7-111">但是，若要生成实际的 Web 应用程序，你可能想要使用实际的数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-111">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="bcdd7-112">此动手实验将演示如何使用数据库引擎以存储和检索音乐商店应用程序所需的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-112">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="bcdd7-113">若要完成此操作，将使用现有数据库启动，并从它创建实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-113">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="bcdd7-114">在本实验中，整个将满足**Database First**方法以及**Code First**方法。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-114">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="bcdd7-115">但是，你还可以使用**Model First**方法，创建相同的模型使用的工具，然后从它生成数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-115">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="bcdd7-116">![数据库第一个 vs。模型优先](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs。模型优先")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-116">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="bcdd7-117">*数据库第一个 vs。模型优先*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-117">*Database First vs. Model First*</span></span>

<span data-ttu-id="bcdd7-118">后生成模型，你会使 StoreController 为存储视图的数据库，而不是使用硬编码数据中获取的数据提供适当的调整。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-118">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="bcdd7-119">不需要进行任何更改视图模板 StoreController 将返回相同的 Viewmodel 到查看模板，因为虽然此时间的数据将来自数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-119">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="bcdd7-120">**代码第一种方法**</span><span class="sxs-lookup"><span data-stu-id="bcdd7-120">**The Code First Approach**</span></span>

<span data-ttu-id="bcdd7-121">代码优先方法使得我们可以定义代码中的模型，而不生成类通常与框架耦合的。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-121">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="bcdd7-122">在代码中首先，模型对象定义与 POCOs，&quot;纯旧 CLR 对象&quot;。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-122">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="bcdd7-123">POCOs 是简单的普通类，不具有任何继承并不实现接口。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-123">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="bcdd7-124">我们可以自动生成数据库，从它们，也可以使用现有数据库并从代码生成的类映射。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-124">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="bcdd7-125">使用此方法的好处是，将模型保持独立于持久性框架 （在这种情况下，实体框架），如 POCOs 类不结合映射框架。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-125">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-126">此实验室基于 ASP.NET MVC 4 和音乐商店示例应用程序的版本自定义和最小化以适应仅显示在本动手实验中的功能。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-126">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="bcdd7-127">如果你想要浏览整个**音乐商店**教程应用程序，你可以找到它在[MVC 音乐商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-127">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="bcdd7-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="bcdd7-128">Prerequisites</span></span>

<span data-ttu-id="bcdd7-129">你必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="bcdd7-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="bcdd7-131">安装</span><span class="sxs-lookup"><span data-stu-id="bcdd7-131">Setup</span></span>

<span data-ttu-id="bcdd7-132">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="bcdd7-132">**Installing Code Snippets**</span></span>

<span data-ttu-id="bcdd7-133">为方便起见，你将沿此实验室管理大部分都是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-133">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="bcdd7-134">若要安装运行的代码段**.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-134">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="bcdd7-135">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 c： 使用代码段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-135">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="bcdd7-136">练习</span><span class="sxs-lookup"><span data-stu-id="bcdd7-136">Exercises</span></span>

<span data-ttu-id="bcdd7-137">此动手实验包含通过在以下练习：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-137">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="bcdd7-138">练习 1： 添加数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-138">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="bcdd7-139">练习 2： 创建使用 Code First 数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-139">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="bcdd7-140">练习 3： 查询参数的数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-140">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="bcdd7-141">每个练习均附带由**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-141">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="bcdd7-142">如果你需要通过在练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-142">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="bcdd7-143">估计时间来完成该实验： **35 分钟**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-143">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="bcdd7-144">练习 1： 添加数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-144">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="bcdd7-145">在此练习中，你将了解如何添加具有 MusicStore 应用程序，到解决方案以便使用其数据的表的数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-145">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="bcdd7-146">一旦使用该模型生成数据库并将其添加到解决方案，你将修改 StoreController 类，以查看模板提供从数据库，而不是使用硬编码值获取的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-146">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="bcdd7-147">任务 1-添加数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-147">Task 1 - Adding a Database</span></span>

<span data-ttu-id="bcdd7-148">在此任务中，你将添加到解决方案 MusicStore 应用程序的主表已创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-148">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="bcdd7-149">打开**开始**解决方案位于**源/Ex1-AddingADatabaseDBFirst/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-149">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

    1. <span data-ttu-id="bcdd7-150">你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-150">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bcdd7-151">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-151">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="bcdd7-152">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-152">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="bcdd7-153">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-153">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-154">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-154">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bcdd7-155">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-155">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bcdd7-156">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-156">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bcdd7-157">添加**MvcMusicStore**数据库文件。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-157">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="bcdd7-158">在本动手实验中，你将使用已创建的数据库调用**MvcMusicStore.mdf**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-158">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="bcdd7-159">为此，请右键单击**应用\_数据**文件夹，指向**添加**，然后单击**现有项**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-159">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="bcdd7-160">浏览到**\Source\Assets**和选择**MvcMusicStore.mdf**文件。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-160">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="bcdd7-161">![添加现有项](aspnet-mvc-4-models-and-data-access/_static/image2.png "添加现有项")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-161">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="bcdd7-162">*添加现有项*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-162">*Adding an Existing Item*</span></span>

    <span data-ttu-id="bcdd7-163">![MvcMusicStore.mdf 数据库文件](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 数据库文件")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-163">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="bcdd7-164">*MvcMusicStore.mdf 数据库文件*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-164">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="bcdd7-165">数据库已添加到项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-165">The database has been added to the project.</span></span> <span data-ttu-id="bcdd7-166">即使数据库位于的解决方案内，您可以查询和更新它，因为它已托管在不同的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-166">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="bcdd7-167">![在解决方案资源管理器的 MvcMusicStore 数据库](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore 数据库在解决方案资源管理器")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-167">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="bcdd7-168">*在解决方案资源管理器的 MvcMusicStore 数据库*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-168">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="bcdd7-169">验证到数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-169">Verify the connection to the database.</span></span> <span data-ttu-id="bcdd7-170">若要执行此操作，请双击**MvcMusicStore.mdf**来建立连接。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-170">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="bcdd7-171">![连接到 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "连接到 MvcMusicStore.mdf")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-171">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="bcdd7-172">*连接到 MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-172">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="bcdd7-173">任务 2-创建数据模型</span><span class="sxs-lookup"><span data-stu-id="bcdd7-173">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="bcdd7-174">在此任务中，你将创建数据模型与在上一任务中添加的数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-174">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="bcdd7-175">创建将表示的数据库的数据模型。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-175">Create a data model that will represent the database.</span></span> <span data-ttu-id="bcdd7-176">为此，请在解决方案资源管理器右击**模型**文件夹，指向**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-176">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="bcdd7-177">在**添加新项**对话框中，选择**数据**模板，然后**ADO.NET 实体数据模型**项。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-177">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="bcdd7-178">数据模型将名称更改为**StoreDB.edmx**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-178">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="bcdd7-179">![添加 StoreDB ADO.NET 实体数据模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "添加 StoreDB ADO.NET 实体数据模型")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-179">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="bcdd7-180">*添加 StoreDB ADO.NET 实体数据模型*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-180">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="bcdd7-181">**实体数据模型向导**将出现。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-181">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="bcdd7-182">此向导将指导你完成创建模型层。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-182">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="bcdd7-183">由于应根据现有的数据库 recentyl 添加创建该模型，请选择**从数据库生成**单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-183">Since the model should be created based on the existing database recentyl added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="bcdd7-184">![选择模型内容](aspnet-mvc-4-models-and-data-access/_static/image7.png "选择模型内容")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-184">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="bcdd7-185">*选择模型内容*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-185">*Choosing the model content*</span></span>
3. <span data-ttu-id="bcdd7-186">要从数据库生成模型，因为你将需要指定要使用的连接。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-186">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="bcdd7-187">单击**新连接**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-187">Click **New Connection**.</span></span>
4. <span data-ttu-id="bcdd7-188">选择**Microsoft SQL Server 数据库文件**单击**继续**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-188">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="bcdd7-189">![选择数据源](aspnet-mvc-4-models-and-data-access/_static/image8.png "选择数据源")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-189">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="bcdd7-190">*选择数据源对话框*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-190">*Choose data source dialog*</span></span>
5. <span data-ttu-id="bcdd7-191">单击**浏览**和选择的数据库**MvcMusicStore.mdf**你在中找到**应用\_数据**文件夹，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-191">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="bcdd7-192">![连接属性](aspnet-mvc-4-models-and-data-access/_static/image9.png "连接属性")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-192">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="bcdd7-193">*连接属性*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-193">*Connection properties*</span></span>
6. <span data-ttu-id="bcdd7-194">生成的类应该具有同名的实体连接字符串，因此其将名称更改为**MusicStoreEntities**单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-194">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="bcdd7-195">![选择数据连接](aspnet-mvc-4-models-and-data-access/_static/image10.png "选择数据连接")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-195">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="bcdd7-196">*选择数据连接*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-196">*Choosing the data connection*</span></span>
7. <span data-ttu-id="bcdd7-197">选择要使用的数据库对象。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-197">Choose the database objects to use.</span></span> <span data-ttu-id="bcdd7-198">因为实体模型将使用只是数据库的表，选择**表**选项，并确保**模型中包括外键列**和**单复数形式所生成对象名称**选项也将被选中。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-198">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="bcdd7-199">更改到模型 Namespace **MvcMusicStore.Model**单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-199">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="bcdd7-200">![选择数据库对象](aspnet-mvc-4-models-and-data-access/_static/image11.png "选择数据库对象")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-200">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="bcdd7-201">*选择数据库对象*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-201">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-202">如果显示安全警告对话框，单击**确定**运行该模板并生成模型实体的类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-202">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="bcdd7-203">用于数据库的实体关系图将出现，将创建一个单独的类映射到数据库的每个表时。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-203">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="bcdd7-204">例如，**专辑**表将由表示**唱片集**类，其中每个表中的列将映射到类属性。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-204">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="bcdd7-205">这将允许你以查询和使用对象，表示数据库中的行。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-205">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="bcdd7-206">![实体关系图](aspnet-mvc-4-models-and-data-access/_static/image12.png "实体关系图")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-206">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="bcdd7-207">*实体关系图*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-207">*Entity diagram*</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-208">T4 模板 (.tt) 运行代码，以生成实体类，并将覆盖具有相同名称的现有类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-208">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="bcdd7-209">在此示例中，类&quot;唱片集&quot;，&quot;流派&quot;和&quot;艺术家&quot;已具有生成的代码覆盖。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-209">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="bcdd7-210">任务 3-生成应用程序</span><span class="sxs-lookup"><span data-stu-id="bcdd7-210">Task 3 - Building the Application</span></span>

<span data-ttu-id="bcdd7-211">在此任务中，你将检查，尽管模型生成已删除**唱片集**，**流派**和**艺术家**模型类，成功生成项目通过使用新的数据模型类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-211">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="bcdd7-212">通过选择生成项目**生成**菜单项，然后**生成 MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-212">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="bcdd7-213">![生成项目](aspnet-mvc-4-models-and-data-access/_static/image13.png "生成项目")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-213">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="bcdd7-214">*生成项目*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-214">*Building the project*</span></span>
2. <span data-ttu-id="bcdd7-215">成功生成项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-215">The project builds successfully.</span></span> <span data-ttu-id="bcdd7-216">为什么它仍工作？</span><span class="sxs-lookup"><span data-stu-id="bcdd7-216">Why does it still work?</span></span> <span data-ttu-id="bcdd7-217">因为数据库表中移除类包括你使用的属性的字段，会**唱片集**和**流派**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-217">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="bcdd7-218">![成功生成](aspnet-mvc-4-models-and-data-access/_static/image14.png "生成成功")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-218">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="bcdd7-219">*生成成功*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-219">*Builds succeeded*</span></span>
3. <span data-ttu-id="bcdd7-220">时设计器的关系图格式显示实体，但它们实际上是 C# 类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-220">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="bcdd7-221">展开**StoreDB.edmx**在解决方案资源管理器中的节点，然后**StoreDB.tt**，你将看到新生成的实体。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-221">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="bcdd7-222">![生成的文件](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成的文件")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-222">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="bcdd7-223">*生成的文件*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-223">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="bcdd7-224">任务 4-查询数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-224">Task 4 - Querying the Database</span></span>

<span data-ttu-id="bcdd7-225">在此任务中，你将更新 StoreController 类，以便不使用硬编码数据，它将查询要检索的信息的数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-225">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="bcdd7-226">打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**名为的类**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="bcdd7-226">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="bcdd7-227">(代码段-*模型的和数据访问-作为 Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-227">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="bcdd7-228">**MusicStoreEntities**类公开在数据库中每个表使用的集合属性。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-228">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="bcdd7-229">更新**浏览**操作方法来检索所有的一种风格**专辑**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-229">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="bcdd7-230">(代码段-*模型和数据访问-Ex1 存储浏览*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-230">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="bcdd7-231">正在使用的.NET 调用一项功能**LINQ** （语言集成查询） 来编写针对这些集合-将执行对数据库的代码并返回强类型查询表达式对象，您可以进行编程针对。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-231">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="bcdd7-232">有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-232">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="bcdd7-233">更新**索引**操作方法来检索所有风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-233">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="bcdd7-234">(代码段-*模型和数据访问-Ex1 存储索引*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-234">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="bcdd7-235">更新**索引**操作方法来检索所有风格和转换到列表的集合。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-235">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="bcdd7-236">(代码段-*模型和数据访问-Ex1 存储 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-236">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="bcdd7-237">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bcdd7-237">Task 5 - Running the Application</span></span>

<span data-ttu-id="bcdd7-238">在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-238">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="bcdd7-239">若要更改视图模板，因为无需**StoreController**和前面一样，将返回相同的实体，尽管这一次的数据将来自数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-239">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="bcdd7-240">重新生成解决方案，按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-240">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bcdd7-241">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-241">The project starts in the Home page.</span></span> <span data-ttu-id="bcdd7-242">验证的菜单**风格**不再是硬编码列表，并直接从数据库检索的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-242">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="bcdd7-244">*从数据库中浏览风格*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-244">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="bcdd7-245">现在浏览到任何流派，并确认专辑填充从数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-245">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="bcdd7-246">![从数据库中浏览专辑](aspnet-mvc-4-models-and-data-access/_static/image17.png "浏览专辑从数据库")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-246">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="bcdd7-247">*从数据库中浏览专辑*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-247">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="bcdd7-248">练习 2： 创建第一次使用代码的数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-248">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="bcdd7-249">在此练习中，你将了解如何使用代码第一种方法使用的表 MusicStore 应用程序，创建数据库以及如何访问其数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-249">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="bcdd7-250">后生成的模型，您将修改 StoreController 视图模板提供从数据库，而不是使用硬编码值获取的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-250">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-251">如果你已完成练习 1，并且已在使用数据库第一种方法，你现在将了解如何获取相同的结果与另一个进程。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-251">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="bcdd7-252">已标记与练习 1 相同的任务以方便你阅读。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-252">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="bcdd7-253">如果你尚未完成练习 1，但想要了解代码第一种方法，你可以从本练习中启动，并获取主题的方方面面。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-253">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="bcdd7-254">任务 1-填充示例数据</span><span class="sxs-lookup"><span data-stu-id="bcdd7-254">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="bcdd7-255">在此任务中，你将使用代码优先最初创建它时填充示例数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-255">In this task, you will populate the database with sample data when it is intially created using Code-First.</span></span>

1. <span data-ttu-id="bcdd7-256">打开**开始**解决方案位于**源/Ex2-CreatingADatabaseCodeFirst/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-256">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="bcdd7-257">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-257">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="bcdd7-258">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-258">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bcdd7-259">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-259">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="bcdd7-260">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-260">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="bcdd7-261">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-261">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-262">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-262">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bcdd7-263">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-263">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bcdd7-264">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-264">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bcdd7-265">添加**SampleData.cs**文件为**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-265">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="bcdd7-266">为此，请右键单击**模型**文件夹，指向**添加**，然后单击**现有项**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-266">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="bcdd7-267">浏览到**\Source\Assets**和选择**SampleData.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-267">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="bcdd7-268">![示例数据填充代码](aspnet-mvc-4-models-and-data-access/_static/image18.png "示例数据填充代码")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-268">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="bcdd7-269">*示例数据填充代码*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-269">*Sample data populate code*</span></span>
3. <span data-ttu-id="bcdd7-270">打开**Global.asax.cs**文件并添加以下*使用*语句。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-270">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="bcdd7-271">(代码段-*模型和数据访问-Ex2 全局 Asax Using*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-271">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="bcdd7-272">在**应用程序\_start （)**方法添加以下行以设置数据库初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-272">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="bcdd7-273">(代码段-*模型和数据访问-Ex2 全局 Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="bcdd7-274">任务 2-配置数据库的连接</span><span class="sxs-lookup"><span data-stu-id="bcdd7-274">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="bcdd7-275">现在，你已有数据库添加到我们的项目中，你将编写**Web.config**文件的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-275">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="bcdd7-276">添加连接字符串中的**Web.config**。为此，请打开**Web.config**在项目根和替换连接字符串中这一行与名为 DefaultConnection  **&lt;connectionStrings&gt;** 部分：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-276">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="bcdd7-277">![Web.config 文件位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 文件位置")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-277">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="bcdd7-278">*Web.config 文件位置*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-278">*Web.config file location*</span></span>


    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="bcdd7-279">任务 3-使用模型</span><span class="sxs-lookup"><span data-stu-id="bcdd7-279">Task 3 - Working with the Model</span></span>

<span data-ttu-id="bcdd7-280">现在，你已配置数据库的连接，你将链接的模型与数据库表。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-280">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="bcdd7-281">在此任务中，你将创建将链接到使用 Code First 数据库类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-281">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="bcdd7-282">请记住，应修改存在 POCO 模型类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-282">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-283">如果你完成练习 1 中，你将注意此步骤所执行的向导。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-283">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="bcdd7-284">通过执行 Code First，您将手动创建将链接到数据实体的类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-284">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>


1. <span data-ttu-id="bcdd7-285">打开 POCO 模型类**流派**从**模型**项目文件夹并包含一个 id。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-285">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="bcdd7-286">使用带名称的 int 属性**GenreId**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-286">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="bcdd7-287">(代码段-*模型和数据访问-Ex2 代码第一个流派*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-287">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="bcdd7-288">若要使用 Code First 的约定，此类流派必须具有主键属性，将自动检测到。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-288">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="bcdd7-289">你可以阅读更多有关代码中这第一个约定[msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-289">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="bcdd7-290">现在，打开 POCO 模型类**唱片集**从**模型**项目文件夹和包含外键，创建具有名称的属性**GenreId**和**ArtistId**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-290">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="bcdd7-291">此类已具有**GenreId**为主键。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-291">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="bcdd7-292">(代码段-*模型和数据访问-Ex2 代码第一个唱片集*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-292">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="bcdd7-293">打开 POCO 模型类**艺术家**和包括**ArtistId**属性。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-293">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="bcdd7-294">(代码段-*模型和数据访问-Ex2 代码第一个艺术家*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-294">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="bcdd7-295">右键单击**模型**项目文件夹，然后选择**添加 |类**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-295">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="bcdd7-296">命名该文件**MusicStoreEntities.cs**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-296">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="bcdd7-297">然后，单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="bcdd7-297">Then, click **Add.**</span></span>

    <span data-ttu-id="bcdd7-298">![添加类](aspnet-mvc-4-models-and-data-access/_static/image20.png "添加类")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-298">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="bcdd7-299">*添加新项*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-299">*Adding a new item*</span></span>

    <span data-ttu-id="bcdd7-300">![添加 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "添加 class2")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-300">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="bcdd7-301">*添加类*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-301">*Adding a class*</span></span>
5. <span data-ttu-id="bcdd7-302">打开你刚创建的类**MusicStoreEntities.cs**，包括命名空间和**System.Data.Entity**和**System.Data.Entity.Infrastructure**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-302">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="bcdd7-303">将类声明来扩展**DbContext**类： 声明一个公共**DBSet** ，并重写**OnModelCreating**方法。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-303">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="bcdd7-304">在此步骤后，你将收到将链接与实体框架模型的域类。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-304">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="bcdd7-305">为此，将替换为以下的类代码：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-305">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="bcdd7-306">(代码段-*模型和数据访问-Ex2 代码第一个 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-306">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="bcdd7-307">使用实体框架**DbContext**和**DBSet**你将能够查询 POCO 类风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-307">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="bcdd7-308">通过扩展**OnModelCreating**中指定的方法，**代码**如何风格将映射到数据库表。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-308">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="bcdd7-309">你可以在此 msdn 文章中找到有关 DBContext 和 DBSet 的详细信息：[链接](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-309">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="bcdd7-310">任务 4-查询数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-310">Task 4 - Querying the Database</span></span>

<span data-ttu-id="bcdd7-311">在此任务中，你将更新 StoreController 类，以便不使用硬编码数据，它将它从数据库中检索。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-311">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-312">此任务是与练习 1 相同。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-312">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="bcdd7-313">如果你完成练习 1 你将会注意这些步骤都相同，则这两种方法 (第一个数据库或代码第一次)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-313">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="bcdd7-314">它们仍然是不同中如何将数据链接模型，但尚未从控制器透明对数据实体的访问权限。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-314">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="bcdd7-315">打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**名为的类**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="bcdd7-315">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="bcdd7-316">(代码段-*模型的和数据访问-作为 Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-316">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="bcdd7-317">**MusicStoreEntities**类公开在数据库中每个表使用的集合属性。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-317">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="bcdd7-318">更新**浏览**操作方法来检索所有的一种风格**专辑**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-318">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="bcdd7-319">(代码段-*模型和数据访问-Ex2 存储浏览*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-319">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="bcdd7-320">正在使用的.NET 调用一项功能**LINQ** （语言集成查询） 来编写针对这些集合-将执行对数据库的代码并返回强类型查询表达式对象，您可以进行编程针对。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-320">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="bcdd7-321">有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-321">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="bcdd7-322">更新**索引**操作方法来检索所有风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-322">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="bcdd7-323">(代码段-*模型和数据访问-Ex2 存储索引*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-323">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="bcdd7-324">更新**索引**操作方法来检索所有风格和转换到列表的集合。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-324">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="bcdd7-325">(代码段-*模型和数据访问-Ex2 存储 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-325">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="bcdd7-326">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bcdd7-326">Task 5 - Running the Application</span></span>

<span data-ttu-id="bcdd7-327">在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-327">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="bcdd7-328">若要更改视图模板，因为无需**StoreController**返回相同**StoreIndexViewModel**和前面一样，但此数据将来自数据库的时间。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-328">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="bcdd7-329">重新生成解决方案，按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-329">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bcdd7-330">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-330">The project starts in the Home page.</span></span> <span data-ttu-id="bcdd7-331">验证的菜单**风格**不再是硬编码列表，并直接从数据库检索的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-331">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="bcdd7-333">*从数据库中浏览风格*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-333">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="bcdd7-334">现在浏览到任何流派，并确认专辑填充从数据库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-334">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="bcdd7-335">![从数据库中浏览专辑](aspnet-mvc-4-models-and-data-access/_static/image23.png "浏览专辑从数据库")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-335">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="bcdd7-336">*从数据库中浏览专辑*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-336">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="bcdd7-337">练习 3： 查询参数的数据库</span><span class="sxs-lookup"><span data-stu-id="bcdd7-337">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="bcdd7-338">在此练习中，您将了解如何使用参数，在数据库中查询以及如何使用查询结果调整，功能可减少号码数据库以更有效的方式访问中检索数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-338">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-339">有关查询结果调整的进一步信息，请访问以下[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-339">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>


<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="bcdd7-340">任务 1-修改 StoreController 从数据库检索专辑</span><span class="sxs-lookup"><span data-stu-id="bcdd7-340">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="bcdd7-341">在此任务中，你将更改**StoreController**类用于访问数据库来检索专辑从特定的风格。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-341">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="bcdd7-342">打开**开始**解决方案位于**Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin**文件夹，如果你想要使用代码为先的方法或**Source\Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin**文件夹，如果你想要使用数据库为先的方法。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-342">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="bcdd7-343">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-343">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="bcdd7-344">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-344">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bcdd7-345">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-345">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="bcdd7-346">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-346">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="bcdd7-347">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-347">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-348">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-348">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bcdd7-349">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-349">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bcdd7-350">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-350">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bcdd7-351">打开**StoreController**类更改**浏览**操作方法。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-351">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="bcdd7-352">为此，请在**解决方案资源管理器**，展开**控制器**文件夹并双击**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-352">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="bcdd7-353">更改**浏览**操作方法来检索特定流派唱片集。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-353">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="bcdd7-354">若要执行此操作，将以下代码：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-354">To do this, replace the following code:</span></span>

    <span data-ttu-id="bcdd7-355">(代码段-*模型和数据访问-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-355">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="bcdd7-356">若要填充的实体集合，你需要使用**包括**方法，以指定你想要太检索唱片集。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-356">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="bcdd7-357">你可以使用。**Single()** LINQ 中的扩展由于在这种情况下只有一个流派预期为唱片集。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-357">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="bcdd7-358">**Single()**方法采用 Lambda 表达式作为一个参数，它在此情况下指定单个流派对象，以便其名称与定义的值相匹配。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-358">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
    > 
    > <span data-ttu-id="bcdd7-359">你将利用一项功能，您可以指示检索流派对象时，你需要加载以及其他相关的实体。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-359">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="bcdd7-360">此功能称为**查询结果调整**，并使您能够减少需要用于访问数据库来检索信息的次数。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-360">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="bcdd7-361">在此方案中，你将想要为你检索流派预提取唱片集。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-361">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
    > 
    > <span data-ttu-id="bcdd7-362">该查询包含**Genres.Include (&quot;专辑&quot;)**以指示你想以及相关唱片集。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-362">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="bcdd7-363">这将导致更高效的应用程序，因为它会检索中的单个数据库请求 Genre 和唱片集的数据。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-363">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="bcdd7-364">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bcdd7-364">Task 2 - Running the Application</span></span>

<span data-ttu-id="bcdd7-365">在此任务中，将运行应用程序，并从数据库中检索特定流派专辑。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-365">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="bcdd7-366">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-366">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bcdd7-367">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-367">The project starts in the Home page.</span></span> <span data-ttu-id="bcdd7-368">将 URL 更改为**/存储/浏览？ 流派 = Pop**以验证正在从数据库检索的结果。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-368">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="bcdd7-369">![浏览按风格](aspnet-mvc-4-models-and-data-access/_static/image24.png "浏览按风格")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-369">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="bcdd7-370">*浏览/存储/浏览？ 流派 = Pop*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-370">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="bcdd7-371">任务 3-访问专辑按 Id</span><span class="sxs-lookup"><span data-stu-id="bcdd7-371">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="bcdd7-372">在此任务中，将重复前面的过程来获取专辑由其 id。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-372">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="bcdd7-373">关闭浏览器，如果需要可以返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-373">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="bcdd7-374">打开**StoreController**类更改**详细信息**操作方法。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-374">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="bcdd7-375">为此，请在**解决方案资源管理器**，展开**控制器**文件夹并双击**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-375">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="bcdd7-376">更改**详细信息**操作方法来检索唱片集详细信息基于其**Id**。若要执行此操作，将以下代码：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-376">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="bcdd7-377">(代码段-*模型和数据访问-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="bcdd7-377">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="bcdd7-378">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bcdd7-378">Task 4 - Running the Application</span></span>

<span data-ttu-id="bcdd7-379">在此任务中，你将在 web 浏览器中运行应用程序，并获得唱片集的详细信息，由其 id。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-379">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="bcdd7-380">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-380">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bcdd7-381">在主页页面中启动项目。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-381">The project starts in the Home page.</span></span> <span data-ttu-id="bcdd7-382">将 URL 更改为**/Store/Details/51**或浏览风格并选择唱片集以验证正在从数据库检索的结果。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-382">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="bcdd7-383">![浏览详细信息](aspnet-mvc-4-models-and-data-access/_static/image25.png "浏览详细信息")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-383">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="bcdd7-384">*浏览 /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-384">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd7-385">此外，你可以部署此应用程序对 Windows Azure 网站以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web Deploy](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-385">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="bcdd7-386">摘要</span><span class="sxs-lookup"><span data-stu-id="bcdd7-386">Summary</span></span>

<span data-ttu-id="bcdd7-387">通过完成本动手实验，你已经学习了 ASP.NET MVC 模型和数据访问的基础知识，请使用**Database First**方法以及**Code First**方法：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-387">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="bcdd7-388">如何将数据库添加到解决方案，以便使用其数据</span><span class="sxs-lookup"><span data-stu-id="bcdd7-388">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="bcdd7-389">如何更新控制器以向提供而不是硬编码的一个数据库中获取数据的视图模板</span><span class="sxs-lookup"><span data-stu-id="bcdd7-389">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="bcdd7-390">如何查询数据库中使用参数</span><span class="sxs-lookup"><span data-stu-id="bcdd7-390">How to query the database using parameters</span></span>
- <span data-ttu-id="bcdd7-391">如何使用查询结果调整，可以减少的数据库访问，一种更有效的方式检索数据</span><span class="sxs-lookup"><span data-stu-id="bcdd7-391">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="bcdd7-392">如何在 Microsoft 实体框架中使用数据库第一个和第一个代码方法，以将与模型数据库链接</span><span class="sxs-lookup"><span data-stu-id="bcdd7-392">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="bcdd7-393">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="bcdd7-393">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="bcdd7-394">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="bcdd7-394">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="bcdd7-395">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-395">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="bcdd7-396">转到[ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-396">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="bcdd7-397">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; *Visual Studio Express 2012 for Web 的 Windows Azure SDK*&quot;。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-397">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="bcdd7-398">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-398">Click on **Install Now**.</span></span> <span data-ttu-id="bcdd7-399">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-399">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="bcdd7-400">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-400">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="bcdd7-401">![安装 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-401">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="bcdd7-402">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-402">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="bcdd7-403">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-403">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="bcdd7-405">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-405">*Accepting the license terms*</span></span>
5. <span data-ttu-id="bcdd7-406">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-406">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="bcdd7-408">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-408">*Installation progress*</span></span>
6. <span data-ttu-id="bcdd7-409">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-409">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="bcdd7-411">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-411">*Installation completed*</span></span>
7. <span data-ttu-id="bcdd7-412">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-412">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="bcdd7-413">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-413">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="bcdd7-415">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-415">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bcdd7-416">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="bcdd7-416">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="bcdd7-417">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-417">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="bcdd7-418">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="bcdd7-418">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="bcdd7-419">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-419">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-420">使用 Windows Azure 可以免费承载 10 个 ASP.NET 网站，然后随着流量增长而扩展。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-420">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="bcdd7-421">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-421">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="bcdd7-422">![登录到 Windows Azure 门户](aspnet-mvc-4-models-and-data-access/_static/image31.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-422">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="bcdd7-423">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-423">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="bcdd7-424">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-424">Click **New** on the command bar.</span></span>

    <span data-ttu-id="bcdd7-425">![创建新网站](aspnet-mvc-4-models-and-data-access/_static/image32.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-425">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="bcdd7-426">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-426">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="bcdd7-427">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-427">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="bcdd7-428">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-428">Then select **Quick Create** option.</span></span> <span data-ttu-id="bcdd7-429">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-429">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-430">Windows Azure 网站是在云中，你可以控制和管理运行的 web 应用程序的宿主。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-430">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="bcdd7-431">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从在门户外部部署。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-431">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="bcdd7-432">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-432">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="bcdd7-433">![创建新的网站使用快速创建](aspnet-mvc-4-models-and-data-access/_static/image33.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-433">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="bcdd7-434">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-434">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="bcdd7-435">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-435">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="bcdd7-436">创建网站后单击下的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-436">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="bcdd7-437">检查新的 Web 站点工作。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-437">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="bcdd7-438">![浏览到新的 web 站点](aspnet-mvc-4-models-and-data-access/_static/image34.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-438">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="bcdd7-439">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-439">*Browsing to the new web site*</span></span>

    <span data-ttu-id="bcdd7-440">![运行网站](aspnet-mvc-4-models-and-data-access/_static/image35.png "运行的网站")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-440">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="bcdd7-441">*运行的网站*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-441">*Web site running*</span></span>
6. <span data-ttu-id="bcdd7-442">返回到门户并单击在网站的名称**名称**列以显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-442">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="bcdd7-443">![打开网站管理页](aspnet-mvc-4-models-and-data-access/_static/image36.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-443">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="bcdd7-444">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-444">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="bcdd7-445">在**仪表板**页上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-445">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-446">*发布配置文件*包含所有 web 应用程序发布到 Windows Azure 网站中的每个启用的发布方法所需的信息。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-446">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="bcdd7-447">发布配置文件包含的 Url、 用户凭据和连接到并针对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-447">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="bcdd7-448">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件以自动执行的这些程序，以便配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-448">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="bcdd7-449">![下载网站发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image37.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-449">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="bcdd7-450">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-450">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="bcdd7-451">到一个已知位置下载发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-451">Download the publish profile file to a known location.</span></span> <span data-ttu-id="bcdd7-452">进一步在本练习中您将了解如何使用此文件来发布 Visual Studio 中的 web 应用程序到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-452">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="bcdd7-453">![保存发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image38.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-453">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="bcdd7-454">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-454">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="bcdd7-455">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="bcdd7-455">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="bcdd7-456">如果你的应用程序将使用 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-456">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="bcdd7-457">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-457">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="bcdd7-458">需要将用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-458">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="bcdd7-459">你可以从你的订阅在 Windows Azure 管理门户中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-459">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="bcdd7-460">如果你没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-460">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="bcdd7-461">请记下的**服务器名称和 URL、 管理员登录名和密码**，如你将在接下来的任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-461">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="bcdd7-462">不创建数据库，它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-462">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="bcdd7-463">![SQL 数据库服务器仪表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-463">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="bcdd7-464">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-464">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="bcdd7-465">在下一个任务将测试从 Visual Studio 中，数据库连接，因此你需要在的服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-465">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="bcdd7-466">若要做到这一点，请单击**配置**，选择的 IP 地址从**当前客户端 IP 地址**并将其粘贴在**起始 IP 地址**和**结束 IP 地址**文本框和单击![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-466">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="bcdd7-468">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-468">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="bcdd7-469">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-469">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认做的更改](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="bcdd7-471">*确认做的更改*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-471">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bcdd7-472">任务 3-发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="bcdd7-472">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="bcdd7-473">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-473">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="bcdd7-474">在**解决方案资源管理器**，右键单击网站项目，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-474">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="bcdd7-475">![发布应用程序](aspnet-mvc-4-models-and-data-access/_static/image43.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-475">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="bcdd7-476">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-476">*Publishing the web site*</span></span>
2. <span data-ttu-id="bcdd7-477">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-477">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="bcdd7-478">![导入发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image44.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-478">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="bcdd7-479">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-479">*Importing publish profile*</span></span>
3. <span data-ttu-id="bcdd7-480">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-480">Click **Validate Connection**.</span></span> <span data-ttu-id="bcdd7-481">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-481">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bcdd7-482">请参阅验证连接按钮旁边将显示绿色的复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-482">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="bcdd7-483">![正在验证连接](aspnet-mvc-4-models-and-data-access/_static/image45.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-483">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="bcdd7-484">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-484">*Validating connection*</span></span>
4. <span data-ttu-id="bcdd7-485">在**设置**页上，在**数据库**部分中，单击你的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-485">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="bcdd7-486">![Web 部署配置](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-486">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="bcdd7-487">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-487">*Web deploy configuration*</span></span>
5. <span data-ttu-id="bcdd7-488">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bcdd7-488">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="bcdd7-489">在**服务器名称**类型 SQL 数据库服务器 URL 使用*tcp:*前缀。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-489">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="bcdd7-490">在**用户名**键入您的服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-490">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="bcdd7-491">在**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-491">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="bcdd7-492">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-492">Type a new database name.</span></span>

    <span data-ttu-id="bcdd7-493">![配置目标连接字符串](aspnet-mvc-4-models-and-data-access/_static/image47.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-493">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="bcdd7-494">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-494">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="bcdd7-495">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-495">Then click **OK**.</span></span> <span data-ttu-id="bcdd7-496">当系统提示创建数据库单击**是**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-496">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="bcdd7-497">![创建数据库](aspnet-mvc-4-models-and-data-access/_static/image48.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-497">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="bcdd7-498">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-498">*Creating the database*</span></span>
7. <span data-ttu-id="bcdd7-499">在默认连接文本框中显示了将用于连接到 Windows Azure 中的 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-499">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="bcdd7-500">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-500">Then click **Next**.</span></span>

    <span data-ttu-id="bcdd7-501">![连接字符串指向 SQL 数据库](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-501">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="bcdd7-502">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-502">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="bcdd7-503">在**预览**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-503">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="bcdd7-504">![Web 应用程序发布](aspnet-mvc-4-models-and-data-access/_static/image50.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-504">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="bcdd7-505">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-505">*Publishing the web application*</span></span>
9. <span data-ttu-id="bcdd7-506">完成发布过程后，默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-506">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="bcdd7-507">附录 c： 使用代码段</span><span class="sxs-lookup"><span data-stu-id="bcdd7-507">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="bcdd7-508">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-508">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="bcdd7-509">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-509">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="bcdd7-510">![使用 Visual Studio 代码段将代码插入到你的项目](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-510">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="bcdd7-511">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-511">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="bcdd7-512">***若要添加代码片段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="bcdd7-512">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="bcdd7-513">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-513">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="bcdd7-514">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-514">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="bcdd7-515">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-515">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="bcdd7-516">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-516">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="bcdd7-517">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-517">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="bcdd7-518">![开始键入代码段名称](aspnet-mvc-4-models-and-data-access/_static/image52.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-518">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="bcdd7-519">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-519">*Start typing the snippet name*</span></span>

<span data-ttu-id="bcdd7-520">![按 Tab 以选择突出显示代码段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-520">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="bcdd7-521">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-521">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="bcdd7-522">![再次按 Tab 和代码段将会扩展](aspnet-mvc-4-models-and-data-access/_static/image54.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-522">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="bcdd7-523">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-523">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="bcdd7-524">***若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-524">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="bcdd7-525">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-525">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="bcdd7-526">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-526">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="bcdd7-527">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="bcdd7-527">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="bcdd7-528">![右键单击你想要插入代码段，并选择插入代码段](aspnet-mvc-4-models-and-data-access/_static/image55.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-528">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="bcdd7-529">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-529">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="bcdd7-530">![通过单击它选取列表中中的相关代码片段](aspnet-mvc-4-models-and-data-access/_static/image56.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="bcdd7-530">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="bcdd7-531">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="bcdd7-531">*Pick the relevant snippet from the list, by clicking on it*</span></span>
