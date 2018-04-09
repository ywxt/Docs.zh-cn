---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (10 的第 8) 中实现继承，并使用实体框架 |Microsoft 文档
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: ee088f841bdb68f4806b0b62be7d379b9eab9f8c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="bebf4-103">在 ASP.NET MVC 应用程序 (10 的第 8) 实现与实体框架的继承</span><span class="sxs-lookup"><span data-stu-id="bebf4-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>
====================
<span data-ttu-id="bebf4-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bebf4-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="bebf4-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="bebf4-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="bebf4-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bebf4-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="bebf4-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="bebf4-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="bebf4-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="bebf4-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="bebf4-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="bebf4-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="bebf4-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="bebf4-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="bebf4-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="bebf4-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="bebf4-112">在前面的教程中，你将处理并发异常。</span><span class="sxs-lookup"><span data-stu-id="bebf4-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="bebf4-113">本教程将演示如何在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="bebf4-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="bebf4-114">在面向对象编程中，你可以使用继承以消除冗余代码。</span><span class="sxs-lookup"><span data-stu-id="bebf4-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="bebf4-115">在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。</span><span class="sxs-lookup"><span data-stu-id="bebf4-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="bebf4-116">不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。</span><span class="sxs-lookup"><span data-stu-id="bebf4-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="bebf4-117">每个-层次结构一个表与每种类型一个表继承</span><span class="sxs-lookup"><span data-stu-id="bebf4-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="bebf4-118">在面向对象编程中，你可以使用继承以使其更轻松地使用相关的类。</span><span class="sxs-lookup"><span data-stu-id="bebf4-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="bebf4-119">例如，`Instructor`和`Student`中的类`School`数据模型共享多个属性，这将导致冗余代码：</span><span class="sxs-lookup"><span data-stu-id="bebf4-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="bebf4-121">假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。</span><span class="sxs-lookup"><span data-stu-id="bebf4-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="bebf4-122">你可以创建`Person`基类其中仅包含那些共享属性，然后进行`Instructor`和`Student`实体继承自该基类，如下面的插图中所示：</span><span class="sxs-lookup"><span data-stu-id="bebf4-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="bebf4-124">有多种方法可以在数据库中表示此继承结构。</span><span class="sxs-lookup"><span data-stu-id="bebf4-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="bebf4-125">您可以对`Person`包括有关学生和教师单个表中的信息的表。</span><span class="sxs-lookup"><span data-stu-id="bebf4-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="bebf4-126">某些列可能仅适用于教师 (`HireDate`)，某些仅向学生 (`EnrollmentDate`)、 某些对这两个 (`LastName`， `FirstName`)。</span><span class="sxs-lookup"><span data-stu-id="bebf4-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="bebf4-127">通常，您将需要*鉴别器*指示哪种类型的每一行的列表示。</span><span class="sxs-lookup"><span data-stu-id="bebf4-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="bebf4-128">例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。</span><span class="sxs-lookup"><span data-stu-id="bebf4-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Table-per-hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="bebf4-130">从单个数据库表生成的实体继承结构的此模式称为*表每个层次结构*(TPH) 继承。</span><span class="sxs-lookup"><span data-stu-id="bebf4-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="bebf4-131">另一种方法是使数据库看起来更像继承结构。</span><span class="sxs-lookup"><span data-stu-id="bebf4-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="bebf4-132">例如，您可以对只有名称字段`Person`表，并具有单独`Instructor`和`Student`具有日期字段的表。</span><span class="sxs-lookup"><span data-stu-id="bebf4-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="bebf4-134">此模式的数据库表，针对每个实体类称为进行*每种类型的表*(TPT) 继承。</span><span class="sxs-lookup"><span data-stu-id="bebf4-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="bebf4-135">TPH 继承模式通常因为 TPT 模式可能会导致复杂的联接查询在实体框架中比 TPT 继承模式提供更好的性能。</span><span class="sxs-lookup"><span data-stu-id="bebf4-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="bebf4-136">本教程将演示如何实现 TPH 继承。</span><span class="sxs-lookup"><span data-stu-id="bebf4-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="bebf4-137">将执行以下步骤来执行该操作：</span><span class="sxs-lookup"><span data-stu-id="bebf4-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="bebf4-138">创建`Person`类并更改`Instructor`和`Student`类派生自`Person`。</span><span class="sxs-lookup"><span data-stu-id="bebf4-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="bebf4-139">将模型数据库映射代码添加到数据库上下文类。</span><span class="sxs-lookup"><span data-stu-id="bebf4-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="bebf4-140">更改`InstructorID`和`StudentID`在整个到项目的引用`PersonID`。</span><span class="sxs-lookup"><span data-stu-id="bebf4-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="bebf4-141">创建 Person 类</span><span class="sxs-lookup"><span data-stu-id="bebf4-141">Creating the Person Class</span></span>

 <span data-ttu-id="bebf4-142">注意： 你将无法将项目编译后更新使用这些类的控制器前创建下面的类。</span><span class="sxs-lookup"><span data-stu-id="bebf4-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="bebf4-143">在*模型*文件夹中，创建*Person.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bebf4-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="bebf4-144">在*Instructor.cs*，派生`Instructor`类`Person`类和删除密钥和名称字段。</span><span class="sxs-lookup"><span data-stu-id="bebf4-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="bebf4-145">代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="bebf4-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="bebf4-146">进行类似更改到*Student.cs*。</span><span class="sxs-lookup"><span data-stu-id="bebf4-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="bebf4-147">`Student`类将类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="bebf4-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="bebf4-148">添加到模型的 Person 实体类型</span><span class="sxs-lookup"><span data-stu-id="bebf4-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="bebf4-149">在*SchoolContext.cs*，添加`DbSet`属性`Person`实体类型：</span><span class="sxs-lookup"><span data-stu-id="bebf4-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="bebf4-150">以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。</span><span class="sxs-lookup"><span data-stu-id="bebf4-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="bebf4-151">当你将看到的当数据库可重新创建，它将具有`Person`表代替了`Student`和`Instructor`表。</span><span class="sxs-lookup"><span data-stu-id="bebf4-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="bebf4-152">分别更改为 PersonID InstructorID 和 StudentID</span><span class="sxs-lookup"><span data-stu-id="bebf4-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="bebf4-153">在*SchoolContext.cs*，在教师课程映射语句中，更改`MapRightKey("InstructorID")`到`MapRightKey("PersonID")`:</span><span class="sxs-lookup"><span data-stu-id="bebf4-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="bebf4-154">此更改不是必需的;它仅更改多对多联接表中的 InstructorID 列的名称。</span><span class="sxs-lookup"><span data-stu-id="bebf4-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="bebf4-155">如果保留 InstructorID 形式的名称，则应用程序将仍能正常工作。</span><span class="sxs-lookup"><span data-stu-id="bebf4-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="bebf4-156">此处是完成*SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="bebf4-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="bebf4-157">接下来，你需要更改`InstructorID`到`PersonID`和`StudentID`到`PersonID`在整个项目***除***中的带时间戳迁移文件*迁移*文件夹。</span><span class="sxs-lookup"><span data-stu-id="bebf4-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="bebf4-158">若要执行该操作将查找和打开仅的文件，需要更改，然后在打开的文件上执行全局更改。</span><span class="sxs-lookup"><span data-stu-id="bebf4-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="bebf4-159">中的唯一文件*迁移*应更改的文件夹是*Migrations\Configuration.cs。*</span><span class="sxs-lookup"><span data-stu-id="bebf4-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="bebf4-160">开始关闭 Visual Studio 中所有打开的文件。</span><span class="sxs-lookup"><span data-stu-id="bebf4-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="bebf4-161">单击**查找和替换--查找所有文件**中**编辑**菜单上，，然后搜索的项目中包含的所有文件`InstructorID`。</span><span class="sxs-lookup"><span data-stu-id="bebf4-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="bebf4-162">打开中的每个文件**查找结果**窗口***除***&lt;时间戳&gt;*\_.cs* 中的迁移文件*迁移*文件夹中，通过双击每个文件的一行。</span><span class="sxs-lookup"><span data-stu-id="bebf4-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="bebf4-163">打开**在文件中替换**对话框和更改**查找**到**所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="bebf4-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="bebf4-164">使用**在文件中替换**对话框以更改所有`InstructorID`到 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="bebf4-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="bebf4-165">找到包含项目中的所有文件`StudentID`。</span><span class="sxs-lookup"><span data-stu-id="bebf4-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="bebf4-166">打开中的每个文件**查找结果**窗口***除***&lt;时间戳&gt;*\_\*.cs*迁移文件在*迁移*文件夹中，通过双击每个文件的一行。</span><span class="sxs-lookup"><span data-stu-id="bebf4-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="bebf4-167">打开**在文件中替换**对话框和更改**查找**到**所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="bebf4-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="bebf4-168">使用**在文件中替换**对话框以更改所有`StudentID`到`PersonID`。</span><span class="sxs-lookup"><span data-stu-id="bebf4-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="bebf4-169">生成项目。</span><span class="sxs-lookup"><span data-stu-id="bebf4-169">Build the project.</span></span>

<span data-ttu-id="bebf4-170">(请注意，此示例演示*缺点*的`classnameID`命名主键的模式。</span><span class="sxs-lookup"><span data-stu-id="bebf4-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="bebf4-171">如果你命名一样主键 ID，而无需前缀的类名称，*没有*重命名需要现在。)</span><span class="sxs-lookup"><span data-stu-id="bebf4-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="bebf4-172">创建和更新迁移文件</span><span class="sxs-lookup"><span data-stu-id="bebf4-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="bebf4-173">在包管理器控制台 (PMC) 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="bebf4-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="bebf4-174">运行`Update-Database`PMC 命令。</span><span class="sxs-lookup"><span data-stu-id="bebf4-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="bebf4-175">由于我们有迁移不知道如何处理的现有数据，该命令将在此时失败。</span><span class="sxs-lookup"><span data-stu-id="bebf4-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="bebf4-176">你收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="bebf4-176">You get the following error:</span></span>

<span data-ttu-id="bebf4-177">*ALTER TABLE 语句与外键约束冲突"FK\_dbo。部门\_dbo。人员\_PersonID"。冲突发生于数据库"ContosoUniversity"表"dbo。Person"，列 PersonID。*</span><span class="sxs-lookup"><span data-stu-id="bebf4-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="bebf4-178">打开*迁移\&lt; 时间戳&gt;\_Inheritance.cs*和替换`Up`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bebf4-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="bebf4-179">运行`update-database`试命令。</span><span class="sxs-lookup"><span data-stu-id="bebf4-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="bebf4-180">很可能会迁移数据和进行架构更改时获得其他错误。</span><span class="sxs-lookup"><span data-stu-id="bebf4-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="bebf4-181">如果您迁移错误无法解决，可以通过更改中的连接字符串来继续本教程*Web.config*文件或删除数据库。</span><span class="sxs-lookup"><span data-stu-id="bebf4-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="bebf4-182">最简单方法是在数据库重命名*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="bebf4-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="bebf4-183">例如，将数据库名称更改为 CU\_测试下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="bebf4-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="bebf4-184">与新数据库，没有数据迁移，和`update-database`命令是更可能完成且未发生错误。</span><span class="sxs-lookup"><span data-stu-id="bebf4-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="bebf4-185">有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="bebf4-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="bebf4-186">如果你接受这种方法，以继续本教程，请跳过部署步骤在本教程中，末尾因为已部署的站点将获取相同的错误，它自动运行迁移时。</span><span class="sxs-lookup"><span data-stu-id="bebf4-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="bebf4-187">如果你想要迁移错误的排查，最佳资源是实体框架论坛或 StackOverflow.com 之一。</span><span class="sxs-lookup"><span data-stu-id="bebf4-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>


## <a name="testing"></a><span data-ttu-id="bebf4-188">正在测试</span><span class="sxs-lookup"><span data-stu-id="bebf4-188">Testing</span></span>

<span data-ttu-id="bebf4-189">运行站点并尝试各种页面。</span><span class="sxs-lookup"><span data-stu-id="bebf4-189">Run the site and try various pages.</span></span> <span data-ttu-id="bebf4-190">一切都和以前一样。</span><span class="sxs-lookup"><span data-stu-id="bebf4-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="bebf4-191">在**服务器资源管理器，**展开**SchoolContext**然后**表**，和你看到**学生**和**教师**已替换为表**人员**表。</span><span class="sxs-lookup"><span data-stu-id="bebf4-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="bebf4-192">展开**人员**表，你会看到它具有所有使用中的列**学生**和**教师**表。</span><span class="sxs-lookup"><span data-stu-id="bebf4-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="bebf4-194">右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。</span><span class="sxs-lookup"><span data-stu-id="bebf4-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="bebf4-195">下图说明了新的 School 数据库的结构：</span><span class="sxs-lookup"><span data-stu-id="bebf4-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="bebf4-197">总结</span><span class="sxs-lookup"><span data-stu-id="bebf4-197">Summary</span></span>

<span data-ttu-id="bebf4-198">每个层次结构一个表继承现在已实现的`Person`， `Student`，和`Instructor`类。</span><span class="sxs-lookup"><span data-stu-id="bebf4-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="bebf4-199">有关此设置和其他的继承结构的详细信息，请参阅[继承映射策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)Morteza Manavi 博客上。</span><span class="sxs-lookup"><span data-stu-id="bebf4-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="bebf4-200">在下一教程中，你将看到一些方式来实现的存储库和单元的工作模式。</span><span class="sxs-lookup"><span data-stu-id="bebf4-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="bebf4-201">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="bebf4-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bebf4-202">[上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="bebf4-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
