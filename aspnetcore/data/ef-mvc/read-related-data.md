---
title: "ASP.NET 核心 MVC 与 EF 核心-读取关联的数据-10 6"
author: tdykstra
description: "在本教程中将读取并显示关联的数据-即，实体框架将加载到导航属性的数据。"
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
# <a name="reading-related-data---ef-core-with-aspnet-core-mvc-tutorial-6-of-10"></a>EF  Core 和 ASP.NET  Core  MVC 教程 —— 读取关联数据 (6 的 10)

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 想要获取有关系列教程的信息，请参阅[第一个教程](intro.md)。

在前面的教程，你已经完成了 School 数据模型。 在本教程中，将读取并显示与实体关联的数据，也就是Entity Framework 将加载到导航属性的数据。

下图显示了您将使用的页。

![课程索引页](read-related-data/_static/courses-index.png)

![教师索引页](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a>预先加载、 显式加载、延迟加载关联数据

对象关系映射 (ORM) 软件（如 Entity Framework ）有以下几种将关联数据加载到实体的导航属性：

* 预先加载。 实体被读取时，会随之检索关联数据。 这通常会导致执行一个检索所有所需的数据的联接查询。 你通过`Include`和`ThenInclude`方法指定 Entity Framework  Core 使用预先加载。

  ![预先加载示例](read-related-data/_static/eager-loading.png)

  你可以使用独立的查询分别检索某些数据， EF会"适配"导航属性。也就是说，EF 会自动将独立检索的实体添加到之前已检索实体的导航属性中。你可以使用`Load`方法而不是使用返回的列表或对象的方法（如`ToList`或`Single`）来获取关联的数据。

  ![单独的查询示例](read-related-data/_static/separate-queries.png)

* 显式加载。 当第一次读取实体时，不检索关联数据。 编写代码在需要关联数据的时候才进行检索。 跟预先加载使用单独的查询类似，而显式加载会将多个查询发送到数据库。 不同之处在于，显式加载会指定要加载的导航属性。 在 Entity Framework  Core  1.1 中可以使用`Load`方法执行显式加载。 例如: 

  ![显式加载示例](read-related-data/_static/explicit-loading.png)

* 延迟加载。 当第一次读取实体时，不检索关联的数据。 但是，第一次尝试访问导航属性时，将自动检索该导航属性所需的数据。 每次尝试从一个从未访问过的导航属性获取数据时，会发送查询到数据库。  Entity Framework  Core  1.0 不支持延迟加载。

### <a name="performance-considerations"></a>性能注意事项

如果你知道每个已检索实体的关联数据，预先加载通常能提供最佳性能，因为数据库执行单个查询通常比执行用于检索每个实体的单独查询效率更高。 例如，假设每个部门都有十个关联的课程。 所有关联数据的预先加载只导致单个 （联接） 查询，只与数据库进行一次通信。 对于每个部门的课程进行单独的查询会导致与数据库进行十一次通信。 当延迟较高时，额外的数据库通信会对性能造成不利影响。

在某些情况下的单独查询会显得更加高效。 查询所有关联数据的预先加载会导致生成一个非常复杂的联接查询语句， SQL Server 无法高效地处理这条查询语句。 或者，如果只需要访问实体集的要处理的子集中的实体的导航属性，单独的查询可能会更加高效因为预先加载所有内容会检索比你需要的更多的数据。 如果性能非常重要，最好手动测试这两种方式的性能以便做出最佳选择。

## <a name="create-a-courses-page-that-displays-department-name"></a>创建显示部门名称的课程页

课程实体包括一个包含部门实体的导航属性，该部门实体用于保存分配的部门。 若要在课程列表中显示分配的部门的名称，你需要从`Course.Department`导航属性的部门实体中获取 Name 属性。

为课程的实体类型创建名为 CourseController 的控制器， 在**视图使用 Entity Framework 的 MVC 控制器**基架对话框使用此前生成学生控制器的相同选项生成 CoursesController 的控制器，如下图所示：

![添加课程控制器](read-related-data/_static/add-courses-controller.png)

打开*CoursesController.cs*并检查`Index`方法。 自动基架使用`Include`方法将`Department`导航属性指定为预先加载。

将`Index`方法替换为以下代码，为返回课程实体的`IQueryable`使用更合适的名称 (`courses`而不是`schoolContext`):

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_RevisedIndexMethod)]

打开*Views/Courses/Index.cshtml*和将模板代码替换为以下代码。 高亮代码显示了 所做的更改：

[!code-html[](intro/samples/cu/Views/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

你已对基架代码进行以下更改：

* 将标题从 Index 更改为 Courses 。

* 添加**Number**列显示`CourseID`属性值。 默认情况下，基架代码不会显示主键，因为通常主键对用户来说时无语义的。 而在Course的主键（CourseID）对用户时有意义的并且你也希望显示CourseID。

* 更改**Department**列用于显示部门名称。 该代码将显示加载到`Department`导航属性的部门实体的`Name`的属性：

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

运行应用并选择**Course**选项卡以查看使用部门名称的列表。

![课程索引页](read-related-data/_static/courses-index.png)

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a>创建显示课程和修读信息的导师页面

在此部分中，你会为 Instructor 实体创建控制器和视图用于显示导师页：

![教师索引页](read-related-data/_static/instructors-index.png)

此页并通过以下方式读取和显示关联的数据：

* 导师列表显示 OfficeAssignment 实体的关联数据。 教师和 OfficeAssignment 实体是一对零或一对一的关系。 你使用预先加载来加载 OfficeAssignment 实体。 如前面所述，当您需要主表检索所有行的关联数据时预先加载是通常更高效。 在这个案例中，你想要显示的是所有导师的 office 分配。

* 当用户选择一个教师时，会显示关联的课程实体。 教师和课程实体是多对多的关系。 使用预先加载方式来加载课程实体和其关联的部门实体。 在这种情况下，因为你只需要显示所选教师课程，单独查询可能会更高效。 但是，此示例演示了如何使用预先加载方式来加载本身是导航属性中的实体内的导航属性。

* 当用户选择某一课程时，会显示来自修读实体集的关联数据。 课程和修读实体是一对多关系。你将对注册实体和其关联的学生实体使用单独查询。

### <a name="create-a-view-model-for-the-instructor-index-view"></a>创建导师 Index 视图的视图模型

导师页显示三个不同表的数据。 因此，你将创建包含三个属性的视图模型，每个视图模型保存了其中一张表中的数据。

在*Models/SchoolViewModels*文件夹中，创建*InstructorIndexData.cs*文件并将原有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="create-the-instructor-controller-and-views"></a>创建导师控制器和视图

创建一个教师控制器具有 EF 读/写操作，如下面的插图中所示：

![添加教师控制器](read-related-data/_static/add-instructors-controller.png)

打开*InstructorsController.cs*和添加 using 语句引入 Viewmodel 命名空间：

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Using)]

将 Index 方法替换为以下代码以实现预先加载关联数据并将其置于视图模型中。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EagerLoading)]

该方法将接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`) 他们分别提供的所选的教师和所选的课程的 ID 值。 参数由页面上的**Select**链接提供。

代码首先创建视图模型的实例并向其中放置导师列表。 该代码指定`Instructor.OfficeAssignment`和`Instructor.CourseAssignments`导航属性为预先加载。 在`CourseAssignments`属性中，`Course`属性被加载，同时在`Course`属性中`Enrollments`和`Department`属性被加载，接着在每个`Enrollment`实体中`Student`被加载加载。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude)]

由于视图始终要求 OfficeAssignment 实体，在同一查询中提取会更加高效。 在 web 页中选择一个教师时会请求显示课程实体，仅当页面需要显示一个课程的情况更多时，单个查询多个查询更高效。

代码重复了`CourseAssignments`和`Course`因为你需要`Course`中的两个属性。 第一此调用`ThenInclude`用于获取`CourseAssignment.Course`， `Course.Enrollments`，和`Enrollment.Student`。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=3-6)]

此时，在代码中，另一个`ThenInclude`将用于导航属性的`Student`，而我们不需要这个属性。 接着对`Instructor`属性重新调用`Include`，因此必须再次链式执行，至此需要获取的是`Course.Department`而不是`Course.Enrollments`。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=7-9)]

当选择一个导师时，会执行下面的代码。 所选的导师从视图模型中的导师列表检索。 视图模型的`Courses`属性会接着从该教师`CourseAssignments`导航属性的课程实体中加载。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=56-62)]

`Where`方法将返回一个集合，但在这个例子下传方法限定了条件导致仅返回单个 Instructor 实体。 `Single`方法将集合转换为单个 Instructor 实体，使你可以访问该实体的`CourseAssignments`属性。 `CourseAssignments`属性包含`CourseAssignment`，在这里仅从`CourseAssignment`获取关联`Course`实体。

当你知道该集合的只有一项时可以使用`Single`方法。 如果集合为空或有多个项，`Single`方法会抛出异常。 替代`Single`的方法是`SingleOrDefault`，它返回默认值 (如果该集合为空则返回 null) 。 虽然`SingleOrDefault`解决了返回数量的问题，但在这个案例中仍会抛出异常 (尝试从 null 引用上查找`Courses`属性)，而异常消息并不能清楚地指出问题的原因。 当调用`Single`方法，你可以直接给`Single`方法传递 Where 条件，而不用单独调用`Where`方法：

```csharp
.Single(i => i.ID == id.Value)
```

而不是：

```csharp
.Where(I => i.ID == id.Value).Single()
```

接下来，如果选择一门课程，从视图模型中的课程列表检索所选的课程。 然后视图模型的`Enrollments`属性和该课程的`Enrollments`导航属性的修读实体一起加载。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=64-69)]

### <a name="modify-the-instructor-index-view"></a>修改导师 Index 视图

在*Views/Instructors/Index.cshtml*文件中，将模板代码替换为以下代码。 高亮代码显示了所做的更改。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=1-64&highlight=1,3-7,15-19,24,26-31,41-54,56)]

你对现有代码做出以下更改：

* 将模型类改为`InstructorIndexData`。

* 将页标题从**Index**改为**Instructors**。

* 添加**Office**列，当`item.OfficeAssignment`不为 null时显示`item.OfficeAssignment.Location`。 （由于导师和办公室分配时一对一或一对零的关系，因此一个导师可能没有关联的 OfficeAssignment 实体。）

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* 添加**Course**列显示每个教师讲授的课程。 有关[显式行转换与`@:`](xref:mvc/views/razor#explicit-line-transition-with-)的 razor 语法可以查看关联文档。

* 添加`class="success"`添加到所选教师的`tr`标签。 此设置对所选行使用 Bootstrap 的背景色。

  ```html
  string selectedRow = "";
  if (item.ID == (int?)ViewData["InstructorID"])
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* 在每个行中的其他链接之前添加**Select**链接标签，点击后会将所选的教师 ID 发送到`Index`方法。

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

运行应用并选择**Instructors**选项卡。一般页面会显示关联 OfficeAssignment 实体的 Location 属性，而如果没有关联 OfficeAssignment 实体时会显示空的单元格。

![未选择任何项教师索引页](read-related-data/_static/instructors-index-no-selection.png)

在*Views/Instructors/Index.cshtml*文件中table标签结束后 （在文件末尾）， 添加以下代码。 此代码用于显示与选中教师关联的课程列表。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=66-101)]

此代码读取视图模型中的`Courses`属性并将其显示出来。 它还提供了**Select**超链接，用于将所选课程 ID 发送到`Index`操作方法。

刷新页面并选择一个教师。 此时你会看到一个网格，用于显示分配给所选教师的课程，对于每个课程中，你将看到其所属部门的名称。

![选择教师索引页教师](read-related-data/_static/instructors-index-instructor-selected.png)

在你刚添加代码块之后，添加下面的代码。 当选中一个课程时，将显示修读该课程的学生的列表。

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=103-125)]

此代码读取了视图模型中的修读属性用于显示修读某课程的学生列表。

再次刷新页面并选择一个导师。 然后选择一个课程，接着查看的已修读该课程的学生和其评级。

![教师索引页教师和所选课程](read-related-data/_static/instructors-index.png)

## <a name="explicit-loading"></a>显式加载

*InstructorsController.cs*中检索讲师列表时，指定`CourseAssignments`导航属性为预先加载。

假设你预期用户只是偶尔查看所选的教师和课程中的修读信息。 在这种情况下，你可能想要的是修读数据在被请求时才会加载。 若要查看使用显式加载的示例，请将`Index`方法替换为以下代码，这将为修读信息移除预先加载并显式加载该属性。 高亮代码显示了更改。

[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ExplicitLoading&highlight=23-29)]

新代码删除了检索 instructor 实体读取修读数据时调用的*ThenInclude*方法的代码。 如果选择了教师和课程，高亮代码会检索所选课程的修读实体和每个修读了该课程的学生实体。

运行应用程序，转到导师 Index 页和显示的内容跟之前没有任何区别，不过已经更改了检索数据的方式。

## <a name="summary"></a>摘要

你现在已经会使用单个查询实现预先加载以及使用多个查询将关联数据读入到导航属性。 在下一个教程你将学习如何更新关联数据。

>[!div class="step-by-step"]
>[上一页](complex-data-model.md)
>[下一页](update-related-data.md)  
