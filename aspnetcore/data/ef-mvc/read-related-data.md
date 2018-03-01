---
title: "读取相关的数据 - EF Core 和 ASP.NET Core MVC 教程（第 6 部分，共 10 部分）"
author: tdykstra
description: "本教程将读取并显示相关的数据，即实体框架加载到导航属性中的数据。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/read-related-data
ms.openlocfilehash: 58b05587458aacad1a633a04f0359a4d2a3605a3
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="reading-related-data---ef-core-with-aspnet-core-mvc-tutorial-6-of-10"></a>读取相关的数据 - EF Core 和 ASP.NET Core MVC 教程（第 6 部分，共 10 部分）

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 Web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC Web 应用程序。有关此教程系列的信息，请参阅[此系列中的第一个教程](intro.md)。

前面的教程完成了学校数据模型。本教程将读取并显示相关数据，即实体框架加载到导航属性中的数据。

下图显示了您将使用的页。

![课程索引页](read-related-data/_static/courses-index.png)

![教师索引页](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a>预先加载、显式加载、延迟加载相关数据

对象关系映射 (ORM) 软件（如 Entity Framework ）可以通过多种方式将相关数据加载到实体的导航属性中：

* 预先加载。读取实体时，会检索与之相关的数据。这通常会导致执行一个检索所有必需数据的联接查询。可以通过`Include`和`ThenInclude`方法在 Entity Framework Core 中指定预先加载。

  ![预先加载示例](read-related-data/_static/eager-loading.png)

  可以使用独立的查询检索某些数据，EF会“适配”导航属性。也就是说，EF 会自动将独立检索的实体添加到之前已检索实体的导航属性的相应位置中。对于检索相关数据的查询，可以使用`Load`方法而不是使用返回列表或对象的方法（如`ToList`或`Single`）。

  ![单独的查询示例](read-related-data/_static/separate-queries.png)

* 显式加载。第一次读取实体时，不检索相关数据。请编写代码，根据需要检索相关数据。显式加载跟使用独立查询的预先加载类似，会将多个查询发送到数据库。不同之处在于，使用显式加载时，代码指定要加载的导航属性。 在

Entity Framework Core 1.1 中，可以使用`Load`方法执行显式加载。例如: 

  ![显式加载示例](read-related-data/_static/explicit-loading.png)

* 延迟加载。第一次读取实体时，不检索相关数据。但是，第一次尝试访问导航属性时，将自动检索该导航属性所需的数据。每次尝试从一个从未访问过的导航属性获取数据时，会发送查询到数据库。Entity Framework Core 1.0 不支持延迟加载。

### <a name="performance-considerations"></a>性能注意事项

如果你知道你需要每个已检索实体的相关数据，则预先加载通常性能最佳，因为数据库执行单个查询通常比执行用于检索每个实体的多个独立查询效率更高。例如，假设每个系有十个相关的课程。预先加载所有相关数据只需要进行一次（联接）查询，只与数据库进行一次通信。对每个系的课程分开进行查询则需要与数据库进行十一次通信。当延迟较高时，额外的数据库通信会对性能造成不利影响。
另一方面，在某些情况下的单独查询会更加高效。在查询中预先加载所有相关数据会导致生成一个非常复杂的联接查询语句，SQL Server 无法高效地处理这条查询语句。或者，如果只需要访问要处理的实体集的一部分的实体的导航属性，单独查询可能会更加高效，因为预先加载所有内容所检索的数据比需要的多。如果性能非常重要，最好测试这两种方式的性能，以便做出最佳选择。

## <a name="create-a-courses-page-that-displays-department-name"></a>创建显示部门名称的课程页

课程实体包括一个包含系实体的导航属性，该系实体属于分配了课程的系。若要在课程列表中显示分配的系的名称，需要从`Course.Department`导航属性的系实体中获取 Name 属性。

为“课程”实体类型创建名为 CourseController 的控制器，对**使用实体框架的带视图的 MVC 控制器**支架使用相同的选项，该支架是此前为“学生”控制器创建的，如下图所示：

![添加课程控制器](read-related-data/_static/add-courses-controller.png)

打开 *CoursesController.cs* 并检查`Index`方法。自动支架使用`Include`方法

将`Department`导航属性指定为预先加载。

将`Index`方法替换为以下代码，对返回课程实体的`IQueryable`使用更合适的名称 (`courses`而不是`schoolContext`)：

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_RevisedIndexMethod)]

打开 *Views/Courses/Index.cshtml*，将模板代码替换为以下代码。突出显示了所做的更改：

[!code-html[](intro/samples/cu/Views/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

你已对基架代码进行以下更改：

* 将标题从 Index 更改为 Courses。

* 添加了 **Number** 列以显示`CourseID`属性值。默认情况下，支架代码不会显示主键，因为通常主键对最终用户来说是无意义的。而在此示例中，主键是有意义的，因此需要显示。

* 更改了用于显示系名称的 **Department** 列。该代码显示加载到`Department`导航属性的系实体的`Name`的属性：

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

运行应用并选择“课程”****选项卡，查看包含系名称的列表。

![课程索引页](read-related-data/_static/courses-index.png)

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a>创建显示课程和注册的教师页面

在此部分，你将为 Instructor 实体创建控制器和视图，用于显示“教师”页：

![教师索引页](read-related-data/_static/instructors-index.png)

此页通过以下方式读取和显示相关的数据：

* 教师列表显示来自 OfficeAssignment 实体的相关数据。Instructor 和 OfficeAssignment 实体是一对零或一对一的关系。将对 OfficeAssignment 实体使用预先加载。如前所述，在需要主表的所有已检索行的相关数据时，预先加载通常更高效。在此示例中，需要显示所有已显示教师的办公室分配情况。

* 当用户选择一个教师时，会显示相关的“课程”实体。“教师”实体和“课程”实体是多对多的关系。将对“课程”实体及其相关的“系”实体使用预先加载。在这种情况下，因为只需要所选教师的课程，单独查询可能会更高效。但是，此示例演示了如何使用预先加载方式来加载本身是导航属性中的实体内的导航属性。

* 当用户选择某一课程时，会显示来自“注册”实体集的相关数据。“课程”实体和“注册”实体是一对多关系。将对“注册”实体及其相关的“学生”实体使用单独查询。

### <a name="create-a-view-model-for-the-instructor-index-view"></a>创建“教师索引”视图的视图模型

“教师”页显示三个不同表的数据。因此，你将创建包含三个属性的视图模型，每个属性保存一个表中的数据。

在 *Models/SchoolViewModels* 文件夹中创建 *InstructorIndexData.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="create-the-instructor-controller-and-views"></a>创建“教师”控制器和视图

创建一个教师控制器具有 EF 读/写操作，如下面的插图中所示：

![添加教师控制器](read-related-data/_static/add-instructors-controller.png)

打开 *InstructorsController.cs*，为 Viewmodel 命名空间添加 using 语句：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Using)]

将 Index 方法替换为以下代码，以便预先加载相关数据并将其置于视图模型中。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EagerLoading)]

该方法接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)。它们分别提供所选教师和所选课程的 ID 值。参数由页面上的“选择”****超链接提供。

代码首先创建视图模型的实例并向其中放置教师列表。该代码将`Instructor.OfficeAssignment`和`Instructor.CourseAssignments`导航属性指定为预先加载。在`CourseAssignments`属性中加载了`Course`属性，同时在`Course`属性中加载了`Enrollments`和`Department`属性，接着在每个`Enrollment`实体中加载了`Student`属性。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude)]

由于视图始终需要 OfficeAssignment 实体，在同一查询中提取会更加高效。在网页中选择一个教师时需要课程实体，因此仅当选择了课程的页面比没有选择课程的页面显示次数更多时，单个查询才比多个查询更高效。

代码重复了`CourseAssignments`和`Course`，因为你需要`Course`中的两个属性。`ThenInclude`调用的第一个字符串用于获取`CourseAssignment.Course`、`Course.Enrollments`和`Enrollment.Student`。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=3-6)]

此时在代码中，另一个`ThenInclude`将用于`Student`的导航属性，而这个属性是不需要的。但是，调用 `Include` 会重新从`Instructor`属性开始，因此必须再次访问该链，这次请指定`Course.Department`而非`Course.Enrollments`。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=7-9)]

选择一个教师时，会执行以下代码。所选教师从视图模型中的教师列表检索。然后，将使用该教师`CourseAssignments`导航属性中的课程实体填充视图模型的`Courses`属性。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=56-62)]

`Where`方法将返回一个集合，但在此示例中，传递到该方法的条件导致仅返回单个 Instructor 实体。`Single`方法将集合转换为单个 Instructor 实体，使你可以访问该实体的`CourseAssignments`属性。`CourseAssignments`属性包含`CourseAssignment`实体，你只需其中的相关`Course`实体。

知道某个集合将只有一个项时，可以对该集合使用`Single`方法。如果传递的集合为空或有多个项，`Single`方法会引发异常。替代的方法是`SingleOrDefault`，它在集合为空时返回默认值 (在此示例中为 null)。但是，在此示例中它仍会引发异常（在尝试查找 null 引用的`Courses`属性时引发），而异常消息并不会太清楚地指出问题的原因。调用`Single`方法，还可以传入 Where 条件，而不必单独调用`Where`方法：

```csharp
.Single(i => i.ID == id.Value)
```

而不是：

```csharp
.Where(I => i.ID == id.Value).Single()
```

接下来，如果选择一门课程，则会从视图模型中的课程列表检索所选课程。然后，视图模型的`Enrollments`属性中会填充该课程的`Enrollments`导航属性中的“注册”实体。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=64-69)]

### <a name="modify-the-instructor-index-view"></a>修改“教师索引”视图

在 *Views/Instructors/Index.cshtml* 文件中，将模板代码替换为以下代码。所做的更改会突出显示。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=1-64&highlight=1,3-7,15-19,24,26-31,41-54,56)]

你对现有代码做出以下更改：

* 将模型类改为`InstructorIndexData`。

* 将页标题从“索引”****改为“教师”****。

* 仅当`item.OfficeAssignment`不为 null 时，才添加用于显示`item.OfficeAssignment.Location`的 **Office** 列。（由于这是一对一或一对零的关系，因此可能没有相关的 OfficeAssignment 实体。）

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* 添加 **Course** 列，用于显示每个教师讲授的课程。有关此 Razor 语法的详细信息，请参阅[使用`@:`进行显式行转换](xref:mvc/views/razor#explicit-line-transition-with-)。

* 添加可将`class="success"`动态添加到所选教师的`tr`元素的代码。这将使用 Bootstrap 类设置所选行的背景色。

  ```html
  string selectedRow = "";
  if (item.ID == (int?)ViewData["InstructorID"])
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* 在每个行中其他链接之前添加标记为“选择”****的新的超链接，以便将所选教师的 ID 发送到`Index`方法。

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

运行应用并选择“教师”****选项卡。该页面会显示相关的 OfficeAssignment 实体的 Location 属性，而在没有相关的 OfficeAssignment 实体时，则会显示空的表单元格。

![未选择任何项教师索引页](read-related-data/_static/instructors-index-no-selection.png)

在 *Views/Instructors/Index.cshtml* 文件中结束表元素后（文件末尾），添加以下代码。此代码用于显示与所选教师相关的课程的列表。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=66-101)]

此代码读取视图模型的`Courses`属性，以便显示课程列表。它还提供一个“选择”****超链接，用于将所选课程的 ID 发送到`Index`操作方法。

刷新页面并选择一位教师。此时会看到一个网格，其中显示分配给所选教师的课程。每个课程都会看到相应系的名称。

![选择教师索引页教师](read-related-data/_static/instructors-index-instructor-selected.png)

在刚添加的代码块之后，添加以下代码。这样就会显示一个注册了所选课程的学生的列表。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=103-125)]

此代码读取视图模型的“注册”属性，以便显示注册了该课程的学生的列表。

再次刷新页面并选择一位教师。然后选择一个课程，查看已注册学生的列表及其分数。

![教师索引页教师和所选课程](read-related-data/_static/instructors-index.png)

## <a name="explicit-loading"></a>显式加载

在 *InstructorsController.cs* 中检索教师列表时，已将`CourseAssignments`导航属性指定为预先加载。

假设你预期用户只是偶尔查看所选教师和课程的注册信息。在这种情况下，可能只需在收到请求时才加载注册数据。若要查看显式加载的示例，请将`Index`方法替换为以下代码，以便删除针对注册的预先加载，改为显式加载该属性。代码更改处已突出显示。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ExplicitLoading&highlight=23-29)]

新代码从检索教师实体的代码中删除了针对注册数据的 *ThenInclude* 方法调用。如果选择了教师和课程，则突出显示的代码会检索所选课程的“注册”实体，以及每个注册的“学生”实体。

现在请运行应用，转到“教师索引”页，你会看到页面的显示内容跟之前没有任何区别，虽然已经更改了数据检索方式。

## <a name="summary"></a>摘要

你现在已将预先加载与单个查询和多个查询配合使用，将相关数据读取到了导航属性中。下一教程介绍如何更新相关数据。

>[!div class="step-by-step"]
>[上一页](complex-data-model.md)
>[下一页](update-related-data.md)  
