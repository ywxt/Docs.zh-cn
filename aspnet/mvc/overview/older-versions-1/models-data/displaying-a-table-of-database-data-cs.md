---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表 (C#) |Microsoft Docs
author: microsoft
description: 在本教程中，我将演示两种方法显示的一组数据库记录。 我将介绍两种方法的格式设置的一组数据库记录在 HTML ta...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 06dc5c9398adb45d5a5ff8f57ff42816c983ee04
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395975"
---
<a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="8cc46-104">显示数据库数据表 (C#)</span><span class="sxs-lookup"><span data-stu-id="8cc46-104">Displaying a Table of Database Data (C#)</span></span>
====================
<span data-ttu-id="8cc46-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8cc46-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8cc46-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="8cc46-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="8cc46-107">在本教程中，我将演示两种方法显示的一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="8cc46-108">我将介绍两种方法的格式设置的一组 HTML 表中的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="8cc46-109">首先，我介绍如何设置格式直接在视图中的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="8cc46-110">接下来，我演示了如何可以充分利用分区，设置格式的数据库记录时。</span><span class="sxs-lookup"><span data-stu-id="8cc46-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>


<span data-ttu-id="8cc46-111">本教程的目的是说明如何在 ASP.NET MVC 应用程序中显示一个 HTML 表的数据库数据。</span><span class="sxs-lookup"><span data-stu-id="8cc46-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="8cc46-112">首先，您将学习如何使用 Visual Studio 中包含的基架工具生成一个视图，它会自动显示的一组记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="8cc46-113">接下来，您将学习如何设置格式的数据库记录时将用作模板的部分。</span><span class="sxs-lookup"><span data-stu-id="8cc46-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="8cc46-114">创建模型类</span><span class="sxs-lookup"><span data-stu-id="8cc46-114">Create the Model Classes</span></span>

<span data-ttu-id="8cc46-115">我们要显示的电影数据库表中的记录集。</span><span class="sxs-lookup"><span data-stu-id="8cc46-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="8cc46-116">电影数据库表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="8cc46-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>


| <span data-ttu-id="8cc46-117">**列名称**</span><span class="sxs-lookup"><span data-stu-id="8cc46-117">**Column Name**</span></span> | <span data-ttu-id="8cc46-118">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="8cc46-118">**Data Type**</span></span> | <span data-ttu-id="8cc46-119">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="8cc46-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cc46-120">Id</span><span class="sxs-lookup"><span data-stu-id="8cc46-120">Id</span></span> | <span data-ttu-id="8cc46-121">Int</span><span class="sxs-lookup"><span data-stu-id="8cc46-121">Int</span></span> | <span data-ttu-id="8cc46-122">False</span><span class="sxs-lookup"><span data-stu-id="8cc46-122">False</span></span> |
| <span data-ttu-id="8cc46-123">标题</span><span class="sxs-lookup"><span data-stu-id="8cc46-123">Title</span></span> | <span data-ttu-id="8cc46-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="8cc46-124">Nvarchar(200)</span></span> | <span data-ttu-id="8cc46-125">False</span><span class="sxs-lookup"><span data-stu-id="8cc46-125">False</span></span> |
| <span data-ttu-id="8cc46-126">主管</span><span class="sxs-lookup"><span data-stu-id="8cc46-126">Director</span></span> | <span data-ttu-id="8cc46-127">Nvarchar （50)</span><span class="sxs-lookup"><span data-stu-id="8cc46-127">NVarchar(50)</span></span> | <span data-ttu-id="8cc46-128">False</span><span class="sxs-lookup"><span data-stu-id="8cc46-128">False</span></span> |
| <span data-ttu-id="8cc46-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="8cc46-129">DateReleased</span></span> | <span data-ttu-id="8cc46-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="8cc46-130">DateTime</span></span> | <span data-ttu-id="8cc46-131">False</span><span class="sxs-lookup"><span data-stu-id="8cc46-131">False</span></span> |


<span data-ttu-id="8cc46-132">若要表示电影表在 ASP.NET MVC 应用程序中，我们需要创建一个模型的类。</span><span class="sxs-lookup"><span data-stu-id="8cc46-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="8cc46-133">在本教程中，我们可以使用 Microsoft Entity Framework 创建我们模型类。</span><span class="sxs-lookup"><span data-stu-id="8cc46-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8cc46-134">在本教程中，我们使用 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="8cc46-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="8cc46-135">但是，务必了解你可以使用各种不同的技术与 ASP.NET MVC 应用程序包括 LINQ to SQL、 NHibernate 或 ADO.NET 从数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="8cc46-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>


<span data-ttu-id="8cc46-136">请按照下列步骤以启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="8cc46-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="8cc46-137">右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="8cc46-138">选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="8cc46-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="8cc46-139">为你的数据模型提供名称*MoviesDBModel.edmx*然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="8cc46-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="8cc46-140">单击添加按钮后，会显示实体数据模型向导 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="8cc46-141">请按照下列步骤以完成向导：</span><span class="sxs-lookup"><span data-stu-id="8cc46-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="8cc46-142">在中**选择模型内容**步骤中，选择**从数据库生成**选项。</span><span class="sxs-lookup"><span data-stu-id="8cc46-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="8cc46-143">在中**选择数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*的连接设置。</span><span class="sxs-lookup"><span data-stu-id="8cc46-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="8cc46-144">单击**下一步**按钮。</span><span class="sxs-lookup"><span data-stu-id="8cc46-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="8cc46-145">在中**选择数据库对象**步骤中，展开表节点中，选择电影表。</span><span class="sxs-lookup"><span data-stu-id="8cc46-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="8cc46-146">输入的命名空间*模型*然后单击**完成**按钮。</span><span class="sxs-lookup"><span data-stu-id="8cc46-146">Enter the namespace *Models* and click the **Finish** button.</span></span>


<span data-ttu-id="8cc46-147">[![创建 LINQ to SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="8cc46-148">**图 01**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>


<span data-ttu-id="8cc46-149">完成实体数据模型向导后，会打开实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="8cc46-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="8cc46-150">在设计器应显示电影实体 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-150">The Designer should display the Movies entity (see Figure 2).</span></span>


<span data-ttu-id="8cc46-151">[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="8cc46-152">**图 02**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>


<span data-ttu-id="8cc46-153">我们需要做出一项更改，然后我们继续。</span><span class="sxs-lookup"><span data-stu-id="8cc46-153">We need to make one change before we continue.</span></span> <span data-ttu-id="8cc46-154">实体数据向导生成一个名为的模型类*电影*表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="8cc46-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="8cc46-155">由于我们将使用电影类来表示特定电影，我们需要修改这个类为名称*电影*而不是*电影*（单数而非复数形式）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="8cc46-156">双击设计器图面上的类的名称并将影片中的类的名称更改为电影。</span><span class="sxs-lookup"><span data-stu-id="8cc46-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="8cc46-157">此更改后，单击**保存**按钮 （软盘图标） 以生成电影类。</span><span class="sxs-lookup"><span data-stu-id="8cc46-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="8cc46-158">创建电影控制器</span><span class="sxs-lookup"><span data-stu-id="8cc46-158">Create the Movies Controller</span></span>

<span data-ttu-id="8cc46-159">现在，我们已有一种方法来表示我们的数据库记录，我们可以创建一个控制器，返回的电影集合。</span><span class="sxs-lookup"><span data-stu-id="8cc46-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="8cc46-160">在 Visual Studio 解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>


<span data-ttu-id="8cc46-161">[![添加控制器菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="8cc46-162">**图 03**: 添加的控制器菜单 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>


<span data-ttu-id="8cc46-163">当**添加控制器**对话框出现时，输入控制器名称 MovieController （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="8cc46-164">单击**添加**按钮以添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="8cc46-164">Click the **Add** button to add the new controller.</span></span>


<span data-ttu-id="8cc46-165">[![添加控制器对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="8cc46-166">**图 04**: 添加控制器对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>


<span data-ttu-id="8cc46-167">我们需要进行修改，以便其返回的数据库记录集公开的电影控制器的 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="8cc46-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="8cc46-168">修改控制器，使它看起来像列表 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="8cc46-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="8cc46-169">**代码清单 1 – Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="8cc46-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="8cc46-170">在列表 1 中，MoviesDBEntities 类用于表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="8cc46-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="8cc46-171">若要使用此类，需要导入如下 MvcApplication1.Models 命名空间：</span><span class="sxs-lookup"><span data-stu-id="8cc46-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="8cc46-172">使用 MvcApplication1.Models;</span><span class="sxs-lookup"><span data-stu-id="8cc46-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="8cc46-173">表达式*实体。MovieSet.ToList()* 从电影数据库表返回所有电影的组。</span><span class="sxs-lookup"><span data-stu-id="8cc46-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="8cc46-174">创建视图</span><span class="sxs-lookup"><span data-stu-id="8cc46-174">Create the View</span></span>

<span data-ttu-id="8cc46-175">若要在 HTML 表中显示的一组数据库记录的最简单方法是利用 Visual Studio 提供的基架。</span><span class="sxs-lookup"><span data-stu-id="8cc46-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="8cc46-176">通过选择菜单选项来生成你的应用程序**生成，生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="8cc46-177">您必须生成应用程序打开之前**添加视图**对话框或数据类不会显示在该对话框。</span><span class="sxs-lookup"><span data-stu-id="8cc46-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="8cc46-178">右键单击 index （） 操作，然后选择菜单选项**添加视图**（请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>


<span data-ttu-id="8cc46-179">[![添加视图](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="8cc46-180">**图 05**： 添加视图 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>


<span data-ttu-id="8cc46-181">在中**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="8cc46-182">选择作为 Movie 类**查看数据类**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="8cc46-183">选择*列表*作为**查看内容**（请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="8cc46-184">选择这些选项将生成一个强类型化视图，显示电影列表。</span><span class="sxs-lookup"><span data-stu-id="8cc46-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>


<span data-ttu-id="8cc46-185">[![添加视图对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="8cc46-186">**图 06**: 添加视图对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>


<span data-ttu-id="8cc46-187">单击后**添加**自动生成的按钮，代码清单 2 中的视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="8cc46-188">此视图包含循环的电影集合并显示每个电影属性所需的代码。</span><span class="sxs-lookup"><span data-stu-id="8cc46-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="8cc46-189">**代码清单 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="8cc46-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="8cc46-190">可以通过选择菜单选项来运行应用程序**调试、 启动调试**（或按 F5 键）。</span><span class="sxs-lookup"><span data-stu-id="8cc46-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="8cc46-191">运行应用程序将启动 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="8cc46-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="8cc46-192">如果导航到 /Movie URL，那么您将看到图 7 中的页。</span><span class="sxs-lookup"><span data-stu-id="8cc46-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>


<span data-ttu-id="8cc46-193">[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="8cc46-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="8cc46-194">**图 07**： 电影的表 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="8cc46-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>


<span data-ttu-id="8cc46-195">如果您不喜欢在图 7 中的数据库记录的网格的外观有关的任何信息则可以只需修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="8cc46-196">例如，可以更改*DateReleased*标头*发布日期*通过修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="8cc46-197">使用部分创建一个模板</span><span class="sxs-lookup"><span data-stu-id="8cc46-197">Create a Template with a Partial</span></span>

<span data-ttu-id="8cc46-198">当视图获取过于复杂时，它最好开始分解为分区的视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="8cc46-199">使用分区可以更轻松地理解和维护你的视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="8cc46-200">我们将创建一个分部，我们可以使用作为模板来设置每个电影数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="8cc46-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="8cc46-201">请按照以下步骤创建分部操作：</span><span class="sxs-lookup"><span data-stu-id="8cc46-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="8cc46-202">右键单击 Views\Movie 文件夹，然后选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="8cc46-203">选中复选框标记为*创建分部视图 (.ascx)*。</span><span class="sxs-lookup"><span data-stu-id="8cc46-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="8cc46-204">命名分部*MovieTemplate*。</span><span class="sxs-lookup"><span data-stu-id="8cc46-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="8cc46-205">选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="8cc46-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="8cc46-206">选择作为电影*查看数据类*。</span><span class="sxs-lookup"><span data-stu-id="8cc46-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="8cc46-207">选择为空*查看内容*。</span><span class="sxs-lookup"><span data-stu-id="8cc46-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="8cc46-208">单击**添加**按钮将部分添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="8cc46-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="8cc46-209">完成这些步骤后，修改部分 MovieTemplate 与列表 3 类似的形式。</span><span class="sxs-lookup"><span data-stu-id="8cc46-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="8cc46-210">**代码清单 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="8cc46-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="8cc46-211">列表 3 中的部分包含的记录单个行的模板。</span><span class="sxs-lookup"><span data-stu-id="8cc46-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="8cc46-212">列表 4 中已修改的索引视图使用 MovieTemplate 部分。</span><span class="sxs-lookup"><span data-stu-id="8cc46-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="8cc46-213">**列表 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="8cc46-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="8cc46-214">列表 4 中的该视图包含 foreach 循环遍历所有电影。</span><span class="sxs-lookup"><span data-stu-id="8cc46-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="8cc46-215">为每个电影 MovieTemplate 部分用于设置格式的电影。</span><span class="sxs-lookup"><span data-stu-id="8cc46-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="8cc46-216">通过调用 RenderPartial() 帮助器方法呈现 MovieTemplate。</span><span class="sxs-lookup"><span data-stu-id="8cc46-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="8cc46-217">已修改的索引视图呈现数据库记录完全相同的 HTML 的表。</span><span class="sxs-lookup"><span data-stu-id="8cc46-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="8cc46-218">但是，已极大地简化视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-218">However, the view has been greatly simplified.</span></span>


<span data-ttu-id="8cc46-219">RenderPartial() 方法是不同于大多数其他帮助器方法，因为它不会返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="8cc46-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="8cc46-220">因此，您必须调用 RenderPartial() 方法使用&lt;%html.renderpartial(); %&gt;而不是&lt;%= Html.RenderPartial(); %&gt;。</span><span class="sxs-lookup"><span data-stu-id="8cc46-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>


## <a name="summary"></a><span data-ttu-id="8cc46-221">总结</span><span class="sxs-lookup"><span data-stu-id="8cc46-221">Summary</span></span>

<span data-ttu-id="8cc46-222">本教程的目的是说明如何在 HTML 表中显示的一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="8cc46-223">首先，您学习了如何通过利用 Microsoft 实体框架的控制器操作返回的一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8cc46-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="8cc46-224">接下来，您学习了如何使用 Visual Studio 基架生成一个视图，它会自动显示的项的集合。</span><span class="sxs-lookup"><span data-stu-id="8cc46-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="8cc46-225">最后，您学习了如何通过利用一个分部的简化视图。</span><span class="sxs-lookup"><span data-stu-id="8cc46-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="8cc46-226">您学习了如何使用部分作为模板，以便您可以设置每个数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="8cc46-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8cc46-227">[上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8cc46-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
