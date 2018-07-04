---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: 使用实体框架 (VB) 创建模型类 |Microsoft Docs
author: microsoft
description: 在本教程中，您将学习如何使用 Microsoft Entity Framework 的 ASP.NET MVC。 了解如何使用实体向导来创建 ADO.NET 实体数据...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: efb8d7206cba2fd5d8db1817d57a4e2813cb5ace
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377183"
---
<a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="0ceda-104">使用实体框架 (VB) 创建模型类</span><span class="sxs-lookup"><span data-stu-id="0ceda-104">Creating Model Classes with the Entity Framework (VB)</span></span>
====================
<span data-ttu-id="0ceda-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0ceda-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0ceda-106">在本教程中，您将学习如何使用 Microsoft Entity Framework 的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="0ceda-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="0ceda-107">了解如何使用实体向导创建一个 ADO.NET 实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ceda-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="0ceda-108">在本教程的过程中，我们构建的 web 应用程序演示了如何选择、 插入、 更新和删除数据库数据使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="0ceda-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>


<span data-ttu-id="0ceda-109">本教程的目的是说明如何创建生成的 ASP.NET MVC 应用程序时使用 Microsoft Entity Framework 数据访问类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="0ceda-110">本教程之前不了解 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="0ceda-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="0ceda-111">本教程结束时，您将了解如何使用实体框架来选择、 插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="0ceda-112">Microsoft Entity Framework 是一种对象关系映射 (O/RM) 工具，可用于从数据库中自动生成的数据访问层。</span><span class="sxs-lookup"><span data-stu-id="0ceda-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="0ceda-113">实体框架可以避免手动生成的数据访问类的枯燥乏味的工作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0ceda-114">没有基本 ASP.NET MVC 和 Microsoft 实体框架之间的连接。</span><span class="sxs-lookup"><span data-stu-id="0ceda-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="0ceda-115">有多种替代方法可用于 ASP.NET MVC 的 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="0ceda-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="0ceda-116">例如，可以构建使用 Microsoft LINQ to SQL、 NHibernate 或 SubSonic 等其他 O/RM 工具在 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>


<span data-ttu-id="0ceda-117">为了说明如何使用 ASP.NET MVC 使用 Microsoft Entity Framework，我们将构建一个简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ceda-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="0ceda-118">我们将创建一个电影数据库应用程序，可用于显示和编辑电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="0ceda-119">本教程假定你有 Visual Studio 2008 或 Visual Web Developer 2008 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="0ceda-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="0ceda-120">若要使用实体框架需要 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="0ceda-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="0ceda-121">可以从以下地址下载 Visual Studio 2008 Service Pack 1 或 Service Pack 1 的 Visual Web Developer:</span><span class="sxs-lookup"><span data-stu-id="0ceda-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)


## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="0ceda-122">创建电影示例数据库</span><span class="sxs-lookup"><span data-stu-id="0ceda-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="0ceda-123">电影数据库应用程序使用名为电影的数据库表，包含以下列：</span><span class="sxs-lookup"><span data-stu-id="0ceda-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="0ceda-124">列名</span><span class="sxs-lookup"><span data-stu-id="0ceda-124">Column Name</span></span> | <span data-ttu-id="0ceda-125">数据类型</span><span class="sxs-lookup"><span data-stu-id="0ceda-125">Data Type</span></span> | <span data-ttu-id="0ceda-126">允许 null 值？</span><span class="sxs-lookup"><span data-stu-id="0ceda-126">Allow Nulls?</span></span> | <span data-ttu-id="0ceda-127">是主键？</span><span class="sxs-lookup"><span data-stu-id="0ceda-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ceda-128">Id</span><span class="sxs-lookup"><span data-stu-id="0ceda-128">Id</span></span> | <span data-ttu-id="0ceda-129">int</span><span class="sxs-lookup"><span data-stu-id="0ceda-129">int</span></span> | <span data-ttu-id="0ceda-130">False</span><span class="sxs-lookup"><span data-stu-id="0ceda-130">False</span></span> | <span data-ttu-id="0ceda-131">True</span><span class="sxs-lookup"><span data-stu-id="0ceda-131">True</span></span> |
| <span data-ttu-id="0ceda-132">标题</span><span class="sxs-lookup"><span data-stu-id="0ceda-132">Title</span></span> | <span data-ttu-id="0ceda-133">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="0ceda-133">nvarchar(100)</span></span> | <span data-ttu-id="0ceda-134">False</span><span class="sxs-lookup"><span data-stu-id="0ceda-134">False</span></span> | <span data-ttu-id="0ceda-135">False</span><span class="sxs-lookup"><span data-stu-id="0ceda-135">False</span></span> |
| <span data-ttu-id="0ceda-136">主管</span><span class="sxs-lookup"><span data-stu-id="0ceda-136">Director</span></span> | <span data-ttu-id="0ceda-137">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="0ceda-137">nvarchar(100)</span></span> | <span data-ttu-id="0ceda-138">False</span><span class="sxs-lookup"><span data-stu-id="0ceda-138">False</span></span> | <span data-ttu-id="0ceda-139">False</span><span class="sxs-lookup"><span data-stu-id="0ceda-139">False</span></span> |

<span data-ttu-id="0ceda-140">通过执行以下步骤，可以将此表添加到 ASP.NET MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="0ceda-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="0ceda-141">右键单击该应用\_在解决方案资源管理器窗口中，选择菜单选项的数据文件夹**添加、 新项。**</span><span class="sxs-lookup"><span data-stu-id="0ceda-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="0ceda-142">从**添加新项**对话框中，选择**SQL Server 数据库**，为数据库名称 MoviesDB.mdf，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="0ceda-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="0ceda-143">双击 MoviesDB.mdf 文件以打开服务器资源管理器/数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="0ceda-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="0ceda-144">展开 MoviesDB.mdf 数据库连接，右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="0ceda-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="0ceda-145">在表设计器中，将添加的 Id、 标题和主管的列。</span><span class="sxs-lookup"><span data-stu-id="0ceda-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="0ceda-146">单击**保存**（它具有的软盘图标） 按钮以保存新表中的名称电影。</span><span class="sxs-lookup"><span data-stu-id="0ceda-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="0ceda-147">创建电影数据库表后，应将一些示例数据添加到表。</span><span class="sxs-lookup"><span data-stu-id="0ceda-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="0ceda-148">右键单击电影表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="0ceda-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="0ceda-149">可以伪造电影数据输入到出现的网格中。</span><span class="sxs-lookup"><span data-stu-id="0ceda-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="0ceda-150">创建 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="0ceda-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="0ceda-151">若要使用实体框架，您需要创建实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ceda-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="0ceda-152">您可以充分利用 Visual Studio*实体数据模型向导*自动从数据库生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ceda-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="0ceda-153">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="0ceda-153">Follow these steps:</span></span>

1. <span data-ttu-id="0ceda-154">右键单击解决方案资源管理器窗口中的 Models 文件夹，然后选择菜单选项**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="0ceda-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="0ceda-155">在中**添加新项**对话框中，选择数据类别 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="0ceda-156">选择**ADO.NET 实体数据模型**模板，为实体数据模型提供名称 MoviesDBModel.edmx，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="0ceda-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="0ceda-157">单击**添加**按钮会启动数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="0ceda-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="0ceda-158">在中**选择模型内容**步骤中，选择**从数据库生成**选项，然后单击**下一步**按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="0ceda-159">在中**选择数据连接**步骤中，选择 MoviesDB.mdf 数据库连接，输入的实体连接设置命名 MoviesDBEntities，然后单击**下一步**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="0ceda-160">在中**选择数据库对象**步骤中，选择的电影数据库表，然后单击**完成**按钮 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="0ceda-161">完成这些步骤后，将打开 ADO.NET 实体数据模型设计器 （实体设计器）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="0ceda-162">**图 1 – 创建新的实体数据模型**</span><span class="sxs-lookup"><span data-stu-id="0ceda-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="0ceda-164">**图 2 – 选择模型内容的步骤**</span><span class="sxs-lookup"><span data-stu-id="0ceda-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="0ceda-166">**图 3-选择您的数据连接**</span><span class="sxs-lookup"><span data-stu-id="0ceda-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="0ceda-168">**图 4-选择数据库对象**</span><span class="sxs-lookup"><span data-stu-id="0ceda-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="0ceda-170">修改 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="0ceda-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="0ceda-171">创建实体数据模型后，可以通过利用实体设计器修改模型 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="0ceda-172">通过双击解决方案资源管理器窗口中的 Models 文件夹中包含的 MoviesDBModel.edmx 文件，可以在任何时候打开实体设计器。</span><span class="sxs-lookup"><span data-stu-id="0ceda-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="0ceda-173">**图 5 – ADO.NET 实体数据模型设计器**</span><span class="sxs-lookup"><span data-stu-id="0ceda-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="0ceda-175">例如，可以使用实体设计器来更改实体模型数据向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="0ceda-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="0ceda-176">该向导创建一个新的名为电影的数据访问类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="0ceda-177">换而言之，该向导为类提供了与数据库表完全相同的名称。</span><span class="sxs-lookup"><span data-stu-id="0ceda-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="0ceda-178">因为我们将使用此类表示特定电影实例，我们应该重命名电影的电影的类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="0ceda-179">如果你想要重命名的实体类，可以双击实体设计器中的类名称，并输入新名称 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="0ceda-180">或者，您可以在实体设计器中选择实体后更改属性窗口中的实体的名称。</span><span class="sxs-lookup"><span data-stu-id="0ceda-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="0ceda-181">**图 6 – 更改实体名称**</span><span class="sxs-lookup"><span data-stu-id="0ceda-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="0ceda-183">请记住保存通过单击保存按钮 （软盘图标） 进行了修改后的实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ceda-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="0ceda-184">在后台，实体设计器生成一的组 Visual Basic.NET 类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="0ceda-185">可以通过从解决方案资源管理器窗口中打开 MoviesDBModel.Designer.vb 文件来查看这些类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>


<span data-ttu-id="0ceda-186">由于所做的更改将被覆盖的下次使用实体设计器不会修改.vb 文件中的代码。</span><span class="sxs-lookup"><span data-stu-id="0ceda-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="0ceda-187">如果你想要扩展的.vb 文件中定义的实体类的功能，则可以创建*分部类*在单独的文件。</span><span class="sxs-lookup"><span data-stu-id="0ceda-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>


#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="0ceda-188">选择使用实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="0ceda-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="0ceda-189">让我们开始构建我们的电影数据库应用程序通过创建页，显示电影记录的列表。</span><span class="sxs-lookup"><span data-stu-id="0ceda-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="0ceda-190">列表 1 中的主页控制器公开名为 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="0ceda-191">Index （） 操作返回的所有电影记录从电影数据库表通过利用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="0ceda-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="0ceda-192">**代码清单 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="0ceda-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="0ceda-193">请注意，在列表 1 中的控制器包含一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="0ceda-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="0ceda-194">构造函数初始化名为的类级字段\_db。</span><span class="sxs-lookup"><span data-stu-id="0ceda-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="0ceda-195">\_Db 字段表示 Microsoft 实体框架所生成的数据库实体。</span><span class="sxs-lookup"><span data-stu-id="0ceda-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="0ceda-196">\_Db 字段是由实体设计器生成 MoviesDBEntities 类的实例。</span><span class="sxs-lookup"><span data-stu-id="0ceda-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="0ceda-197">\_Db 字段使用 index （） 操作中，若要从电影数据库表中检索的记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="0ceda-198">表达式\_db。MovieSet 表示的所有记录电影数据库表中。</span><span class="sxs-lookup"><span data-stu-id="0ceda-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="0ceda-199">Tolist （） 方法用于将电影该集转换到 Movie 对象的泛型集合： 列表 （的电影）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="0ceda-200">电影记录检索到实体的 LINQ 帮助。</span><span class="sxs-lookup"><span data-stu-id="0ceda-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="0ceda-201">在列表 1 中的 index （） 操作使用 LINQ*方法语法*检索组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="0ceda-202">如果您愿意，您可以使用 LINQ*查询语法*相反。</span><span class="sxs-lookup"><span data-stu-id="0ceda-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="0ceda-203">以下两个语句执行完全相同的操作：</span><span class="sxs-lookup"><span data-stu-id="0ceda-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="0ceda-204">使用您找到最直观任何 LINQ 语法 （方法语法或查询语法）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="0ceda-205">没有两个方法之间的性能差异-唯一的区别是样式。</span><span class="sxs-lookup"><span data-stu-id="0ceda-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="0ceda-206">代码清单 2 中的视图用于显示电影记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="0ceda-207">**代码清单 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="0ceda-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="0ceda-208">代码清单 2 中的视图包含**为每个**循环，循环访问每个电影记录并显示电影记录的标题和主管属性的值。</span><span class="sxs-lookup"><span data-stu-id="0ceda-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="0ceda-209">请注意，每个记录旁边显示的编辑和删除链接。</span><span class="sxs-lookup"><span data-stu-id="0ceda-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="0ceda-210">此外，该视图的底部将显示添加电影链接 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="0ceda-211">**图 7-索引视图**</span><span class="sxs-lookup"><span data-stu-id="0ceda-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="0ceda-213">索引视图是*类型化视图*。</span><span class="sxs-lookup"><span data-stu-id="0ceda-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="0ceda-214">索引视图具有&lt;%@ 页 %&gt;包括 Inherits 属性的指令。</span><span class="sxs-lookup"><span data-stu-id="0ceda-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="0ceda-215">Inherits 特性将强类型列表的泛型集合 Movie 对象 – 列表 （的电影） 的 ViewData.Model 属性强制转换。</span><span class="sxs-lookup"><span data-stu-id="0ceda-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="0ceda-216">插入使用实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="0ceda-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="0ceda-217">实体框架可用于轻松地将新记录插入到数据库表。</span><span class="sxs-lookup"><span data-stu-id="0ceda-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="0ceda-218">代码清单 3 包含两个新的操作添加到 Home 控制器类可用于将新记录插入到电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="0ceda-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="0ceda-219">**代码清单 3 – Controllers\HomeController.vb （添加方法）**</span><span class="sxs-lookup"><span data-stu-id="0ceda-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="0ceda-220">第一个 add （） 操作只需返回的视图。</span><span class="sxs-lookup"><span data-stu-id="0ceda-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="0ceda-221">该视图包含一个窗体添加一个新的电影数据库记录 （请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="0ceda-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="0ceda-222">在提交表单时，会调用第二个 add （） 操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="0ceda-223">请注意，使用 AcceptVerbs 属性修饰的第二个 add （） 操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="0ceda-224">只有在执行 HTTP POST 操作时，可以调用此操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="0ceda-225">换而言之，仅可以发布 HTML 窗体时调用此操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="0ceda-226">第二个 add （） 操作的 ASP.NET MVC TryUpdateModel() 方法帮助创建实体框架 Movie 类的新实例。</span><span class="sxs-lookup"><span data-stu-id="0ceda-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="0ceda-227">TryUpdateModel() 方法采用传递给 add （） 方法 FormCollection 中的字段，并将这些 HTML 窗体字段的值分配给 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="0ceda-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>


<span data-ttu-id="0ceda-228">使用实体框架时，使用 TryUpdateModel 或 UpdateModel 方法来更新实体类的属性时，必须提供"允许列表"的属性。</span><span class="sxs-lookup"><span data-stu-id="0ceda-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>


<span data-ttu-id="0ceda-229">接下来，add （） 操作执行一些简单的窗体的验证。</span><span class="sxs-lookup"><span data-stu-id="0ceda-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="0ceda-230">操作可验证的标题和主管属性具有值。</span><span class="sxs-lookup"><span data-stu-id="0ceda-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="0ceda-231">如果没有验证错误，则会将一条验证错误消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="0ceda-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="0ceda-232">如果没有任何验证错误则会将新电影记录添加到电影数据库表的实体框架帮助。</span><span class="sxs-lookup"><span data-stu-id="0ceda-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="0ceda-233">新记录添加到具有以下两行代码的数据库：</span><span class="sxs-lookup"><span data-stu-id="0ceda-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="0ceda-234">第一行代码将新的电影实体添加到跟踪的实体框架的电影的集。</span><span class="sxs-lookup"><span data-stu-id="0ceda-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="0ceda-235">第二行代码将保存到电影正在跟踪与基础数据库进行了任何更改。</span><span class="sxs-lookup"><span data-stu-id="0ceda-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="0ceda-236">**图 8-添加视图**</span><span class="sxs-lookup"><span data-stu-id="0ceda-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="0ceda-238">使用实体框架的更新数据库记录</span><span class="sxs-lookup"><span data-stu-id="0ceda-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="0ceda-239">可以遵循几乎相同的方法来编辑使用实体框架的数据库记录为我们只需遵循来插入新的数据库记录的方法。</span><span class="sxs-lookup"><span data-stu-id="0ceda-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="0ceda-240">列表 4 包含名为 edit （） 的两个新控制器操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="0ceda-241">第一个 edit （） 操作返回 HTML 窗体以编辑电影记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="0ceda-242">第二个的 edit （） 操作将尝试更新数据库。</span><span class="sxs-lookup"><span data-stu-id="0ceda-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="0ceda-243">**列表 4 – Controllers\HomeController.vb （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="0ceda-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="0ceda-244">第二个 edit （） 操作首先会从正在编辑的电影 Id 相匹配的数据库中检索电影记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="0ceda-245">以下受 LINQ to 实体语句获取特定 Id 相匹配的第一个数据库记录：</span><span class="sxs-lookup"><span data-stu-id="0ceda-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="0ceda-246">接下来，TryUpdateModel() 方法用于将 HTML 窗体字段的值分配给电影实体的属性。</span><span class="sxs-lookup"><span data-stu-id="0ceda-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="0ceda-247">请注意，提供允许列表来指定要更新的确切属性。</span><span class="sxs-lookup"><span data-stu-id="0ceda-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="0ceda-248">接下来，执行一些简单的验证，以便验证影片标题和主管属性具有值。</span><span class="sxs-lookup"><span data-stu-id="0ceda-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="0ceda-249">如果这两个属性缺少一个值，然后验证错误消息添加到 ModelState 并 ModelState.IsValid 返回值 false。</span><span class="sxs-lookup"><span data-stu-id="0ceda-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="0ceda-250">最后，如果没有任何验证错误，则基础的电影数据库表被更新的任何更改通过调用 savechanges （） 方法。</span><span class="sxs-lookup"><span data-stu-id="0ceda-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="0ceda-251">在编辑数据库记录时，需要传递到执行数据库更新的控制器操作正在编辑的记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="0ceda-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="0ceda-252">否则，控制器操作不会知道哪条记录以更新基础数据库中。</span><span class="sxs-lookup"><span data-stu-id="0ceda-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="0ceda-253">列表 5 中所包含的编辑视图包括隐藏的窗体字段表示正在编辑的数据库记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="0ceda-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="0ceda-254">**列表 5 – Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="0ceda-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="0ceda-255">删除使用实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="0ceda-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="0ceda-256">最终的数据库操作，我们需要解决本教程中，正在删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="0ceda-257">可以在列表 6 中使用的控制器操作以删除特定数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="0ceda-258">**代码清单 6-\Controllers\HomeController.vb （删除操作）**</span><span class="sxs-lookup"><span data-stu-id="0ceda-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="0ceda-259">Delete （） 操作首先检索的电影 Id 相匹配的实体传递给该操作。</span><span class="sxs-lookup"><span data-stu-id="0ceda-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="0ceda-260">接下来，电影是从数据库中删除通过调用 savechanges （） 方法后跟 DeleteObject() 方法。</span><span class="sxs-lookup"><span data-stu-id="0ceda-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="0ceda-261">最后，用户已重定向回到索引视图。</span><span class="sxs-lookup"><span data-stu-id="0ceda-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="0ceda-262">总结</span><span class="sxs-lookup"><span data-stu-id="0ceda-262">Summary</span></span>

<span data-ttu-id="0ceda-263">本教程的目的是演示如何通过利用 ASP.NET MVC 和 Microsoft 实体框架构建数据库驱动的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ceda-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="0ceda-264">您学习了如何生成应用程序，可用于选择、 插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="0ceda-265">首先，我们讨论了如何使用实体数据模型向导生成实体数据模型从 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="0ceda-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="0ceda-266">接下来，您将了解如何使用 LINQ to Entities 从数据库表中检索一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="0ceda-267">最后，我们使用实体框架来插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0ceda-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0ceda-268">[上一页](validation-with-the-data-annotation-validators-cs.md)
> [下一页](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0ceda-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
