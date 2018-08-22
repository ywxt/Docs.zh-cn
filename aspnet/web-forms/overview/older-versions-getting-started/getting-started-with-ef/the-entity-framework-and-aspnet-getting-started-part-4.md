---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 4 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: f4a8e7f1cafd169f392485ff4ecb260073209210
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824648"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="34c04-104">Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 4 部分</span><span class="sxs-lookup"><span data-stu-id="34c04-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>
====================
<span data-ttu-id="34c04-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="34c04-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="34c04-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="34c04-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="34c04-107">有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="34c04-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data"></a><span data-ttu-id="34c04-108">使用相关数据</span><span class="sxs-lookup"><span data-stu-id="34c04-108">Working with Related Data</span></span>

<span data-ttu-id="34c04-109">在上一教程使用了`EntityDataSource`到筛选器、 排序和分组数据的控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="34c04-110">在本教程中将显示和更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="34c04-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="34c04-111">你将创建讲师页显示的讲师列表。</span><span class="sxs-lookup"><span data-stu-id="34c04-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="34c04-112">当您选择一名讲师时，您会看到由该讲师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="34c04-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="34c04-113">当您选择一门课程时，你将看到课程和参加该课程的学生列表的详细信息。</span><span class="sxs-lookup"><span data-stu-id="34c04-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="34c04-114">你可以编辑教师姓名、 雇佣日期和办公室分配。</span><span class="sxs-lookup"><span data-stu-id="34c04-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="34c04-115">办公室分配是通过导航属性访问单独的实体集。</span><span class="sxs-lookup"><span data-stu-id="34c04-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="34c04-116">您可以链接到标记中或在代码中的详细信息数据的主数据。</span><span class="sxs-lookup"><span data-stu-id="34c04-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="34c04-117">在本教程的此部分中，将使用这两种方法。</span><span class="sxs-lookup"><span data-stu-id="34c04-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="34c04-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="34c04-119">显示和更新在 GridView 控件中的相关的实体</span><span class="sxs-lookup"><span data-stu-id="34c04-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="34c04-120">创建一个名为的新 web 页*Instructors.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:</span><span class="sxs-lookup"><span data-stu-id="34c04-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="34c04-121">此标记创建`EntityDataSource`控件，以选择讲师和启用更新。</span><span class="sxs-lookup"><span data-stu-id="34c04-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="34c04-122">`div`元素配置标记呈现在左侧，以便可以稍后添加在右侧的列。</span><span class="sxs-lookup"><span data-stu-id="34c04-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="34c04-123">之间`EntityDataSource`标记和结束`</div>`标记中，添加以下标记创建`GridView`控件和一个`Label`控件，将使用错误消息：</span><span class="sxs-lookup"><span data-stu-id="34c04-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="34c04-124">这`GridView`控件启用行选择、 突出显示所选的行与一种浅灰色背景颜色，并指定的处理程序 （其中你将创建更高版本）`SelectedIndexChanged`和`Updating`事件。</span><span class="sxs-lookup"><span data-stu-id="34c04-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="34c04-125">它还指定`PersonID`为`DataKeyNames`属性，以便在所选行的键值可以传递到你稍后将添加的另一个控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="34c04-126">最后一列包含的导航属性中存储的讲师的办公室分配`Person`实体因为来自关联的实体。</span><span class="sxs-lookup"><span data-stu-id="34c04-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="34c04-127">请注意，`EditItemTemplate`元素指定`Eval`而不是`Bind`，这是因为`GridView`控件不能直接绑定到导航属性来更新它们。</span><span class="sxs-lookup"><span data-stu-id="34c04-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="34c04-128">将更新代码中的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="34c04-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="34c04-129">若要执行此操作，将需要对引用`TextBox`控件中，将获取并保存，在`TextBox`控件的`Init`事件。</span><span class="sxs-lookup"><span data-stu-id="34c04-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="34c04-130">遵循`GridView`控件是`Label`用于错误消息的控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="34c04-131">控件的`Visible`属性是`false`，和视图状态处于关闭状态，以便该标签将显示仅当代码使其可见中出现错误。</span><span class="sxs-lookup"><span data-stu-id="34c04-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="34c04-132">打开*Instructors.aspx.cs*文件，并添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="34c04-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="34c04-133">分部类名称声明，以保存对 office 分配文本框中的引用后立即添加私有类字段。</span><span class="sxs-lookup"><span data-stu-id="34c04-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="34c04-134">添加的存根`SelectedIndexChanged`事件处理程序，将为更高版本中添加代码。</span><span class="sxs-lookup"><span data-stu-id="34c04-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="34c04-135">此外将添加的办公室分配的处理程序`TextBox`控件的`Init`事件，以便可以将存储到的引用`TextBox`控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="34c04-136">将使用此引用来获取用户输入以更新与导航属性关联的实体的值。</span><span class="sxs-lookup"><span data-stu-id="34c04-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="34c04-137">将使用`GridView`控件的`Updating`要更新的事件`Location`属性关联的`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="34c04-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="34c04-138">添加以下处理程序`Updating`事件：</span><span class="sxs-lookup"><span data-stu-id="34c04-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="34c04-139">此代码的运行时在用户单击**更新**中`GridView`行。</span><span class="sxs-lookup"><span data-stu-id="34c04-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="34c04-140">代码使用 LINQ to Entities 来检索`OfficeAssignment`与当前关联的实体`Person`实体，使用`PersonID`从事件参数所选行。</span><span class="sxs-lookup"><span data-stu-id="34c04-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="34c04-141">代码然后会执行以下操作，具体取决于中的值之一`InstructorOfficeTextBox`控件：</span><span class="sxs-lookup"><span data-stu-id="34c04-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="34c04-142">如果在文本框中有一个值，并且没有任何`OfficeAssignment`实体来更新，它将创建一个。</span><span class="sxs-lookup"><span data-stu-id="34c04-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="34c04-143">如果在文本框中有一个值，并且没有`OfficeAssignment`实体，它会更新`Location`属性值。</span><span class="sxs-lookup"><span data-stu-id="34c04-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="34c04-144">如果文本框为空且`OfficeAssignment`实体存在，它会删除该实体。</span><span class="sxs-lookup"><span data-stu-id="34c04-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="34c04-145">在此之后，它将保存所做的更改到数据库。</span><span class="sxs-lookup"><span data-stu-id="34c04-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="34c04-146">如果发生异常，它将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="34c04-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="34c04-147">运行页。</span><span class="sxs-lookup"><span data-stu-id="34c04-147">Run the page.</span></span>

<span data-ttu-id="34c04-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="34c04-149">单击**编辑**和所有字段都更改为文本框中。</span><span class="sxs-lookup"><span data-stu-id="34c04-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="34c04-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="34c04-151">更改任何这些值，包括**办公室分配**。</span><span class="sxs-lookup"><span data-stu-id="34c04-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="34c04-152">单击**更新**，将看到反映在列表中的更改。</span><span class="sxs-lookup"><span data-stu-id="34c04-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="34c04-153">在一个单独的控件中显示相关的实体</span><span class="sxs-lookup"><span data-stu-id="34c04-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="34c04-154">每一名讲师可以教授一个或多个课程，因此将添加`EntityDataSource`控件和一个`GridView`控件以列出与讲师中选择任何讲师的课程`GridView`控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="34c04-155">若要创建标题和`EntityDataSource`控件的课程实体中，添加以下标记之间的错误消息`Label`控件和关闭`</div>`标记：</span><span class="sxs-lookup"><span data-stu-id="34c04-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="34c04-156">`Where`参数包含的值`PersonID`中选择其行讲师的`InstructorsGridView`控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="34c04-157">`Where`属性包含一个可获取所有关联的嵌套 select 命令`Person`中的实体`Course`实体的`People`导航属性并选择`Course`实体仅当其中一个关联`Person`实体包含所选`PersonID`值。</span><span class="sxs-lookup"><span data-stu-id="34c04-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="34c04-158">若要创建`GridView`控件。 添加以下标记紧跟`CoursesEntityDataSource`控件 (在关闭前`</div>`标记):</span><span class="sxs-lookup"><span data-stu-id="34c04-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="34c04-159">因为如果选择没有讲师时，将会不显示任何课程`EmptyDataTemplate`元素是包含。</span><span class="sxs-lookup"><span data-stu-id="34c04-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="34c04-160">运行页。</span><span class="sxs-lookup"><span data-stu-id="34c04-160">Run the page.</span></span>

<span data-ttu-id="34c04-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="34c04-162">选择有一个或多个课程分配，一名讲师和课程列表中显示。</span><span class="sxs-lookup"><span data-stu-id="34c04-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="34c04-163">(注意： 尽管数据库架构允许多个课程，但提供与数据库的测试数据中没有讲师实际上有多个课程。</span><span class="sxs-lookup"><span data-stu-id="34c04-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="34c04-164">您可以课程向数据库添加您自己使用**服务器资源管理器**窗口或*CoursesAdd.aspx*页上，你将添加在下一个教程。)</span><span class="sxs-lookup"><span data-stu-id="34c04-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="34c04-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="34c04-166">`CoursesGridView`控件显示几个课程字段。</span><span class="sxs-lookup"><span data-stu-id="34c04-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="34c04-167">若要显示某课程的所有详细信息，请将使用`DetailsView`控件为用户选择课程。</span><span class="sxs-lookup"><span data-stu-id="34c04-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="34c04-168">中*Instructors.aspx*，将以下标记添加结束后`</div>`标记 (请确保将此标记**后**右 div 标记，不在此之前它):</span><span class="sxs-lookup"><span data-stu-id="34c04-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="34c04-169">此标记创建`EntityDataSource`绑定到控件`Courses`实体集。</span><span class="sxs-lookup"><span data-stu-id="34c04-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="34c04-170">`Where`属性选择课程使用`CourseID`课程中的选定行的值`GridView`控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="34c04-171">该标记指定的处理程序`Selected`事件，你将使用用于显示学生成绩的更高版本，它是另一个层次结构中较低的级别。</span><span class="sxs-lookup"><span data-stu-id="34c04-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="34c04-172">在中*Instructors.aspx.cs*，创建以下存根`CourseDetailsEntityDataSource_Selected`方法。</span><span class="sxs-lookup"><span data-stu-id="34c04-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="34c04-173">（你将填写此存根 （stub） 本教程的后面，现在，您需要它，因此该页将编译并运行。）</span><span class="sxs-lookup"><span data-stu-id="34c04-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="34c04-174">运行页。</span><span class="sxs-lookup"><span data-stu-id="34c04-174">Run the page.</span></span>

<span data-ttu-id="34c04-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="34c04-176">最初没有课程详细信息由于任何课程不选择。</span><span class="sxs-lookup"><span data-stu-id="34c04-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="34c04-177">选择有课程分配，一名讲师，然后选择一门课程，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="34c04-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="34c04-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="34c04-179">使用 EntityDataSource"选择"事件，以显示相关的数据</span><span class="sxs-lookup"><span data-stu-id="34c04-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="34c04-180">最后，你想要显示的所有已注册的学生和所选课程及其成绩。</span><span class="sxs-lookup"><span data-stu-id="34c04-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="34c04-181">若要执行此操作，将使用`Selected`的事件`EntityDataSource`控件绑定到该课程`DetailsView`。</span><span class="sxs-lookup"><span data-stu-id="34c04-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="34c04-182">在中*Instructors.aspx*，添加以下标记后的`DetailsView`控件：</span><span class="sxs-lookup"><span data-stu-id="34c04-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="34c04-183">此标记创建`ListView`显示的学生和所选课程及其成绩列表的控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="34c04-184">由于将数据绑定控件在代码中，未不指定任何数据源。</span><span class="sxs-lookup"><span data-stu-id="34c04-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="34c04-185">`EmptyDataTemplate`元素提供任何课程不选择时显示一条消息，这种情况下，没有显示任何学生。</span><span class="sxs-lookup"><span data-stu-id="34c04-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="34c04-186">`LayoutTemplate`元素创建一个 HTML 表以显示的列表和`ItemTemplate`指定要显示的列。</span><span class="sxs-lookup"><span data-stu-id="34c04-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="34c04-187">学生 ID 和学生等级取自`StudentGrade`实体，并且学生姓名摘自`Person`实体框架使中可用的实体`Person`导航属性`StudentGrade`实体。</span><span class="sxs-lookup"><span data-stu-id="34c04-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="34c04-188">在*Instructors.aspx.cs*，将用作存根带`CourseDetailsEntityDataSource_Selected`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="34c04-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="34c04-189">此事件的事件参数提供了一个集合，它将具有零个项，如果未选择任何内容或一个项的窗体中的所选的数据如果`Course`选择实体。</span><span class="sxs-lookup"><span data-stu-id="34c04-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="34c04-190">如果`Course`选择实体后，该代码使用`First`方法将集合转换为单个对象。</span><span class="sxs-lookup"><span data-stu-id="34c04-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="34c04-191">然后，它获取`StudentGrade`实体的导航属性，将其转换为一个集合，并将绑定`GradesListView`到集合的控件。</span><span class="sxs-lookup"><span data-stu-id="34c04-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="34c04-192">这足够大，以显示成绩，但你想要确保第一次显示的页将显示空数据模板中的消息，只要未选择一门课程。</span><span class="sxs-lookup"><span data-stu-id="34c04-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="34c04-193">若要执行此操作，创建以下方法，你将调用从两个位置：</span><span class="sxs-lookup"><span data-stu-id="34c04-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="34c04-194">调用此新方法从`Page_Load`方法来显示将显示的页的空数据模板第一个时间。</span><span class="sxs-lookup"><span data-stu-id="34c04-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="34c04-195">并调用它从`InstructorsGridView_SelectedIndexChanged`方法时选择讲师时引发该事件，因为这意味着新课程加载到课程`GridView`尚未选择控件和 none。</span><span class="sxs-lookup"><span data-stu-id="34c04-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="34c04-196">下面是两个调用：</span><span class="sxs-lookup"><span data-stu-id="34c04-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="34c04-197">运行页。</span><span class="sxs-lookup"><span data-stu-id="34c04-197">Run the page.</span></span>

<span data-ttu-id="34c04-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="34c04-199">选择讲师的课程分配，并选择课程。</span><span class="sxs-lookup"><span data-stu-id="34c04-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="34c04-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="34c04-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="34c04-201">您现在已经了解了多种用于处理相关数据。</span><span class="sxs-lookup"><span data-stu-id="34c04-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="34c04-202">在以下教程中，您将学习如何添加现有实体之间的关系如何删除关系，以及如何添加新的实体具有与现有实体的关系。</span><span class="sxs-lookup"><span data-stu-id="34c04-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34c04-203">[上一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="34c04-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
