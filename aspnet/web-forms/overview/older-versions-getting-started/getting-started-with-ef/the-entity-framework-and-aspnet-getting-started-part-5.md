---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 5 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: b175bb8d6edb8b59c14da59f4576e9029e663dde
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835254"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="09490-104">Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 5 部分</span><span class="sxs-lookup"><span data-stu-id="09490-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>
====================
<span data-ttu-id="09490-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="09490-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="09490-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="09490-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="09490-107">有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="09490-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data-continued"></a><span data-ttu-id="09490-108">使用相关数据，继续执行</span><span class="sxs-lookup"><span data-stu-id="09490-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="09490-109">开始使用上一教程中`EntityDataSource`控件能够使用相关数据。</span><span class="sxs-lookup"><span data-stu-id="09490-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="09490-110">显示多个级别的层次结构和编辑导航属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="09490-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="09490-111">在本教程中将继续使用相关数据，通过添加和删除关系以及添加新实体具有与现有实体的关系。</span><span class="sxs-lookup"><span data-stu-id="09490-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="09490-112">你将创建页添加课程分配给部门。</span><span class="sxs-lookup"><span data-stu-id="09490-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="09490-113">部门已经存在，并且在创建新的课程，同时你将建立它与现有院系之间的关系。</span><span class="sxs-lookup"><span data-stu-id="09490-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="09490-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="09490-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="09490-115">你还将创建适用于多对多关系通过将一名讲师分配给一门课程 （添加您选择的两个实体之间的关系） 的页面或从一门课程中删除一名讲师 (删除两个实体之间的关系，您选择）。</span><span class="sxs-lookup"><span data-stu-id="09490-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="09490-116">在数据库中，添加一名讲师和课程之间的关系会导致新行添加到`CourseInstructor`关联表; 中删除关系涉及删除行从`CourseInstructor`关联表。</span><span class="sxs-lookup"><span data-stu-id="09490-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="09490-117">但是，您执行此操作在实体框架中通过参考的情况下设置导航属性`CourseInstructor`显式表。</span><span class="sxs-lookup"><span data-stu-id="09490-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="09490-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="09490-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="09490-119">将具有关系的实体添加到现有实体</span><span class="sxs-lookup"><span data-stu-id="09490-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="09490-120">创建一个名为的新 web 页*CoursesAdd.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:</span><span class="sxs-lookup"><span data-stu-id="09490-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="09490-121">此标记创建`EntityDataSource`选择课程，这样的插入，并且指定的的控件的处理程序`Inserting`事件。</span><span class="sxs-lookup"><span data-stu-id="09490-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="09490-122">将使用该处理程序来更新`Department`导航属性时的新`Course`创建实体。</span><span class="sxs-lookup"><span data-stu-id="09490-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="09490-123">标记还会创建`DetailsView`用于添加新控件`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="09490-124">此标记使用的绑定的字段`Course`实体属性。</span><span class="sxs-lookup"><span data-stu-id="09490-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="09490-125">你必须输入`CourseID`值，因为这不是系统生成的 ID 字段。</span><span class="sxs-lookup"><span data-stu-id="09490-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="09490-126">相反，它是创建过程时必须手动指定课程编号。</span><span class="sxs-lookup"><span data-stu-id="09490-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="09490-127">使用的模板字段`Department`导航属性因为导航属性不能用于`BoundField`控件。</span><span class="sxs-lookup"><span data-stu-id="09490-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="09490-128">模板字段提供用于选择院系的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="09490-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="09490-129">下拉列表绑定到`Departments`实体集通过使用`Eval`而非`Bind`、 再次因为不能直接将导航属性绑定来更新它们。</span><span class="sxs-lookup"><span data-stu-id="09490-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="09490-130">指定的处理程序`DropDownList`控件的`Init`事件，以便你可以通过更新的代码中存储对用于控件的引用`DepartmentID`外键。</span><span class="sxs-lookup"><span data-stu-id="09490-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="09490-131">在中*CoursesAdd.aspx.cs*只是分部类声明后，添加一个类字段以保存对引用`DepartmentsDropDownList`控件：</span><span class="sxs-lookup"><span data-stu-id="09490-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="09490-132">添加的处理程序`DepartmentsDropDownList`控件的`Init`事件，以便可以将存储到控件的引用。</span><span class="sxs-lookup"><span data-stu-id="09490-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="09490-133">这样就可以获取用户输入的值，并使用它来更新`DepartmentID`的值`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="09490-134">添加的处理程序`DetailsView`控件的`Inserting`事件：</span><span class="sxs-lookup"><span data-stu-id="09490-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="09490-135">当用户单击`Insert`，则`Inserting`插入新记录之前引发事件。</span><span class="sxs-lookup"><span data-stu-id="09490-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="09490-136">在处理程序中的代码获取`DepartmentID`从`DropDownList`控制，并使用它来设置值将用于`DepartmentID`属性的`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="09490-137">实体框架将会负责处理添加到此课程`Courses`导航属性关联的`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="09490-138">它还会添加到部门`Department`导航属性`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="09490-139">运行页。</span><span class="sxs-lookup"><span data-stu-id="09490-139">Run the page.</span></span>

<span data-ttu-id="09490-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="09490-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="09490-141">输入 ID、 title、 数信用额度，并选择一个部门，然后单击**插入**。</span><span class="sxs-lookup"><span data-stu-id="09490-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="09490-142">运行*Courses.aspx*页，然后选择同一个部门，以确定新课程。</span><span class="sxs-lookup"><span data-stu-id="09490-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="09490-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="09490-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="09490-144">使用多对多关系</span><span class="sxs-lookup"><span data-stu-id="09490-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="09490-145">之间的关系`Courses`实体集和`People`实体集是多对多关系。</span><span class="sxs-lookup"><span data-stu-id="09490-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="09490-146">一个`Course`实体具有名为的导航属性`People`，可以包含零、 一个或多个相关`Person`实体 （表示讲师分配该课程的教授）。</span><span class="sxs-lookup"><span data-stu-id="09490-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="09490-147">和一个`Person`实体具有名为的导航属性`Courses`，可以包含零、 一个或多个相关`Course`实体 (表示课程分配该讲师教授)。</span><span class="sxs-lookup"><span data-stu-id="09490-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="09490-148">一个讲师可能教授多个课程和一门课程可能由多位讲师讲授。</span><span class="sxs-lookup"><span data-stu-id="09490-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="09490-149">在本演练的此部分中，您将添加和删除之间的关系`Person`和`Course`通过更新相关的实体的导航属性的实体。</span><span class="sxs-lookup"><span data-stu-id="09490-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="09490-150">创建一个名为的新 web 页*InstructorsCourses.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:</span><span class="sxs-lookup"><span data-stu-id="09490-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="09490-151">此标记创建`EntityDataSource`检索的名称的控件和`PersonID`的`Person`讲师的实体。</span><span class="sxs-lookup"><span data-stu-id="09490-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="09490-152">一个`DropDrownList`控件绑定到`EntityDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="09490-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="09490-153">`DropDownList`控制指定的处理程序`DataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="09490-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="09490-154">你将使用此处理程序到 databind 这两个下拉列表中，显示课程。</span><span class="sxs-lookup"><span data-stu-id="09490-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="09490-155">标记还会创建将课程分配到所选讲师的使用的控件的以下组：</span><span class="sxs-lookup"><span data-stu-id="09490-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="09490-156">一个`DropDownList`用于选择一门课程，分配的控件。</span><span class="sxs-lookup"><span data-stu-id="09490-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="09490-157">使用当前未指派给所选讲师的课程，将填充此控件。</span><span class="sxs-lookup"><span data-stu-id="09490-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="09490-158">一个`Button`控件以启动分配。</span><span class="sxs-lookup"><span data-stu-id="09490-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="09490-159">一个`Label`控件来显示一条错误消息，如果分配将失败。</span><span class="sxs-lookup"><span data-stu-id="09490-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="09490-160">最后，标记还创建一组控件用于移除所选讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="09490-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="09490-161">在中*InstructorsCourses.aspx.cs*，添加 using 语句：</span><span class="sxs-lookup"><span data-stu-id="09490-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="09490-162">添加用于填充两个下拉列表显示课程的一个方法：</span><span class="sxs-lookup"><span data-stu-id="09490-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="09490-163">此代码获取中的所有课程`Courses`实体集，并都获取从课程`Courses`导航属性`Person`显示所选讲师的实体。</span><span class="sxs-lookup"><span data-stu-id="09490-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="09490-164">然后，确定将哪些课程分配给该讲师，并相应地填充下拉列表。</span><span class="sxs-lookup"><span data-stu-id="09490-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="09490-165">添加的处理程序`Assign`按钮的`Click`事件：</span><span class="sxs-lookup"><span data-stu-id="09490-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="09490-166">此代码获取`Person`显示所选讲师的实体获取`Course`选定课程的实体，并将添加到所选的课程`Courses`讲师的导航属性`Person`实体。</span><span class="sxs-lookup"><span data-stu-id="09490-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="09490-167">然后，将所做的更改保存到数据库并重新填充下拉列表，因此可以立即看到结果。</span><span class="sxs-lookup"><span data-stu-id="09490-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="09490-168">添加的处理程序`Remove`按钮的`Click`事件：</span><span class="sxs-lookup"><span data-stu-id="09490-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="09490-169">此代码获取`Person`显示所选讲师的实体获取`Course`选定课程的实体，并删除从所选的课程`Person`实体的`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="09490-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="09490-170">然后，将所做的更改保存到数据库并重新填充下拉列表，因此可以立即看到结果。</span><span class="sxs-lookup"><span data-stu-id="09490-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="09490-171">将代码添加到`Page_Load`时没有错误报告，并为添加处理程序，可确保错误消息的方法不可见`DataBound`和`SelectedIndexChanged`讲师下拉列表来填充课程下拉列表的事件：</span><span class="sxs-lookup"><span data-stu-id="09490-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="09490-172">运行页。</span><span class="sxs-lookup"><span data-stu-id="09490-172">Run the page.</span></span>

<span data-ttu-id="09490-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="09490-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="09490-174">选择讲师。</span><span class="sxs-lookup"><span data-stu-id="09490-174">Select an instructor.</span></span> <span data-ttu-id="09490-175"><strong>分配一门课程</strong>下拉列表显示的课程的教师不讲解，并<strong>删除一门课程</strong>下拉列表显示已分配给讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="09490-175">The <strong>Assign a Course</strong> drop-down list displays the courses that the instructor doesn't teach, and the <strong>Remove a Course</strong> drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="09490-176">在中<strong>分配一门课程</strong>部分，选择一门课程，然后单击<strong>分配</strong>。</span><span class="sxs-lookup"><span data-stu-id="09490-176">In the <strong>Assign a Course</strong> section, select a course and then click <strong>Assign</strong>.</span></span> <span data-ttu-id="09490-177">本课程将移到<strong>删除一门课程</strong>下拉列表。</span><span class="sxs-lookup"><span data-stu-id="09490-177">The course moves to the <strong>Remove a Course</strong> drop-down list.</span></span> <span data-ttu-id="09490-178">选择在一门课程<strong>删除一门课程</strong>部分，然后单击<strong>删除</strong><em>。</em></span><span class="sxs-lookup"><span data-stu-id="09490-178">Select a course in the <strong>Remove a Course</strong> section and click <strong>Remove</strong><em>.</em></span></span> <span data-ttu-id="09490-179">本课程将移到<strong>分配一门课程</strong>下拉列表。</span><span class="sxs-lookup"><span data-stu-id="09490-179">The course moves to the <strong>Assign a Course</strong> drop-down list.</span></span>

<span data-ttu-id="09490-180">现已了解其他一些方法，使用相关数据。</span><span class="sxs-lookup"><span data-stu-id="09490-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="09490-181">在以下教程中，您将了解如何在数据模型中使用继承来提高您的应用程序的可维护性。</span><span class="sxs-lookup"><span data-stu-id="09490-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="09490-182">[上一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="09490-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>
