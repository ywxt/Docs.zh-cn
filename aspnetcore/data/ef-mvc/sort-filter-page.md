---
title: "ASP.NET 核心 MVC 与 EF 核心的排序、 筛选器、 分页-10 3"
author: tdykstra
description: "在本教程中，你将添加排序、 筛选和分页功能页上使用 ASP.NET Core 和实体框架核心。"
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/sort-filter-page
ms.openlocfilehash: feb4a50c9e5602064e7d493b6991485949903f47
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="sorting-filtering-paging-and-grouping---ef-core-with-aspnet-core-mvc-tutorial-3-of-10"></a>排序、筛选、分页和分组 - EF Core 和 ASP.NET Core MVC 教程（第 3 部分，共 10 部分）

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 Web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC Web 应用程序。有关此教程系列的信息，请参阅[此系列的第一个教程](intro.md)。

在前面的教程中，你实现了一组用于“学生”实体的基本 CRUD 操作的网页。在本教程中，你将向“学生索引”页添加排序、筛选和分页功能。你还将创建具有简单分组功能的页面。

下图显示该页面在完成后的样子。列标题是链接，用户可以通过单击它使数据按该列排序。反复单击列标题就会在升序排列和降序排列之间切换。

![学生索引页](sort-filter-page/_static/paging.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>将列排序链接添加到学生索引页

若要向“学生索引”页添加排序功能，需要更改“学生”控制器的`Index`方法并向“学生索引”视图添加代码。

### <a name="add-sorting-functionality-to-the-index-method"></a>向 Index 方法添加排序功能

在 *StudentsController.cs* 中，用以下代码替换`Index`方法：

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]

此代码从 URL 中的查询字符串接收`sortOrder`参数。ASP.NET Core MVC 提供的查询字符串值作为参数传递给操作方法。参数将是 "Name" 或 "Date" 字符串，后面可以选择性地跟一个下划线和用于指定降序的字符串“desc”。默认排序方式为升序。

第一次请求“索引”页时，没有任何查询字符串。学生按姓氏升序显示，也就是`switch`语句中贯穿示例所确定的默认排序方式。当用户单击列标题超链接时，将在查询字符串中提供相应的`sortOrder`值。

视图通过两个`ViewData`元素（NameSortParm 和 DateSortParm）使用相应的查询字符串值配置列标题超链接。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]

这些是三元语句。第一个语句指定在`sortOrder`参数为 null 或空的情况下，应将 NameSortParm 设置为 "name_desc"；否则应将它设置为空字符串。这两个语句使得视图能够设置列标题超链接，如下所示：

| 当前排序顺序 | 姓氏超链接 | 日期超链接 |
|:--------------------:|:-------------------:|:--------------:|
| 姓氏升序排列 | 降序 | 升序 |
| 姓氏降序排列 | 升序 | 升序 |
| 日期升序排列 | 升序 | 降序 |
| 日期降序排列 | 升序 | 升序 |

该方法使用 LINQ to Entities 指定要作为排序依据的列。代码在 switch 语句之前创建`IQueryable`变量，在 switch 语句中对其进行修改，然后在`switch`语句之后调用`ToListAsync`方法。创建和修改`IQueryable`变量时，不会向数据库发送任何查询。在调用`ToListAsync`之类的方法将`IQueryable`对象转换为集合之前，不会执行查询。因此，在执行`return View`语句之前，此代码生成的单个查询不会执行。

有很多列时，此代码可能变得很冗长。[本系列的最后一个教程](advanced.md#dynamic-linq)介绍如何编写代码，以便在一个字符串变量中传递`OrderBy`列的名称。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>向“学生索引”视图添加列标题超链接

使用以下代码替换 *Views/Students/Index.cshtml* 中的代码，以便添加列标题超链接。更改的行已突出显示。

[!code-html[](intro/samples/cu/Views/Students/Index2.cshtml?highlight=16,22)]

此代码根据`ViewData`属性中的信息，使用相应的查询字符串值来设置超链接。

运行应用，选择“学生”****选项卡，然后单击“姓”****和****“注册日期”列标题，验证是否能够排序。

![名称顺序中的学生索引页](sort-filter-page/_static/name-order.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>向“学生索引”页添加搜索框

若要向“学生索引”页添加筛选功能，请向视图添加一个文本框和提交按钮，并在`Index`方法中进行相应的更改。可以在文本框中输入字符串，以便在姓字段和名字段中进行相应的搜索。

### <a name="add-filtering-functionality-to-the-index-method"></a>向 Index 方法添加筛选功能

在 *StudentsController.cs* 中，将`Index`方法替换为以下代码（所做更改已突出显示）。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]

你已向`Index`方法添加`searchString`参数。搜索字符串值来自之后会添加到“索”引视图中的文本框。你还向 LINQ 语句添加了 where 子句，该子句只选择姓或名中包含搜索字符串的学生。添加 where 子句的语句只有在有值可供搜索的时候才执行。

> [!NOTE]
> 在这里，你是在`IQueryable`对象上调用`Where`方法，而筛选器则在服务器上进行处理。在某些情况下，你可能会对内存中集合调用充当扩展方法的`Where`方法。（例如，假设你更改对`_context.Students`的引用，这样它就会引用可返回`IEnumerable`集合的存储库方法而不是 EF`DbSet`。）通常情况下，结果是相同的，但在某些情况下可能会有所不同。
>
>例如，默认情况下 .NET Framework 在实现`Contains`方法时会进行区分大小写的比较，但在 SQL Server 中，这取决于 SQL Server 实例的排序规则设置。该设置默认为不区分大小写。可以调用`ToUpper`方法，使测试明确区分大小写：*Where (s = > s.LastName.ToUpper().Contains(searchString.ToUpper())*。这样做可确保在将来更改代码，以便使用可返回`IEnumerable`集合的存储库而不是`IQueryable`对象的情况下，结果还能保持相同。（对`IEnumerable`集合调用`Contains`方法时，将获得 .NET Framework 实现；对`IQueryable`对象调用它时，则会获得数据库提供程序实现。）但是，此解决方案会对性能产生负面影响。`ToUpper`代码会将函数加入到 TSQL SELECT 语句的 WHERE 子句中。这样做会妨碍优化程序使用索引。假设多数情况下 SQL 已安装为不区分大小写，则在迁移到区分大小写的数据存储之前，最好避免使用`ToUpper`

### <a name="add-a-search-box-to-the-student-index-view"></a>向“学生索引”视图添加一个搜索框

在 *Views/Student/Index.cshtml* 中，将突出显示的代码添加到开始表标签之前，以便创建标题、文本框、“搜索”按钮。****

[!code-html[](intro/samples/cu/Views/Students/Index3.cshtml?range=9-23&highlight=5-13)]

此代码通过使用`<form>`[标记帮助器](xref:mvc/views/tag-helpers/intro)添加搜索文本框和按钮。默认情况下，`<form>`标记帮助器使用 POST 提交表单数据，这意味着，参数在 HTTP 消息正文中传递，而不是在 URL 中作为查询字符串传递。指定 HTTP GET 时，表单数据是在 URL 中作为查询字符串传递，这使得用户能够将该 URL 加入到书签中。W3C 指南建议在操作未导致更新时使用 GET。

运行应用，选择“学生”****选项卡，输入搜索字符串，然后单击"搜索"，验证筛选功能是否正常。

![使用筛选的学生索引页](sort-filter-page/_static/filtering.png)

请注意该 URL 包含搜索字符串。

```html
http://localhost:5813/Students?SearchString=an
```

如果将此页加入书签，则在使用书签时会获得筛选后的列表。添加`method="get"`到`form`标记中就会生成查询字符串。

在此阶段，如果单击列标题排序链接，则会丢失在“搜索”框中输入的筛选器值。下一部分将修复此问题。

## <a name="add-paging-functionality-to-the-students-index-page"></a>向“学生索引”页添加分页功能

为了向“学生索引”页添加分页功能，需要创建`PaginatedList`类，以便使用`Skip`和`Take`语句对服务器上的数据进行筛选，而不必始终检索所有的表行。接下来需对`Index`方法做更多的更改，并将分页按钮添加到`Index`视图中。下图显示了分页按钮。

![学生索引页，带有分页链接](sort-filter-page/_static/paging.png)

在项目文件夹中创建`PaginatedList.cs`，然后将模板代码替换为以下代码。

[!code-csharp[Main](intro/samples/cu/PaginatedList.cs)]

此代码中的`CreateAsync`方法使用页大小和页码，并对`IQueryable`应用相应的`Skip`和`Take`语句。对`IQueryable`调用`ToListAsync`时，该方法将返回一个只包含请求页的列表。属性`HasPreviousPage`和`HasNextPage`可用来启用或禁用“上一页”****和****“下一页”分页按钮。

由于构造函数不能运行异步代码，因此使用`CreateAsync`方法而不是构造函数来创建`PaginatedList<T>`对象。

## <a name="add-paging-functionality-to-the-index-method"></a>向 Index 方法添加分页功能

在 *StudentsController.cs* 中，将`Index`方法替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]

该代码向方法签名中添加一个页码参数、一个当前排序顺序参数和一个当前筛选器参数。

```csharp
public async Task<IActionResult> Index(
    string sortOrder,
    string currentFilter,
    string searchString,
    int? page)
```

第一次显示页面时，或者如果用户没有单击分页或排序链接，所有参数都将为 null。如果单击了分页链接，页面变量将包含要显示的页码。

名为 CurrentSort 的`ViewData`元素为视图提供当前排序顺序，因为此值必须包含在分页链接中，以便在分页时保持排序顺序相同。

名为 CurrentFilter 的`ViewData`元素为视图提供当前筛选器字符串。此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。

如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。在文本框中输入值并按下“提交”按钮时，搜索字符串将被更改。在这种情况下，searchString 参数不为 null。

```csharp
if (searchString != null)
{
    page = 1;
}
else
{
    searchString = currentFilter;
}
```

在`Index`方法最后，`PaginatedList.CreateAsync`方法会将学生查询转换为支持分页的集合类型中的学生的单个页面。然后将学生的单个页面传递给视图。

```csharp
return View(await PaginatedList<Student>.CreateAsync(students.AsNoTracking(), page ?? 1, pageSize));
```

`PaginatedList.CreateAsync`方法使用页号。两个问号表示 null 合并运算符。Null 合并运算符为可以为 null 的类型定义一个默认值；表达式`(page ?? 1)`意味着在页面有值的情况下返回页面的值，在页面为 null 的情况下返回 1。

## <a name="add-paging-links-to-the-student-index-view"></a>向“学生索引”视图添加分页链接

在 *Views/Students/Index.cshtml* 中，将现有代码替换为以下代码。突出显示所作更改。

[!code-html[](intro/samples/cu/Views/Students/Index.cshtml?highlight=1,27,30,33,61-79)]

页面顶部的`@model`语句指定视图现在获取的是`PaginatedList<T>`对象，而不是`List<T>`对象。

列标题链接使用查询字符串将当前的搜索字符串传递到控制器，以便用户可以在筛选结果中进行排序：

```html
<a asp-action="Index" asp-route-sortOrder="@ViewData["DateSortParm"]" asp-route-currentFilter ="@ViewData["CurrentFilter"]">Enrollment Date</a>
```

分页按钮由标记帮助器显示：

```html
<a asp-action="Index"
   asp-route-sortOrder="@ViewData["CurrentSort"]"
   asp-route-page="@(Model.PageIndex - 1)"
   asp-route-currentFilter="@ViewData["CurrentFilter"]"
   class="btn btn-default @prevDisabled">
   Previous
</a>
```

运行应用并转到学生页。

![学生索引页，带有分页链接](sort-filter-page/_static/paging.png)

单击以确保分页工作原理的不同的排序顺序中的分页链接。 然后输入搜索字符串，然后重试以验证分页还适用正确使用排序和筛选的分页。

## <a name="create-an-about-page-that-shows-student-statistics"></a>创建显示学生统计信息的“关于”页

对于 Contoso 大学网站的“关于”页，将显示每个注册日期注册了多少名学生。这需要对组进行分组和简单计算。若要完成此操作，需要执行以下操作：

* 为需要传递给视图的数据创建一个视图模型类。

* 修改主控制器中的 About 方法。

* 修改关于视图。

### <a name="create-the-view-model"></a>创建视图模型

在 *Models* 文件夹中创建 *SchoolViewModels* 文件夹。

在新的文件夹中，添加 *EnrollmentDateGroup.cs* 类文件并将模板代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]

### <a name="modify-the-home-controller"></a>修改主控制器

在 *HomeController.cs* 文件顶部添加以下 using 语句：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]

在类的左大括号之后立即为数据库上下文添加一个类变量，并从 ASP.NET Core DI 获取上下文的实例：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]

将 `About` 方法替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]

LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在`EnrollmentDateGroup`视图模型对象的集合中。
> [!NOTE] 
> 在 1.0 版 Entity Framework Core 中，整个结果集被返回给客户端，并在客户端上完成分组。在某些情况下，这可能会造成性能问题。请务必使用生产数据量测试性能，必要时请使用原始 SQL 在服务器上进行分组。有关如何使用原始 SQL 的信息，请参阅[本系列中的最后一个教程](advanced.md)。

### <a name="modify-the-about-view"></a>修改“关于”视图

将 *Views/Home/About.cshtml* 文件中的代码替换为以下代码：

[!code-html[](intro/samples/cu/Views/Home/About.cshtml)]

运行应用并转到“关于”页。表格中会显示每个注册日期的学生计数。

![有关页面](sort-filter-page/_static/about.png)

## <a name="summary"></a>摘要

在本教程中，你已了解了如何执行排序、筛选、分页和分组。在下一个教程中，你将了解如何使用迁移来处理数据模型更改。

>[!div class="step-by-step"]
[上一页](crud.md)
[下一页](migrations.md)  
