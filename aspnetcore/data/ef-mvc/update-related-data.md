---
title: "ASP.NET 核心 MVC 与 EF 核心-更新与关联的数据-7 个 10"
author: tdykstra
description: "在本教程中你将更新的更新外键字段和导航属性的关联的数据。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/update-related-data
ms.openlocfilehash: 4085ca9340291f6ab594285360f3b65738699098
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="updating-related-data---ef-core-with-aspnet-core-mvc-tutorial-7-of-10"></a>EF Core 和 ASP.NET Core MVC 教程 —— 更新关联的数据 (7 个 10)

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 想要获取有关系列教程的信息，请参阅[第一个教程](intro.md)。

通过前面的教程已经学会了如何显示关联的数据;在本教程中你将通过更新外键字段和导航属性更新关联数据。

下图是一些您将使用到的页面。

![课程编辑页面](update-related-data/_static/course-edit.png)

![导师编辑页](update-related-data/_static/instructor-edit-courses.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>自定义课程创建页和编辑页

创建新的课程实体时，它必须与现有部门有关系。 为了便于实现这种关系，基架构建的代码包含了控制器方法以及创建和编辑视图中，试图中拥有用于选择部门的下拉列表。 下拉列表用于设置`Course.DepartmentID`外键属性，而这正是 Entity Framework 需要的，以便于加载`Department`与相应的部门实体的导航属性。 你将使用基架构建的代码，但将对其做略微的更改以添加错误处理和对下拉列表进行排序。

在*CoursesController.cs*、 删除原来的四个创建和编辑方法，将他们替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]

HttpPost 的 `Edit` 方法后，创建一个新方法来加载下拉列表的部门信息。

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]

`PopulateDepartmentsDropDownList`方法列出所有部门的信息并将他们按名称排序，为下拉列表创建`SelectList`集合，并将集合传递到该视图的`ViewBag`。 该方法接受可选`selectedDepartment`参数，调用代码通过该参数指定渲染该下拉列表时选定的项。 该视图会将"DepartmentID"传递到`<select>`标记帮助器，帮助器就会知道要在`ViewBag`对象中查找名称为"DepartmentID"的`SelectList`。

HttpGet的`Create`方法调用无参数的`PopulateDepartmentsDropDownList`，因为对应新课程的部门可能尚未建立所以不用设置选定的部门：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]

HttpGet`Edit`方法设置了选定的项，该项是正在编辑的课程所属部门的 ID :

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]

两个 HttpPost 方法：`Create`和`Edit`还包括在出现错误之后重新显示页面时设置选定项的代码。 这可确保在重新显示面以显示错误消息时，能保持选择的部门处于被选择状态。

### <a name="add-asnotracking-to-details-and-delete-methods"></a>添加 .AsNoTracking 到 Details 和 Delete 方法

若要优化课程详情页和删除页的性能，在`Details`和 HttpGet `Delete`方法中调用`AsNoTracking`。

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]

### <a name="modify-the-course-views"></a>修改课程视图

在*Views/Courses/Create.cshtml*中，添加"Select Department"选项到**Department**下拉列表中，将标题从**DepartmentID**改为**Department**，并添加一条验证消息。

[!code-html[Main](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]

在*Views/Courses/Edit.cshtml*中，对部门字段作相同的更改。

另外在*Views/Courses/Edit.cshtml*中，**Title**字段之前添加课程编号字段。 因为课程编号是为主键，它只用于显示不能对其更改。

[!code-html[Main](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]

编辑视图中的课程编号存在一个隐藏的字段 (`<input type="hidden">`) 。 添加`<label>`标记帮助器不会不需要隐藏字段，因为当用户单击**编辑**页上的**Save**时，隐藏字段的存在使得课程编号不会存在于被发布的数据中。

在*Views/Courses/Delete.cshtml*、 在顶部添加课程编号字段并将部门 ID 更改为部门名称。

[!code-html[Main](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]

在*Views/Courses/Details.cshtml*中，作相同的更改。

### <a name="test-the-course-pages"></a>测试课程页面

运行应用程序中，选择**Course**选项卡，单击**Create New**，然后输入新的课程数据：

![课程创建页](update-related-data/_static/course-create.png)

单击**Create**。 课程索引页会在列表中显示新添加的课程。 索引页列表中的部门名称来自于导航属性，显示已正确建立关系。

课程索引页中的课程上单击**Edit**。

![课程编辑页面](update-related-data/_static/course-edit.png)

更改页面上的数据，然后单击**Save**。 课程索引页会显示已更新的课程数据。

## <a name="add-an-edit-page-for-instructors"></a>添加导师编辑页面

编辑一个导师记录时，你想能够同时编辑分配给导师的办公室。 Instructor 实体和 OfficeAssignment 实体有一对零或者一对一的关系，这意味着你的代码必须处理以下情况：

* 如果用户删除办公室分配，并且最初具有一个值，则删除 OfficeAssignment 实体。

* 如果用户输入办公室分配值，它最初值为空，则创建一个新的 OfficeAssignment 实体。

* 如果用户更改一个办公室分配的值，更改现有 OfficeAssignment 实体中的值。

### <a name="update-the-instructors-controller"></a>更新导师控制器

在*InstructorsController.cs*，更改 HttpGet`Edit` 方法中的代码，以便它加载 Instructor 实体的`OfficeAssignment`导航属性并调用`AsNoTracking`:

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]

将 HttpPost`Edit` 方法替换为以下代码用于更新办公室分配：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]

该代码执行以下任务：

-  方法名称改为`EditPost`因为现在签名和为 HttpGet`Edit`方法相同 (使用`ActionName`属性表示仍使用`/Edit/`URL )。

-  使用预先加载从数据库获取当前 Instructor 实体的`OfficeAssignment`导航属性。 这与HttpGet`Edit`方法相同。

-  使用模型联编程序中的值更新检索到的 Instructor 实体。 `TryUpdateModel`重载方法将你想要包括的属性添加到白名单。 这可以防止过度发布（参阅[第二个教程](crud.md)）。

    <!-- Snippets do not play well with <ul> [!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=241-244)] -->

    ```csharp
    if (await TryUpdateModelAsync<Instructor>(
        instructorToUpdate,
        "",
        i => i.FirstMidName, i => i.LastName, i => i.HireDate, i => i.OfficeAssignment))
    ```
    
-   如果办公室地址为空，将 Instructor.OfficeAssignment 属性设为 null，以便删除 OfficeAssignment 表中的关联的行。

    <!-- Snippets do not play well with <ul>  "intro/samples/cu/Controllers/InstructorsController.cs"} -->

    ```csharp
    if (String.IsNullOrWhiteSpace(instructorToUpdate.OfficeAssignment?.Location))
    {
        instructorToUpdate.OfficeAssignment = null;
    }
    ```

- 将所做的更改保存到数据库。

### <a name="update-the-instructor-edit-view"></a>更新导师编辑页面

在*Views/Instructors/Edit.cshtml*，在**Save**按钮之前添加新字段以编辑办公室地址：

[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]

运行应用程序，选择**Instructors**选项卡，并依次点击**Edit**。 更改**Office Location**单击**Save**。

![导师编辑页](update-related-data/_static/instructor-edit-office.png)

## <a name="add-course-assignments-to-the-instructor-edit-page"></a>将课程分配添加到导师编辑页

导师可以教授任意数量的课程。 现在你将增强导师编辑页的功能，添加一组复选框用于更改课程分配，如下图所示：

![课程导师编辑页](update-related-data/_static/instructor-edit-courses.png)

当然，Instructor 实体和 Course 实体之间是多对多的关系。 若要添加和删除关系，你添加和删除 CourseAssignments 联接实体集中的实体。

一组的复选框构成的UI使你能够更改课程和导师之间的分配关系。 复选框显示了数据库中的每个课程，已分配给当前导师的课程会自动选中。 用户可以选择或清除复选框来更改课程分配。 如果课程数很大，你将可能想要使用不同的方法在视图中显示数据，但操作联接实体创建或删除关系的方法是相同的。

### <a name="update-the-instructors-controller"></a>更新导师控制器

若要给视图复选框列表提供数据，可以使用视图模型类。

在*SchoolViewModels*文件夹中创建*AssignedCourseData.cs*，并将原有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

在*InstructorsController.cs*中，将 HttpGet`Edit`方法替换为以下代码。 高亮代码显示了所做的更改。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]

该代码为`Courses`导航使用了预先加载并调用新创建的`PopulateAssignedCourseData`方法，该方法通过`AssignedCourseData`视图模型类为复选框序列提供信息。

`PopulateAssignedCourseData`方法中的代码使用视图模型类读取所有课程实体，加载课程列表。代码接着检查每个课程是否存在于导师`Courses`导航属性中。 若想在检查某一课程是否已经分配给导师时高效检索，可以将已分配给导师的课程放入`HashSet`集合。 分配给该导师的课程的`Assigned`属性设置为 true 。 视图将使用此属性来确定哪些复选框必须显示为选定状态。 最后，该列表传递给中的视图的`ViewData`。

接下来，添加用户单击**Save**时执行的代码。 将`EditPost`方法替换为以下代码，并添加一个新方法来更新`Instructor` 实体内的 `Courses` 导航属性。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]

现在的方法签名不同于 HttpGet`Edit`方法，所以方法名称可以从`EditPost`改回`Edit`。

由于该视图不包含课程实体的集合，模型联编程序不能自动更新`CourseAssignments`导航属性。 因而应该在新创建的`UpdateInstructorCourses`方法中更新`CourseAssignments`导航属性，而不是使用模型联编程序。 所以你需要在模型绑定中去除`CourseAssignments`的属性。 这不需要对调用`TryUpdateModel`的代码作任何更改因为您正在使用重载白名单而且`CourseAssignments`并不在包括列表中。

如果没有复选框被选中，`UpdateInstructorCourses`会使用空集合初始化`CourseAssignments`导航属性并返回：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]

然后循环访问数据库中的所有课程，并对比当前在视图中选择的课程和分配给该导师的课程。 为了便于高效的查找，后面的两个集合都存储在`HashSet`中。

如果某一课程的复选框被选中了，但课程不在`Instructor.CourseAssignments`导航属性中，该课程会添加到导航属性中。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]

如果某一课程复选框未被选中，但课程在`Instructor.CourseAssignments`导航属性中，会从导航属性删除该课程。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]

### <a name="update-the-instructor-views"></a>更新导师视图

在*Views/Instructors/Edit.cshtml*中，通过在**Office**字段的`div`之后**Save**按钮之前添加以下代码以添加**Course**复选框组。

<a id="notepad"></a>
> [!NOTE] 
> 当你将代码粘贴到 Visual Studio 时，分行将更改，这样会分割代码。可以使用 Ctrl + Z 撤消自动格式化。这将修复分行错误，使它们看起来像这里的代码。 代码缩进不一定是完美的但`@</tr><tr>`， `@:<td>`， `@:</td>`，和`@:</tr>`行都必须在单独的行中，如果不这样做会抛出运行时错误。 可以按 tab 键三次来整理了新代码与原有代码。

[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]

代码创建了一个 HTML 表格，包含三列。 每列由复选框，课程编号和课程名称组成。 每个复选框的名称都相同 ("selectedCourses")，使得模型联编程序指导他们是一组的。 每个复选框的值设置为`CourseID`的值。 页面发布时，模型联编程序会将包含选定课程信息的数组传递给控制器。

当复选框首次渲染时，分配给该导师的课程会显示为被选中状态。

运行应用程序中，选择**Instructors**选项卡卡，然后单击**Edit**以查看一个导师的**编辑**页。

![课程导师编辑页](update-related-data/_static/instructor-edit-courses.png)

更改课程分配并保存。 所做的更改会反映在索引页面中。

> [!NOTE] 
> 用此处编辑导师课程数据的方法适用于有限数量的课程。 对于大量的课程集合，会需要不同的 UI 界面以及不同的更新方法。

## <a name="update-the-delete-page"></a>更新删除页

在*InstructorsController.cs*，删除`DeleteConfirmed`方法并在原来的位置插入以下代码。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]

此代码进行以下更改：

* 为`CourseAssignments`导航属性执行预先加载。必须有这步操作否则 EF 不清楚与`CourseAssignment`关联的实体然后就不能将其删除。若要避免在此处读取它们你可以在数据库中配置级联删除。

* 如果要删除的导师被指定为某些部门的管理员，则将部门与该导师的分配关系移除。

## <a name="add-office-location-and-courses-to-the-create-page"></a>将办公室地址和课程添加到创建页

在*InstructorsController.cs*中，删除 HttpGet 和 HttpPost`Create`方法，然后在原来位置添加以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]

除了最初没有选中课程的情况，此代码和`Edit`方法基本类似。 HttpGet`Create`方法调用`PopulateAssignedCourseData`方法不是因为需要存在选择的课程，而是为了给视图中的`foreach` 循环提供空集合（否则视图代码将抛出空引用异常）。

HttpPost`Create`方法在检查验证错误和向数据库添加新导师之前将每个选定的课程添加到`CourseAssignments`导航属性。即使模型有错误也会将课程添加进导航属性中所以当模型错误时（例如，用户输入一个无效的日期）会重新显示包括错误消息的页面，然后自动还原对课程选择所做的任何更改。

请注意，若要添加课程到`CourseAssignments`导航属性，你必须将该导航属性初始化为空集合：

```csharp
instructor.CourseAssignments = new List<CourseAssignment>();
```

在控制器代码中作为此操作的替代方法，你可以通过更改导师模型属性的 getter 在集合不存在时自动创建集合，如下所示：

```csharp
private ICollection<CourseAssignment> _courseAssignments;
public ICollection<CourseAssignment> CourseAssignments
{
    get
    {
        return _courseAssignments ?? (_courseAssignments = new List<CourseAssignment>());
    }
    set
    {
        _courseAssignments = value;
    }
}
```

如果你以这种方式修改`CourseAssignments`属性，可以删除控制器中的显式初始化属性的代码。

在*Views/Instructor/Create.cshtml*中、 在提交按钮之前为课程添加办公室地址文本框和复选框。 跟编辑页类似，[修复 Visual Studio 粘贴代码时的格式问题](#notepad)。

[!code-html[Main](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]

运行应用程序并创建一个导师进行测试。 

## <a name="handling-transactions"></a>处理事务

如[CRUD 教程](crud.md)中所述， Entity Framework 隐式实现事务。 在你需要更多的控制场景，-例如，如果你想要在 Entity Framework 外部中执行事务操作，请参阅[事务](https://docs.microsoft.com/ef/core/saving/transactions)。

## <a name="summary"></a>摘要

你现在已经完成使用关联的数据的教程。 在下一步的教程中，你将了解如何处理并发冲突。

>[!div class="step-by-step"]
[上一页](read-related-data.md)
[下一页](concurrency.md)  
