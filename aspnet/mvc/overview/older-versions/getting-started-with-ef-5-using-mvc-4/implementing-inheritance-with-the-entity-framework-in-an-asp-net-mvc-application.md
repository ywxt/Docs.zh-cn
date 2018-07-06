---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (8 为 10) 中实现与实体框架的继承 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b39fc609007d437dd0845f9087dd5a32272cebe9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821271"
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="46c95-103">在 ASP.NET MVC 应用程序 (8 为 10) 中实现继承，使用实体框架</span><span class="sxs-lookup"><span data-stu-id="46c95-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>
====================
<span data-ttu-id="46c95-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="46c95-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="46c95-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="46c95-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="46c95-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="46c95-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="46c95-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="46c95-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="46c95-108">您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。</span><span class="sxs-lookup"><span data-stu-id="46c95-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="46c95-109">如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="46c95-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="46c95-110">通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="46c95-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="46c95-111">一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="46c95-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="46c95-112">在上一教程中，你将处理并发异常。</span><span class="sxs-lookup"><span data-stu-id="46c95-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="46c95-113">本教程将演示如何在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="46c95-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="46c95-114">在面向对象的编程中，可以使用继承来消除冗余代码。</span><span class="sxs-lookup"><span data-stu-id="46c95-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="46c95-115">在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。</span><span class="sxs-lookup"><span data-stu-id="46c95-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="46c95-116">不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。</span><span class="sxs-lookup"><span data-stu-id="46c95-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="46c95-117">每个-层次结构一个表与每个类型一个表继承</span><span class="sxs-lookup"><span data-stu-id="46c95-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="46c95-118">在面向对象的编程中，可以使用继承以便更轻松地使用相关的类。</span><span class="sxs-lookup"><span data-stu-id="46c95-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="46c95-119">例如，`Instructor`并`Student`中的类`School`数据模型共享多个属性，这会导致冗余代码：</span><span class="sxs-lookup"><span data-stu-id="46c95-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="46c95-121">假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。</span><span class="sxs-lookup"><span data-stu-id="46c95-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="46c95-122">您可以创建`Person`基类其中只包含这些共享属性，请`Instructor`和`Student`实体继承自该基类，如以下插图所示：</span><span class="sxs-lookup"><span data-stu-id="46c95-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="46c95-124">有多种方法可以在数据库中表示此继承结构。</span><span class="sxs-lookup"><span data-stu-id="46c95-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="46c95-125">您可以`Person`包括有关学生和教师单个表中的信息的表。</span><span class="sxs-lookup"><span data-stu-id="46c95-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="46c95-126">某些列可能仅适用于教师 (`HireDate`)，一些仅面向学生 (`EnrollmentDate`)、 一些对这两个 (`LastName`， `FirstName`)。</span><span class="sxs-lookup"><span data-stu-id="46c95-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="46c95-127">通常情况下，您必须*鉴别器*指示哪种类型的每一行的列表示。</span><span class="sxs-lookup"><span data-stu-id="46c95-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="46c95-128">例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。</span><span class="sxs-lookup"><span data-stu-id="46c95-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![每个 hierarchy_example 表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="46c95-130">从单个数据库表生成实体继承结构的此模式称为*每个层次结构一个表*(TPH) 继承。</span><span class="sxs-lookup"><span data-stu-id="46c95-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="46c95-131">另一种方法是使数据库看起来更像继承结构。</span><span class="sxs-lookup"><span data-stu-id="46c95-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="46c95-132">例如，您可以仅将姓名字段`Person`表，并具有单独`Instructor`和`Student`具有日期字段的表。</span><span class="sxs-lookup"><span data-stu-id="46c95-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="46c95-134">此模式的数据库表，针对每个实体的类称为进行*每种类型的表*(TPT) 继承。</span><span class="sxs-lookup"><span data-stu-id="46c95-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="46c95-135">TPH 继承模式通常比 TPT 继承模式，实体框架中提供更好的性能因为 TPT 模式会导致复杂的联接查询。</span><span class="sxs-lookup"><span data-stu-id="46c95-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="46c95-136">本教程将演示如何实现 TPH 继承。</span><span class="sxs-lookup"><span data-stu-id="46c95-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="46c95-137">你将执行的操作，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="46c95-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="46c95-138">创建`Person`类，并更改`Instructor`并`Student`类继承`Person`。</span><span class="sxs-lookup"><span data-stu-id="46c95-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="46c95-139">将模型数据库的映射代码添加到数据库上下文类。</span><span class="sxs-lookup"><span data-stu-id="46c95-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="46c95-140">更改`InstructorID`并`StudentID`整个到项目引用`PersonID`。</span><span class="sxs-lookup"><span data-stu-id="46c95-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="46c95-141">创建 Person 类</span><span class="sxs-lookup"><span data-stu-id="46c95-141">Creating the Person Class</span></span>

 <span data-ttu-id="46c95-142">注意： 你将无法创建下面的类，直到更新使用这些类的控制器后编译项目。</span><span class="sxs-lookup"><span data-stu-id="46c95-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="46c95-143">在中*模型*文件夹中，创建*Person.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="46c95-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="46c95-144">在中*Instructor.cs*，派生`Instructor`类`Person`类，并删除键和姓名字段。</span><span class="sxs-lookup"><span data-stu-id="46c95-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="46c95-145">代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="46c95-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="46c95-146">进行到类似的更改*Student.cs*。</span><span class="sxs-lookup"><span data-stu-id="46c95-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="46c95-147">`Student`类看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="46c95-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="46c95-148">将 Person 实体类型添加到模型</span><span class="sxs-lookup"><span data-stu-id="46c95-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="46c95-149">在中*SchoolContext.cs*，添加`DbSet`属性`Person`实体类型：</span><span class="sxs-lookup"><span data-stu-id="46c95-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="46c95-150">以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。</span><span class="sxs-lookup"><span data-stu-id="46c95-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="46c95-151">当您将看到，当数据库是重新创建，它将具有`Person`表来代替`Student`和`Instructor`表。</span><span class="sxs-lookup"><span data-stu-id="46c95-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="46c95-152">更改为 PersonID InstructorID 和 StudentID</span><span class="sxs-lookup"><span data-stu-id="46c95-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="46c95-153">在中*SchoolContext.cs*，在讲师-课程映射语句中，更改`MapRightKey("InstructorID")`到`MapRightKey("PersonID")`:</span><span class="sxs-lookup"><span data-stu-id="46c95-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="46c95-154">此更改不是必需的;它仅更改在多对多联接表中的 InstructorID 列的名称。</span><span class="sxs-lookup"><span data-stu-id="46c95-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="46c95-155">如果保留 InstructorID 作为名称，该应用程序将仍正常工作。</span><span class="sxs-lookup"><span data-stu-id="46c95-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="46c95-156">下面是已完成*SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="46c95-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="46c95-157">接下来你需要更改`InstructorID`到`PersonID`并`StudentID`到`PersonID`在整个项目***除***加盖时间戳迁移文件中*迁移*文件夹。</span><span class="sxs-lookup"><span data-stu-id="46c95-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="46c95-158">若要执行此操作将查找和打开文件，需要进行更改，然后在打开的文件上执行全局更改。</span><span class="sxs-lookup"><span data-stu-id="46c95-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="46c95-159">中唯一的文件*迁移*应更改的文件夹是*migrations\ configuration.cs。*</span><span class="sxs-lookup"><span data-stu-id="46c95-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="46c95-160">首先关闭 Visual Studio 中所有打开的文件。</span><span class="sxs-lookup"><span data-stu-id="46c95-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="46c95-161">单击**查找和替换--的所有文件**中**编辑**菜单中，并在项目中包含的所有文件然后搜索`InstructorID`。</span><span class="sxs-lookup"><span data-stu-id="46c95-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="46c95-162">打开每个文件中的**查找结果**窗口***除***&lt;时间戳&gt;*\_.cs* 中的迁移文件*迁移*文件夹中，通过双击每个文件的一行。</span><span class="sxs-lookup"><span data-stu-id="46c95-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="46c95-163">打开**在文件中替换**对话框，并更改**查找**到**所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="46c95-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="46c95-164">使用**在文件中替换**对话框，可以更改所有`InstructorID`到 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="46c95-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="46c95-165">包含在项目中找到的所有文件`StudentID`。</span><span class="sxs-lookup"><span data-stu-id="46c95-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="46c95-166">打开每个文件中的**查找结果**窗口***除***&lt;时间戳&gt;*\_\*.cs*迁移文件在中*迁移*文件夹中，通过双击每个文件的一行。</span><span class="sxs-lookup"><span data-stu-id="46c95-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="46c95-167">打开**在文件中替换**对话框，并更改**查找**到**所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="46c95-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="46c95-168">使用**在文件中替换**对话框，可以更改所有`StudentID`到`PersonID`。</span><span class="sxs-lookup"><span data-stu-id="46c95-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="46c95-169">生成项目。</span><span class="sxs-lookup"><span data-stu-id="46c95-169">Build the project.</span></span>

<span data-ttu-id="46c95-170">(请注意，此示例演示*缺点*的`classnameID`命名主键的模式。</span><span class="sxs-lookup"><span data-stu-id="46c95-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="46c95-171">如果不前缀的类名称，命名主键 ID*没有*重命名需要现在。)</span><span class="sxs-lookup"><span data-stu-id="46c95-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="46c95-172">创建和更新的迁移文件</span><span class="sxs-lookup"><span data-stu-id="46c95-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="46c95-173">在包管理器控制台 (PMC) 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="46c95-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="46c95-174">运行`Update-Database`PMC 命令。</span><span class="sxs-lookup"><span data-stu-id="46c95-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="46c95-175">该命令将在这里失败，因为我们已将迁移并不知道如何处理的现有数据。</span><span class="sxs-lookup"><span data-stu-id="46c95-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="46c95-176">你收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="46c95-176">You get the following error:</span></span>

<span data-ttu-id="46c95-177">*ALTER TABLE 语句与 FOREIGN KEY 约束冲突"FK\_dbo。部门\_dbo。人员\_PersonID"。冲突发生于数据库"ContosoUniversity"表"dbo。Person"，列 PersonID。*</span><span class="sxs-lookup"><span data-stu-id="46c95-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="46c95-178">打开*迁移\&l t; 时间戳&gt;\_Inheritance.cs* ，并将为`Up`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="46c95-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="46c95-179">运行`update-database`试命令。</span><span class="sxs-lookup"><span data-stu-id="46c95-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="46c95-180">就可以将迁移数据，也使架构更改时遇到其他错误。</span><span class="sxs-lookup"><span data-stu-id="46c95-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="46c95-181">如果获取的迁移错误则不能解决，可以通过更改中的连接字符串来继续本教程*Web.config*文件或删除的数据库。</span><span class="sxs-lookup"><span data-stu-id="46c95-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="46c95-182">最简单方法是在数据库重命名*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="46c95-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="46c95-183">例如，将数据库名称更改为 CU\_测试，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="46c95-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="46c95-184">使用新数据库没有数据迁移，和`update-database`命令是更有望完成且未出错。</span><span class="sxs-lookup"><span data-stu-id="46c95-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="46c95-185">有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="46c95-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="46c95-186">如果你接受这种方法，以继续本教程，跳过部署步骤放在结束本教程中，由于已部署的站点会产生相同的错误，它会自动运行迁移时。</span><span class="sxs-lookup"><span data-stu-id="46c95-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="46c95-187">如果你想要解决的迁移错误，最佳资源是 Entity Framework 论坛或 StackOverflow.com 之一。</span><span class="sxs-lookup"><span data-stu-id="46c95-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>


## <a name="testing"></a><span data-ttu-id="46c95-188">正在测试</span><span class="sxs-lookup"><span data-stu-id="46c95-188">Testing</span></span>

<span data-ttu-id="46c95-189">运行站点，并尝试各种页面。</span><span class="sxs-lookup"><span data-stu-id="46c95-189">Run the site and try various pages.</span></span> <span data-ttu-id="46c95-190">一切都和以前一样。</span><span class="sxs-lookup"><span data-stu-id="46c95-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="46c95-191">中**服务器资源管理器**展开**SchoolContext** ，然后**表**，并可以看到**学生**和**讲师**已替换为表**人员**表。</span><span class="sxs-lookup"><span data-stu-id="46c95-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="46c95-192">展开**Person**表，会看到它具有所有使用中的列**学生**并**讲师**表。</span><span class="sxs-lookup"><span data-stu-id="46c95-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="46c95-194">右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。</span><span class="sxs-lookup"><span data-stu-id="46c95-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="46c95-195">下图说明了新的 School 数据库的结构：</span><span class="sxs-lookup"><span data-stu-id="46c95-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="46c95-197">总结</span><span class="sxs-lookup"><span data-stu-id="46c95-197">Summary</span></span>

<span data-ttu-id="46c95-198">现在为实现每个层次结构一个表继承`Person`， `Student`，和`Instructor`类。</span><span class="sxs-lookup"><span data-stu-id="46c95-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="46c95-199">有关此设置和其他继承结构的详细信息，请参阅[继承映射策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)Morteza Manavi 博客上。</span><span class="sxs-lookup"><span data-stu-id="46c95-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="46c95-200">在下一教程中，您将看到一些方法来实现存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="46c95-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="46c95-201">其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="46c95-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="46c95-202">[上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="46c95-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
