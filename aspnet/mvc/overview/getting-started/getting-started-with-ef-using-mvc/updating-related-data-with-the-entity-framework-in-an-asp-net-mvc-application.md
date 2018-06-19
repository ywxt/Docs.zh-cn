---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用实体框架中的 ASP.NET MVC 应用程序更新相关的数据 |Microsoft 文档
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/01/2015
ms.topic: article
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: cf4a6183e068e8668eb706d9a9e311616649e863
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875612"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="c4934-103">使用实体框架中的 ASP.NET MVC 应用程序更新相关的数据</span><span class="sxs-lookup"><span data-stu-id="c4934-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="c4934-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c4934-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="c4934-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="c4934-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="c4934-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4934-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="c4934-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="c4934-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="c4934-108">在前面的教程中显示相关的数据;在本教程中，你将更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c4934-108">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="c4934-109">对于大多数关系，这可以通过更新外键字段或导航属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-109">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="c4934-110">对于多对多关系，实体框架不联接表直接公开，因此添加和删除实体到和从相应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-110">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="c4934-111">下图显示了一些将使用的页面。</span><span class="sxs-lookup"><span data-stu-id="c4934-111">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![对于课程教师编辑](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="c4934-115">自定义课程创建页和编辑页</span><span class="sxs-lookup"><span data-stu-id="c4934-115">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="c4934-116">创建新的课程实体时，该实体必须与现有系相关联。</span><span class="sxs-lookup"><span data-stu-id="c4934-116">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="c4934-117">为了便于实现这种关联，基架代码包含了控制器方法以及创建和编辑视图，其中包括用于选择系的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="c4934-117">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="c4934-118">下拉列表设置`Course.DepartmentID`外键属性，而这正是实体框架需要以便加载`Department`使用相应的导航属性`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-118">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="c4934-119">你将使用基架代码，但需要对其略作更改以添加错误处理并对下拉列表排序。</span><span class="sxs-lookup"><span data-stu-id="c4934-119">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="c4934-120">在*CourseController.cs*，删除四个`Create`和`Edit`方法，并用它们替换下面的代码：</span><span class="sxs-lookup"><span data-stu-id="c4934-120">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="c4934-121">添加以下`using`语句开头的文件：</span><span class="sxs-lookup"><span data-stu-id="c4934-121">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="c4934-122">`PopulateDepartmentsDropDownList`方法获取按名称排序的所有部门的列表，创建`SelectList`集合有关的下拉列表，并将集合传递到该视图`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-122">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="c4934-123">该方法接受可选`selectedDepartment`参数，调用代码可通过该参数指定呈现该下拉列表时选定的项。</span><span class="sxs-lookup"><span data-stu-id="c4934-123">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="c4934-124">该视图将传递名称`DepartmentID`到[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)帮助器，然后帮助器就会知道要查找的`ViewBag`对象`SelectList`名为`DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="c4934-124">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="c4934-125">`HttpGet` `Create`方法调用`PopulateDepartmentsDropDownList`而无需设置选定的项，因为新课程部门不尚未建立的方法：</span><span class="sxs-lookup"><span data-stu-id="c4934-125">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="c4934-126">`HttpGet` `Edit`方法设置选定的项，基于部门已分配给过程中正在编辑的 ID:</span><span class="sxs-lookup"><span data-stu-id="c4934-126">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="c4934-127">`HttpPost`方法同时`Create`和`Edit`还包括当它们在错误之后重新显示页时设置选定的项的代码：</span><span class="sxs-lookup"><span data-stu-id="c4934-127">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="c4934-128">此代码可确保当重新显示页以显示错误消息，选择任何部门保持所选。</span><span class="sxs-lookup"><span data-stu-id="c4934-128">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="c4934-129">课程视图已基架使用下拉列表的部门字段中，但不希望 DepartmentID 标题为此字段中，因此请以下突出显示将更改为*Views\Course\Create.cshtml*到文件更改的标题。</span><span class="sxs-lookup"><span data-stu-id="c4934-129">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="c4934-130">进行中相同的更改*Views\Course\Edit.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="c4934-130">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="c4934-131">通常 scaffolder 不搭建基架为主键由于密钥的值由数据库生成和不能更改，而不是有意义的值，向用户显示。</span><span class="sxs-lookup"><span data-stu-id="c4934-131">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="c4934-132">基架的课程实体包含为文本框`CourseID`字段它理解，因为`DatabaseGeneratedOption.None`属性意味着用户应该可以输入的主键值。</span><span class="sxs-lookup"><span data-stu-id="c4934-132">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="c4934-133">但它不理解，因为该号码是有意义你想要在其他视图中查看它，因此你需要手动添加它。</span><span class="sxs-lookup"><span data-stu-id="c4934-133">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="c4934-134">在*Views\Course\Edit.cshtml*，添加课程数字字段之前**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="c4934-134">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="c4934-135">因为它是主键，它会显示，但不能更改。</span><span class="sxs-lookup"><span data-stu-id="c4934-135">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="c4934-136">已存在一个隐藏的字段 (`Html.HiddenFor`帮助程序) 编辑视图中的过程编号。</span><span class="sxs-lookup"><span data-stu-id="c4934-136">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="c4934-137">添加*Html.LabelFor*帮助器不会消除隐藏字段的需要，因为它不会导致课程编号，以包括在已发布数据中，当用户单击**保存**编辑页上。</span><span class="sxs-lookup"><span data-stu-id="c4934-137">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="c4934-138">在*Views\Course\Delete.cshtml*和*Views\Course\Details.cshtml*、 更改部门名称的标题从"名称"到"部门"以及添加课程数字字段之前**标题**字段。</span><span class="sxs-lookup"><span data-stu-id="c4934-138">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="c4934-139">运行**创建**页 (显示课程索引页，然后单击**新建**) 和新的课程中输入数据：</span><span class="sxs-lookup"><span data-stu-id="c4934-139">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="c4934-141">单击“创建” 。</span><span class="sxs-lookup"><span data-stu-id="c4934-141">Click **Create**.</span></span> <span data-ttu-id="c4934-142">课程索引页会显示新添加到列表中的过程。</span><span class="sxs-lookup"><span data-stu-id="c4934-142">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="c4934-143">“索引”页列表中的院系名称来自导航属性，表明已正确建立关系。</span><span class="sxs-lookup"><span data-stu-id="c4934-143">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="c4934-145">运行**编辑**页 (显示课程索引页，然后单击**编辑**课程上)。</span><span class="sxs-lookup"><span data-stu-id="c4934-145">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="c4934-147">更改页面上的数据，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="c4934-147">Change data on the page and click **Save**.</span></span> <span data-ttu-id="c4934-148">课程索引页会显示已更新的课程数据。</span><span class="sxs-lookup"><span data-stu-id="c4934-148">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="c4934-149">添加教师编辑页</span><span class="sxs-lookup"><span data-stu-id="c4934-149">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="c4934-150">编辑讲师记录时，有时希望能更新讲师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="c4934-150">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="c4934-151">`Instructor`实体具有对零或一一个关系`OfficeAssignment`实体，这意味着必须处理的以下情况：</span><span class="sxs-lookup"><span data-stu-id="c4934-151">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="c4934-152">如果用户清除 office 分配，并且最初具有一个值，你必须删除并删除`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-152">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="c4934-153">如果用户输入 office 分配值，并且它最初为空，则必须创建一个新`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-153">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="c4934-154">如果用户更改一个办公室分配的值，则必须更改中的现有值`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-154">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="c4934-155">打开*InstructorController.cs*并查看`HttpGet``Edit`方法：</span><span class="sxs-lookup"><span data-stu-id="c4934-155">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="c4934-156">此处的基架的代码不符合要求。</span><span class="sxs-lookup"><span data-stu-id="c4934-156">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="c4934-157">设置数据的下拉列表中，但您需要的是文本框。</span><span class="sxs-lookup"><span data-stu-id="c4934-157">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="c4934-158">此方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4934-158">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="c4934-159">此代码将删除`ViewBag`语句，并将添加为关联的预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-159">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="c4934-160">无法执行与预先加载`Find`方法，因此`Where`和`Single`方法用于改为选择 instructor。</span><span class="sxs-lookup"><span data-stu-id="c4934-160">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="c4934-161">替换`HttpPost``Edit`方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="c4934-161">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="c4934-162">可处理 office 分配更新：</span><span class="sxs-lookup"><span data-stu-id="c4934-162">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="c4934-163">对引用`RetryLimitExceededException`需要`using`语句; 若要将其添加，请右键单击`RetryLimitExceededException`，然后单击**解决** - **使用 System.Data.Entity.Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="c4934-163">The reference to `RetryLimitExceededException` requires a `using` statement; to add it, right-click `RetryLimitExceededException`, and then click **Resolve** - **using System.Data.Entity.Infrastructure**.</span></span>

![解决重试异常](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="c4934-165">该代码执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c4934-165">The code does the following:</span></span>

- <span data-ttu-id="c4934-166">方法名称更改为`EditPost`因为签名现在为相同`HttpGet`方法 (`ActionName`属性指定 /Edit/ URL 仍使用)。</span><span class="sxs-lookup"><span data-stu-id="c4934-166">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="c4934-167">使用 `OfficeAssignment` 导航属性的预先加载从数据库获取当前的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-167">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="c4934-168">这是你未与相同`HttpGet``Edit`方法。</span><span class="sxs-lookup"><span data-stu-id="c4934-168">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="c4934-169">用模型绑定器中的值更新检索到的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-169">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="c4934-170">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)使用重载使你能够*允许列表*你想要包括的属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-170">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="c4934-171">这可以防止过度发布中所述[第二个教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="c4934-171">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="c4934-172">如果 office 位置为空，设置`Instructor.OfficeAssignment`为 null 的属性，以便中的相关的行`OfficeAssignment`表将被删除。</span><span class="sxs-lookup"><span data-stu-id="c4934-172">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="c4934-173">将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="c4934-173">Saves the changes to the database.</span></span>

<span data-ttu-id="c4934-174">在*Views\Instructor\Edit.cshtml*后面`div`元素**雇用日期**字段中，添加以进行编辑的办公地点的新字段：</span><span class="sxs-lookup"><span data-stu-id="c4934-174">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="c4934-175">运行页面 (选择**教师**选项卡，然后单击**编辑**教师上)。</span><span class="sxs-lookup"><span data-stu-id="c4934-175">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="c4934-176">更改“办公室位置”，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="c4934-176">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="c4934-178">添加课程分配到教师编辑页</span><span class="sxs-lookup"><span data-stu-id="c4934-178">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="c4934-179">讲师可能教授任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-179">Instructors may teach any number of courses.</span></span> <span data-ttu-id="c4934-180">现在可以通过使用一组复选框来更改课程分配，从而增强“讲师编辑”页面的性能，如以下屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="c4934-180">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="c4934-182">之间的关系`Course`和`Instructor`实体是多对多，这意味着你没有直接访问联接表中的外键属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-182">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="c4934-183">相反，你添加和删除实体，并从`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-183">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="c4934-184">用于更改讲师所对应的课程的 UI 是一组复选框。</span><span class="sxs-lookup"><span data-stu-id="c4934-184">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="c4934-185">该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。</span><span class="sxs-lookup"><span data-stu-id="c4934-185">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="c4934-186">用户可以通过选择或清除复选框来更改课程分配。</span><span class="sxs-lookup"><span data-stu-id="c4934-186">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="c4934-187">如果课程数大得多，你将可能想要使用不同的方法来在视图中，显示数据的但你将使用相同的方法的操作才能创建或删除关系的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-187">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="c4934-188">若要为复选框列表的视图提供数据，可使用视图模型类。</span><span class="sxs-lookup"><span data-stu-id="c4934-188">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="c4934-189">创建*AssignedCourseData.cs*中*Viewmodel*文件夹和替换现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4934-189">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="c4934-190">在*InstructorController.cs*，替换`HttpGet``Edit`方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="c4934-190">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="c4934-191">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="c4934-191">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="c4934-192">该代码为 `Courses`导航属性添加了预先加载，并调用新的`PopulateAssignedCourseData`方法使用`AssignedCourseData`视图模型类为复选框数组提供信息。</span><span class="sxs-lookup"><span data-stu-id="c4934-192">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="c4934-193">中的代码`PopulateAssignedCourseData`方法读取通过所有`Course`才能加载课程使用视图的列表的实体模型类。</span><span class="sxs-lookup"><span data-stu-id="c4934-193">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="c4934-194">对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-194">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="c4934-195">若要检查是否将某一课程分配给教师时，请创建高效的查找，分配给教师的课程已放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合。</span><span class="sxs-lookup"><span data-stu-id="c4934-195">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="c4934-196">`Assigned`属性设置为`true`教师分配课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-196">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="c4934-197">视图将使用此属性来确定应将哪些复选框显示为选中状态。</span><span class="sxs-lookup"><span data-stu-id="c4934-197">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="c4934-198">最后，该列表传递给中的视图`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-198">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="c4934-199">接下来，添加用户单击“保存”时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="c4934-199">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="c4934-200">替换`EditPost`方法替换为以下代码，调用更新的新方法`Courses`导航属性`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-200">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="c4934-201">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="c4934-201">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="c4934-202">方法签名现在是不同于`HttpGet``Edit`方法，以便从更改方法名称`EditPost`回`Edit`。</span><span class="sxs-lookup"><span data-stu-id="c4934-202">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="c4934-203">由于该视图不包含一套`Course`实体，不能自动更新模型联编程序`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-203">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="c4934-204">而不是使用模型联编程序更新`Courses`导航属性，则将执行该操作在新`UpdateInstructorCourses`方法。</span><span class="sxs-lookup"><span data-stu-id="c4934-204">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="c4934-205">为此，需要从模型绑定中排除 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="c4934-205">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="c4934-206">这不需要对调用代码的任何更改[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)因为您正在使用*允许列表*重载和`Courses`不在包括列表中。</span><span class="sxs-lookup"><span data-stu-id="c4934-206">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="c4934-207">如果没有复选框已选中中的代码`UpdateInstructorCourses`初始化`Courses`对空集合的导航属性：</span><span class="sxs-lookup"><span data-stu-id="c4934-207">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="c4934-208">之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-208">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="c4934-209">为便于高效查找，后两个集合存储在 `HashSet` 对象中。</span><span class="sxs-lookup"><span data-stu-id="c4934-209">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="c4934-210">如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。</span><span class="sxs-lookup"><span data-stu-id="c4934-210">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="c4934-211">如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-211">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="c4934-212">在*Views\Instructor\Edit.cshtml*，添加**课程**字段与非数组的复选框，通过添加以下代码后立即`div`元素`OfficeAssignment`字段和之前`div`元素**保存**按钮：</span><span class="sxs-lookup"><span data-stu-id="c4934-212">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="c4934-213">粘贴完毕后的代码，如果换行和缩进看起来像它们在此处执行操作，以便它如下所示这里看到手动修复所有内容。</span><span class="sxs-lookup"><span data-stu-id="c4934-213">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="c4934-214">缩进不一定要完美，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@</tr>` 行必须各成一行（如下所示），否则会出现运行时错误。</span><span class="sxs-lookup"><span data-stu-id="c4934-214">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="c4934-215">此代码将创建一个具有三列的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="c4934-215">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="c4934-216">每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。</span><span class="sxs-lookup"><span data-stu-id="c4934-216">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="c4934-217">所有复选框都具有相同的名称，即 selectedCourses，以告知模型绑定器将它们视为一组。</span><span class="sxs-lookup"><span data-stu-id="c4934-217">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="c4934-218">`value`的每个复选框的属性设置的值为`CourseID.`发页面，当模型联编程序会将数组传递给组成的控制器`CourseID`仅复选框进行选择的值。</span><span class="sxs-lookup"><span data-stu-id="c4934-218">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="c4934-219">当最初呈现复选框时，为分配给教师的课程的那些具有`checked`属性，后者选择它们 （它们检查的显示）。</span><span class="sxs-lookup"><span data-stu-id="c4934-219">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="c4934-220">更改课程作业之后, 你将需要能够验证所做的更改，当站点恢复时`Index`页。</span><span class="sxs-lookup"><span data-stu-id="c4934-220">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="c4934-221">因此，你需要将列添加到该页面中的表。</span><span class="sxs-lookup"><span data-stu-id="c4934-221">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="c4934-222">在这种情况下不需要使用`ViewBag`对象，因为已经在你想要显示的信息`Courses`导航属性`Instructor`您传递到页其作为模型的实体。</span><span class="sxs-lookup"><span data-stu-id="c4934-222">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="c4934-223">在*Views\Instructor\Index.cshtml*，添加**课程**标题紧跟**Office**标题下，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="c4934-223">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="c4934-224">然后添加新的详细信息单元紧跟 office 位置详细信息单元：</span><span class="sxs-lookup"><span data-stu-id="c4934-224">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="c4934-225">运行**教师索引**页后，可以查看分配给每个教师课程：</span><span class="sxs-lookup"><span data-stu-id="c4934-225">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="c4934-227">单击**编辑**教师若要查看编辑页上。</span><span class="sxs-lookup"><span data-stu-id="c4934-227">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

<span data-ttu-id="c4934-229">更改某些课程作业，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="c4934-229">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="c4934-230">所做的更改将反映在“索引”页上。</span><span class="sxs-lookup"><span data-stu-id="c4934-230">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="c4934-231">注意： 采取此处编辑教师课程数据的做法适用于没有有限的数量的课程。</span><span class="sxs-lookup"><span data-stu-id="c4934-231">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="c4934-232">若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="c4934-232">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  
 

## <a name="update-the-deleteconfirmed-method"></a><span data-ttu-id="c4934-233">更新 DeleteConfirmed 方法</span><span class="sxs-lookup"><span data-stu-id="c4934-233">Update the DeleteConfirmed Method</span></span>

<span data-ttu-id="c4934-234">在*InstructorController.cs*，删除`DeleteConfirmed`方法并插入以下代码在其位置。</span><span class="sxs-lookup"><span data-stu-id="c4934-234">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="c4934-235">此代码做出以下更改：</span><span class="sxs-lookup"><span data-stu-id="c4934-235">This code makes the following change:</span></span>

- <span data-ttu-id="c4934-236">如果教师被指定为任何部门的管理员，移除该部门教师分配。</span><span class="sxs-lookup"><span data-stu-id="c4934-236">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="c4934-237">不使用此代码，如果你试图删除一个教师已指定为某个部门的管理员将得到一个引用完整性错误。</span><span class="sxs-lookup"><span data-stu-id="c4934-237">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="c4934-238">此代码不会处理作为多个部门的管理员分配一个教师的情形。</span><span class="sxs-lookup"><span data-stu-id="c4934-238">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="c4934-239">在最后一个教程中，你将添加代码，以防止发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="c4934-239">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="c4934-240">向“创建”页添加办公室位置和课程</span><span class="sxs-lookup"><span data-stu-id="c4934-240">Add office location and courses to the Create page</span></span>

<span data-ttu-id="c4934-241">在*InstructorController.cs*，删除`HttpGet`和`HttpPost``Create`方法，然后在它们的位置添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4934-241">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>


[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="c4934-242">此代码将类似于你看到的针对编辑方法只不过最初没有课程均被选中。</span><span class="sxs-lookup"><span data-stu-id="c4934-242">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="c4934-243">`HttpGet` `Create`方法调用`PopulateAssignedCourseData`方法不是因为可能存在但在选择的课程，以便提供为空集合`foreach`（否则查看代码将引发空引用异常的视图中的循环).</span><span class="sxs-lookup"><span data-stu-id="c4934-243">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="c4934-244">HttpPost 创建方法将添加到模板代码检查有验证错误，向数据库添加新教师之前的课程导航属性的每个所选的过程。</span><span class="sxs-lookup"><span data-stu-id="c4934-244">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="c4934-245">课程会添加即使有模型错误以便模型错误 （例如，用户键控无效的日期） 时，以便当页则重新显示具有一条错误消息，将自动还原所做的任何课程选择。</span><span class="sxs-lookup"><span data-stu-id="c4934-245">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="c4934-246">请注意，为了能够向 `Courses` 导航属性添加课程，必须将该属性初始化为空集合：</span><span class="sxs-lookup"><span data-stu-id="c4934-246">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="c4934-247">除了在控制器代码中进行此操作之外，还可以在“讲师”模型中进行此操作，方法是将属性 getter 更改为不存在集合时自动创建集合，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="c4934-247">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="c4934-248">如果通过这种方式修改 `Courses` 属性，则可以删除控制器中的显式属性初始化代码。</span><span class="sxs-lookup"><span data-stu-id="c4934-248">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="c4934-249">在*Views\Instructor\Create.cshtml*、 office 位置中添加文本框和复选框的课程，雇佣日期字段后，和之前**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="c4934-249">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="c4934-250">粘贴代码后，可以修复换行符和缩进，如你此前编辑页。</span><span class="sxs-lookup"><span data-stu-id="c4934-250">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="c4934-251">运行创建页，然后添加一个教师。</span><span class="sxs-lookup"><span data-stu-id="c4934-251">Run the Create page and add an instructor.</span></span>

![使用课程创建教师](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<a id="transactions"></a>
## <a name="handling-transactions"></a><span data-ttu-id="c4934-253">处理事务</span><span class="sxs-lookup"><span data-stu-id="c4934-253">Handling Transactions</span></span>

<span data-ttu-id="c4934-254">中所述[基本 CRUD 功能教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)，默认情况下实体框架隐式实现事务。</span><span class="sxs-lookup"><span data-stu-id="c4934-254">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="c4934-255">有关方案，你需要更多的控制-例如，如果你想要包括在实体框架外部事务-中执行的操作，请参阅[使用事务](https://msdn.microsoft.com/data/dn456843)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="c4934-255">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="summary"></a><span data-ttu-id="c4934-256">总结</span><span class="sxs-lookup"><span data-stu-id="c4934-256">Summary</span></span>

<span data-ttu-id="c4934-257">你现在已经完成此简介使用相关数据。</span><span class="sxs-lookup"><span data-stu-id="c4934-257">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="c4934-258">到目前为止这些教程中使用过执行同步 I/O 代码。</span><span class="sxs-lookup"><span data-stu-id="c4934-258">So far in these tutorials you've worked with code that does synchronous I/O.</span></span> <span data-ttu-id="c4934-259">你可以进行应用程序通过实现异步代码中，更有效地使用 web 服务器资源和这便是你将在下一步的教程。</span><span class="sxs-lookup"><span data-stu-id="c4934-259">You can make the application use web server resources more efficiently by implementing asynchronous code, and that's what you'll do in the next tutorial.</span></span>

<span data-ttu-id="c4934-260">请在如何喜欢本教程的方式，我们可以提高上，留下反馈。</span><span class="sxs-lookup"><span data-stu-id="c4934-260">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="c4934-261">你还可以请求新主题[教我编写代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="c4934-261">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="c4934-262">在找不到其他实体框架资源的链接[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="c4934-262">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4934-263">[上一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="c4934-263">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
