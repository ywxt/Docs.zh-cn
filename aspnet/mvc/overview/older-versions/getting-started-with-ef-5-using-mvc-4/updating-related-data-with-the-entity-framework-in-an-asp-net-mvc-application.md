---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用实体框架在 ASP.NET MVC 应用程序 (共 10 个 6) 更新相关的数据 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: dde9d5022823b252e59949144e3021a53c0bdd3a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371666"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="8d2a7-103">使用实体框架在 ASP.NET MVC 应用程序 (共 10 个 6) 更新相关的数据</span><span class="sxs-lookup"><span data-stu-id="8d2a7-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>
====================
<span data-ttu-id="8d2a7-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8d2a7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8d2a7-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="8d2a7-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="8d2a7-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="8d2a7-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="8d2a7-108">您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="8d2a7-109">如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="8d2a7-110">通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="8d2a7-111">一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="8d2a7-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="8d2a7-112">上一教程中显示相关的数据;在本教程中将更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="8d2a7-113">对于大多数关系，这可以通过更新相应的外键字段。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="8d2a7-114">对于多对多关系，实体框架不会联接表直接公开，因此您必须显式添加和删除实体与相应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="8d2a7-115">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="8d2a7-118">自定义课程的创建和编辑页面</span><span class="sxs-lookup"><span data-stu-id="8d2a7-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="8d2a7-119">创建新的课程实体时，新实体必须与现有院系有关系。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="8d2a7-120">为此，基架代码需包括控制器方法、创建视图和编辑视图，且视图中应包括用于选择院系的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="8d2a7-121">下拉列表设置`Course.DepartmentID`外键属性，而这正是 Entity Framework 加载所需`Department`导航属性具有相应`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="8d2a7-122">将用到基架代码，但需对其稍作更改，以便添加错误处理和对下拉列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="8d2a7-123">在中*CourseController.cs*，删除四个`Edit`和`Create`方法，并用它们替换下面的代码：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="8d2a7-124">`PopulateDepartmentsDropDownList`方法获取按名称排序的所有部门列表，创建`SelectList`集合有关的下拉列表，并将集合传递给视图`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="8d2a7-125">该方法可以使用可选的 `selectedDepartment` 参数，而调用的代码可以通过该参数来指定呈现下拉列表时被选择的项。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="8d2a7-126">该视图会将名称传递`DepartmentID`到[`DropDownList`帮助器](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)，并帮助器就会知道要查找的`ViewBag`对象`SelectList`名为`DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="8d2a7-127">`HttpGet` `Create`方法调用`PopulateDepartmentsDropDownList`方法而无需设置的所选的项，因为新课程的院系尚未建立：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="8d2a7-128">`HttpGet` `Edit`方法设置选定的项，基于已分配给正在编辑的课程的院系 ID:</span><span class="sxs-lookup"><span data-stu-id="8d2a7-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="8d2a7-129">`HttpPost`两个方法`Create`和`Edit`还包括设置选定的项时它们在错误之后重新显示页面的代码：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="8d2a7-130">此代码可确保当页面重新显示错误消息，选择任何院系保持所选。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="8d2a7-131">在中*Views\Course\Create.cshtml*，添加突出显示的代码创建一个新课程编号字段之前**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="8d2a7-132">默认情况下，如前面的教程中所述，主键字段不基架，但此主键是有意义，因此您希望用户能够输入密钥的值。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="8d2a7-133">在中*Views\Course\Edit.cshtml*， *Views\Course\Delete.cshtml*，并*Views\Course\Details.cshtml*，将添加一个课程编号字段之前**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="8d2a7-134">因为它是主键，它将显示，但不能更改。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="8d2a7-135">运行**创建**页面 (显示课程索引页，然后单击**创建新**) 并输入新课程的数据：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="8d2a7-137">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-137">Click **Create**.</span></span> <span data-ttu-id="8d2a7-138">课程索引页将显示新课程添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="8d2a7-139">索引页列表中的院系名称来自导航属性，表明已正确建立关系。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="8d2a7-141">运行**编辑**页面 (显示课程索引页，然后单击**编辑**课程上)。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="8d2a7-143">更改页面上的数据，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="8d2a7-144">课程索引页将显示已更新的课程数据。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="8d2a7-145">添加讲师的编辑页面</span><span class="sxs-lookup"><span data-stu-id="8d2a7-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="8d2a7-146">编辑讲师记录时，有时希望能更新讲师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="8d2a7-147">`Instructor`实体具有对零或一一的关系与`OfficeAssignment`实体，这意味着必须处理以下情况：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="8d2a7-148">如果用户清除办公室分配，并且它最初具有一个值，必须删除并删除`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="8d2a7-149">如果用户输入了办公室分配值并且该值最初为空，则必须创建一个新`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="8d2a7-150">如果用户更改了办公室分配的值，则必须更改中的现有值`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="8d2a7-151">打开*InstructorController.cs*并查看`HttpGet``Edit`方法：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="8d2a7-152">基架的代码不符合要求。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="8d2a7-153">它设置数据的下拉列表中，但您所需要的是文本框。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="8d2a7-154">此方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="8d2a7-155">此代码将删除`ViewBag`语句，并将关联的预先加载添加`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="8d2a7-156">无法执行与预先加载`Find`方法，因此`Where`和`Single`改为使用方法来选择讲师。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="8d2a7-157">替换`HttpPost``Edit`用下面的代码的方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="8d2a7-158">用于处理办公室分配更新：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="8d2a7-159">该代码执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-159">The code does the following:</span></span>

- <span data-ttu-id="8d2a7-160">使用 `OfficeAssignment` 导航属性的预先加载从数据库获取当前的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="8d2a7-161">这是与中的操作相同`HttpGet``Edit`方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="8d2a7-162">用模型绑定器中的值更新检索到的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="8d2a7-163">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)使用重载使你能够*允许列表*你想要包括的属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="8d2a7-164">这可以防止过度提交，如中所述[第二个教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="8d2a7-165">如果办公室位置为空，则设置`Instructor.OfficeAssignment`属性设置为 null，以便中的相关的行`OfficeAssignment`表将被删除。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="8d2a7-166">将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-166">Saves the changes to the database.</span></span>

<span data-ttu-id="8d2a7-167">在*Views\Instructor\Edit.cshtml*后面`div`元素**雇佣日期**字段中，添加新的字段编辑办公室位置：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="8d2a7-168">运行页 (选择**讲师**选项卡，然后单击**编辑**上)。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="8d2a7-169">更改“办公室位置”，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="8d2a7-171">添加课程分配给讲师编辑页</span><span class="sxs-lookup"><span data-stu-id="8d2a7-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="8d2a7-172">讲师可能教授任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="8d2a7-173">现在可以通过使用一组复选框来更改课程分配，从而增强讲师编辑页面的性能，如以下屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="8d2a7-175">之间的关系`Course`和`Instructor`实体是多对多，这意味着没有到联接表的直接访问。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="8d2a7-176">相反，您将添加和删除实体，与`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="8d2a7-177">用于更改讲师所对应的课程的 UI 是一组复选框。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="8d2a7-178">该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="8d2a7-179">用户可以通过选择或清除复选框来更改课程分配。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="8d2a7-180">如果课程数量过大，可能想要使用不同的方法在视图中，显示数据的但会使用相同的操作才能创建或删除关系的导航属性的方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="8d2a7-181">若要为复选框列表的视图提供数据，将使用视图模型类。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="8d2a7-182">创建*AssignedCourseData.cs*中*Viewmodel*文件夹并将替换为以下代码的现有代码：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="8d2a7-183">在中*InstructorController.cs*，替换`HttpGet``Edit`用下面的代码的方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="8d2a7-184">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="8d2a7-185">该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="8d2a7-186">中的代码`PopulateAssignedCourseData`方法读取所有`Course`才能加载一系列课程使用视图的实体的模型。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="8d2a7-187">对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="8d2a7-188">若要创建高效的查找，检查是否分配给讲师的课程时，分配给讲师的课程将放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="8d2a7-189">`Assigned`属性设置为`true`讲师的课程分配。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="8d2a7-190">视图将使用此属性来确定应将哪些复选框显示为选中状态。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="8d2a7-191">最后，该列表传递给视图中`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="8d2a7-192">接下来，添加用户单击“保存”时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="8d2a7-193">替换`HttpPost``Edit`方法调用更新的新方法的以下代码替换`Courses`导航属性`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="8d2a7-194">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="8d2a7-195">由于视图不包含一系列`Course`实体，模型绑定器不能自动更新`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="8d2a7-196">而不是使用模型联编程序来更新 Course 导航属性，则将执行该操作在新`UpdateInstructorCourses`方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="8d2a7-197">为此，需要从模型绑定中排除 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="8d2a7-198">这不需要对调用代码的任何更改[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)因为您正在使用*允许列表*重载和`Courses`不在包括列表中。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="8d2a7-199">如果没有复选框已选中中的代码`UpdateInstructorCourses`初始化`Courses`具有一个空集合导航属性：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="8d2a7-200">之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="8d2a7-201">为便于高效查找，后两个集合存储在 `HashSet` 对象中。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="8d2a7-202">如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="8d2a7-203">如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="8d2a7-204">在中*Views\Instructor\Edit.cshtml*，添加**课程**字段通过添加以下突出显示的复选框的数组的代码后立即`div`元素`OfficeAssignment`字段：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="8d2a7-205">此代码将创建一个具有三列的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="8d2a7-206">每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="8d2a7-207">所有复选框均都具有相同的名称 ("selectedCourses")，通知它们是作为一个组来处理的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="8d2a7-208">`value`的每个复选框的属性设置为值`CourseID.`发布页面时，模型绑定器会将数组传递给控制器组成`CourseID`仅复选框进行选择的值。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="8d2a7-209">最初呈现复选框，用于分配给讲师的课程具有`checked`属性，后者选择它们 （显示处于选中状态）。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="8d2a7-210">更改课程分配之后, 你将想要能够验证所做的更改，当在站点恢复时`Index`页。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="8d2a7-211">因此，需要将列添加到该页面中的表。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="8d2a7-212">在这种情况下不需要使用`ViewBag`对象，因为已经在你想要显示的信息`Courses`导航属性`Instructor`您传递到页作为模型的实体。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="8d2a7-213">在中*Views\Instructor\Index.cshtml*，添加**课程**标题紧跟**Office**标题，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="8d2a7-214">然后，添加新的详细信息单元格紧跟 office 位置详细信息单元：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="8d2a7-215">运行**讲师索引**页面，查看分配给每位讲师的课程：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="8d2a7-217">单击**编辑**上以查看编辑页。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="8d2a7-219">更改某些课程分配，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="8d2a7-220">所作更改将反映在索引页上。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="8d2a7-221">注意： 所编辑讲师课程数据的方法适用于有限数量的课程。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="8d2a7-222">若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  
 

## <a name="update-the-delete-method"></a><span data-ttu-id="8d2a7-223">更新 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="8d2a7-223">Update the Delete Method</span></span>

<span data-ttu-id="8d2a7-224">更改 HttpPost Delete 方法中的代码，以便删除讲师时删除 office 分配记录 （如果有）：</span><span class="sxs-lookup"><span data-stu-id="8d2a7-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]


<span data-ttu-id="8d2a7-225">如果尝试删除分配给某个部门以管理员身份的教师，您将收到引用完整性错误。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="8d2a7-226">请参阅[本教程中的当前版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)的其他代码，将自动从任何院系的讲师分配以管理员身份删除讲师。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="8d2a7-227">总结</span><span class="sxs-lookup"><span data-stu-id="8d2a7-227">Summary</span></span>

<span data-ttu-id="8d2a7-228">现在已经完成此简介使用相关数据。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="8d2a7-229">到目前为止，这些教程中所做的一项完整的 CRUD 操作，但尚未处理并发问题。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="8d2a7-230">下一步教程中将引入并发的主题，说明选项来处理它，并添加到您已编写为一个实体类型的 CRUD 代码处理的并发。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="8d2a7-231">指向其他实体框架资源，可找到的末尾[此系列中的最后一个教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8d2a7-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d2a7-232">[上一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="8d2a7-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
