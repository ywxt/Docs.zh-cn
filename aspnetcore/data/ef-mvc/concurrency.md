---
title: "ASP.NET 核心 MVC 与 EF 核心-并发-8 的 10"
author: tdykstra
description: "本教程演示如何处理冲突，当多个用户在同一时间更新同一实体。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/concurrency
ms.openlocfilehash: c271488d4da72ba340f3617ac20c7b6da2574c69
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="handling-concurrency-conflicts---ef-core-with-aspnet-core-mvc-tutorial-8-of-10"></a>EF  Core 和 ASP.NET  Core  MVC 教程 —— 处理并发冲突 (8 / 10)

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 有关系列教程的详细信息，请参阅[第一个教程](intro.md)。

在前面教程中，您学会了如何更新相关数据。本教程将演示当多个用户在同一时间更新同一实体时如何处理冲突。

你将创建部门实体页面并处理并发错误。 下图为与部门相关的编辑和删除的页面，页面中还包含了发生并发冲突时提示的消息。

![部门编辑页](concurrency/_static/edit-error.png)

![部门删除页](concurrency/_static/delete-error.png)

## <a name="concurrency-conflicts"></a>并发冲突

当一个用户查看实体的数据并进行编辑，在该用户所做的更改写入数据库之前又有一个用户更新了实体数据，此时就会发生并发冲突。 如果不启用此类冲突的检测，任何人更新数据库都会覆盖其他用户所做的更改。 在某些应用程序中，这种操作带来的风险是可以接受的： 当只有有少量用户或少量更改同时发生，或者某些更改被覆盖不是特别重要，如果并发编程的开销超过其带来的好处。 那么，你不必为此应用程序处理并发冲突。

### <a name="pessimistic-concurrency-locking"></a>保守式并发 （锁定）

如果你的应用程序需要防止并发场景下意外丢失数据，其中一种方法就是使用数据库锁。 这种方法称为保守式并发。 例如，从数据库读取行之前，你请求的锁是只读或允许更新的。 如果在锁定行并进行更新时，不允许其他用户对该的只读或更新请求，因为它们将获取的数据时正在进行更改的数据的副本。 如果锁定一行用于只读，其他人也可以将其锁定用于只读但不能用于更新。

管理锁也有缺点。 它会使得编程上更加复杂。 它需要大量的数据库管理资源，并且当用于和应用程序增加时会导致性能问题。 出于这些原因，不是所有数据库管理系统都支持保守式并发。 并且 Entity Framework  Core 没有内置支持保守，因此本教程不向你展示如何实现它。

### <a name="optimistic-concurrency"></a>开放式并发

保守式并发的替代方法是开放式并发。 开放式并发意味着允许冲突并发发生，然后作出相应的反应。 例如，Jane 访问部门编辑页，并将英语部门的预算金额从 $350,000.00 变为 0.00 美元。

![将预算更改为 0](concurrency/_static/change-budget.png)

Jane 单击**保存**之前，John 访问同一页上，并将开始日期字段从 2007 年 9 月 1 日的更改为 2013 年 9 月 1 日。

![更改为 2013年的开始日期](concurrency/_static/change-date.png)

Jane 先单击**保存**，看到更改后浏览器返回到索引页面。

![更改为零的预算](concurrency/_static/budget-zero.png)

然后 John 单击**保存**，编辑页上的预算仍显示为 $350,000.00 。 接下来如何操作取决于如何处理并发冲突。

可选的操作包括：

* 你可以跟踪的用户修改的属性，并在数据库更新相应的列。

     在示例场景中，任何数据将不会丢失，因为两个用户更新了不同的属性。 下一次有人浏览英语部门，他们将看到 Jane 的零美元的预算和 John 的 2013 年 9 月 1 日开始日期。 这种更新方法可以减少可能导致数据丢失的冲突数，但如果对一个实体的同一属性进行竞争更改时它无法避免数据丢失。  Entity Framework 是否可以处理这种冲突取决于你是如何实现更新代码的。在一个 web 应用程序中通常是不现实的，因为它可能需要维护大量的状态，以便跟踪实体的所有原始属性值以及更改值。 维护大量的状态会影响应用程序性能，因为它不仅需要服务器资源也包括 web 页面本身 （如隐藏的字段） 或 cookie。

* 你可以让 John 的更改覆盖 Jane 的更改。

     下一次有人浏览英语部门时，他们将看到 2013 年 9 月 1 日和还原的 $350,000.00 值。 这称为*客户端优先*或*最后优先*方案。 （从客户端获得的所有值都优先于在数据库存储的值。）如本部分的简介中所述，如果您不执行任何并发处理的编码，这种方案将自动执行。

* 你可以防止 John 的更改更新到数据库中。

     通常情况下，将显示一条错误消息， 显示数据的当前状态并允许他重新应用他的更改。 这称为*存储优先*方案。 （数据存储值优先于客户端提交的值。）在本教程中，你将实现存储优先方案。 此方法可确保在用户没有收到发生什么的通知的情况下，不会覆盖任何更改。

### <a name="detecting-concurrency-conflicts"></a>检测并发冲突

您可以通过处理 Entity Framework 引发的`DbConcurrencyException`异常来解决冲突。 为了知道何时触发这些异常， Entity Framework 必须能够检测到冲突的发生。 因此，你必须正确配置数据库和数据模型。 有关启用冲突检测的选项包括：

* 在数据库表中，包括可以用于确定当行已更改的跟踪列。 然后，你可以配置 Entity Framework 可以在 Where 子句的 SQL 更新或删除命令中包含该列。

     跟踪列的数据类型通常是`rowversion`。 `rowversion`值是每次更新行时自动递增的序列号。 在 Update 或 Delete 命令中，Where 子句中包括跟踪列 （原始行的版本） 的原始值。 如果正在更新的行已由其他用户更改时`rowversion`列会不同于原始值，因此由于 Where 子句的存在 Update 或 Delete 语句找不到更新的行。 当 Entity Framework 找不到任何行被 Update 或 Delete 命令更新（即，受影响的行数为零） 时，这种现象会被 Entity Framework 认为是并发冲突。

* 配置 Entity Framework 使得在 Update 和 Delete 命令的 Where 子句中包括表中每个列的原始值。

     像第一个选项那样，如果行内的的数据在读取之后发生了更改 Where 子句不会返回任何行用于更新， Entity Framework 会认为发生了并发冲突。 对于有许多列的数据库表，此方法会导致臃肿的 Where 子句，并可能需要维护大量的状态。 如前文所述，保留大量的状态信息可能会影响应用程序性能。 因此通常不建议使用此方法，这不是本教程使用的方法。

     如果您想要实现这种并发的方法，则必须通过添加`ConcurrencyCheck`特性来标记实体中的所有非主键属性用于跟踪属性来实现并发性。 所做的更改使 Entity Framework 能够在 Update 和 Delete 语句的 SQL Where 子句中包含所有列的初始值。

本教程的其余部分中你会添加`rowversion`来跟踪部门实体的属性，创建一个控制器和视图，并进行测试以验证功能实现完全。

## <a name="add-a-tracking-property-to-the-department-entity"></a>将跟踪属性添加到部门实体

在*Models/Department.cs*，添加名为 RowVersion 的跟踪属性：

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Final&highlight=26,27)]

`Timestamp`属性指定此列将被包含在发送到数据库的 Update 和 Delete 命令的 Where 子句中。 该特性称为`Timestamp`是因为之前版本的 SQL Server 使用 SQL`timestamp`数据类型而不是 SQL`rowversion`数据类型。 .NET `rowversion`类型为字节数组。

如果想要使用 fluent API，则可以使用`IsConcurrencyToken`方法 (*Data/SchoolContext.cs*) 来指定跟踪属性，在下面的示例所示：

```csharp
modelBuilder.Entity<Department>()
    .Property(p => p.RowVersion).IsConcurrencyToken();
```

因为添加了一个属性，更改数据库模型，因此你需要执行一个迁移。

保存所做的更改和生成项目，然后在命令窗口中输入以下命令：

```console
dotnet ef migrations add RowVersion
```

```console
dotnet ef database update
```

## <a name="create-a-departments-controller-and-views"></a>创建部门控制器和视图

如你此前学生、 课程和教师一样搭建部门控制器和视图。

![基架部门](concurrency/_static/add-departments-controller.png)

在*DepartmentsController.cs*文件中，将出现的四个"FirstMidName"更改为"FullName"，以便部门管理员下拉列表将包含教师的完整名称而不是只是姓。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_Dropdown)]

## <a name="update-the-departments-index-view"></a>更新部门索引视图

基架引擎在索引视图中创建了 RowVersion 列，然而我们不希望显示该字段。

将*Views/Departments/Index.cshtml*替换为以下代码。

[!code-html[Main](intro/samples/cu/Views/Departments/Index.cshtml?highlight=4,7,44)]

该代买将标题改为"Department"、 删除 RowVersion 列，然后显示管理员的完整姓名而不仅仅显示管理员的名字。

## <a name="update-the-edit-methods-in-the-departments-controller"></a>更新部门控制器中的编辑方法

在 HttpGet`Edit`方法和`Details`方法中，添加`AsNoTracking`。 在 HttpGet`Edit`方法，将管理员设置为预先加载。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_EagerLoading&highlight=2,3)]

将 HttpPost`Edit`方法替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_EditPost)]

代码首先尝试读取要更新的部门。 如果`SingleOrDefaultAsync`方法返回的是 null，部门已被另一个用户删除。 在这种情况下代码使用已发布的表单值创建一个新的部门实体，以便编辑页可以重新显示并显示错误消息。 当只需要显示错误消息，而不重新显示部门字段的消息时，你不需要重新创建部门实体。

视图在隐藏的字段中保存原来的`RowVersion`值，该方法通过`rowVersion`参数接收视图中的值。 在调用`SaveChanges`之前，你必须将原始的`RowVersion`属性值放在实体的`OriginalValues`的集合中。

```csharp
_context.Entry(departmentToUpdate).Property("RowVersion").OriginalValue = rowVersion;
```

然后在 Entity Framework 创建 SQL UPDATE 命令时，该命令将包含一个 WHERE 子句用于查找具有原始`RowVersion`值的行。 如果更新命令没有影响任何行 (也就是没有行具有原始的`RowVersion`值)， Entity Framework 将引发`DbUpdateConcurrencyException`异常。

该异常的 catch 块中的代码从异常对象上的`Entries`属性获取受影响的部门实体。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?range=164)]

`Entries`集合将仅有一个`EntityEntry`对象。  该对象可用于获取用户输入的值和数据库当前的值。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?range=165-166)]

该代码将具有针对数据库中的值和用户在编辑页上所输入的值不一致的每个列添加自定义错误消息 （下面为简洁起见只有一个字段）。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?range=174-178)]

最后，代码将`departmentToUpdate`的`RowVersion`值设置为从数据库检索到的新值。 在重新显示页时，此`RowVersion`新值将存储在隐藏的字段，用户下一次单击时**保存**时，因为编辑页重新显示时发生的并发错误将被捕获。

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?range=199-200)]

`ModelState.Remove`语句是必需的，因为`ModelState`具有旧的`RowVersion`值。 在视图中，`ModelState`字段同时存在时，将优先使用模型属性值。

## <a name="update-the-department-edit-view"></a>更新部门编辑视图

在*Views/Departments/Edit.cshtml*中，进行以下更改：

* 在`DepartmentID`属性的隐藏的字段之后添加隐藏的字段用于保存`RowVersion`属性值。

* 将"Select Administrator"选项添加到下拉列表中。

[!code-html[Main](intro/samples/cu/Views/Departments/Edit.cshtml?highlight=16,34-36)]

## <a name="test-concurrency-conflicts-in-the-edit-page"></a>在编辑页中测试并发冲突

运行应用并转到部门索引页。 右键单击英语部门的**Edit**超链接并选择**新选项卡中打开**，然后单击英语部门的**Edit**超链接。 现在两个浏览器选项卡显示相同的信息。

更改第一个浏览器选项卡中的字段，然后单击**Save**。

![部门编辑更改后的第 1 页](concurrency/_static/edit-after-change-1.png)

浏览器将显示更改值后的索引页。

更改第二个浏览器选项卡中的字段。

![部门编辑更改后的第 2 页](concurrency/_static/edit-after-change-2.png)

单击**Save** 。 你会看到一条错误消息：

![部门编辑页错误消息](concurrency/_static/edit-error.png)

单击**保存**时。 保存在第二个浏览器选项卡中输入的值。 索引页面显示时，将显示保存的值。

## <a name="update-the-delete-page"></a>更新删除页

对于删除页中， Entity Framework 使用部门编辑页面类似的方式检测由某个用户引起的并发冲突。 当 HttpGet`Delete`方法显示确认视图，该视图在隐藏字段中包括原始的`RowVersion`值。 然后，该值将供 用户确认删除时调用的HttpPost`Delete`方法使用。 当 Entity Framework 创建 SQL DELETE 命令时，它在 WHERE 子句中包含原始的`RowVersion`值。 如果命令的结果影响零行 （含义后显示删除确认页，已更改行），则会引发一个并发异常， HttpGet`Delete`将错误标志设置为 true 然后重新显示确认页，确认页中包含了一条错误消息。 没有行受到影响还有可能是因为已经由其他用户删除改行，在这种情况下不会显示任何错误消息。

### <a name="update-the-delete-methods-in-the-departments-controller"></a>更新部门控制器中的删除方法

在*DepartmentsController.cs*中，将 HttpGet`Delete`方法替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_DeleteGet&highlight=1,10,14-17,21-29)]

该方法将接受可选参数，该值指示该页是否在发生并发错误后重新显示。 如果此标志为 true 且部门不存在，则它已经被另一个用户中删除。 在这种情况下，代码将重定向到索引页面。  如果此标志为 true 且部门依旧存在，则它已被另一个用户改变数据。 在这种情况下，代码使用`ViewData`将一条错误消息发送到视图。  

HttpPost`Delete`方法(名为`DeleteConfirmed`)中的代码 替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_DeletePost&highlight=1,3,5-8,11-18)]

在您更换掉的基架代码中，该方法仅接受记录的 ID:


```csharp
public async Task<IActionResult> DeleteConfirmed(int id)
```

你已将此参数更改一个由模型联编程序创建的部门实体实例。这样 EF 会访问记录的主键和 RowVersion 的属性值。

```csharp
public async Task<IActionResult> Delete(Department department)
```

您还将操作方法名称更改为`Delete`。 基架的代码使用`DeleteConfirmed`名称是为了给 HttpPost 方法提供一个唯一的签名。 （CLR 需要具有不同的参数的重载方法。）现在签名是唯一的，可以使用 MVC 的约定， HttpPost 和 HttpGet 删除方法使用相同的名称。

如果该部门已删除，`AnyAsync`方法会返回 false，应用程序只需将返回到 Index 方法。

如果捕获到并发错误，则该代码会重新显示删除确认页，并提供一个标志，指示它应显示并发错误消息。

### <a name="update-the-delete-view"></a>更新删除视图

在*Views/Departments/Delete.cshtml*中，将基架的代码替换为下面的代码用于添加错误消息字段和隐藏 DepartmentID 和 RowVersion 属性的字段。 高亮代码显示了所做的更改。

[!code-html[Main](intro/samples/cu/Views/Departments/Delete.cshtml?highlight=9,38,44,45,48)]

代码中做出以下更改：

* 在`h2`和`h3`标题之间添加一条错误消息。

* 在**Administrator**字段中将 FirstMidName 替换为 FullName。

* 删除 RowVersion 字段。

* 添加`RowVersion`属性的隐藏字段。

运行应用并转到部门索引页。 右键单击英语部门的**Delete**超链接并选择**在新选项卡中打开**，然后在第一个选项卡中英语部门的单击**Edit**超链接。

在第一个窗口中，更改一个值，然后单击**保存**:

![在删除之前的更改后的部门编辑页](concurrency/_static/edit-after-change-for-delete.png)

在第二个选项卡上，单击**Delete**。可以看到页面上的并发错误消息，并会使用当前数据库中的值刷新部门值。

![出现并发错误的部门删除确认页](concurrency/_static/delete-error.png)

如果你单击**删除**同样，在重定向到已删除部门的索引页。

## <a name="update-details-and-create-views"></a>更新详情和创建视图

可以选择删除基架代码创建的详情和创建视图。

将*Views/Departments/Details.cshtml*替换为以下代码，删除 RowVersion 列并显示管理员的完整名称。

[!code-html[Main](intro/samples/cu/Views/Departments/Details.cshtml?highlight=35)]

将*Views/Departments/Create.cshtml*替换为以下代码，将**Select Administrator**添加到下拉列表中。

[!code-html[Main](intro/samples/cu/Views/Departments/Create.cshtml?highlight=32-34)]

## <a name="summary"></a>摘要

这篇文章简要介绍了如何处理并发冲突。 有关如何在 EF Core 中处理并发的详细信息，可以参阅[并发冲突](https://docs.microsoft.com/ef/core/saving/concurrency)。 下一个教程演示如何实现教师和学生实体的单体系单表继承模式。

>[!div class="step-by-step"]
[上一页](update-related-data.md)
[下一页](inheritance.md)  
