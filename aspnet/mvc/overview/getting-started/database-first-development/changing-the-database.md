---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 首先使用 ASP.NET MVC 的 EF 数据库： 更改数据库 |Microsoft 文档
author: tfitzmac
description: 使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 63ee8768a43dbdac80922e3adbedd3378c10da73
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879317"
---
<a name="ef-database-first-with-aspnet-mvc-changing-the-database"></a><span data-ttu-id="dc1ac-104">首先使用 ASP.NET MVC 的 EF 数据库： 更改数据库</span><span class="sxs-lookup"><span data-stu-id="dc1ac-104">EF Database First with ASP.NET MVC: Changing the Database</span></span>
====================
<span data-ttu-id="dc1ac-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dc1ac-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dc1ac-106">使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="dc1ac-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="dc1ac-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="dc1ac-109">此系列的一部分的重点介绍对数据库结构进行更新和传播在整个 web 应用程序所做的更改。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-109">This part of the series focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>


## <a name="add-a-column"></a><span data-ttu-id="dc1ac-110">添加列</span><span class="sxs-lookup"><span data-stu-id="dc1ac-110">Add a column</span></span>

<span data-ttu-id="dc1ac-111">如果你的数据库中更新表的结构，你需要确保所做的更改将传播到数据模型、 视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-111">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="dc1ac-112">对于本教程中，你将在要记录学生的名字的学生表中添加新列。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-112">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="dc1ac-113">若要添加此列，打开数据库项目中，并打开 Student.sql 文件。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-113">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="dc1ac-114">通过在设计器或 T-SQL 代码中，添加一个名为列**MiddleName** NVARCHAR(50) 并允许 NULL 值。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-114">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

![添加中间名](changing-the-database/_static/image1.png)

<span data-ttu-id="dc1ac-116">将此更改部署到您的本地数据库中，通过启动您的数据库项目 （或 F5）。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-116">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="dc1ac-117">新字段添加到表中。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-117">The new field is added to the table.</span></span> <span data-ttu-id="dc1ac-118">如果在 SQL Server 对象资源管理器中未看到它，请单击窗格中的刷新按钮。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-118">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![显示新的列](changing-the-database/_static/image2.png)

<span data-ttu-id="dc1ac-120">新的列存在于数据库表中，但它当前不存在的数据模型类中。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-120">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="dc1ac-121">你必须更新以包括新列的模型。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-121">You must update the model to include your new column.</span></span> <span data-ttu-id="dc1ac-122">在**模型**文件夹中，打开**ContosoModel.edmx**显示模型关系图文件。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-122">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="dc1ac-123">请注意，学生模型不包含 MiddleName 属性。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-123">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="dc1ac-124">右键单击设计图面上的任意位置，然后选择**从数据库更新模型**。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-124">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

![更新模型](changing-the-database/_static/image3.png)

<span data-ttu-id="dc1ac-126">在更新向导中，选择**刷新**选项卡和**学生**表。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-126">In the Update Wizard, select the **Refresh** tab and the **Student** table.</span></span>

![更新向导](changing-the-database/_static/image4.png)

<span data-ttu-id="dc1ac-128">单击 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-128">Click **Finish**.</span></span>

<span data-ttu-id="dc1ac-129">更新过程完成后，数据库关系图包括新**MiddleName**属性。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="dc1ac-130">保存**ContosoModel.edmx**文件。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="dc1ac-131">你必须将此文件保存为新的属性传播到**Student.cs**类。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="dc1ac-132">您现在已更新数据库和模型。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="dc1ac-133">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-133">Build the solution.</span></span>

<span data-ttu-id="dc1ac-134">遗憾的是，视图仍会包含新属性。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-134">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="dc1ac-135">要更新视图有两个选项-你可以重新生成这些视图通过再次添加基架学生类，或者可以手动向现有视图添加新属性。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-135">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="dc1ac-136">在本教程中，你将添加基架再次因为你不进行了任何自定义的更改到自动生成视图。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-136">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="dc1ac-137">你可以考虑手动将属性添加到视图中进行了更改并不希望丢失这些更改时。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-137">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="dc1ac-138">若要确保视图是重新创建，删除**学生**下的文件夹**视图**，并删除**StudentsController**。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-138">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="dc1ac-139">然后，右键单击**控制器**文件夹和将基架添加**学生**模型。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-139">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="dc1ac-140">同样，控制器命名**StudentsController**。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-140">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="dc1ac-141">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-141">Select **OK**.</span></span>

<span data-ttu-id="dc1ac-142">视图现在包含 MiddleName 属性。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-142">The views now contain the MiddleName property.</span></span>

![显示中间名](changing-the-database/_static/image5.png)

<span data-ttu-id="dc1ac-144">在下一步的部分中，将添加代码以自定义视图的显示有关学生记录的详细信息。</span><span class="sxs-lookup"><span data-stu-id="dc1ac-144">In the next section, you will add code to customize the view for showing details about a student record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dc1ac-145">[上一页](generating-views.md)
> [下一页](customizing-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="dc1ac-145">[Previous](generating-views.md)
[Next](customizing-a-view.md)</span></span>
