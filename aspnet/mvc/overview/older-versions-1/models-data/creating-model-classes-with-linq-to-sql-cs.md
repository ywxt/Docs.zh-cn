---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: 使用 LINQ to SQL (C#) 创建模型类 |Microsoft 文档
author: microsoft
description: 本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。 在本教程中，你将学习如何构建模型 c...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: 1f30ff6c97e565059c57c55f26d2dff477774aeb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-model-classes-with-linq-to-sql-c"></a><span data-ttu-id="bd4e4-104">使用 LINQ to SQL (C#) 创建模型类</span><span class="sxs-lookup"><span data-stu-id="bd4e4-104">Creating Model Classes with LINQ to SQL (C#)</span></span>
====================
<span data-ttu-id="bd4e4-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="bd4e4-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="bd4e4-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> <span data-ttu-id="bd4e4-107">本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-107">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="bd4e4-108">在本教程中，你将学习如何生成模型的类，并通过利用 Microsoft LINQ to SQL 中执行数据库访问。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-108">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>


<span data-ttu-id="bd4e4-109">本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-109">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="bd4e4-110">在本教程中，你将学习如何构建模型类和通过利用 Microsoft LINQ to SQL 中执行数据库访问</span><span class="sxs-lookup"><span data-stu-id="bd4e4-110">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL</span></span>

<span data-ttu-id="bd4e4-111">在本教程中，我们构建基本的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-111">In this tutorial, we build a basic Movie database application.</span></span> <span data-ttu-id="bd4e4-112">我们首先创建可能的最快和最简单的方法电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-112">We start by creating the Movie database application in the fastest and easiest way possible.</span></span> <span data-ttu-id="bd4e4-113">我们直接从我们的控制器操作中执行所有我们数据访问。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-113">We perform all of our data access directly from our controller actions.</span></span>

<span data-ttu-id="bd4e4-114">接下来，你将了解如何使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-114">Next, you learn how to use the Repository pattern.</span></span> <span data-ttu-id="bd4e4-115">使用存储库模式需要稍有更多工作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-115">Using the Repository pattern requires a little more work.</span></span> <span data-ttu-id="bd4e4-116">但是，采用此模式的优点是它使你能够构建的应用程序适应更改，并可以轻松地测试。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-116">However, the advantage of adopting this pattern is that it enables you to build applications that are adaptable to change and can be easily tested.</span></span>

## <a name="what-is-a-model-class"></a><span data-ttu-id="bd4e4-117">什么是模型类？</span><span class="sxs-lookup"><span data-stu-id="bd4e4-117">What is a Model Class?</span></span>

<span data-ttu-id="bd4e4-118">MVC 模型包含所有未包含在 MVC 视图或 MVC 控制器中的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-118">An MVC model contains all of the application logic that is not contained in an MVC view or MVC controller.</span></span> <span data-ttu-id="bd4e4-119">具体而言，MVC 模型包含的所有应用程序业务和数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-119">In particular, an MVC model contains all of your application business and data access logic.</span></span>

<span data-ttu-id="bd4e4-120">可以使用各种不同的技术来实现数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-120">You can use a variety of different technologies to implement your data access logic.</span></span> <span data-ttu-id="bd4e4-121">例如，你可以生成数据访问类使用的 Microsoft 实体框架、 NHibernate、 Subsonic 或 ADO.NET 类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-121">For example, you can build your data access classes using the Microsoft Entity Framework, NHibernate, Subsonic, or ADO.NET classes.</span></span>

<span data-ttu-id="bd4e4-122">在本教程中，我可以使用 LINQ to SQL 来查询和更新数据库。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-122">In this tutorial, I use LINQ to SQL to query and update the database.</span></span> <span data-ttu-id="bd4e4-123">LINQ to SQL 可为你提供与 Microsoft SQL Server 数据库交互的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-123">LINQ to SQL provides you with a very easy method of interacting with a Microsoft SQL Server database.</span></span> <span data-ttu-id="bd4e4-124">但是，务必了解 ASP.NET MVC framework 未绑定到 LINQ to SQL 以任何方式。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-124">However, it is important to understand that the ASP.NET MVC framework is not tied to LINQ to SQL in any way.</span></span> <span data-ttu-id="bd4e4-125">ASP.NET MVC 适用于任何数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-125">ASP.NET MVC is compatible with any data access technology.</span></span>

## <a name="create-a-movie-database"></a><span data-ttu-id="bd4e4-126">创建电影数据库</span><span class="sxs-lookup"><span data-stu-id="bd4e4-126">Create a Movie Database</span></span>

<span data-ttu-id="bd4e4-127">在此教程--若要演示如何生成模型类-我们构建一个简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-127">In this tutorial -- in order to illustrate how you can build model classes -- we build a simple Movie database application.</span></span> <span data-ttu-id="bd4e4-128">第一步是创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-128">The first step is to create a new database.</span></span> <span data-ttu-id="bd4e4-129">右键单击该应用\_在解决方案资源管理器窗口中，然后选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-129">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span> <span data-ttu-id="bd4e4-130">选择**SQL Server 数据库**模板，使其名称 MoviesDB.mdf，并单击**添加**按钮 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-130">Select the **SQL Server Database** template, give it the name MoviesDB.mdf, and click the **Add** button (see Figure 1).</span></span>


<span data-ttu-id="bd4e4-131">[![添加新的 SQL Server 数据库](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-131">[![Adding a new SQL Server Database](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)</span></span>

<span data-ttu-id="bd4e4-132">**图 01**： 添加新的 SQL Server 数据库 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-132">**Figure 01**: Adding a new SQL Server Database ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))</span></span>


<span data-ttu-id="bd4e4-133">创建新的数据库后，你可以通过双击 MoviesDB.mdf 文件，在应用中的打开数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-133">After you create the new database, you can open the database by double-clicking the MoviesDB.mdf file in the App\_Data folder.</span></span> <span data-ttu-id="bd4e4-134">双击 MoviesDB.mdf 文件打开服务器资源管理器窗口 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-134">Double-clicking the MoviesDB.mdf file opens the Server Explorer window (see Figure 2).</span></span>

<span data-ttu-id="bd4e4-135">服务器资源管理器窗口时使用 Visual Web Developer 调用数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-135">The Server Explorer window is called the Database Explorer window when using Visual Web Developer.</span></span>


<span data-ttu-id="bd4e4-136">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-136">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)</span></span>

<span data-ttu-id="bd4e4-137">**图 02**： 使用服务器资源管理器窗口 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-137">**Figure 02**: Using the Server Explorer window ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))</span></span>


<span data-ttu-id="bd4e4-138">我们需要将表添加到我们表示我们电影的数据库。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-138">We need to add one table to our database that represents our movies.</span></span> <span data-ttu-id="bd4e4-139">右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-139">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="bd4e4-140">选择此菜单选项将打开表设计器 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-140">Selecting this menu option opens the Table Designer (see Figure 3).</span></span>


<span data-ttu-id="bd4e4-141">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-141">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)</span></span>

<span data-ttu-id="bd4e4-142">**图 03**： 表设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-142">**Figure 03**: The Table Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))</span></span>


<span data-ttu-id="bd4e4-143">我们需要将以下各列添加到我们的数据库表：</span><span class="sxs-lookup"><span data-stu-id="bd4e4-143">We need to add the following columns to our database table:</span></span>

| <span data-ttu-id="bd4e4-144">**列名称**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-144">**Column Name**</span></span> | <span data-ttu-id="bd4e4-145">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-145">**Data Type**</span></span> | <span data-ttu-id="bd4e4-146">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-146">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd4e4-147">Id</span><span class="sxs-lookup"><span data-stu-id="bd4e4-147">Id</span></span> | <span data-ttu-id="bd4e4-148">Int</span><span class="sxs-lookup"><span data-stu-id="bd4e4-148">Int</span></span> | <span data-ttu-id="bd4e4-149">False</span><span class="sxs-lookup"><span data-stu-id="bd4e4-149">False</span></span> |
| <span data-ttu-id="bd4e4-150">标题</span><span class="sxs-lookup"><span data-stu-id="bd4e4-150">Title</span></span> | <span data-ttu-id="bd4e4-151">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-151">Nvarchar(200)</span></span> | <span data-ttu-id="bd4e4-152">False</span><span class="sxs-lookup"><span data-stu-id="bd4e4-152">False</span></span> |
| <span data-ttu-id="bd4e4-153">控制器</span><span class="sxs-lookup"><span data-stu-id="bd4e4-153">Director</span></span> | <span data-ttu-id="bd4e4-154">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-154">Nvarchar(50)</span></span> | <span data-ttu-id="bd4e4-155">False</span><span class="sxs-lookup"><span data-stu-id="bd4e4-155">False</span></span> |

<span data-ttu-id="bd4e4-156">你需要执行到 Id 列的两个特殊操作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-156">You need to do two special things to the Id column.</span></span> <span data-ttu-id="bd4e4-157">首先，你需要将 Id 列标记为主键列，通过在表设计器中选择列并单击项的图标。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-157">First, you need to mark the Id column as a primary key column by selecting the column in the Table Designer and clicking the icon of a key.</span></span> <span data-ttu-id="bd4e4-158">LINQ to SQL 要求你在执行插入或更新对数据库时指定主键列。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-158">LINQ to SQL requires you to specify your primary key columns when performing inserts or updates against the database.</span></span>

<span data-ttu-id="bd4e4-159">接下来，你需要将 Id 列标记为标识列，通过是将值分配给**是标识**属性 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-159">Next, you need to mark the Id column as an Identity column by assigning the value Yes to the **Is Identity** property (see Figure 3).</span></span> <span data-ttu-id="bd4e4-160">标识列是自动将分配较新的数字，每当将新的数据行添加到表的列。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-160">An Identity column is a column that is assigned a new number automatically whenever you add a new row of data to a table.</span></span>

## <a name="create-linq-to-sql-classes"></a><span data-ttu-id="bd4e4-161">创建 LINQ to SQL 类</span><span class="sxs-lookup"><span data-stu-id="bd4e4-161">Create LINQ to SQL Classes</span></span>

<span data-ttu-id="bd4e4-162">我们的 MVC 模型将包含 LINQ to SQL 类表示 tblMovie 数据库表。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-162">Our MVC model will contain LINQ to SQL classes that represent the tblMovie database table.</span></span> <span data-ttu-id="bd4e4-163">若要创建这些 LINQ to SQL 类的最简单方法是右键单击 Models 文件夹，选择**添加、 新项**，选择 LINQ to SQL 类模板，将类命名 Movie.dbml，然后单击**添加**按钮 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-163">The easiest way to create these LINQ to SQL classes is to right-click the Models folder, select **Add, New Item**, select the LINQ to SQL Classes template, give the classes the name Movie.dbml, and click the **Add** button (see Figure 4).</span></span>


<span data-ttu-id="bd4e4-164">[![创建 LINQ to SQL 类](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-164">[![Creating LINQ to SQL classes](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)</span></span>

<span data-ttu-id="bd4e4-165">**图 04**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-165">**Figure 04**: Creating LINQ to SQL classes ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))</span></span>


<span data-ttu-id="bd4e4-166">立即创建电影 LINQ to SQL 类后，将显示对象关系设计器。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-166">Immediately after you create the Movie LINQ to SQL Classes, the Object Relational Designer appears.</span></span> <span data-ttu-id="bd4e4-167">你可以将数据库表从服务器资源管理器窗口拖动对象关系设计器创建 LINQ to SQL 类表示特定数据库表。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-167">You can drag database tables from the Server Explorer window onto the Object Relational Designer to create LINQ to SQL Classes that represent particular database tables.</span></span> <span data-ttu-id="bd4e4-168">我们需要添加 tblMovie 数据库表拖放到对象关系设计器 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-168">We need to add the tblMovie database table onto the Object Relational Designer (see Figure 5).</span></span>


<span data-ttu-id="bd4e4-169">[![使用对象关系设计器](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-169">[![Using the Object Relational Designer](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)</span></span>

<span data-ttu-id="bd4e4-170">**图 05**： 使用对象关系设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-170">**Figure 05**: Using the Object Relational Designer  ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))</span></span>


<span data-ttu-id="bd4e4-171">默认情况下，对象关系设计器创建一个具有类与数据库表拖到设计器上非常相同的名称。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-171">By default, the Object Relational Designer creates a class with the very same name as the database table that you drag onto the Designer.</span></span> <span data-ttu-id="bd4e4-172">但是，我们不想调用我们类`tblMovie`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-172">However, we don't want to call our class `tblMovie`.</span></span> <span data-ttu-id="bd4e4-173">因此，单击设计器中的类的名称，并将类的名称更改为影片。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-173">Therefore, click the name of the class in the Designer and change the name of the class to Movie.</span></span>

<span data-ttu-id="bd4e4-174">最后，请记住单击**保存**按钮 （软盘图片） 将 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-174">Finally, remember to click the **Save** button (the picture of the floppy) to save the LINQ to SQL Classes.</span></span> <span data-ttu-id="bd4e4-175">否则，不会由对象关系设计器生成 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-175">Otherwise, the LINQ to SQL Classes won't be generated by the Object Relational Designer.</span></span>

## <a name="using-linq-to-sql-in-a-controller-action"></a><span data-ttu-id="bd4e4-176">在控制器操作中使用 LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="bd4e4-176">Using LINQ to SQL in a Controller Action</span></span>

<span data-ttu-id="bd4e4-177">现在，我们已我们 LINQ to SQL 类，我们可以使用这些类以从数据库检索数据。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-177">Now that we have our LINQ to SQL classes, we can use these classes to retrieve data from the database.</span></span> <span data-ttu-id="bd4e4-178">在本部分中，你将了解如何使用 LINQ to SQL 类直接中的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-178">In this section, you learn how to use LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="bd4e4-179">我们将在的 MVC 视图中显示 tblMovies 数据库表中的影片的列表。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-179">We'll display the list of movies from the tblMovies database table in an MVC view.</span></span>

<span data-ttu-id="bd4e4-180">首先，我们需要修改 HomeController 类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-180">First, we need to modify the HomeController class.</span></span> <span data-ttu-id="bd4e4-181">你的应用程序的 Controllers 文件夹中找不到此类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-181">This class can be found in the Controllers folder of your application.</span></span> <span data-ttu-id="bd4e4-182">修改类，使其类似列表 1 中的类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-182">Modify the class so it looks like the class in Listing 1.</span></span>

<span data-ttu-id="bd4e4-183">**列表 1 – `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-183">**Listing 1 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

<span data-ttu-id="bd4e4-184">`Index()`列表 1 中的操作使用 LINQ to SQL DataContext 类 ( `MovieDataContext`) 来表示`MoviesDB`数据库。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-184">The `Index()` action in Listing 1 uses a LINQ to SQL DataContext class (the `MovieDataContext`) to represent the `MoviesDB` database.</span></span> <span data-ttu-id="bd4e4-185">`MoveDataContext`由 Visual Studio 对象关系设计器生成类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-185">The `MoveDataContext` class was generated by the Visual Studio Object Relational Designer.</span></span>

<span data-ttu-id="bd4e4-186">对 DataContext 以检索从电影的所有执行 LINQ 查询`tblMovies`数据库表。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-186">A LINQ query is performed against the DataContext to retrieve all of the movies from the `tblMovies` database table.</span></span> <span data-ttu-id="bd4e4-187">影片列表分配到一个名为的本地变量`movies`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-187">The list of movies is assigned to a local variable named `movies`.</span></span> <span data-ttu-id="bd4e4-188">最后，影片列表传递到视图查看数据。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-188">Finally, the list of movies is passed to the view through view data.</span></span>

<span data-ttu-id="bd4e4-189">为了显示电影，我们接下来需要修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-189">In order to show the movies, we next need to modify the Index view.</span></span> <span data-ttu-id="bd4e4-190">你可以查找中的索引视图`Views\Home\`文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-190">You can find the Index view in the `Views\Home\` folder.</span></span> <span data-ttu-id="bd4e4-191">更新索引视图，以便它如下所示列出 2 中的视图。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-191">Update the Index view so that it looks like the view in Listing 2.</span></span>

<span data-ttu-id="bd4e4-192">**列出 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-192">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

<span data-ttu-id="bd4e4-193">请注意，已修改的索引视图包括`<%@ import namespace %>`指令在视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-193">Notice that the modified Index view includes an `<%@ import namespace %>` directive at the top of the view.</span></span> <span data-ttu-id="bd4e4-194">此指令导入`MvcApplication1.Models namespace`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-194">This directive imports the `MvcApplication1.Models namespace`.</span></span> <span data-ttu-id="bd4e4-195">我们需要此命名空间才能使用`model`类-具体而言，`Movie`类-在视图中的。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-195">We need this namespace in order to work with the `model` classes – in particular, the `Movie` class -- in the view.</span></span>

<span data-ttu-id="bd4e4-196">列出 2 中的视图包含`foreach`循环访问所有所表示的项的循环`ViewData.Model`属性。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-196">The view in Listing 2 contains a `foreach` loop that iterates through all of the items represented by the `ViewData.Model` property.</span></span> <span data-ttu-id="bd4e4-197">值`Title`属性显示每个`movie`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-197">The value of the `Title` property is displayed for each `movie`.</span></span>

<span data-ttu-id="bd4e4-198">请注意，值`ViewData.Model`属性被强制转换为`IEnumerable`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-198">Notice that the value of the `ViewData.Model` property is cast to an `IEnumerable`.</span></span> <span data-ttu-id="bd4e4-199">这是需循环访问的内容`ViewData.Model`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-199">This is necessary in order to loop through the contents of `ViewData.Model`.</span></span> <span data-ttu-id="bd4e4-200">此处的另一个选项是创建一个强类型`view`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-200">Another option here is to create a strongly-typed `view`.</span></span> <span data-ttu-id="bd4e4-201">当你创建一个强类型`view`，您将转换`ViewData.Model`视图的代码隐藏类中的特定类型的属性。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-201">When you create a strongly-typed `view`, you cast the `ViewData.Model` property to a particular type in a view's code-behind class.</span></span>

<span data-ttu-id="bd4e4-202">如果运行修改后的应用程序`HomeController`类和索引视图，则会收到一个空白页。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-202">If you run the application after modifying the `HomeController` class and the Index view then you will get a blank page.</span></span> <span data-ttu-id="bd4e4-203">你将获得一个空白页，因为在没有电影记录`tblMovies`数据库表。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-203">You'll get a blank page because there are no movie records in the `tblMovies` database table.</span></span>

<span data-ttu-id="bd4e4-204">才可添加到记录`tblMovies`数据库表中，右键单击`tblMovies`数据库 （在 Visual Web Developer 的数据库资源管理器窗口） 中的服务器资源管理器窗口中表并选择显示表数据菜单选项。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-204">In order to add records to the `tblMovies` database table, right-click the `tblMovies` database table in the Server Explorer window (Database Explorer window in Visual Web Developer) and select the menu option Show Table Data.</span></span> <span data-ttu-id="bd4e4-205">你可以将插入`movie`使用网格显示 （请参阅图 6） 的记录。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-205">You can insert `movie` records by using the grid that appears (see Figure 6).</span></span>


<span data-ttu-id="bd4e4-206">[![插入电影](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-206">[![Inserting movies](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)</span></span>

<span data-ttu-id="bd4e4-207">**图 06**： 插入电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-207">**Figure 06**: Inserting movies([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))</span></span>


<span data-ttu-id="bd4e4-208">添加到某些数据库记录后`tblMovies`表和你运行应用程序，你将看到图 7 中的页。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-208">After you add some database records to the `tblMovies` table, and you run the application, you'll see the page in Figure 7.</span></span> <span data-ttu-id="bd4e4-209">项目符号列表中将显示所有影片数据库记录。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-209">All of the movie database records are displayed in a bulleted list.</span></span>


<span data-ttu-id="bd4e4-210">[![显示与索引视图的电影](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-210">[![Displaying movies with the Index view](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)</span></span>

<span data-ttu-id="bd4e4-211">**图 07**： 显示与索引视图的电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="bd4e4-211">**Figure 07**: Displaying movies with the Index view([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))</span></span>


## <a name="using-the-repository-pattern"></a><span data-ttu-id="bd4e4-212">使用存储库模式</span><span class="sxs-lookup"><span data-stu-id="bd4e4-212">Using the Repository Pattern</span></span>

<span data-ttu-id="bd4e4-213">在上一节中，我们使用 LINQ to SQL 类直接中的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-213">In the previous section, we used LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="bd4e4-214">我们使用`MovieDataContex`t 类直接从`Index()`控制器操作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-214">We used the `MovieDataContex` t class directly from the `Index()` controller action.</span></span> <span data-ttu-id="bd4e4-215">没有任何问题时执行此操作对于简单的应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-215">There is nothing wrong with doing this in the case of a simple application.</span></span> <span data-ttu-id="bd4e4-216">但是，控制器类中直接使用 LINQ to SQL 的工作创建问题时你需要生成更复杂的应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-216">However, working directly with LINQ to SQL in a controller class creates problems when you need to build a more complex application.</span></span>

<span data-ttu-id="bd4e4-217">在控制器类内使用 LINQ to SQL 难以将来切换数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-217">Using LINQ to SQL within a controller class makes it difficult to switch data access technologies in the future.</span></span> <span data-ttu-id="bd4e4-218">例如，你可能决定可以从使用 Microsoft LINQ to SQL 将用作你的数据访问技术的 Microsoft 实体框架切换。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-218">For example, you might decide to switch from using Microsoft LINQ to SQL to using the Microsoft Entity Framework as your data access technology.</span></span> <span data-ttu-id="bd4e4-219">在这种情况下，你将需要重写访问该数据库在你的应用程序的每个控制器。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-219">In that case, you would need to rewrite every controller that accesses the database within your application.</span></span>

<span data-ttu-id="bd4e4-220">在控制器类内使用 LINQ to SQL 还使难以生成你的应用程序的单元测试。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-220">Using LINQ to SQL within a controller class also makes it difficult to build unit tests for your application.</span></span> <span data-ttu-id="bd4e4-221">通常情况下，你不想要执行单元测试时，与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-221">Normally, you do not want to interact with a database when performing unit tests.</span></span> <span data-ttu-id="bd4e4-222">你想要使用你的单元测试来测试你的应用程序逻辑和不是你的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-222">You want to use your unit tests to test your application logic and not your database server.</span></span>

<span data-ttu-id="bd4e4-223">即以生成一个 MVC 应用程序更适应未来更改并要更轻松地测试，则应考虑使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-223">In order to build an MVC application that is more adaptable to future change and that can be more easily tested, you should consider using the Repository pattern.</span></span> <span data-ttu-id="bd4e4-224">当你使用的存储库模式时，你将创建包含所有数据库访问逻辑的一个单独的存储库类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-224">When you use the Repository pattern, you create a separate repository class that contains all of your database access logic.</span></span>

<span data-ttu-id="bd4e4-225">当你创建存储库类时，你将创建一个接口来表示所有存储库类所使用的方法。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-225">When you create the repository class, you create an interface that represents all of the methods used by the repository class.</span></span> <span data-ttu-id="bd4e4-226">在你的控制器，你将编写针对接口而不是存储库代码。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-226">Within your controllers, you write your code against the interface instead of the repository.</span></span> <span data-ttu-id="bd4e4-227">这样一来，你可以实现在将来使用不同的数据访问技术的存储库。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-227">That way, you can implement the repository using different data access technologies in the future.</span></span>

<span data-ttu-id="bd4e4-228">中列出的 3 的接口名为`IMovieRepository`，它表示一个名为的单个方法`ListAll()`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-228">The interface in Listing 3 is named `IMovieRepository` and it represents a single method named `ListAll()`.</span></span>

<span data-ttu-id="bd4e4-229">**列出 3 – `Models\IMovieRepository.cs`**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-229">**Listing 3 – `Models\IMovieRepository.cs`**</span></span>

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

<span data-ttu-id="bd4e4-230">列出 4 中的存储库类实现`IMovieRepository`接口。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-230">The repository class in Listing 4 implements the `IMovieRepository` interface.</span></span> <span data-ttu-id="bd4e4-231">请注意，它包含一个名为方法`ListAll()`相对应的所需的方法`IMovieRepository`接口。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-231">Notice that it contains a method named `ListAll()` that corresponds to the method required by the `IMovieRepository` interface.</span></span>

<span data-ttu-id="bd4e4-232">**列出 4 – `Models\MovieRepository.cs`**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-232">**Listing 4 – `Models\MovieRepository.cs`**</span></span>

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

<span data-ttu-id="bd4e4-233">最后，`MoviesController`列出 5 中的类使用的存储库模式。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-233">Finally, the `MoviesController` class in Listing 5 uses the Repository pattern.</span></span> <span data-ttu-id="bd4e4-234">它不再使用 LINQ to SQL 类直接。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-234">It no longer uses LINQ to SQL classes directly.</span></span>

<span data-ttu-id="bd4e4-235">**列出 5- `Controllers\MoviesController.cs`**</span><span class="sxs-lookup"><span data-stu-id="bd4e4-235">**Listing 5 – `Controllers\MoviesController.cs`**</span></span>

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

<span data-ttu-id="bd4e4-236">请注意，`MoviesController`中列出 5 类都具有两个构造函数。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-236">Notice that the `MoviesController` class in Listing 5 has two constructors.</span></span> <span data-ttu-id="bd4e4-237">第一个构造函数，无参数构造函数中，称为应用程序运行时。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-237">The first constructor, the parameterless constructor, is called when your application is running.</span></span> <span data-ttu-id="bd4e4-238">此构造函数创建的实例`MovieRepository`类并将其传递给第二个构造函数。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-238">This constructor creates an instance of the `MovieRepository` class and passes it to the second constructor.</span></span>

<span data-ttu-id="bd4e4-239">第二个构造函数具有单个参数：`IMovieRepository`参数。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-239">The second constructor has a single parameter: an `IMovieRepository` parameter.</span></span> <span data-ttu-id="bd4e4-240">此构造函数只需将参数的值分配给名为的类级字段`_repository`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-240">This constructor simply assigns the value of the parameter to a class-level field named `_repository`.</span></span>

<span data-ttu-id="bd4e4-241">`MoviesController`类正在调用的依赖关系注入模式软件设计模式的优点。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-241">The `MoviesController` class is taking advantage of a software design pattern called the Dependency Injection pattern.</span></span> <span data-ttu-id="bd4e4-242">具体而言，它使用调用构造函数依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-242">In particular, it is using something called Constructor Dependency Injection.</span></span> <span data-ttu-id="bd4e4-243">你可以阅读更多有关通过阅读以下文章 Martin Fowler 通过此模式：</span><span class="sxs-lookup"><span data-stu-id="bd4e4-243">You can read more about this pattern by reading the following article by Martin Fowler:</span></span>

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

<span data-ttu-id="bd4e4-244">请注意，中的代码的所有`MoviesController`（不包括第一个构造函数） 的类与交互`IMovieRepository`而不是实际接口`MovieRepository`类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-244">Notice that all of the code in the `MoviesController` class (with the exception of the first constructor) interacts with the `IMovieRepository` interface instead of the actual `MovieRepository` class.</span></span> <span data-ttu-id="bd4e4-245">代码而不是该接口的具体实现的抽象接口与交互。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-245">The code interacts with an abstract interface instead of a concrete implementation of the interface.</span></span>

<span data-ttu-id="bd4e4-246">如果你想要修改应用程序使用的数据访问技术，则你可以只是要实施`IMovieRepository`使用备用数据库访问技术的类接口。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-246">If you want to modify the data access technology used by the application then you can simply implement the `IMovieRepository` interface with a class that uses the alternative database access technology.</span></span> <span data-ttu-id="bd4e4-247">例如，你可以创建`EntityFrameworkMovieRepository`类或`SubSonicMovieRepository`类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-247">For example, you could create an `EntityFrameworkMovieRepository` class or a `SubSonicMovieRepository` class.</span></span> <span data-ttu-id="bd4e4-248">由于针对接口进行编程控制器类，因此可以传递的新实现`IMovieRepository`到控制器类和类将继续工作。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-248">Because the controller class is programmed against the interface, you can pass a new implementation of `IMovieRepository` to the controller class and the class would continue to work.</span></span>

<span data-ttu-id="bd4e4-249">此外，如果你想要测试`MoviesController`类，则可以将假的电影存储库类中，以便传递`HomeController`。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-249">Furthermore, if you want to test the `MoviesController` class, then you can pass a fake movie repository class to the `HomeController`.</span></span> <span data-ttu-id="bd4e4-250">你可以实现`IMovieRepository`与不执行实际访问数据库，但包含所有所需的方法的类的类`IMovieRepository`接口。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-250">You can implement the `IMovieRepository` class with a class that does not actually access the database but contains all of the required methods of the `IMovieRepository` interface.</span></span> <span data-ttu-id="bd4e4-251">这样一来，你可以将单元测试`MoviesController`不用真正访问实际的数据库的类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-251">That way, you can unit test the `MoviesController` class without actually accessing a real database.</span></span>

## <a name="summary"></a><span data-ttu-id="bd4e4-252">总结</span><span class="sxs-lookup"><span data-stu-id="bd4e4-252">Summary</span></span>

<span data-ttu-id="bd4e4-253">本教程的目标是演示如何利用 Microsoft LINQ to SQL 来创建 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-253">The goal of this tutorial was to demonstrate how you can create MVC model classes by taking advantage of Microsoft LINQ to SQL.</span></span> <span data-ttu-id="bd4e4-254">有关 ASP.NET MVC 应用程序中显示数据库数据的两种策略，我们探讨。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-254">We examined two strategies for displaying database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="bd4e4-255">首先，我们创建 LINQ to SQL 类，并使用直接中的控制器操作的类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-255">First, we created LINQ to SQL classes and used the classes directly within a controller action.</span></span> <span data-ttu-id="bd4e4-256">使用 LINQ to SQL 类控制器中，您可以快速并轻松地在 MVC 应用程序中显示数据库数据。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-256">Using LINQ to SQL classes within a controller enables you to quickly and easily display database data in an MVC application.</span></span>

<span data-ttu-id="bd4e4-257">接下来，我们探讨了显示数据库数据的稍微有些困难，但肯定更良性的路径。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-257">Next, we explored a slightly more difficult, but definitely more virtuous, path for displaying database data.</span></span> <span data-ttu-id="bd4e4-258">我们采用存储库模式的优点，并放在单独的存储库类中的所有我们数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-258">We took advantage of the Repository pattern and placed all of our database access logic in a separate repository class.</span></span> <span data-ttu-id="bd4e4-259">在我们控制器中，我们已写入所有我们针对而不是具体的类接口的代码。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-259">In our controller, we wrote all of our code against an interface instead of a concrete class.</span></span> <span data-ttu-id="bd4e4-260">存储库模式的优点是，它使我们能够轻松地在将来更改数据库访问技术，并且它允许我们能够轻松地测试我们控制器类。</span><span class="sxs-lookup"><span data-stu-id="bd4e4-260">The advantage of the Repository pattern is that it enables us to easily change database access technologies in the future and it enables us to easily test our controller classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bd4e4-261">[上一页](creating-model-classes-with-the-entity-framework-cs.md)
> [下一页](displaying-a-table-of-database-data-cs.md)</span><span class="sxs-lookup"><span data-stu-id="bd4e4-261">[Previous](creating-model-classes-with-the-entity-framework-cs.md)
[Next](displaying-a-table-of-database-data-cs.md)</span></span>
