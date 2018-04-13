---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用实体框架 (C#) 创建模型类 |Microsoft 文档
author: microsoft
description: 在本教程中，您将学习如何与 Microsoft 实体框架使用 ASP.NET MVC。 了解如何使用实体向导创建 ADO.NET 实体 Da...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: b0a79da580f14d5ae6bcfaaa00d3900234dc662e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-model-classes-with-the-entity-framework-c"></a><span data-ttu-id="b2603-104">使用实体框架 (C#) 创建模型类</span><span class="sxs-lookup"><span data-stu-id="b2603-104">Creating Model Classes with the Entity Framework (C#)</span></span>
====================
<span data-ttu-id="b2603-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b2603-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b2603-106">在本教程中，您将学习如何与 Microsoft 实体框架使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="b2603-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="b2603-107">了解如何使用实体向导创建 ADO.NET 实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b2603-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="b2603-108">在本教程的过程中，我们生成的 web 应用程序演示如何以选择、 插入、 更新和删除通过使用实体框架的数据库数据。</span><span class="sxs-lookup"><span data-stu-id="b2603-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>


<span data-ttu-id="b2603-109">本教程旨在说明如何创建生成 ASP.NET MVC 应用程序时使用 Microsoft 实体框架的数据访问类。</span><span class="sxs-lookup"><span data-stu-id="b2603-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="b2603-110">本教程假定之前不了解的 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="b2603-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="b2603-111">本教程结束时，你将了解如何使用实体框架来选择、 插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b2603-112">Microsoft 实体框架是一种对象关系映射 (O/RM) 工具，使您能够从数据库中自动生成的数据访问层。</span><span class="sxs-lookup"><span data-stu-id="b2603-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="b2603-113">实体框架，可避免手动生成你的数据访问类的繁琐工作。</span><span class="sxs-lookup"><span data-stu-id="b2603-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

<span data-ttu-id="b2603-114">为了说明如何使用 Microsoft 实体框架使用 ASP.NET MVC，我们将生成一个简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="b2603-114">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="b2603-115">我们将创建的电影数据库应用程序，可显示和编辑电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-115">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="b2603-116">本教程假定你有 Visual Studio 2008 或 Visual Web Developer 2008 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="b2603-116">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="b2603-117">若要使用实体框架需要 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="b2603-117">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="b2603-118">你可以从以下地址下载 Visual Studio 2008 Service Pack 1 或 Service Pack 1 的 Visual Web Developer:</span><span class="sxs-lookup"><span data-stu-id="b2603-118">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)


> [!NOTE] 
> 
> <span data-ttu-id="b2603-119">ASP.NET MVC 和 Microsoft 实体框架之间没有基本连接。</span><span class="sxs-lookup"><span data-stu-id="b2603-119">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b2603-120">有多种可选方案对你可以使用使用 ASP.NET MVC 的 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="b2603-120">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="b2603-121">例如，你可以构建使用其他 O/RM 工具，如 Microsoft LINQ to SQL、 NHibernate 或 SubSonic 你 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="b2603-121">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>


## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="b2603-122">创建电影示例数据库</span><span class="sxs-lookup"><span data-stu-id="b2603-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="b2603-123">电影数据库应用程序使用名为电影的数据库表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="b2603-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="b2603-124">列名</span><span class="sxs-lookup"><span data-stu-id="b2603-124">Column Name</span></span> | <span data-ttu-id="b2603-125">数据类型</span><span class="sxs-lookup"><span data-stu-id="b2603-125">Data Type</span></span> | <span data-ttu-id="b2603-126">允许 null 值？</span><span class="sxs-lookup"><span data-stu-id="b2603-126">Allow Nulls?</span></span> | <span data-ttu-id="b2603-127">是主键？</span><span class="sxs-lookup"><span data-stu-id="b2603-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2603-128">Id</span><span class="sxs-lookup"><span data-stu-id="b2603-128">Id</span></span> | <span data-ttu-id="b2603-129">int</span><span class="sxs-lookup"><span data-stu-id="b2603-129">int</span></span> | <span data-ttu-id="b2603-130">False</span><span class="sxs-lookup"><span data-stu-id="b2603-130">False</span></span> | <span data-ttu-id="b2603-131">True</span><span class="sxs-lookup"><span data-stu-id="b2603-131">True</span></span> |
| <span data-ttu-id="b2603-132">标题</span><span class="sxs-lookup"><span data-stu-id="b2603-132">Title</span></span> | <span data-ttu-id="b2603-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="b2603-133">nvarchar(100)</span></span> | <span data-ttu-id="b2603-134">False</span><span class="sxs-lookup"><span data-stu-id="b2603-134">False</span></span> | <span data-ttu-id="b2603-135">False</span><span class="sxs-lookup"><span data-stu-id="b2603-135">False</span></span> |
| <span data-ttu-id="b2603-136">控制器</span><span class="sxs-lookup"><span data-stu-id="b2603-136">Director</span></span> | <span data-ttu-id="b2603-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="b2603-137">nvarchar(100)</span></span> | <span data-ttu-id="b2603-138">False</span><span class="sxs-lookup"><span data-stu-id="b2603-138">False</span></span> | <span data-ttu-id="b2603-139">False</span><span class="sxs-lookup"><span data-stu-id="b2603-139">False</span></span> |

<span data-ttu-id="b2603-140">通过执行以下步骤，可以将此表添加到 ASP.NET MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="b2603-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="b2603-141">右键单击该应用\_在解决方案资源管理器窗口中，然后选择菜单选项的数据文件夹**添加、 新项。**</span><span class="sxs-lookup"><span data-stu-id="b2603-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="b2603-142">从**添加新项**对话框中，选择**SQL Server 数据库**，使数据库名称 MoviesDB.mdf，并单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="b2603-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="b2603-143">双击 MoviesDB.mdf 文件以打开服务器资源管理器/数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="b2603-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="b2603-144">展开 MoviesDB.mdf 数据库连接，右键单击表文件夹中，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="b2603-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="b2603-145">在表设计器中，添加的 Id、 标题和控制器列。</span><span class="sxs-lookup"><span data-stu-id="b2603-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="b2603-146">单击**保存**（它具有的软盘图标） 的按钮以保存新的表中名称电影。</span><span class="sxs-lookup"><span data-stu-id="b2603-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="b2603-147">创建电影数据库表后，你应将一些示例数据添加到表中。</span><span class="sxs-lookup"><span data-stu-id="b2603-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="b2603-148">右键单击的电影表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="b2603-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="b2603-149">可以将假影片数据输入出现的网格中。</span><span class="sxs-lookup"><span data-stu-id="b2603-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="b2603-150">创建 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="b2603-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b2603-151">若要使用实体框架，你需要创建实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b2603-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="b2603-152">你可以利用 Visual Studio*实体数据模型向导*自动从数据库生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b2603-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="b2603-153">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="b2603-153">Follow these steps:</span></span>

1. <span data-ttu-id="b2603-154">右键单击解决方案资源管理器窗口中的 Models 文件夹，然后选择菜单选项**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="b2603-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="b2603-155">在**添加新项**对话框中，选择数据类别 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="b2603-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="b2603-156">选择**ADO.NET 实体数据模型**模板，为实体数据模型提供的名称 MoviesDBModel.edmx，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="b2603-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="b2603-157">单击**添加**按钮会启动数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="b2603-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="b2603-158">在**选择模型内容**步骤中，选择**从数据库生成**选项，然后单击**下一步**按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="b2603-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="b2603-159">在**选择你的数据连接**步骤，选择 MoviesDB.mdf 数据库连接，输入的实体连接设置命名 MoviesDBEntities，并单击**下一步**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="b2603-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="b2603-160">在**选择数据库对象**步骤，选择电影数据库表，然后单击**完成**按钮 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="b2603-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="b2603-161">完成这些步骤后，将打开 ADO.NET 实体数据模型设计器 （实体设计器）。</span><span class="sxs-lookup"><span data-stu-id="b2603-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="b2603-162">**图 1 – 创建新的实体数据模型**</span><span class="sxs-lookup"><span data-stu-id="b2603-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

<span data-ttu-id="b2603-164">**图 2 – 选择模型内容步骤**</span><span class="sxs-lookup"><span data-stu-id="b2603-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

<span data-ttu-id="b2603-166">**图 3-选择你的数据连接**</span><span class="sxs-lookup"><span data-stu-id="b2603-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

<span data-ttu-id="b2603-168">**图 4-选择数据库对象**</span><span class="sxs-lookup"><span data-stu-id="b2603-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="b2603-170">修改 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="b2603-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b2603-171">创建实体数据模型后，你可以通过利用在实体设计器中修改模型 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="b2603-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="b2603-172">通过双击解决方案资源管理器窗口中的 Models 文件夹中包含的 MoviesDBModel.edmx 文件，可以在任何时候打开实体设计器。</span><span class="sxs-lookup"><span data-stu-id="b2603-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="b2603-173">**图 5 – ADO.NET 实体数据模型设计器**</span><span class="sxs-lookup"><span data-stu-id="b2603-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

<span data-ttu-id="b2603-175">例如，实体设计器可用于更改的实体模型数据向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="b2603-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="b2603-176">该向导创建一个新的名为电影的数据访问类。</span><span class="sxs-lookup"><span data-stu-id="b2603-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="b2603-177">换而言之，该向导为类提供了与数据库表非常相同的名称。</span><span class="sxs-lookup"><span data-stu-id="b2603-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="b2603-178">因为我们将使用此类来表示特定电影实例，我们应该重命名电影电影的类。</span><span class="sxs-lookup"><span data-stu-id="b2603-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="b2603-179">如果你想要重命名的实体类，你可以双击实体设计器中的类名称，输入新名称 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="b2603-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="b2603-180">或者，你可以在实体设计器中选择实体后更改属性窗口中的实体的名称。</span><span class="sxs-lookup"><span data-stu-id="b2603-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="b2603-181">**图 6 – 更改实体名称**</span><span class="sxs-lookup"><span data-stu-id="b2603-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

<span data-ttu-id="b2603-183">请记住保存通过单击保存按钮 （软盘图标） 进行了修改后的实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b2603-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="b2603-184">在后台，实体设计器生成一组的 C# 类。</span><span class="sxs-lookup"><span data-stu-id="b2603-184">Behind the scenes, the Entity Designer generates a set of C# classes.</span></span> <span data-ttu-id="b2603-185">你可以通过从解决方案资源管理器窗口中打开 MoviesDBModel.Designer.cs 文件来查看这些类。</span><span class="sxs-lookup"><span data-stu-id="b2603-185">You can view these classes by opening the MoviesDBModel.Designer.cs file from the Solution Explorer window.</span></span>


<span data-ttu-id="b2603-186">由于所做的更改将覆盖下次使用实体设计器时，不要修改 Designer.cs 文件中的代码。</span><span class="sxs-lookup"><span data-stu-id="b2603-186">Don't modify the code in the Designer.cs file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="b2603-187">如果你想要扩展 Designer.cs 文件中定义的实体类的功能，则可以创建*分部类*在单独的文件。</span><span class="sxs-lookup"><span data-stu-id="b2603-187">If you want to extend the functionality of the entity classes defined in the Designer.cs file then you can create *partial classes* in separate files.</span></span>


#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="b2603-188">选择与实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="b2603-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b2603-189">让我们开始构建我们电影数据库应用程序创建页，显示的电影记录的列表。</span><span class="sxs-lookup"><span data-stu-id="b2603-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="b2603-190">列表 1 中的主页控制器公开名为 index （） 的操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="b2603-191">Index （） 操作返回的所有影片记录电影数据库表中通过利用的实体框架。</span><span class="sxs-lookup"><span data-stu-id="b2603-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="b2603-192">**列表 1 – Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="b2603-192">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

<span data-ttu-id="b2603-193">请注意列表 1 中的控制器包含一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="b2603-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="b2603-194">构造函数初始化名为的类级字段\_db。</span><span class="sxs-lookup"><span data-stu-id="b2603-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="b2603-195">\_Db 字段表示生成的 Microsoft 实体框架的数据库实体。</span><span class="sxs-lookup"><span data-stu-id="b2603-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="b2603-196">\_Db 字段是由实体设计器生成的 MoviesDBEntities 类的实例。</span><span class="sxs-lookup"><span data-stu-id="b2603-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>


<span data-ttu-id="b2603-197">为了在主控制器中使用 theMoviesDBEntities 类，你必须导入 MovieEntityApp.Models 命名空间 (*MVCProjectName*。模型）。</span><span class="sxs-lookup"><span data-stu-id="b2603-197">In order to use theMoviesDBEntities class in the Home controller, you must import the MovieEntityApp.Models namespace (*MVCProjectName*.Models).</span></span>


<span data-ttu-id="b2603-198">\_Db 字段使用 index （） 操作中，若要检索电影数据库表中的记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-198">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="b2603-199">表达式\_db。MovieSet 表示的所有记录电影数据库表中。</span><span class="sxs-lookup"><span data-stu-id="b2603-199">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="b2603-200">Tolist （） 方法用于将电影该集转换到的电影对象的泛型集合 (列表&lt;电影&gt;)。</span><span class="sxs-lookup"><span data-stu-id="b2603-200">The ToList() method is used to convert the set of movies into a generic collection of Movie objects (List&lt;Movie&gt;).</span></span>

<span data-ttu-id="b2603-201">LINQ to Entities 的帮助检索电影记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-201">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="b2603-202">列表 1 中的 index （） 操作使用 LINQ*方法语法*检索的数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="b2603-202">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="b2603-203">如果你愿意，你可以使用 LINQ*查询语法*相反。</span><span class="sxs-lookup"><span data-stu-id="b2603-203">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="b2603-204">下面的两个语句执行非常相同的操作：</span><span class="sxs-lookup"><span data-stu-id="b2603-204">The following two statements do the very same thing:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

<span data-ttu-id="b2603-205">使用你发现最直观无论 LINQ 语法 – 方法语法或查询语法 –。</span><span class="sxs-lookup"><span data-stu-id="b2603-205">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="b2603-206">没有任何区别两种方法之间的性能 – 唯一的区别是样式。</span><span class="sxs-lookup"><span data-stu-id="b2603-206">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="b2603-207">列出 2 中的视图用于显示电影记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-207">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="b2603-208">**列出 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="b2603-208">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

<span data-ttu-id="b2603-209">列出 2 中的视图包含**foreach**循环，循环访问每个电影记录，并显示电影记录的标题和控制器属性的值。</span><span class="sxs-lookup"><span data-stu-id="b2603-209">The view in Listing 2 contains a **foreach** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="b2603-210">请注意，每个记录旁边显示的编辑和删除链接。</span><span class="sxs-lookup"><span data-stu-id="b2603-210">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="b2603-211">此外，该视图的底部将显示添加电影链接 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="b2603-211">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="b2603-212">**图 7-索引视图**</span><span class="sxs-lookup"><span data-stu-id="b2603-212">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

<span data-ttu-id="b2603-214">索引视图是*类型化视图*。</span><span class="sxs-lookup"><span data-stu-id="b2603-214">The Index view is a *typed view*.</span></span> <span data-ttu-id="b2603-215">索引视图包括&lt;%@ 页 %&gt;指令与*Inherits*将强制转换的电影对象强类型化的泛型列表集合的模型属性的属性 (列表&lt;电影)。</span><span class="sxs-lookup"><span data-stu-id="b2603-215">The Index view includes a &lt;%@ Page %&gt; directive with an *Inherits* attribute that casts the Model property to a strongly typed generic List collection of Movie objects (List&lt;Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="b2603-216">插入与实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="b2603-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b2603-217">可以使用实体框架，以便可以方便地将新记录插入数据库表。</span><span class="sxs-lookup"><span data-stu-id="b2603-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="b2603-218">列出 3 包含两个新的操作添加到 Home 控制器类可用于将新记录插入电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="b2603-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="b2603-219">**列出 3 – Controllers\HomeController.cs （Add 方法）**</span><span class="sxs-lookup"><span data-stu-id="b2603-219">**Listing 3 – Controllers\HomeController.cs (Add methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

<span data-ttu-id="b2603-220">第一项 add （） 操作只需返回的视图。</span><span class="sxs-lookup"><span data-stu-id="b2603-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="b2603-221">该视图包含用于添加新的影片数据库的窗体记录 （请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="b2603-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="b2603-222">当在提交表单时，将调用第二个 add （） 操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="b2603-223">请注意，使用 AcceptVerbs 特性修饰的第二个 add （） 操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="b2603-224">只有在执行 HTTP POST 操作时，可以调用此操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="b2603-225">换而言之，仅当发布 HTML 窗体时，才可以调用此操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="b2603-226">第二个 add （） 操作创建 ASP.NET MVC TryUpdateModel() 方法的帮助的实体框架电影类的新实例。</span><span class="sxs-lookup"><span data-stu-id="b2603-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="b2603-227">TryUpdateModel() 方法采用传递给 add （） 方法 FormCollection 中的字段，并将这些 HTML 窗体字段的值分配给电影类。</span><span class="sxs-lookup"><span data-stu-id="b2603-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>


<span data-ttu-id="b2603-228">在使用实体框架时，使用的 TryUpdateModel 或 UpdateModel 方法来更新实体类的属性时，必须提供"允许列表"的属性。</span><span class="sxs-lookup"><span data-stu-id="b2603-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>


<span data-ttu-id="b2603-229">接下来，add （） 操作执行一些简单的表单验证。</span><span class="sxs-lookup"><span data-stu-id="b2603-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="b2603-230">操作可验证的标题和控制器属性具有值。</span><span class="sxs-lookup"><span data-stu-id="b2603-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="b2603-231">如果没有验证错误，则会将验证错误消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="b2603-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="b2603-232">如果没有任何验证错误然后会将新的影片记录添加到实体框架的帮助的电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="b2603-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="b2603-233">新的记录添加到以下两行代码的数据库：</span><span class="sxs-lookup"><span data-stu-id="b2603-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

<span data-ttu-id="b2603-234">第一行代码将新的影片实体添加到跟踪的实体框架的电影的集。</span><span class="sxs-lookup"><span data-stu-id="b2603-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="b2603-235">代码的第二行将保存到电影跟踪返回到基础数据库进行了任何更改。</span><span class="sxs-lookup"><span data-stu-id="b2603-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="b2603-236">**图 8-添加视图**</span><span class="sxs-lookup"><span data-stu-id="b2603-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="b2603-238">与实体框架的更新数据库记录</span><span class="sxs-lookup"><span data-stu-id="b2603-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="b2603-239">你可以按照几乎相同的方法来编辑与实体框架的数据库记录为我们刚插入的新的数据库记录的方法。</span><span class="sxs-lookup"><span data-stu-id="b2603-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="b2603-240">列出 4 包含名为 edit （） 的两个新控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="b2603-241">第一个 edit （） 操作返回用于编辑电影记录 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="b2603-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="b2603-242">第二个 edit （） 操作尝试更新数据库。</span><span class="sxs-lookup"><span data-stu-id="b2603-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="b2603-243">**列出 4 – Controllers\HomeController.cs （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="b2603-243">**Listing 4 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

<span data-ttu-id="b2603-244">通过从与正在编辑的影片的 Id 匹配的数据库中检索的影片记录启动第二个 edit （） 操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="b2603-245">以下受 LINQ to Entities 语句获取的特定 Id 匹配的第一条数据库记录：</span><span class="sxs-lookup"><span data-stu-id="b2603-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

<span data-ttu-id="b2603-246">接下来，TryUpdateModel() 方法用于将 HTML 窗体字段的值分配给电影实体的属性。</span><span class="sxs-lookup"><span data-stu-id="b2603-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="b2603-247">请注意，提供允许列表来指定要更新的确切属性。</span><span class="sxs-lookup"><span data-stu-id="b2603-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="b2603-248">接下来，执行一些简单的验证，以便验证影片标题和控制器属性具有值。</span><span class="sxs-lookup"><span data-stu-id="b2603-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="b2603-249">如果这两个属性缺少一个值，然后验证错误消息添加到 ModelState 并 ModelState.IsValid 返回值 false。</span><span class="sxs-lookup"><span data-stu-id="b2603-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="b2603-250">最后，如果不不存在任何验证错误，然后基础的电影数据库表是使用更新的任何更改通过调用 savechanges （） 方法。</span><span class="sxs-lookup"><span data-stu-id="b2603-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="b2603-251">在编辑数据库记录时，请将传递到执行数据库更新的控制器操作正在编辑的记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="b2603-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="b2603-252">否则，控制器操作不会知道哪一记录基础数据库中更新。</span><span class="sxs-lookup"><span data-stu-id="b2603-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="b2603-253">包含在列出 5 中，编辑视图包括隐藏的表单字段表示正在编辑的数据库记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="b2603-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="b2603-254">**列出 5 – Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="b2603-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="b2603-255">删除与实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="b2603-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b2603-256">最终的数据库操作，我们需要处理在本教程中，正在删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="b2603-257">可以使用列出 6 中的控制器操作以删除特定的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="b2603-258">**列出 6-\Controllers\HomeController.cs （删除操作）**</span><span class="sxs-lookup"><span data-stu-id="b2603-258">**Listing 6 -- \Controllers\HomeController.cs (Delete action)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

<span data-ttu-id="b2603-259">Delete （） 操作首先检索的影片的 Id 匹配的实体传递到操作。</span><span class="sxs-lookup"><span data-stu-id="b2603-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="b2603-260">接下来，影片从数据库删除通过调用 DeleteObject() 方法跟 savechanges （） 方法。</span><span class="sxs-lookup"><span data-stu-id="b2603-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="b2603-261">最后，用户重定向回索引视图。</span><span class="sxs-lookup"><span data-stu-id="b2603-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="b2603-262">总结</span><span class="sxs-lookup"><span data-stu-id="b2603-262">Summary</span></span>

<span data-ttu-id="b2603-263">本教程的目的是演示如何利用 ASP.NET MVC 和 Microsoft 实体框架可以生成数据库驱动的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b2603-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b2603-264">您学习了如何生成该应用程序，你可以选择、 插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b2603-265">首先，我们讨论了如何使用实体数据模型向导生成 Visual Studio 中从一个实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b2603-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="b2603-266">接下来，你将了解如何使用 LINQ to Entities 从数据库表中检索一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="b2603-267">最后，我们使用实体框架来插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b2603-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b2603-268">下一篇</span><span class="sxs-lookup"><span data-stu-id="b2603-268">Next</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
