---
title: "ASP.NET 核心 MVC 与 EF 核心-CRUD-2 的 10"
author: tdykstra
description: 
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/crud
ms.openlocfilehash: a7e0d4ff3d57e42dd7e33ffb5f26f2143520be87
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="create-read-update-and-delete---ef-core-with-aspnet-core-mvc-tutorial-2-of-10"></a>使用 ASP.NET Core MVC 和 EF Core 实现创建、读取、更新和删除教程(2 / 10)

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示了如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC  web 应用程序。 有关系列教程的信息，请参阅[第一个教程](intro.md)。

在前面的教程中，你使用 Entity Framework 和 SQL Server LocalDB 创建了一个用于存储和显示数据的 MVC 应用程序。 在本教程中，你将回顾和自定义MVC 基架自动为你在控制器和视图中创建的 CRUD （创建、 读取、 更新、 删除）代码。

> [!NOTE] 
> 使用仓库模式在控制器和数据访问层之间创建一个抽象层是常见的做法。为了使得本教程更简单和更专注与 EF 本身，这里没有使用仓库模式。查阅[本系列最后一个教程](advanced.md)可以获取更多有关与仓库模式的信息
在本教程中，您对以下页面进行处理：

![学生详细信息页](crud/_static/student-details.png)

![学生创建页](crud/_static/student-create.png)

![学生编辑页](crud/_static/student-edit.png)

![学生删除页](crud/_static/student-delete.png)

## <a name="customize-the-details-page"></a>自定义详细信息页

学生索引页的基架代码中省略了`Enrollments`属性，因为该属性是一个集合。 在**详细信息**页上，你将会在 HTML 表上显示集合的内容。

在*Controllers/StudentsController.cs*，在和详细信息视图相关的操作方法中使用`SingleOrDefaultAsync`方法来检索单个`Student`实体。 如以下突出显示的代码中所示，添加调用`Include`。 `ThenInclude`和`AsNoTracking`方法的代码。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Details&highlight=8-12)]

`Include`和`ThenInclude`方法使得上下文加载`Student.Enrollments`导航属性，并将`Enrollment.Course`导航属性添加到每个`Enrollment`中。  你将在[读取相关的数据](read-related-data.md)教程中了解相关方法。

`AsNoTracking`方法返回的实体在当前上下文的生存期不会更新的场景中可以提高性能。 你将在本教程末尾了解更多有关`AsNoTracking`的信息。

### <a name="route-data"></a>路由数据

传递给`Details`方法的关键值来自*数据路由*。 路由数据是模型联编程序在 URL 段中找到的数据。 例如，默认的路由指明了控制器、 操作方法和 id ：

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Route&highlight=5)]

在下面的 URL 中，根据默认路由获得下面的路由数据，对应的控制器为`Instructor`，操作方法为`Index`、 id 为`1`。

```
http://localhost:1230/Instructor/Index/1?courseID=2021
```

URL 的最后部分 ("?courseID=2021") 是一个查询字符串。 如果将`id`作为查询字符串值传递,模型联编程序也会将 ID 值作为参数传递给`Details`方法：

```
http://localhost:1230/Instructor/Index?id=1&CourseID=2021
```

在Index页中，通过 Razor 视图中的标记帮助器创建 Url。 在以下 Razor 代码中，`id`参数与默认路由匹配，因此`id`被添加到路由数据中。

```html
<a asp-action="Edit" asp-route-id="@item.ID">Edit</a>
```

当`item.ID`为 6 时生成以下 HTML :

```html
<a href="/Students/Edit/6">Edit</a>
```

在以下 Razor 代码中，`studentID`与默认路由中的参数不匹配，因此，它以查询字符串的形式添加到 Url 。

```html
<a asp-action="Edit" asp-route-studentID="@item.ID">Edit</a>
```

有关标记帮助的详细信息，请参阅[中 ASP.NET Core 标记帮助程序](xref:mvc/views/tag-helpers/intro)。

### <a name="add-enrollments-to-the-details-view"></a>添加修读信息到详细信息视图

打开*Views/Students/Details.cshtml*。 每个字段都使用`DisplayNameFor`和`DisplayFor`来显示，如下面的示例中所示：

[!code-html[](intro/samples/cu/Views/Students/Details.cshtml?range=13-18&highlight=2,5)]

最后一个字段后和在`</dl>`闭合标记前，添加以下代码以显示修读信息列表：

[!code-html[](intro/samples/cu/Views/Students/Details.cshtml?range=31-52)]

如果粘贴代码后，代码缩进有误，按 CTRL-K-D 格式化代码。

此代码循环访问`Enrollments`导航属性中的实体。 对于每个修读信息，显示课程标题和评分。 课程标题在修读信息实体内`Course`导航属性中的课程实体中检索。

运行应用程序，选择**Student**选项卡卡，然后单击**详细信息**一名学生的链接。 为所选学生查看课程和年级的列表：

![学生详细信息页](crud/_static/student-details.png)

## <a name="update-the-create-page"></a>更新创建页

在*StudentsController.cs*，修改 HttpPost`Create`方法，在其中添加 try catch 块和从`Bind`特性中删除 ID 值。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Create&highlight=4,6-7,14-21)]

此代码主要的功能是将由 ASP.NET MVC 模型联编程序创建的学生实体添加到学生实体集中，然后将所做的更改保存到数据库。 （模型联编程序是 ASP.NET MVC 的功能，它能让你更轻松地处理表单提交的数据; 模型联编程序将已提交的表单值转换为 CLR 类型，并将其作为参数传递给对应的操作方法。 接着，模型联编程序会使用表单提交的属性实例化学生实体。）

你从`Bind`特性特性中删除`ID`，因为当插入行时 SQL Server 将自动设置 ID 为主键。 在这里主键应该是来自用户输入的值不不是自动设置的 ID 值。

除`Bind`属性，try catch 块是对基架的代码仅有的更改。 如果正在对所做的更改进行保存时捕捉到了继承自`DbUpdateException`的异常，将显示通用的错误消息。 `DbUpdateException`有时由外部程序造成，而不一定是编程错误，因此建议用户以重试一遍以排查错误来源。 尽管在此示例中没有体现，但在生产环境中运行的应用程序会记录异常。 有关详细信息，请参阅**深入探索日志**主题中[监视和遥测 （使用 Azure构建真实世界云应用程序）](https://docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)。

`ValidateAntiForgeryToken`特性有助于防止跨站点请求伪造 (CSRF) 攻击。 令牌通过[表单标签帮助器](xref:mvc/views/working-with-forms#the-form-tag-helper)自动注入到页面中，并自动加入到用户提交的表单信息中。 `ValidateAntiForgeryToken`特性使得令牌生效。 有关 CSRF 的详细信息，请参阅[反请求伪造](../../security/anti-request-forgery.md)。

<a id="overpost"></a>
### <a name="security-note-about-overposting"></a>关于过度发布的安全说明

在创建的情景下，在基架的代码中的`Create`方法里加入`Bind`特性是防止过度发布的一种方法。 例如，假设学生实体包含你不希望此网页更改的`Secret`属性。

```csharp
public class Student
{
    public int ID { get; set; }
    public string LastName { get; set; }
    public string FirstMidName { get; set; }
    public DateTime EnrollmentDate { get; set; }
    public string Secret { get; set; }
}
```

即使在网页上没有修改`Secret`的字段，黑客可以使用 Fiddler 之类的工具或编写一些 JavaScript，发布`Secret`的值。 当没有`Bind`属性限制时，模型联编程序将使用`Secret`表单值并使用它来创建学生实体实例。 然后为黑客指定的任何`Secret`表单值都将在你的数据库中更新。 下图显示 Fiddler 工具添加`Secret`（值为"OverPost"） 到待发布的表单值。

![Fiddler 添加机密字段](crud/_static/fiddler.png)

随后"OverPost"成功添加到新插入行的`Secret`列，即使你不希望网页能够设置该属性。

你可以先从数据库读取实体，然后调用`TryUpdateModel`方法，并在显式允许的属性列表中传递，这样做能够在编辑场景中有效防止过度发布。 在这系列教程中广泛使用这种方法。

开发人员更喜欢使用另外一种方法来防止过度发布，那就是使用视图模型，而不是绑定实体类与模型。 视图模型中只包含你想更新的属性。 当 MVC 模型联编程序执行完成后，将根据需要使用 AutoMapper 等工具将视图模型属性复制到实体实例。 对实体实例使用`_context.Entry`将其状态设置为`Unchanged`，然后将每个视图模型中的实体属性的`Property("PropertyName").IsModified`设置为 true 。 该方法同时适用于编辑和创建场景。

### <a name="test-the-create-page"></a>测试创建页

*Views/Students/Create.cshtml*中的代码对每个字段使用`label`， `input`，和`span`（用于验证消息）标签帮助器。

运行应用程序中，选择**Students**卡，然后单击**Create**。

输入名称和日期。 请尝试输入无效的日期，如果你的浏览器可以做到这一点 （某些浏览器强制你要使用日期选取器）。然后单击**Create**可查看错误消息。

![日期验证错误](crud/_static/date-error.png)

默认情况下; 你获取到的是服务器端验证，在之后的教程中，你将知道如何通过添加特性来生成客户端验证的代码。 以下高亮代码演示了`Create`方法中的模型验证。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Create&highlight=8)]

将日期更改为有效的值并单击**Create**，查看在**Index**页上显示的新学生。

## <a name="update-the-edit-page"></a>更新编辑页

在*StudentController.cs*，正如你在`Details`方法中看到的，`Edit`的HttpGet方法 (不是`HttpPost`特性) 使用`SingleOrDefaultAsync`方法来检索所选的学生实体。 在这里你不需要更改此方法。

### <a name="recommended-httppost-edit-code-read-and-update"></a>建议的 HttpPost 编辑代码： 读取和更新

将HttpPost 编辑操作方法替换为以下代码。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ReadFirst)]

这些更改是防止过度发布实现安全的最佳做法。 基架生成了`Bind`属性，并将使用`Modified`标志模型联编程序所创建的实体添加实体集。 基架生成的代码不建议应用于很多场景，因为`Bind`属性将清除任何未在`Include`参数列出字段的预先存在的数据。

新的代码读取现有实体然后调用`TryUpdateModel`[基于用户输入的已发布的表单数据](xref:mvc/models/model-binding#how-model-binding-works)更新检索到的实体的字段。  Entity Framework 的自动跟踪更改机制会根据表单输入更改设置了`Modified`标志的字段。 当`SaveChanges`方法被调用时， Entity Framework 创建 SQL 语句更新数据库行。 并发冲突将被忽略，只有用户更改了的表格列会更新的奥数据库中。 （后面的教程演示如何处理并发冲突。）

作为防止过度发布的最佳实践，可通过**编辑**页更新的字段应该包含在`TryUpdateModel`的白名单参数中。 （在参数列表中字段列表前的空字符串表示从下面开始就是表单字段。）当前没有额外要保护的字段，但列出你想要模型联编程序绑定的字段，这样可以确保在将来将字段添加到数据模型，它们能够在你显式将其添加到白名单之前自动受到保护。

通过这些更改，HttpPost`Edit`方法与 HttpGet`Edit`方法的签名相同; 因此重命名方法为`EditPost`。

### <a name="alternative-httppost-edit-code-create-and-attach"></a>可选的 HttpPost 编辑代码： 创建和附加

上面展示的建议的 HttpPost 编辑代码可确保仅会更新已更改的列，并保留你不希望包括进模型绑定的属性的数据。 但是，这种方案需要先读取数据导致了额外的数据库读取，甚至导致需要编写复杂的代码来处理并发冲突。 现在介绍一种可选的方法就是将模型联编程序创建的实体附加到 EF 上下文并将其标记为已修改。 (不要将你的项目中的相关代码替换为以下代码，以下代码只用来演示一种可选方法。) 

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_CreateAndAttach)]

在 web 页 UI 中包含实体中的所有字段并可以随意更新他们时，可以使用此方法。

基架的创建的代码使用的就是创建和附加方法，但仅捕获`DbUpdateConcurrencyException`异常并返回 404 错误代码。  这个示例中展示了捕获所有和数据库更新有关异常并显示错误消息。

### <a name="entity-states"></a>实体状态

数据库上下文保持跟踪在内存中的实体是否与数据库中对应的行同步，此信息能够确定在调用`SaveChanges`方法时发生了什么情况。 例如，当将一个新实体传递到`Add`方法，该实体的状态设置为`Added`。 然后当你调用`SaveChanges`方法，数据库上下文发出 SQL INSERT 指令令。

实体可能处于以下状态之一：

* `Added`。 实体在数据库中尚不存在。 `SaveChanges`方法发出 INSERT 语句。

* `Unchanged`。 `SaveChanges`方法无需对此实体执行任何操作。 当从数据库读取实体时，该实体从此状态开始。

* `Modified`。 实体的某些或所有属性值发生了改变。 `SaveChanges`方法发出 UPDATE 语句。

* `Deleted`。 实体已标记为删除。 `SaveChanges`方法发出 DELETE 语句。

* `Detached`。 数据库上下文不跟踪该实体 。

在桌面应用中，状态更改通常会自动设置。 读取实体并对它的一些属性值进行更改将导致其实体状态自动更改为`Modified`。 然后调用`SaveChanges`， Entity Framework 生成 SQL UPDATE 语句更新你更改的实际属性。

在 web 应用中，读取实体和显示要编辑其数据的`DbContext`在页面渲染之后才被处理。 当调用 HttpPost`Edit`操作方法时、 会进行新的 web 请求然后您将使用`DbContext`的新实例。 如果你重新读取该新上下文中的实体，则相当与模拟桌面应用来处理。

但如果不希望执行额外的读取操作，你必须使用由模型联编程序创建的实体对象。  执行此操作的最简单方法是将实体状态设置为`Modified`，和前面可选的 HttpPost 编辑代码中的做法一样。 然后调用`SaveChanges`时， Entity Framework 更新数据库的所有列，因为上下文无法知道您更改了哪些属性。

如果你想要避免使用先读取的方法，但你还想要 SQL UPDATE 语句仅更新用户实际更改的字段，则代码会更复杂。 你必须以某种方式保存的原始值 (如通过使用隐藏的字段)，以便它们在调用 HttpPost`Edit`方法时可用。 然后你可以使用原始值创建一个学生实体，调用原始版本的`Attach`方法，使用新值更新实体的值，然后调用`SaveChanges`。

### <a name="test-the-edit-page"></a>测试的编辑页

运行应用程序中，选择**Students**选项卡，然后单击**Edit**超链接。

![学生编辑页](crud/_static/student-edit.png)

更改某些数据，再单击**Save**。 **Index**页将被打开并可以在其中查看更改后的数据。

## <a name="update-the-delete-page"></a>更新删除页

在*StudentController.cs*中，正如你在详细信息视图和编辑方法所看到，HttpGet `Delete`方法的模板代码使用`SingleOrDefaultAsync`方法来检索所选的学生实体。 但是，若要在调用`SaveChanges`失败时抛出自定义错误消息时，需要将某些功能添加到此方法以及相应的视图中。

当你看到的更新，创建和删除操作都需要两个操作方法。 调用响应 GET 请求的方法用于显示相关页面为用户提供普准或取消删除操作的机会。如果用户批准它，则创建 POST 请求。 当发生这种情况，调用HttpPost`Delete`方法，然后该方法 执行删除操作。

将 try catch 块添加到 HttpPost`Delete`方法以处理更新数据库时可能出现的任何错误。 如果发生错误，HttpPost Delete 方法调用 HttpGet Delete 方法，向其传入指示发生错误的参数。然后 HttpGet Delete 方法重新显示确认页以及错误消息，向用户提供机会取消或重试。

 将 HttpGet`Delete`替换替换为以下代码，用管理错误报告。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DeleteGet&highlight=1,9,16-21)]

此代码接受可选参数，该参数能指出这个方法是否在出现故障(保存更改失败)后调用的。 此参数为 false 时，HttpGet`Delete`在上一次没有失败的情况下调用。 当为了响应 HttpPost`Delete`方法中对数据库更新的错误时，该参数是 true，并且将一条错误消息传递给视图。

### <a name="the-read-first-approach-to-httppost-delete"></a>HttpPost 先读取的删除方法

用以下代码替换 HttpPost`Delete`操作方法 (名为`DeleteConfirmed`) ，该方法执行实际的删除操作并捕获任何有关数据库更新错误的异常。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DeleteWithReadFirst&highlight=6,8-11,13-14,18-23)]

此代码检索所选的实体，然后调用`Remove`方法将实体的状态设置为`Deleted`， 然后调用`SaveChanges`生成 SQL DELETE 命令。

### <a name="the-create-and-attach-approach-to-httppost-delete"></a>HttpPost 创建和附加的删除方法

如果优先考虑提高大容量应用程序的性能，则通过只使用主键来实例化实体使用然后将实体状态设置为`deleted`来避免不必要的 SQL 查询密钥值。 这就是 Entity Framework 删除该实体所需要做的所有步骤。 （不要将此代码放在你的项目; 仅用于阐释一种可选的方法。）

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DeleteWithoutReadFirst&highlight=7-8)]

如果有跟实体相关的数据要删除，请确保数据库中配置了级联删除。 使用此方法删除实体时，EF 可能不知道有相关的实体要被删除。

### <a name="update-the-delete-view"></a>更新删除视图

在*Views/Student/Delete.cshtml*中，在 h2 标题和 h3 标题之间添加一条错误消息，如下所示：

[!code-html[](intro/samples/cu/Views/Students/Delete.cshtml?range=7-9&highlight=2)]

运行应用程序中，选择**Student**卡，然后单击**Delete**超链接：

![删除确认页面](crud/_static/student-delete.png)

单击**Delete**。 索引页面没有显示已删除的学生。 （你将在并发教程看到错误处理的操作代码）。

## <a name="closing-database-connections"></a>关闭数据库连接

上下文实例在你完成工作的时候必须尽可能快地处理以释放维持数据库连接的资源。 ASP.NET Core 内置的[依赖注入](../../fundamentals/dependency-injection.md)会为你完成该任务。

在*Startup.cs*，你调用[AddDbContext 扩展方法](https://github.com/aspnet/EntityFrameworkCore/blob/03bcb5122e3f577a84498545fcf130ba79a3d987/src/Microsoft.EntityFrameworkCore/EntityFrameworkServiceCollectionExtensions.cs)想ASP.NET DI 容器中提供`DbContext`的类。 该方法在默认情况下将服务生存期设置为`Scoped`。 `Scoped`表示与 web 请求生命周期和上下文对象生命周期一致，`Dispose`方法将 web 请求结束时自动调用。

## <a name="handling-transactions"></a>处理事务

默认情况下 Entity Framework 隐式实现事务。 在对多个行或表进行更改，然后调用`SaveChanges`的场景中， Entity Framework 可自动确保所做的更改要么全部成功要么全部失败。 如果一些更改成功完成，之后发生了错误，则这些更改会自动回滚。 在你需要更多控制的场景中--例如，如果你想要在事务中包含在 Entity Framework 外部的操作，请参阅[事务](https://docs.microsoft.com/ef/core/saving/transactions)。

## <a name="no-tracking-queries"></a>不跟踪查询

当数据库上下文检索表行，并创建表示它们的实体对象时，默认情况下它将跟踪内存中的实体是否与数据库同步。 内存中的数据充当缓存，并在更新实体时使用。 此缓存在 web 应用程序中通常是不必要的因为上下文实例通常生存期较短 （一个新的上下文实力为每个请求创建和释放） 和上下文读取再次使用该实体通常释放实体。

可以通过调用`AsNoTracking`方法来禁用对实体对象内存的跟踪。 你可能想要执行此操作的典型场景包括：

* 在上下文生命周期内无需更新任何实体，并且您不需要 EF [通过单独的查询来自动加载检索到的实体的导航属性](read-related-data.md)。 通常来说控制器的 HttpGet 操作方法满足这些条件。

* 正在运行检索大量数据的查询，并仅更新返回的数据的一小部分。 在大型查询中关闭跟踪可能会更有效，并在之后为需要更新的少量实体执行查询。

* 你想要对一个实体附加跟踪以便其进行更新，但出于其他目的之前已经检索过相同的实体。 因为该实体已经在数据库上下文被跟踪，不能将想要更改的实体附加耿总。 处理这种情况的一种方法是在前面的查询调用`AsNoTracking`。

有关详细信息，请参阅[跟踪 vs 不跟踪](https://docs.microsoft.com/ef/core/querying/tracking)。

## <a name="summary"></a>摘要

你现在具有一组完整的对学生实体执行简单 CRUD 操作的页。 在下一步的教程，你将扩展**Index**页上的功能，实现排序、 筛选和分页。

>[!div class="step-by-step"]
[上一页](intro.md)
[下一页](sort-filter-page.md)  
