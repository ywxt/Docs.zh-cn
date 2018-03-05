---
title: "更新相关的数据 - EF Core 和 ASP.NET Core MVC 教程（第 7 部分，共 10 部分）"
author: tdykstra
description: "本教程将通过更新外键字段和导航属性来更新相关的数据。"
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
# <a name="updating-related-data---ef-core-with-aspnet-core-mvc-tutorial-7-of-10"></a>更新相关的数据 - EF Core 和 ASP.NET Core MVC 教程（第 7 部分，共 10 部分

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 Web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC Web 应用程序。有关教程系列的信息，请参阅[此系列中的第一个教程](intro.md)。

前面的教程已显示相关的数据；本教程将通过更新外键字段和导航属性更新相关的数据。

下图显示了一些将使用的页面。

![课程编辑页面](update-related-data/_static/course-edit.png)

![教师编辑页](update-related-data/_static/instructor-edit-courses.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>自定义课程创建页和编辑页

创建新的课程实体时，该实体必须与现有系相关联。为了便于实现这种关联，基架代码包含了控制器方法以及创建和编辑视图，其中包括用于选择系的下拉列表。下拉列表用于设置 `Course.DepartmentID` 外键属性，而这正是实体框架需要的，目的是加载 `Department` 导航属性与相应的 Department 实体。你将使用基架代码，但需要对其略作更改以添加错误处理并对下拉列表排序。

在 *CoursesController.cs* 中删除四个创建和编辑方法，将其替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]

在`Edit`HttpPost 方法后创建一个新方法来加载下拉列表的系信息。

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]

`PopulateDepartmentsDropDownList`方法可以获取一个列表，其中包含按名称排序的所有系，可以为下拉列表创建`SelectList`集合，并将集合传递到`ViewBag`中的视图。该方法接受可选`selectedDepartment`参数，调用代码可通过该参数指定呈现该下拉列表时选定的项。该视图会将名称“DepartmentID”传递到`<select>`标记帮助器，帮助器就会知道在`ViewBag`对象中查找名为“DepartmentID”的`SelectList`。

HttpGet`Create`方法调用尚未设置选定项的`PopulateDepartmentsDropDownList`方法，因为尚未确定负责新课程的系：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]

HttpGet`Edit`方法根据系的 ID 设置选定的项，该系已被指定负责要编辑的课程：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]

`Create`和`Edit`的 HttpPost 方法还包括在出现错误之后重新显示页面时设置选定项的代码。这可确保在重新显示页面以显示错误消息时，选定的系仍处于选定状态。

### <a name="add-asnotracking-to-details-and-delete-methods"></a>添加 .AsNoTracking 到 Details 和 Delete 方法

若要优化“课程详细信息”页和“删除”页的性能，请在`Details`和 HttpGet `Delete`方法中添加`AsNoTracking`调用。

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]

	### <a name="modify-the-course-views"></a>修改“课程”视图

在 *Views/Courses/Create.cshtml* 中，将“选择系”选项添加到“系”****下拉列表中，将标题从 **DepartmentID** 更改为“系”****，并添加一条验证消息。

[!code-html[Main](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]

在 *Views/Courses/Edit.cshtml* 中，对“系”字段所做的更改与在 *Create.cshtml* 中所做的更改相同。

另外，请在 *Views/Courses/Edit.cshtml* 中的“标题”****字段之前添加课程编号字段。因为课程编号是主键，它只用于显示，不能对其进行更改。

[!code-html[Main](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]

“编辑”视图中的课程编号存在一个隐藏的字段 (`<input type="hidden">`) 。添加`<label>`标记帮助器不会导致不需要隐藏字段，因为当用户单击“编辑”****页上的“保存”****时，隐藏字段的存在使得课程编号不会包括在已发布的数据中。

在 *Views/Courses/Delete.cshtml* 的顶部添加课程编号字段并将系 ID 更改为系名称。

[!code-html[Main](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]

在 *Views/Courses/Details.cshtml* 中进行的更改与对 *Delete.cshtml* 所做的更改相同。

### <a name="test-the-course-pages"></a>测试“课程”页

运行应用，选择“课程”****选项卡，单击“新建”****，然后输入新课程的数据：

![课程创建页](update-related-data/_static/course-create.png)

单击“创建”****。“课程索引”页面随即显示，并且新课程已添加在列表中。“索引”页列表中的院系名称来自导航属性，表明已正确建立关系。

在“课程索引”页中的课程上，单击“编辑”****。

![课程编辑页面](update-related-data/_static/course-edit.png)

更改页面上的数据，然后单击“保存”****。含有更新后的课程数据的“课程索引”页面随即显示。

## <a name="add-an-edit-page-for-instructors"></a>添加讲师的编辑页面

编辑讲师记录时，有时希望能更新讲师的办公室分配。Instructor 实体和 OfficeAssignment 实体之间存在一对零或一对一的关系，这意味着代码必须处理以下情况：

* 如果用户清除了办公室分配，并且办公室分配最初具有一个值，则删除 OfficeAssignment 实体。

* 如果用户输入了办公室分配值，并且该值最初为空，则创建一个新的 OfficeAssignment 实体。

* 如果用户更改一个办公室分配的值，更改现有 OfficeAssignment 实体中的值。

### <a name="update-the-instructors-controller"></a>更新讲师控制器

在 *InstructorsController.cs* 中，更改 HttpGet`Edit`方法中的代码，使其加载 Instructor 实体的`OfficeAssignment`导航属性并调用`AsNoTracking`：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]

将 HttpPost`Edit`方法替换为以下代码，以便处理办公室分配更新：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]

该代码执行以下任务：

- 将方法名称更改为`EditPost`，因为现在的签名与 HttpGet`Edit`方法相同（`ActionName` 特性指定仍然使用 `/Edit/`URL）。

- 使用 `OfficeAssignment` 导航属性的预先加载从数据库获取当前的 Instructor 实体。此操作与在 HttpGet`Edit` 方法中进行的操作相同。

- 将检索出的 Instructor 实体更新为模型绑定器中的值。通过 `TryUpdateModel` 重载可以将想包括的属性列入到允许列表。这样可以防止[第二个教程](crud.md)中所述的过度发布。

    <!-- Snippets don't play well with <ul> [!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=241-244)] -->

    ```csharp
    if (await TryUpdateModelAsync<Instructor>(
        instructorToUpdate,
        "",
        i => i.FirstMidName, i => i.LastName, i => i.HireDate, i => i.OfficeAssignment))
    ```
    
- 如果办公室位置为空，请将 Instructor.OfficeAssignment 属性设置为 null，以便删除 OfficeAssignment 表中的相关行。

    <!-- Snippets do not play well with <ul>  "intro/samples/cu/Controllers/InstructorsController.cs"} -->

    ```csharp
    if (String.IsNullOrWhiteSpace(instructorToUpdate.OfficeAssignment?.Location))
    {
        instructorToUpdate.OfficeAssignment = null;
    }
    ```

- 将所做的更改保存到数据库。

### <a name="update-the-instructor-edit-view"></a>更新“讲师编辑”视图

在 *Views/Instructors/Edit.cshtml* 中，在“保存”****按钮之前的末尾处，添加一个用于编辑办公室位置的新字段：

[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]

运行应用，选择“讲师”****选项卡，然后单击讲师页面上的“编辑”****。更改“办公室位置”****，然后单击“保存”****。

![讲师编辑页](update-related-data/_static/instructor-edit-office.png)

## <a name="add-course-assignments-to-the-instructor-edit-page"></a>向“讲师编辑”页添加课程分配

讲师可能教授任意数量的课程。现在可以通过使用一组复选框来更改课程分配，从而增强“讲师编辑”页面的性能，如以下屏幕截图所示：

![课程讲师编辑页](update-related-data/_static/instructor-edit-courses.png)

Course 和 Instructor 实体之间是多对多的关系。若要添加和删除关系，可以向 CourseAssignments 联接实体集添加实体和从中删除实体。

用于更改讲师所对应的课程的 UI 是一组复选框。该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。用户可以通过选择或清除复选框来更改课程分配。如果课程的数量过大，建议使用其他方法在视图中呈现数据，但创建或删除关系的方法与操作联接实体的方法相同。

### <a name="update-the-instructors-controller"></a>更新讲师控制器

若要为复选框列表的视图提供数据，可使用视图模型类。

在 *SchoolViewModels* 文件夹中创建 *AssignedCourseData.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

在 *InstructorsController.cs* 中，将 HttpGet`Edit` 方法替换为以下代码。突出显示所做的更改。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]

该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。

`PopulateAssignedCourseData` 方法中的代码会读取所有 Course 实体，以便使用视图模型类加载课程列表。对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。为高效检查某门课程是否被分配给了讲师，可将分配给该讲师的课程放置于 `HashSet` 集合中。对于分配给讲师的课程，`Assigned` 属性设置为 true。视图将使用此属性来确定应将哪些复选框显示为选中状态。最后，该列表会被传递给 `ViewData` 中的视图。

接下来，添加用户单击“保存”****时执行的代码。将 `EditPost` 方法替换为以下代码，并添加一个新方法，用于更新 `Instructor` 实体的 `Courses` 导航属性。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]

现在的方法签名与 HttpGet`Edit` 方法不同，因此方法名称将从 `EditPost` 变回 `Edit`。

视图没有 Course 实体的集合，因此模型绑定器无法自动更新 `CourseAssignments` 导航属性。可在新的 `UpdateInstructorCourses` 方法中更新 `CourseAssignments` 导航属性，而不必使用模型绑定器。为此，需要从模型绑定中排除 `CourseAssignments` 属性。此操作无需对调用 `TryUpdateModel` 的代码进行任何更改，因为使用的是允许列表重载，并且 `CourseAssignments` 不包括在该列表中。

如果未选中任何复选框，则 `UpdateInstructorCourses` 中的代码将使用空集合初始化 `CourseAssignments` 导航属性，并返回以下内容：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]

之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。为便于高效查找，后两个集合存储在 `HashSet` 对象中。

如果某课程的复选框处于选中状态，但该课程不在 `Instructor.CourseAssignments` 导航属性中，则会将该课程添加到导航属性中的集合中。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]

如果某课程的复选框未处于选中状态，但该课程存在于 `Instructor.CourseAssignments` 导航属性中，则会从导航属性中删除该课程。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]

### <a name="update-the-instructor-views"></a>更新“讲师”视图

在 *Views/Instructors/Edit.cshtml* 中，通过在“办公室”****字段的 `div` 元素之后和“保存”****按钮的 `div` 元素之前添加以下代码，添加带有一系列复选框的“课程”****字段。

<a id="notepad"></a>
> [!NOTE] 
> 将代码粘贴到 Visual Studio 中时，换行符会发生更改，从而导致代码中断。按 Ctrl+Z 一次可撤消自动格式设置。这样可以修复换行符，使其看起来如此处所示。缩进不一定要完美，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@:</tr>` 行必须各成一行（如下所示），否则会出现运行时错误。选中新的代码块后，按 Tab 三次，使新代码与现有代码对齐。可在[此处](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)查看此问题的状态。

[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]

此代码将创建一个具有三列的 HTML 表。每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。所有复选框都具有相同的名称，即 selectedCourses，以告知模型绑定器将它们视为一组。每个复选框的值特性被设置为 `CourseID` 的值。发布页面时，模型绑定器会向控制器传递一个数组，其中只包括所选复选框的 `CourseID` 值。

这些复选框最开始呈现时，对于分配给讲师的课程的复选框，其特性处于选中状态。

运行应用，选择“讲师”****选项卡，然后单击讲师页面上的“编辑”****以查看“编辑”****页。

![课程讲师编辑页](update-related-data/_static/instructor-edit-courses.png)

更改某些课程分配并单击“保存”。所做的更改将反映在“索引”页上。

> [!NOTE] 
> 此处所使用的编辑讲师课程数据的方法适用于数量有限的课程。若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。

## <a name="update-the-delete-page"></a>更新删除页

在 *InstructorsController.cs* 中，删除 `DeleteConfirmed` 方法，并在其位置插入以下代码。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]

此代码进行以下更改：

* 对 `CourseAssignments` 导航属性执行预先加载。必须包括此内容，否则 EF 不知道相关的 `CourseAssignment` 实体，也不会删除它们。为避免在此处阅读它们，可以在数据库中配置级联删除。

* 如果要删除的讲师被指派为某些系的管理员，则需从这些系中删除该讲师分配。

## <a name="add-office-location-and-courses-to-the-create-page"></a>向“创建”页添加办公室位置和课程

在 *InstructorsController.cs* 中，删除 HttpGet 和 HttpPost`Create` 方法，然后在其位置添加以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]

此代码与 `Edit` 方法中所示内容类似，只是最开始未选择任何课程。HttpGet`Create` 方法调用 `PopulateAssignedCourseData` 方法不是因为可能有课程处于选中状态，而是为了在视图中为 `foreach` 循环提供空集合（否则该视图代码将引发空引用异常）。

检查是否存在验证错误并向数据库添加新讲师之前，HttpPost`Create` 方法会将每个选定课程添加到 `CourseAssignments` 导航属性。即使存在模型错误也会添加课程，因此出现模型错误（例如用户键入了无效的日期）并且页面重新显示并出现错误消息时，所作的任何课程选择都会自动还原。

请注意，为了能够向 `CourseAssignments` 导航属性添加课程，必须将该属性初始化为空集合：

```csharp
instructor.CourseAssignments = new List<CourseAssignment>();
```

除了在控制器代码中进行此操作之外，还可以在“讲师”模型中进行此操作，方法是将属性 getter 更改为不存在集合时自动创建集合，如以下示例所示：

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

如果通过这种方式修改 `CourseAssignments` 属性，则可以删除控制器中的显式属性初始化代码。

在 *Views/Instructor/Create.cshtml* 中，添加一个办公室位置文本框和课程的复选框，然后按“提交”按钮。与“编辑”页面中一样，[如果粘贴代码时 Visual Studio 重新设置了其格式，则修复该格式](#notepad)。

[!code-html[Main](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]

通过运行应用并创建讲师来进行测试。

## <a name="handling-transactions"></a>处理事务

如 [CRUD 教程](crud.md)中所述，实体框架隐式实现事务。如果需要更多控制操作（例如，如果想要在事务中包含在实体框架外部完成的操作），请参阅[事务](https://docs.microsoft.com/ef/core/saving/transactions)。

## <a name="summary"></a>摘要

处理相关数据的介绍至此已告一段落。下一个教程将介绍如何处理并发冲突。

>[!div class="step-by-step"]
[上一页](read-related-data.md)
[下一页](concurrency.md)  
