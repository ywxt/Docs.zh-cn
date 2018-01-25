---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: "使用实体框架 ASP.NET MVC 应用程序 (6 的 10) 中更新相关的数据 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 2ca76364a2e9a71dc92644bd579345ae3c304a69
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="9037c-103">使用实体框架 ASP.NET MVC 应用程序 (6 的 10) 中更新相关的数据</span><span class="sxs-lookup"><span data-stu-id="9037c-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>
====================
<span data-ttu-id="9037c-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9037c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="9037c-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="9037c-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="9037c-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9037c-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="9037c-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9037c-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="9037c-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="9037c-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="9037c-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="9037c-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="9037c-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="9037c-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="9037c-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="9037c-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="9037c-112">在前面的教程中显示相关的数据;在本教程中，你将更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="9037c-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="9037c-113">对于大多数关系，这可以通过更新相应的外键字段。</span><span class="sxs-lookup"><span data-stu-id="9037c-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="9037c-114">对于多对多关系，实体框架不联接表直接公开，因此你必须显式添加和删除实体到和从相应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="9037c-115">下图显示了您将使用的页。</span><span class="sxs-lookup"><span data-stu-id="9037c-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="9037c-118">课程中自定义创建和编辑页</span><span class="sxs-lookup"><span data-stu-id="9037c-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="9037c-119">创建新的课程实体时，它必须具有与现有部门的关系。</span><span class="sxs-lookup"><span data-stu-id="9037c-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="9037c-120">为了便于执行这种情况，基架的代码包括控制器方法以及创建和编辑视图中包括用于选择部门的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="9037c-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="9037c-121">下拉列表设置`Course.DepartmentID`外键属性，而这正是实体框架需要以便加载`Department`使用相应的导航属性`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="9037c-122">你将使用基架的代码，但将其更改略有为添加错误处理和下拉列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="9037c-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="9037c-123">在*CourseController.cs*，删除四个`Edit`和`Create`方法，并用它们替换下面的代码：</span><span class="sxs-lookup"><span data-stu-id="9037c-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="9037c-124">`PopulateDepartmentsDropDownList`方法获取按名称排序的所有部门的列表，创建`SelectList`集合有关的下拉列表，并将集合传递到该视图`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="9037c-125">该方法接受可选`selectedDepartment`允许指定呈现下拉列表时将选定的项的调用代码的参数。</span><span class="sxs-lookup"><span data-stu-id="9037c-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="9037c-126">该视图将传递名称`DepartmentID`到[`DropDownList`帮助器](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)，和帮助器就会知道要查找的`ViewBag`对象`SelectList`名为`DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="9037c-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="9037c-127">`HttpGet` `Create`方法调用`PopulateDepartmentsDropDownList`而无需设置选定的项，因为新课程部门不尚未建立的方法：</span><span class="sxs-lookup"><span data-stu-id="9037c-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="9037c-128">`HttpGet` `Edit`方法设置选定的项，基于部门已分配给过程中正在编辑的 ID:</span><span class="sxs-lookup"><span data-stu-id="9037c-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="9037c-129">`HttpPost`方法同时`Create`和`Edit`还包括当它们在错误之后重新显示页时设置选定的项的代码：</span><span class="sxs-lookup"><span data-stu-id="9037c-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="9037c-130">此代码可确保当重新显示页以显示错误消息，选择任何部门保持所选。</span><span class="sxs-lookup"><span data-stu-id="9037c-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="9037c-131">在*Views\Course\Create.cshtml*，添加突出显示的代码，以创建新之前的课程数字字段**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="9037c-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="9037c-132">默认情况下，前面的教程中所述，主键字段不基架，但此主键是有意义，因此你希望用户能够输入密钥的值。</span><span class="sxs-lookup"><span data-stu-id="9037c-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="9037c-133">在*Views\Course\Edit.cshtml*， *Views\Course\Delete.cshtml*，和*Views\Course\Details.cshtml*，添加课程数字字段之前**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="9037c-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="9037c-134">因为它是主键，它会显示，但不能更改。</span><span class="sxs-lookup"><span data-stu-id="9037c-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="9037c-135">运行**创建**页 (显示课程索引页，然后单击**新建**) 和新的课程中输入数据：</span><span class="sxs-lookup"><span data-stu-id="9037c-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="9037c-137">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="9037c-137">Click **Create**.</span></span> <span data-ttu-id="9037c-138">课程索引页会显示新添加到列表中的过程。</span><span class="sxs-lookup"><span data-stu-id="9037c-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="9037c-139">索引页列表中的部门名称来自于导航属性，显示已正确建立关系。</span><span class="sxs-lookup"><span data-stu-id="9037c-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="9037c-141">运行**编辑**页 (显示课程索引页，然后单击**编辑**课程上)。</span><span class="sxs-lookup"><span data-stu-id="9037c-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="9037c-143">更改页面上的数据，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="9037c-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="9037c-144">课程索引页会显示已更新的课程数据。</span><span class="sxs-lookup"><span data-stu-id="9037c-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="9037c-145">添加教师编辑页</span><span class="sxs-lookup"><span data-stu-id="9037c-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="9037c-146">编辑教师记录时，你想要能够更新教师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="9037c-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="9037c-147">`Instructor`实体具有对零或一一个关系`OfficeAssignment`实体，这意味着必须处理的以下情况：</span><span class="sxs-lookup"><span data-stu-id="9037c-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="9037c-148">如果用户清除 office 分配，并且最初具有一个值，你必须删除并删除`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="9037c-149">如果用户输入 office 分配值，并且它最初为空，则必须创建一个新`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="9037c-150">如果用户更改一个办公室分配的值，则必须更改中的现有值`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="9037c-151">打开*InstructorController.cs*并查看`HttpGet``Edit`方法：</span><span class="sxs-lookup"><span data-stu-id="9037c-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="9037c-152">此处的基架的代码不符合要求。</span><span class="sxs-lookup"><span data-stu-id="9037c-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="9037c-153">设置数据的下拉列表中，但您需要的是文本框。</span><span class="sxs-lookup"><span data-stu-id="9037c-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="9037c-154">此方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9037c-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="9037c-155">此代码将删除`ViewBag`语句，并将添加为关联的预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="9037c-156">无法执行与预先加载`Find`方法，因此`Where`和`Single`方法用于改为选择 instructor。</span><span class="sxs-lookup"><span data-stu-id="9037c-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="9037c-157">替换`HttpPost``Edit`方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9037c-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="9037c-158">可处理 office 分配更新：</span><span class="sxs-lookup"><span data-stu-id="9037c-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="9037c-159">该代码执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="9037c-159">The code does the following:</span></span>

- <span data-ttu-id="9037c-160">获取当前`Instructor`中使用的预先加载的数据库实体`OfficeAssignment`导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="9037c-161">这是你未与相同`HttpGet``Edit`方法。</span><span class="sxs-lookup"><span data-stu-id="9037c-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="9037c-162">更新检索`Instructor`模型联编程序中的值的实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="9037c-163">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)使用重载使你能够*白名单*你想要包括的属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="9037c-164">这可以防止过度发布中所述[第二个教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9037c-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="9037c-165">如果 office 位置为空，设置`Instructor.OfficeAssignment`为 null 的属性，以便中的相关的行`OfficeAssignment`表将被删除。</span><span class="sxs-lookup"><span data-stu-id="9037c-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="9037c-166">将所做的更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="9037c-166">Saves the changes to the database.</span></span>

<span data-ttu-id="9037c-167">在*Views\Instructor\Edit.cshtml*后面`div`元素**雇用日期**字段中，添加以进行编辑的办公地点的新字段：</span><span class="sxs-lookup"><span data-stu-id="9037c-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="9037c-168">运行页面 (选择**教师**选项卡，然后单击**编辑**教师上)。</span><span class="sxs-lookup"><span data-stu-id="9037c-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="9037c-169">更改**办公地点**单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="9037c-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="9037c-171">添加课程分配到教师编辑页</span><span class="sxs-lookup"><span data-stu-id="9037c-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="9037c-172">教师可能讲解任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="9037c-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="9037c-173">现在你将通过添加更改过程分配使用一组复选框，如下面的屏幕快照中所示的功能增强教师编辑页：</span><span class="sxs-lookup"><span data-stu-id="9037c-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="9037c-175">之间的关系`Course`和`Instructor`实体是多对多，这意味着你没有直接访问联接表。</span><span class="sxs-lookup"><span data-stu-id="9037c-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="9037c-176">相反，你将在其中添加和删除实体，并从`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="9037c-177">使你能够更改哪些课程 UI 教师是分配给是一组的复选框。</span><span class="sxs-lookup"><span data-stu-id="9037c-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="9037c-178">显示数据库中每个课程复选框，并选择 instructor 当前分配给那些。</span><span class="sxs-lookup"><span data-stu-id="9037c-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="9037c-179">用户可以选择或清除复选框来更改过程分配。</span><span class="sxs-lookup"><span data-stu-id="9037c-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="9037c-180">如果课程数大得多，你将可能想要使用不同的方法来在视图中，显示数据的但你将使用相同的方法的操作才能创建或删除关系的导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="9037c-181">若要提供的复选框列表视图的数据，你将使用视图模型类。</span><span class="sxs-lookup"><span data-stu-id="9037c-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="9037c-182">创建*AssignedCourseData.cs*中*Viewmodel*文件夹和替换现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9037c-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="9037c-183">在*InstructorController.cs*，替换`HttpGet``Edit`方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9037c-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="9037c-184">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="9037c-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="9037c-185">该代码将添加为预先加载`Courses`导航属性并调用新`PopulateAssignedCourseData`方法以提供有关复选框的数组使用信息`AssignedCourseData`查看模型类。</span><span class="sxs-lookup"><span data-stu-id="9037c-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="9037c-186">中的代码`PopulateAssignedCourseData`方法读取通过所有`Course`才能加载课程使用视图的列表的实体模型类。</span><span class="sxs-lookup"><span data-stu-id="9037c-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="9037c-187">对于每个课程中，代码检查过程中是否存在于教师`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="9037c-188">若要检查是否将某一课程分配给教师时，请创建高效的查找，分配给教师的课程已放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合。</span><span class="sxs-lookup"><span data-stu-id="9037c-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="9037c-189">`Assigned`属性设置为`true`教师分配课程。</span><span class="sxs-lookup"><span data-stu-id="9037c-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="9037c-190">该视图将使用此属性来确定哪些复选框必须显示为选择。</span><span class="sxs-lookup"><span data-stu-id="9037c-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="9037c-191">最后，该列表传递给中的视图`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="9037c-192">接下来，添加在用户单击时执行的代码与**保存**。</span><span class="sxs-lookup"><span data-stu-id="9037c-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="9037c-193">替换`HttpPost``Edit`方法替换为以下代码，调用更新的新方法`Courses`导航属性`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="9037c-194">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="9037c-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="9037c-195">由于该视图不包含一套`Course`实体，不能自动更新模型联编程序`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="9037c-196">而不是使用模型联编程序更新的课程导航属性，则将执行该操作在新`UpdateInstructorCourses`方法。</span><span class="sxs-lookup"><span data-stu-id="9037c-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="9037c-197">因此你需要以排除`Courses`模型绑定中的属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="9037c-198">这不需要对调用代码的任何更改[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)因为您正在使用*白名单*重载和`Courses`不在包括列表中。</span><span class="sxs-lookup"><span data-stu-id="9037c-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="9037c-199">如果没有复选框已选中中的代码`UpdateInstructorCourses`初始化`Courses`对空集合的导航属性：</span><span class="sxs-lookup"><span data-stu-id="9037c-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="9037c-200">该代码，然后循环访问数据库中的所有课程，并检查对当前分配给与在视图中选择的教师的每个课程。</span><span class="sxs-lookup"><span data-stu-id="9037c-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="9037c-201">为了便于高效的查找，后者的两个集合都存储在`HashSet`对象。</span><span class="sxs-lookup"><span data-stu-id="9037c-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="9037c-202">如果选择某一课程复选框，但过程不在`Instructor.Courses`导航属性，过程添加到集合中的导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="9037c-203">如果未选择某一课程复选框，但过程处于`Instructor.Courses`导航属性，过程删除从导航属性。</span><span class="sxs-lookup"><span data-stu-id="9037c-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="9037c-204">在*Views\Instructor\Edit.cshtml*，添加**课程**字段通过添加以下突出显示的复选框的数组的代码后立即`div`元素`OfficeAssignment`字段：</span><span class="sxs-lookup"><span data-stu-id="9037c-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="9037c-205">此代码将创建一个 HTML 表，包含三列。</span><span class="sxs-lookup"><span data-stu-id="9037c-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="9037c-206">处于每个列组成课程编号及标题的标题后跟一个复选框。</span><span class="sxs-lookup"><span data-stu-id="9037c-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="9037c-207">所有对应的复选框具有相同的名称 ("selectedCourses")，通知它们将被视为一组模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="9037c-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="9037c-208">`value`的每个复选框的属性设置的值为`CourseID.`发页面，当模型联编程序会将数组传递给组成的控制器`CourseID`仅复选框进行选择的值。</span><span class="sxs-lookup"><span data-stu-id="9037c-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="9037c-209">当最初呈现复选框时，为分配给教师的课程的那些具有`checked`属性，后者选择它们 （它们检查的显示）。</span><span class="sxs-lookup"><span data-stu-id="9037c-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="9037c-210">更改课程作业之后, 你将需要能够验证所做的更改，当站点恢复时`Index`页。</span><span class="sxs-lookup"><span data-stu-id="9037c-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="9037c-211">因此，你需要将列添加到该页面中的表。</span><span class="sxs-lookup"><span data-stu-id="9037c-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="9037c-212">在这种情况下不需要使用`ViewBag`对象，因为已经在你想要显示的信息`Courses`导航属性`Instructor`您传递到页其作为模型的实体。</span><span class="sxs-lookup"><span data-stu-id="9037c-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="9037c-213">在*Views\Instructor\Index.cshtml*，添加**课程**标题紧跟**Office**标题下，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="9037c-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="9037c-214">然后添加新的详细信息单元紧跟 office 位置详细信息单元：</span><span class="sxs-lookup"><span data-stu-id="9037c-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="9037c-215">运行**教师索引**页后，可以查看分配给每个教师课程：</span><span class="sxs-lookup"><span data-stu-id="9037c-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="9037c-217">单击**编辑**教师若要查看编辑页上。</span><span class="sxs-lookup"><span data-stu-id="9037c-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="9037c-219">更改某些课程作业，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="9037c-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="9037c-220">所做的更改会反映在索引页面。</span><span class="sxs-lookup"><span data-stu-id="9037c-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="9037c-221">注意： 编辑教师课程数据而采取的做法适用于没有有限的数量的课程。</span><span class="sxs-lookup"><span data-stu-id="9037c-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="9037c-222">对于则大得多的集合，会需要不同的 UI 以及不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="9037c-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  
 

## <a name="update-the-delete-method"></a><span data-ttu-id="9037c-223">更新 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="9037c-223">Update the Delete Method</span></span>

<span data-ttu-id="9037c-224">更改 HttpPost 删除方法中的代码，以便在 office 分配记录 （如果有） 被删除时删除教师：</span><span class="sxs-lookup"><span data-stu-id="9037c-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]


<span data-ttu-id="9037c-225">如果你尝试删除分配给以管理员身份的部门的教师，你将获得一个引用完整性错误。</span><span class="sxs-lookup"><span data-stu-id="9037c-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="9037c-226">请参阅[本教程的当前版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)将自动删除任何部门其中教师分配以管理员身份从教师的其他代码。</span><span class="sxs-lookup"><span data-stu-id="9037c-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="9037c-227">摘要</span><span class="sxs-lookup"><span data-stu-id="9037c-227">Summary</span></span>

<span data-ttu-id="9037c-228">你现在已经完成此简介使用相关数据。</span><span class="sxs-lookup"><span data-stu-id="9037c-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="9037c-229">到目前为止这些教程中所做的一项完整的 CRUD 的操作，但尚未处理并发问题。</span><span class="sxs-lookup"><span data-stu-id="9037c-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="9037c-230">下一教程将介绍并发的主题，说明用于处理它，选项并添加到您已经编写了一个实体类型的 CRUD 代码处理的并发。</span><span class="sxs-lookup"><span data-stu-id="9037c-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="9037c-231">可以在的末尾找到的其他实体框架资源的链接[本系列最后一个教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9037c-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="9037c-232">[上一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="9037c-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
