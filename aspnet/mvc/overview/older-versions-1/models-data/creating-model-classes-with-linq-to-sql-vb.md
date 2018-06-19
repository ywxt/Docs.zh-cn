---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: 使用 LINQ to SQL (VB) 创建模型类 |Microsoft 文档
author: microsoft
description: 本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。 在本教程中，你将学习如何构建模型 c...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 5438838123c40d82afbda191a48878d6dca80736
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874806"
---
<a name="creating-model-classes-with-linq-to-sql-vb"></a><span data-ttu-id="49351-104">使用 LINQ to SQL (VB) 中创建模型类</span><span class="sxs-lookup"><span data-stu-id="49351-104">Creating Model Classes with LINQ to SQL (VB)</span></span>
====================
<span data-ttu-id="49351-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="49351-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="49351-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="49351-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> <span data-ttu-id="49351-107">本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。</span><span class="sxs-lookup"><span data-stu-id="49351-107">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="49351-108">在本教程中，你将学习如何生成模型的类，并通过利用 Microsoft LINQ to SQL 中执行数据库访问。</span><span class="sxs-lookup"><span data-stu-id="49351-108">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>


<span data-ttu-id="49351-109">本教程旨在说明创建 ASP.NET MVC 应用程序的模型类的一个方法。</span><span class="sxs-lookup"><span data-stu-id="49351-109">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="49351-110">在本教程中，你将学习如何生成模型的类，并通过利用 Microsoft LINQ to SQL 中执行数据库访问。</span><span class="sxs-lookup"><span data-stu-id="49351-110">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>

<span data-ttu-id="49351-111">在本教程中，我们构建基本的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-111">In this tutorial, we build a basic Movie database application.</span></span> <span data-ttu-id="49351-112">我们首先创建可能的最快和最简单的方法电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-112">We start by creating the Movie database application in the fastest and easiest way possible.</span></span> <span data-ttu-id="49351-113">我们直接从我们的控制器操作中执行所有我们数据访问。</span><span class="sxs-lookup"><span data-stu-id="49351-113">We perform all of our data access directly from our controller actions.</span></span>

<span data-ttu-id="49351-114">接下来，你将了解如何使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="49351-114">Next, you learn how to use the Repository pattern.</span></span> <span data-ttu-id="49351-115">使用存储库模式需要稍有更多工作。</span><span class="sxs-lookup"><span data-stu-id="49351-115">Using the Repository pattern requires a little more work.</span></span> <span data-ttu-id="49351-116">但是，采用此模式的优点是它使你能够构建的应用程序适应更改，并可以轻松地测试。</span><span class="sxs-lookup"><span data-stu-id="49351-116">However, the advantage of adopting this pattern is that it enables you to build applications that are adaptable to change and can be easily tested.</span></span>

## <a name="what-is-a-model-class"></a><span data-ttu-id="49351-117">什么是模型类？</span><span class="sxs-lookup"><span data-stu-id="49351-117">What is a Model Class?</span></span>

<span data-ttu-id="49351-118">MVC 模型包含所有未包含在 MVC 视图或 MVC 控制器中的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="49351-118">An MVC model contains all of the application logic that is not contained in an MVC view or MVC controller.</span></span> <span data-ttu-id="49351-119">具体而言，MVC 模型包含的所有应用程序业务和数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="49351-119">In particular, an MVC model contains all of your application business and data access logic.</span></span>

<span data-ttu-id="49351-120">可以使用各种不同的技术来实现数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="49351-120">You can use a variety of different technologies to implement your data access logic.</span></span> <span data-ttu-id="49351-121">例如，你可以生成数据访问类使用的 Microsoft 实体框架、 NHibernate、 Subsonic 或 ADO.NET 类。</span><span class="sxs-lookup"><span data-stu-id="49351-121">For example, you can build your data access classes using the Microsoft Entity Framework, NHibernate, Subsonic, or ADO.NET classes.</span></span>

<span data-ttu-id="49351-122">在本教程中，我可以使用 LINQ to SQL 来查询和更新数据库。</span><span class="sxs-lookup"><span data-stu-id="49351-122">In this tutorial, I use LINQ to SQL to query and update the database.</span></span> <span data-ttu-id="49351-123">LINQ to SQL 可为你提供与 Microsoft SQL Server 数据库交互的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="49351-123">LINQ to SQL provides you with a very easy method of interacting with a Microsoft SQL Server database.</span></span> <span data-ttu-id="49351-124">但是，务必了解 ASP.NET MVC framework 未绑定到 LINQ to SQL 以任何方式。</span><span class="sxs-lookup"><span data-stu-id="49351-124">However, it is important to understand that the ASP.NET MVC framework is not tied to LINQ to SQL in any way.</span></span> <span data-ttu-id="49351-125">ASP.NET MVC 适用于任何数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="49351-125">ASP.NET MVC is compatible with any data access technology.</span></span>

## <a name="create-a-movie-database"></a><span data-ttu-id="49351-126">创建电影数据库</span><span class="sxs-lookup"><span data-stu-id="49351-126">Create a Movie Database</span></span>

<span data-ttu-id="49351-127">在此教程--若要演示如何生成模型类-我们构建一个简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-127">In this tutorial -- in order to illustrate how you can build model classes -- we build a simple Movie database application.</span></span> <span data-ttu-id="49351-128">第一步是创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="49351-128">The first step is to create a new database.</span></span> <span data-ttu-id="49351-129">右键单击该应用\_在解决方案资源管理器窗口中，然后选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="49351-129">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span> <span data-ttu-id="49351-130">选择 SQL Server 数据库的模板，将其命名 MoviesDB.mdf，然后单击**添加**按钮 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="49351-130">Select the SQL Server Database template, give it the name MoviesDB.mdf, and click the **Add** button (see Figure 1).</span></span>


<span data-ttu-id="49351-131">[![添加新的 SQL Server 数据库](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="49351-131">[![Adding a new SQL Server Database](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)</span></span>

<span data-ttu-id="49351-132">**图 01**： 添加新的 SQL Server 数据库 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="49351-132">**Figure 01**: Adding a new SQL Server Database ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))</span></span>


<span data-ttu-id="49351-133">创建新的数据库后，你可以通过双击 MoviesDB.mdf 文件，在应用中的打开数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="49351-133">After you create the new database, you can open the database by double-clicking the MoviesDB.mdf file in the App\_Data folder.</span></span> <span data-ttu-id="49351-134">双击 MoviesDB.mdf 文件打开服务器资源管理器窗口 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="49351-134">Double-clicking the MoviesDB.mdf file opens the Server Explorer window (see Figure 2).</span></span>


|   | <span data-ttu-id="49351-135">服务器资源管理器窗口时使用 Visual Web Developer 调用数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="49351-135">The Server Explorer window is called the Database Explorer window when using Visual Web Developer.</span></span> |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

<span data-ttu-id="49351-136">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="49351-136">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)</span></span>

<span data-ttu-id="49351-137">**图 02**： 使用服务器资源管理器窗口 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="49351-137">**Figure 02**: Using the Server Explorer window ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))</span></span>


<span data-ttu-id="49351-138">我们需要将表添加到我们表示我们电影的数据库。</span><span class="sxs-lookup"><span data-stu-id="49351-138">We need to add one table to our database that represents our movies.</span></span> <span data-ttu-id="49351-139">右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="49351-139">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="49351-140">选择此菜单选项将打开表设计器 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="49351-140">Selecting this menu option opens the Table Designer (see Figure 3).</span></span>


<span data-ttu-id="49351-141">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="49351-141">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)</span></span>

<span data-ttu-id="49351-142">**图 03**： 表设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="49351-142">**Figure 03**: The Table Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))</span></span>


<span data-ttu-id="49351-143">我们需要将以下各列添加到我们的数据库表：</span><span class="sxs-lookup"><span data-stu-id="49351-143">We need to add the following columns to our database table:</span></span>

| <span data-ttu-id="49351-144">**列名称**</span><span class="sxs-lookup"><span data-stu-id="49351-144">**Column Name**</span></span> | <span data-ttu-id="49351-145">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="49351-145">**Data Type**</span></span> | <span data-ttu-id="49351-146">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="49351-146">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49351-147">Id</span><span class="sxs-lookup"><span data-stu-id="49351-147">Id</span></span> | <span data-ttu-id="49351-148">Int</span><span class="sxs-lookup"><span data-stu-id="49351-148">Int</span></span> | <span data-ttu-id="49351-149">False</span><span class="sxs-lookup"><span data-stu-id="49351-149">False</span></span> |
| <span data-ttu-id="49351-150">标题</span><span class="sxs-lookup"><span data-stu-id="49351-150">Title</span></span> | <span data-ttu-id="49351-151">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="49351-151">Nvarchar(200)</span></span> | <span data-ttu-id="49351-152">False</span><span class="sxs-lookup"><span data-stu-id="49351-152">False</span></span> |
| <span data-ttu-id="49351-153">控制器</span><span class="sxs-lookup"><span data-stu-id="49351-153">Director</span></span> | <span data-ttu-id="49351-154">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="49351-154">Nvarchar(50)</span></span> | <span data-ttu-id="49351-155">False</span><span class="sxs-lookup"><span data-stu-id="49351-155">False</span></span> |

<span data-ttu-id="49351-156">你需要执行到 Id 列的两个特殊操作。</span><span class="sxs-lookup"><span data-stu-id="49351-156">You need to do two special things to the Id column.</span></span> <span data-ttu-id="49351-157">首先，你需要将 Id 列标记为主键列，通过在表设计器中选择列并单击项的图标。</span><span class="sxs-lookup"><span data-stu-id="49351-157">First, you need to mark the Id column as a primary key column by selecting the column in the Table Designer and clicking the icon of a key.</span></span> <span data-ttu-id="49351-158">LINQ to SQL 要求你在执行插入或更新对数据库时指定主键列。</span><span class="sxs-lookup"><span data-stu-id="49351-158">LINQ to SQL requires you to specify your primary key columns when performing inserts or updates against the database.</span></span>

<span data-ttu-id="49351-159">接下来，你需要将 Id 列标记为标识列，通过是将值分配给**是标识**属性 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="49351-159">Next, you need to mark the Id column as an Identity column by assigning the value Yes to the **Is Identity** property (see Figure 3).</span></span> <span data-ttu-id="49351-160">标识列是自动将分配较新的数字，每当将新的数据行添加到表的列。</span><span class="sxs-lookup"><span data-stu-id="49351-160">An Identity column is a column that is assigned a new number automatically whenever you add a new row of data to a table.</span></span>

<span data-ttu-id="49351-161">进行这些更改后，保存名称 tblMovie 表。</span><span class="sxs-lookup"><span data-stu-id="49351-161">After you make these changes, save the table with the name tblMovie.</span></span> <span data-ttu-id="49351-162">可以通过单击保存按钮保存该表。</span><span class="sxs-lookup"><span data-stu-id="49351-162">You can save the table by clicking the Save button.</span></span>

## <a name="create-linq-to-sql-classes"></a><span data-ttu-id="49351-163">创建 LINQ to SQL 类</span><span class="sxs-lookup"><span data-stu-id="49351-163">Create LINQ to SQL Classes</span></span>

<span data-ttu-id="49351-164">我们的 MVC 模型将包含 LINQ to SQL 类表示 tblMovie 数据库表。</span><span class="sxs-lookup"><span data-stu-id="49351-164">Our MVC model will contain LINQ to SQL classes that represent the tblMovie database table.</span></span> <span data-ttu-id="49351-165">若要创建这些 LINQ to SQL 类的最简单方法是右键单击 Models 文件夹，选择**添加、 新项**，选择 LINQ to SQL 类模板，将类命名 Movie.dbml，然后单击**添加**按钮 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="49351-165">The easiest way to create these LINQ to SQL classes is to right-click the Models folder, select **Add, New Item**, select the LINQ to SQL Classes template, give the classes the name Movie.dbml, and click the **Add** button (see Figure 4).</span></span>


<span data-ttu-id="49351-166">[![创建 LINQ to SQL 类](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="49351-166">[![Creating LINQ to SQL classes](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)</span></span>

<span data-ttu-id="49351-167">**图 04**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="49351-167">**Figure 04**: Creating LINQ to SQL classes ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))</span></span>


<span data-ttu-id="49351-168">立即创建电影 LINQ to SQL 类后，将显示对象关系设计器。</span><span class="sxs-lookup"><span data-stu-id="49351-168">Immediately after you create the Movie LINQ to SQL Classes, the Object Relational Designer appears.</span></span> <span data-ttu-id="49351-169">你可以将数据库表从服务器资源管理器窗口拖动对象关系设计器创建 LINQ to SQL 类表示特定数据库表。</span><span class="sxs-lookup"><span data-stu-id="49351-169">You can drag database tables from the Server Explorer window onto the Object Relational Designer to create LINQ to SQL Classes that represent particular database tables.</span></span> <span data-ttu-id="49351-170">我们需要添加 tblMovie 数据库表拖放到对象关系设计器 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="49351-170">We need to add the tblMovie database table onto the Object Relational Designer (see Figure 4).</span></span>


<span data-ttu-id="49351-171">[![使用对象关系设计器](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="49351-171">[![Using the Object Relational Designer](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)</span></span>

<span data-ttu-id="49351-172">**图 05**： 使用对象关系设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="49351-172">**Figure 05**: Using the Object Relational Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))</span></span>


<span data-ttu-id="49351-173">默认情况下，对象关系设计器创建一个具有类与数据库表拖到设计器上非常相同的名称。</span><span class="sxs-lookup"><span data-stu-id="49351-173">By default, the Object Relational Designer creates a class with the very same name as the database table that you drag onto the Designer.</span></span> <span data-ttu-id="49351-174">但是，我们不想调用我们类 tblMovie。</span><span class="sxs-lookup"><span data-stu-id="49351-174">However, we don't want to call our class tblMovie.</span></span> <span data-ttu-id="49351-175">因此，单击设计器中的类的名称，并将类的名称更改为影片。</span><span class="sxs-lookup"><span data-stu-id="49351-175">Therefore, click the name of the class in the Designer and change the name of the class to Movie.</span></span>

<span data-ttu-id="49351-176">最后，请记住单击**保存**按钮 （软盘图片） 将 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="49351-176">Finally, remember to click the **Save** button (the picture of the floppy) to save the LINQ to SQL Classes.</span></span> <span data-ttu-id="49351-177">否则，不会由对象关系设计器生成 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="49351-177">Otherwise, the LINQ to SQL Classes won't be generated by the Object Relational Designer.</span></span>

## <a name="using-linq-to-sql-in-a-controller-action"></a><span data-ttu-id="49351-178">在控制器操作中使用 LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="49351-178">Using LINQ to SQL in a Controller Action</span></span>

<span data-ttu-id="49351-179">现在，我们已我们 LINQ to SQL 类，我们可以使用这些类以从数据库检索数据。</span><span class="sxs-lookup"><span data-stu-id="49351-179">Now that we have our LINQ to SQL classes, we can use these classes to retrieve data from the database.</span></span> <span data-ttu-id="49351-180">在本部分中，你将了解如何使用 LINQ to SQL 类直接中的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="49351-180">In this section, you learn how to use LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="49351-181">我们将在的 MVC 视图中显示 tblMovies 数据库表中的影片的列表。</span><span class="sxs-lookup"><span data-stu-id="49351-181">We'll display the list of movies from the tblMovies database table in an MVC view.</span></span>

<span data-ttu-id="49351-182">首先，我们需要修改 HomeController 类。</span><span class="sxs-lookup"><span data-stu-id="49351-182">First, we need to modify the HomeController class.</span></span> <span data-ttu-id="49351-183">你的应用程序的 Controllers 文件夹中找不到此类。</span><span class="sxs-lookup"><span data-stu-id="49351-183">This class can be found in the Controllers folder of your application.</span></span> <span data-ttu-id="49351-184">修改类，使其类似列表 1 中的类。</span><span class="sxs-lookup"><span data-stu-id="49351-184">Modify the class so it looks like the class in Listing 1.</span></span>

<span data-ttu-id="49351-185">**列表 1 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="49351-185">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

<span data-ttu-id="49351-186">列表 1 中的 index （） 操作使用 LINQ to SQL DataContext 类 (MovieDataContext) 来表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="49351-186">The Index() action in Listing 1 uses a LINQ to SQL DataContext class (the MovieDataContext) to represent the MoviesDB database.</span></span> <span data-ttu-id="49351-187">MoveDataContext 类是通过 Visual Studio 对象关系设计器生成的。</span><span class="sxs-lookup"><span data-stu-id="49351-187">The MoveDataContext class was generated by the Visual Studio Object Relational Designer.</span></span>

<span data-ttu-id="49351-188">对 DataContext 以从 tblMovies 数据库表中检索所有影片执行 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="49351-188">A LINQ query is performed against the DataContext to retrieve all of the movies from the tblMovies database table.</span></span> <span data-ttu-id="49351-189">影片列表分配给一个名为电影的本地变量。</span><span class="sxs-lookup"><span data-stu-id="49351-189">The list of movies is assigned to a local variable named movies.</span></span> <span data-ttu-id="49351-190">最后，影片列表传递到视图查看数据。</span><span class="sxs-lookup"><span data-stu-id="49351-190">Finally, the list of movies is passed to the view through view data.</span></span>

<span data-ttu-id="49351-191">为了显示电影，我们接下来需要修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="49351-191">In order to show the movies, we next need to modify the Index view.</span></span> <span data-ttu-id="49351-192">你可以在 Views\Home\ 文件夹中找到索引视图。</span><span class="sxs-lookup"><span data-stu-id="49351-192">You can find the Index view in the Views\Home\ folder.</span></span> <span data-ttu-id="49351-193">更新索引视图，以便它如下所示列出 2 中的视图。</span><span class="sxs-lookup"><span data-stu-id="49351-193">Update the Index view so that it looks like the view in Listing 2.</span></span>

<span data-ttu-id="49351-194">**列出 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="49351-194">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

<span data-ttu-id="49351-195">请注意，已修改的索引视图包括&lt;%@ 导入命名空间 %&gt;指令在视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="49351-195">Notice that the modified Index view includes an &lt;%@ import namespace %&gt; directive at the top of the view.</span></span> <span data-ttu-id="49351-196">此指令导入 MvcApplication1 命名空间。</span><span class="sxs-lookup"><span data-stu-id="49351-196">This directive imports the MvcApplication1 namespace.</span></span> <span data-ttu-id="49351-197">若要使用的模型类-具体而言，电影类-在视图中的，我们需要此命名空间。</span><span class="sxs-lookup"><span data-stu-id="49351-197">We need this namespace in order to work with the model classes – in particular, the Movie class -- in the view.</span></span>

<span data-ttu-id="49351-198">列出 2 中的视图包含一个 For 循环访问的所有项由 ViewData.Model 属性表示每个循环。</span><span class="sxs-lookup"><span data-stu-id="49351-198">The view in Listing 2 contains a For Each loop that iterates through all of the items represented by the ViewData.Model property.</span></span> <span data-ttu-id="49351-199">为每个影片显示标题属性的值。</span><span class="sxs-lookup"><span data-stu-id="49351-199">The value of the Title property is displayed for each movie.</span></span>

<span data-ttu-id="49351-200">请注意 ViewData.Model 属性的值被强制转换为 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="49351-200">Notice that the value of the ViewData.Model property is cast to an IEnumerable.</span></span> <span data-ttu-id="49351-201">这是需循环访问 ViewData.Model 的内容。</span><span class="sxs-lookup"><span data-stu-id="49351-201">This is necessary in order to loop through the contents of ViewData.Model.</span></span> <span data-ttu-id="49351-202">此处的另一个选项是创建强类型视图。</span><span class="sxs-lookup"><span data-stu-id="49351-202">Another option here is to create a strongly-typed view.</span></span> <span data-ttu-id="49351-203">当创建强类型化视图时，你在视图的代码隐藏类转换将 ViewData.Model 属性设为特定类型。</span><span class="sxs-lookup"><span data-stu-id="49351-203">When you create a strongly-typed view, you cast the ViewData.Model property to a particular type in a view's code-behind class.</span></span>

<span data-ttu-id="49351-204">如果你运行后修改 HomeController 类和索引视图，则会收到一个空白页的应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-204">If you run the application after modifying the HomeController class and the Index view then you will get a blank page.</span></span> <span data-ttu-id="49351-205">你将获得一个空白页，因为 tblMovies 数据库表中没有电影的记录。</span><span class="sxs-lookup"><span data-stu-id="49351-205">You'll get a blank page because there are no movie records in the tblMovies database table.</span></span>

<span data-ttu-id="49351-206">为了向 tblMovies 数据库表添加记录，右键单击服务器资源管理器窗口 （在 Visual Web Developer 的数据库资源管理器窗口） 中的 tblMovies 数据库表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="49351-206">In order to add records to the tblMovies database table, right-click the tblMovies database table in the Server Explorer window (Database Explorer window in Visual Web Developer) and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="49351-207">你可以通过使用显示 （请参见图 5） 的网格插入电影记录。</span><span class="sxs-lookup"><span data-stu-id="49351-207">You can insert movie records by using the grid that appears (see Figure 5).</span></span>


<span data-ttu-id="49351-208">[![插入电影](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="49351-208">[![Inserting movies](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)</span></span>

<span data-ttu-id="49351-209">**图 06**： 插入电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="49351-209">**Figure 06**: Inserting movies([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))</span></span>


<span data-ttu-id="49351-210">将某些数据库记录添加到 tblMovies 表，并运行应用程序后，你将看到图 7 中的页。</span><span class="sxs-lookup"><span data-stu-id="49351-210">After you add some database records to the tblMovies table, and you run the application, you'll see the page in Figure 7.</span></span> <span data-ttu-id="49351-211">项目符号列表中将显示所有影片数据库记录。</span><span class="sxs-lookup"><span data-stu-id="49351-211">All of the movie database records are displayed in a bulleted list.</span></span>


<span data-ttu-id="49351-212">[![显示与索引视图的电影](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="49351-212">[![Displaying movies with the Index view](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)</span></span>

<span data-ttu-id="49351-213">**图 07**： 显示与索引视图的电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="49351-213">**Figure 07**: Displaying movies with the Index view([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))</span></span>


## <a name="using-the-repository-pattern"></a><span data-ttu-id="49351-214">使用存储库模式</span><span class="sxs-lookup"><span data-stu-id="49351-214">Using the Repository Pattern</span></span>

<span data-ttu-id="49351-215">在上一节中，我们使用 LINQ to SQL 类直接中的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="49351-215">In the previous section, we used LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="49351-216">我们使用 MovieDataContext 类直接从 index （） 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="49351-216">We used the MovieDataContext class directly from the Index() controller action.</span></span> <span data-ttu-id="49351-217">没有任何问题时执行此操作对于简单的应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-217">There is nothing wrong with doing this in the case of a simple application.</span></span> <span data-ttu-id="49351-218">但是，控制器类中直接使用 LINQ to SQL 的工作创建问题时你需要生成更复杂的应用程序。</span><span class="sxs-lookup"><span data-stu-id="49351-218">However, working directly with LINQ to SQL in a controller class creates problems when you need to build a more complex application.</span></span>

<span data-ttu-id="49351-219">在控制器类内使用 LINQ to SQL 难以将来切换数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="49351-219">Using LINQ to SQL within a controller class makes it difficult to switch data access technologies in the future.</span></span> <span data-ttu-id="49351-220">例如，你可能决定可以从使用 Microsoft LINQ to SQL 将用作你的数据访问技术的 Microsoft 实体框架切换。</span><span class="sxs-lookup"><span data-stu-id="49351-220">For example, you might decide to switch from using Microsoft LINQ to SQL to using the Microsoft Entity Framework as your data access technology.</span></span> <span data-ttu-id="49351-221">在这种情况下，你将需要重写访问该数据库在你的应用程序的每个控制器。</span><span class="sxs-lookup"><span data-stu-id="49351-221">In that case, you would need to rewrite every controller that accesses the database within your application.</span></span>

<span data-ttu-id="49351-222">在控制器类内使用 LINQ to SQL 还使难以生成你的应用程序的单元测试。</span><span class="sxs-lookup"><span data-stu-id="49351-222">Using LINQ to SQL within a controller class also makes it difficult to build unit tests for your application.</span></span> <span data-ttu-id="49351-223">通常情况下，你不想要执行单元测试时，与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="49351-223">Normally, you do not want to interact with a database when performing unit tests.</span></span> <span data-ttu-id="49351-224">你想要使用你的单元测试来测试你的应用程序逻辑和不是你的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="49351-224">You want to use your unit tests to test your application logic and not your database server.</span></span>

<span data-ttu-id="49351-225">即以生成一个 MVC 应用程序更适应未来更改并要更轻松地测试，则应考虑使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="49351-225">In order to build an MVC application that is more adaptable to future change and that can be more easily tested, you should consider using the Repository pattern.</span></span> <span data-ttu-id="49351-226">当你使用的存储库模式时，你将创建包含所有数据库访问逻辑的一个单独的存储库类。</span><span class="sxs-lookup"><span data-stu-id="49351-226">When you use the Repository pattern, you create a separate repository class that contains all of your database access logic.</span></span>

<span data-ttu-id="49351-227">当你创建存储库类时，你将创建一个接口来表示所有存储库类所使用的方法。</span><span class="sxs-lookup"><span data-stu-id="49351-227">When you create the repository class, you create an interface that represents all of the methods used by the repository class.</span></span> <span data-ttu-id="49351-228">在你的控制器，你将编写针对接口而不是存储库代码。</span><span class="sxs-lookup"><span data-stu-id="49351-228">Within your controllers, you write your code against the interface instead of the repository.</span></span> <span data-ttu-id="49351-229">这样一来，你可以实现在将来使用不同的数据访问技术的存储库。</span><span class="sxs-lookup"><span data-stu-id="49351-229">That way, you can implement the repository using different data access technologies in the future.</span></span>

<span data-ttu-id="49351-230">中列出的 3 的接口名称为 IMovieRepository，它表示一个名为 ListAll() 的单个方法。</span><span class="sxs-lookup"><span data-stu-id="49351-230">The interface in Listing 3 is named IMovieRepository and it represents a single method named ListAll().</span></span>

<span data-ttu-id="49351-231">**列出 3 – `Models\IMovieRepository.vb`**</span><span class="sxs-lookup"><span data-stu-id="49351-231">**Listing 3 – `Models\IMovieRepository.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

<span data-ttu-id="49351-232">列出 4 中的存储库类实现 IMovieRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="49351-232">The repository class in Listing 4 implements the IMovieRepository interface.</span></span> <span data-ttu-id="49351-233">请注意，它包含一个名为 IMovieRepository 接口所需的方法对应的 ListAll() 方法。</span><span class="sxs-lookup"><span data-stu-id="49351-233">Notice that it contains a method named ListAll() that corresponds to the method required by the IMovieRepository interface.</span></span>

<span data-ttu-id="49351-234">**列出 4 – `Models\MovieRepository.vb`**</span><span class="sxs-lookup"><span data-stu-id="49351-234">**Listing 4 – `Models\MovieRepository.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

<span data-ttu-id="49351-235">最后，在列出 5 MoviesController 类使用的存储库模式。</span><span class="sxs-lookup"><span data-stu-id="49351-235">Finally, the MoviesController class in Listing 5 uses the Repository pattern.</span></span> <span data-ttu-id="49351-236">它不再使用 LINQ to SQL 类直接。</span><span class="sxs-lookup"><span data-stu-id="49351-236">It no longer uses LINQ to SQL classes directly.</span></span>

<span data-ttu-id="49351-237">**列出 5- `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="49351-237">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

<span data-ttu-id="49351-238">请注意，在列出 5 MoviesController 类有两个构造函数。</span><span class="sxs-lookup"><span data-stu-id="49351-238">Notice that the MoviesController class in Listing 5 has two constructors.</span></span> <span data-ttu-id="49351-239">第一个构造函数，无参数构造函数中，称为应用程序运行时。</span><span class="sxs-lookup"><span data-stu-id="49351-239">The first constructor, the parameterless constructor, is called when your application is running.</span></span> <span data-ttu-id="49351-240">此构造函数创建 MovieRepository 类的实例，并将其传递给第二个构造函数。</span><span class="sxs-lookup"><span data-stu-id="49351-240">This constructor creates an instance of the MovieRepository class and passes it to the second constructor.</span></span>

<span data-ttu-id="49351-241">第二个构造函数具有单个参数： IMovieRepository 参数。</span><span class="sxs-lookup"><span data-stu-id="49351-241">The second constructor has a single parameter: an IMovieRepository parameter.</span></span> <span data-ttu-id="49351-242">此构造函数只需将参数的值分配给名为的类级字段\_存储库。</span><span class="sxs-lookup"><span data-stu-id="49351-242">This constructor simply assigns the value of the parameter to a class-level field named \_repository.</span></span>

<span data-ttu-id="49351-243">MoviesController 类正在调用的依赖关系注入模式软件设计模式的优点。</span><span class="sxs-lookup"><span data-stu-id="49351-243">The MoviesController class is taking advantage of a software design pattern called the Dependency Injection pattern.</span></span> <span data-ttu-id="49351-244">具体而言，它使用调用构造函数依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="49351-244">In particular, it is using something called Constructor Dependency Injection.</span></span> <span data-ttu-id="49351-245">你可以阅读更多有关通过阅读以下文章 Martin Fowler 通过此模式：</span><span class="sxs-lookup"><span data-stu-id="49351-245">You can read more about this pattern by reading the following article by Martin Fowler:</span></span>

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

<span data-ttu-id="49351-246">请注意，所有 MoviesController 类 （不包括第一个构造函数） 中的代码与 IMovieRepository 接口交互而不是实际的 MovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="49351-246">Notice that all of the code in the MoviesController class (with the exception of the first constructor) interacts with the IMovieRepository interface instead of the actual MovieRepository class.</span></span> <span data-ttu-id="49351-247">代码而不是该接口的具体实现的抽象接口与交互。</span><span class="sxs-lookup"><span data-stu-id="49351-247">The code interacts with an abstract interface instead of a concrete implementation of the interface.</span></span>

<span data-ttu-id="49351-248">如果你想要修改应用程序使用的数据访问技术然后可以只需实现使用备用数据库访问技术的类具有的 IMovieRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="49351-248">If you want to modify the data access technology used by the application then you can simply implement the IMovieRepository interface with a class that uses the alternative database access technology.</span></span> <span data-ttu-id="49351-249">例如，你可以创建 EntityFrameworkMovieRepository 类或 SubSonicMovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="49351-249">For example, you could create an EntityFrameworkMovieRepository class or a SubSonicMovieRepository class.</span></span> <span data-ttu-id="49351-250">因为控制器类针对接口进行编程，你可以将 IMovieRepository 的新实现传递给控制器类和类将继续工作。</span><span class="sxs-lookup"><span data-stu-id="49351-250">Because the controller class is programmed against the interface, you can pass a new implementation of IMovieRepository to the controller class and the class would continue to work.</span></span>

<span data-ttu-id="49351-251">此外，如果你想要测试 MoviesController 类，则可以为 MoviesController 传递一个假电影存储库类。</span><span class="sxs-lookup"><span data-stu-id="49351-251">Furthermore, if you want to test the MoviesController class, then you can pass a fake movie repository class to the MoviesController.</span></span> <span data-ttu-id="49351-252">你可以实现与不会实际访问数据库，但包含所有 IMovieRepository 接口所需方法的类的 IMovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="49351-252">You can implement the IMovieRepository class with a class that does not actually access the database but contains all of the required methods of the IMovieRepository interface.</span></span> <span data-ttu-id="49351-253">这样一来，你可以无需实际访问实际数据库单元测试 MoviesController 类。</span><span class="sxs-lookup"><span data-stu-id="49351-253">That way, you can unit test the MoviesController class without actually accessing a real database.</span></span>

## <a name="summary"></a><span data-ttu-id="49351-254">总结</span><span class="sxs-lookup"><span data-stu-id="49351-254">Summary</span></span>

<span data-ttu-id="49351-255">本教程的目标是演示如何利用 Microsoft LINQ to SQL 来创建 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="49351-255">The goal of this tutorial was to demonstrate how you can create MVC model classes by taking advantage of Microsoft LINQ to SQL.</span></span> <span data-ttu-id="49351-256">有关 ASP.NET MVC 应用程序中显示数据库数据的两种策略，我们探讨。</span><span class="sxs-lookup"><span data-stu-id="49351-256">We examined two strategies for displaying database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="49351-257">首先，我们创建 LINQ to SQL 类，并使用直接中的控制器操作的类。</span><span class="sxs-lookup"><span data-stu-id="49351-257">First, we created LINQ to SQL classes and used the classes directly within a controller action.</span></span> <span data-ttu-id="49351-258">使用 LINQ to SQL 类控制器中，您可以快速并轻松地在 MVC 应用程序中显示数据库数据。</span><span class="sxs-lookup"><span data-stu-id="49351-258">Using LINQ to SQL classes within a controller enables you to quickly and easily display database data in an MVC application.</span></span>

<span data-ttu-id="49351-259">接下来，我们探讨了显示数据库数据的稍微有些困难，但肯定更良性的路径。</span><span class="sxs-lookup"><span data-stu-id="49351-259">Next, we explored a slightly more difficult, but definitely more virtuous, path for displaying database data.</span></span> <span data-ttu-id="49351-260">我们采用存储库模式的优点，并放在单独的存储库类中的所有我们数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="49351-260">We took advantage of the Repository pattern and placed all of our database access logic in a separate repository class.</span></span> <span data-ttu-id="49351-261">在我们控制器中，我们已写入所有我们针对而不是具体的类接口的代码。</span><span class="sxs-lookup"><span data-stu-id="49351-261">In our controller, we wrote all of our code against an interface instead of a concrete class.</span></span> <span data-ttu-id="49351-262">存储库模式的优点是，它使我们能够轻松地在将来更改数据库访问技术，并且它允许我们能够轻松地测试我们控制器类。</span><span class="sxs-lookup"><span data-stu-id="49351-262">The advantage of the Repository pattern is that it enables us to easily change database access technologies in the future and it enables us to easily test our controller classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="49351-263">[上一页](creating-model-classes-with-the-entity-framework-vb.md)
> [下一页](displaying-a-table-of-database-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="49351-263">[Previous](creating-model-classes-with-the-entity-framework-vb.md)
[Next](displaying-a-table-of-database-data-vb.md)</span></span>
