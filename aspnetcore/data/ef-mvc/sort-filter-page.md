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
# <a name="sorting-filtering-paging-and-grouping---ef-core-with-aspnet-core-mvc-tutorial-3-of-10"></a>使用 ASP.NET Core MVC 和 EF Core 实现排序、 筛选、 分页和分组教程(3 / 10)

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 想要获取有关系列教程的信息，请参阅[第一个教程](intro.md)。

在前面的教程，你可以实现一组的用于学生实体的基本 CRUD 操作网页。 在本教程将向学生索引页添加排序、 筛选和分页功能。 你还将创建具有简单分组功能的页面。

下图显示你完成本教程后相关页面的样子。 列标题时一个链接，用户可以单击它使数据按该列排序。 反复单击列标题在升序排列和降序排列之间切换。

![学生索引页](sort-filter-page/_static/paging.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>将列排序链接添加到学生索引页

为了添加排序学生索引页，你将更改学生控制器中的`Index`方法并向学生索引视图添加相关的代码。

### <a name="add-sorting-functionality-to-the-index-method"></a>向 Index 方法添加排序功能

在*StudentsController.cs*，用以下代码替换`Index`方法：

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]

此代码从 URL 中的查询字符串中接收`sortOrder`参数。 ASP.NET Core MVC 提供的查询字符串作为参数传递给的操作方法。 "Name"或"Date"，后面可以选择性跟用于指定降序顺序的下划线和"desc"构成参数字符串。 默认排序顺序为升序。

第一次请求索引页时，没有任何查询字符串。 学生按姓氏升序显示也就是`switch`语句中的缺省值中的排序方式。 当用户单击列标题的超链接，将向`Index`方法提供相应的`sortOrder`查询字符串。

视图使用`ViewData`元素中两个元素 （NameSortParm 和 DateSortParm） 对应的查询字符串值配置列标题超链接。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]

这两个语句都使用了三目运算符。 第一个语句指如果`sortOrder`参数为 null 或为空则 NameSortParm 应设置为"name_desc"; 否则，它应设置为一个空字符串。 这两个语句使试图能够如下所示设置列标题的超链接：

|  当前的排序顺序  | Last Name 超链接 | Date 超链接 |
|:--------------------:|:-------------------:|:--------------:|
| Last Name 升序排列  | descending          | ascending      |
| Last Name 降序排列 | ascending           | ascending      |
| Date 升序排列       | ascending           | descending     |
| Date 降序排列      | ascending           | ascending      |

该方法使用 LINQ to Entities 指定要作为排序依据的列。 代码在switch 语句之前创建了`IQueryable`变量然后在 switch 语句中对其进行修改，并在`switch`语句之后调用`ToListAsync`方法。 当你创建和修改`IQueryable`变量时数据库不会接收到任何查询。 在您调用如`ToListAsync`等方法将`IQueryable`转换为集合对象之前不会执行查询。 因此，在`return View`语句之前此代码只会执行一个查询。

此代码会获得具有大量列的冗长信息。 [本系列最后一个教程](advanced.md#dynamic-linq)将演示如何编写代码，使你可以使用字符串将需要`OrderBy`的行的名称作为参数传递给方法。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>向学生索引视图的列标题添加超链接

用以下代码替换*Views/Students/Index.cshtml*，以添加列标题超链接。 高亮代码为已更改的行。

[!code-html[](intro/samples/cu/Views/Students/Index2.cshtml?highlight=16,22)]

代码中使用了`ViewData`元素中的信息来以相应的查询字符串值设置超链接。

运行应用程序中，选择**Students**卡，然后单击**Last Name**和**Enrollment Date**列标题，以验证该排序成功。

![名称顺序中的学生索引页](sort-filter-page/_static/name-order.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>向学生索引页添加搜索框

向视图添加一个文本框和提交按钮来向索引页添加搜索框，并在`Index`方法中做相应更改。 你可以在文本框中输入字符串搜索名字和姓氏字段中的内容。

### <a name="add-filtering-functionality-to-the-index-method"></a>向索引方法添加筛选功能

在*StudentsController.cs*，将`Index`方法替换为以下代码 （突出显示所做的更改）。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]

在`Index`方法中添加`searchString`参数。 搜索字符串值来自之后会添加到索引视图中的文本框。 你还向 LINQ 语句 添加了where 子句来选择仅名字或姓氏包含搜索字符串的学生。 添加 where 子句的语句只有在要搜索值的时候才执行。

> [!NOTE]
> 此处对`IQueryable`对象调用`Where`方法，筛选器将在服务器上处理。 在某些场景下你可能会对内存中集合调用作为扩展方法的`Where`。 (例如，假设你使用`_context.Students`引用，不同于 EF`DbSet`，它返回`IEnumerable`集合的存储库方法的引用。)结果通常将相同，但在某些情况下可能会不同。
>
>例如，默认情况下 .NET Framework 实现的`Contains`方法是对大小写敏感的，但 SQL Server 中由 SQL Server 的排序规则确定。 SQL Server 默认不区分大小写。 您可以调用`ToUpper`方法使得其大小写敏感：*Where (s = > s.LastName.ToUpper()。Contains(searchString.ToUpper())*。 这样做能确保如果将来使用返回`IEnumerable`集合的存储库方法而不是`IQueryable`对象来修改相关代码，结果还能保持相同。 (当你对`IEnumerable`集合调用`Contains`方法，你将获取.NET Framework 的实现; 当对`IQueryable`对象调用它，则会得到数据库驱动的实现。)但是，此解决方案会对性能产生负面影响。 `ToUpper`将函数加入到 TSQL SELECT 语句的 WHERE 子句中。 这样做会是的索引优化失去效果。 假设 SQL 大多是是大小写不敏感，在你将数据迁移到大小写敏感的数据存储库之前最好避免`ToUpper`代码。

### <a name="add-a-search-box-to-the-student-index-view"></a>向学生索引视图添加一个搜索框

打开*Views/Student/Index.cshtml*，在table标签之前添加高亮代码以在页面中创建标题，**Search**文本框，按钮。

[!code-html[](intro/samples/cu/Views/Students/Index3.cshtml?range=9-23&highlight=5-13)]

此代码通过使用`<form>`[标记帮助器](xref:mvc/views/tag-helpers/intro)添加搜索文本框和按钮。 默认情况下，`<form>`标记帮助器默认使用 post 方法提交数据，这意味着，参数在 HTTP 消息正文中传输表单数据，而不是在 URL 查询字符串上显示并传输。指定使用 HTTP GET 时，表单数据是通过 URL 查询字符串传输，这使得用户能够使用该 URL 来创建书签。 W3C 指南建议当操作未导致更新时使用 GET 方法。

运行应用程序，选择**Students**选项卡，输入搜索字符串，然后单击搜索以验证筛选是否正常工作。

![使用筛选的学生索引页](sort-filter-page/_static/filtering.png)

请注意该 URL 包含搜索字符串。

```html
http://localhost:5813/Students?SearchString=an
```

如果将此页加入书签，使用书签时你将获得筛选后的列表。 添加`method="get"`到`form`标签中是导致生成查询字符串的原因。

在此阶段，如果您单击列标题的排序链接你将丢失url上的查询字符串值。 下一部分将修复此问题。

## <a name="add-paging-functionality-to-the-students-index-page"></a>向学生索引页添加分页功能

为了向学生索引页添加分页功能，你需要创建`PaginatedList`类，该类使用`Skip`和`Take`语句来对服务器上的数据进行筛选而不是始终检索所有的表行。 接下来你将对`Index`方法做更多的修改并将分页按钮添加到`Index`视图中。 如下图所示添加了分页按钮的学生索引页。

![学生索引页，带有分页链接](sort-filter-page/_static/paging.png)

在项目文件夹中，创建`PaginatedList.cs`，然后将模板代码替换为下面的代码。

[!code-csharp[Main](intro/samples/cu/PaginatedList.cs)]

代码中的`CreateAsync`方法获得页面数和当前页码，并对`IQueryable`执行 相应的`Skip`和`Take`语句。 当`IQueryable`调用`ToListAsync`时，该方法将返回只包含在请求页里的学生列表。 属性`HasPreviousPage`和`HasNextPage`可用来启用或禁用**Previous**和**Next**分页按钮。

由于构造函数里不能运行异步代码，`CreateAsync`方法被用作构造函数而只用于创建一个`PaginatedList<T>`对象。

## <a name="add-paging-functionality-to-the-index-method"></a>向索引方法添加分页功能

在*StudentsController.cs*中，用以下代码替换`Index`方法。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]

代码中将总页数参数、 当前的排序顺序参数和当前的筛选器参数添加到方法签名中。

```csharp
public async Task<IActionResult> Index(
    string sortOrder,
    string currentFilter,
    string searchString,
    int? page)
```

第一次显示页面，或如果用户未单击分页或排序链接，则所有参数都为null。 如果单击分页链接，页面变量将包含要显示的页码。

名为 CurrentSort 的`ViewData`元素提供了当前已排序的试图，因为这必须包含在分页链接中以保持排序顺序在分页时相同。

名为 CurrentFilter 的`ViewData`元素提供了当前已筛选的视图。为了在分页过程中维护筛选规则以及在页面重新显示的时候把筛选值恢复到文本框中，该值一定要被包含进分页链接里

如果分页期间更改搜索字符串，显示的页会被重置为 1，因为新的筛选器可能会导致显示不同的数据。 在文本框中输入了值以及按下提交按钮搜索字符串就会改变。 在这种情况下，`searchString`参数不为 null。

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

在`Index`方法的结尾，`PaginatedList.CreateAsync`方法将学生查询转换为支持分页的集合类型，集合中包含了刚好能放进单页的学生实体。 然后将这个单页大小的学生集合 传递给视图。

```csharp
return View(await PaginatedList<Student>.CreateAsync(students.AsNoTracking(), page ?? 1, pageSize));
```

`PaginatedList.CreateAsync`方法从参数中获取页号。 两个问号表示 null 合并运算符。 Null 合并运算符可以为 null 的类型定义一个默认值; 表达式`(page ?? 1)`意味着返回的值如果`page`参数为 null 则返回 1，如果指定了一个值则返回指定的值。

## <a name="add-paging-links-to-the-student-index-view"></a>向学生索引视图添加分页链接

在*Views/Students/Index.cshtml*中，用以下代码替换现有代码。 高亮代码为更改的代码。

[!code-html[](intro/samples/cu/Views/Students/Index.cshtml?highlight=1,27,30,33,61-79)]

在页面顶部`@model`的语句表示视图现在获取的是`PaginatedList<T>`对象而不是`List<T>`对象。

列标题链接使用查询字符串将当前的搜索字符串传递到控制器，以便用户可以在筛选结果中进行排序：

```html
<a asp-action="Index" asp-route-sortOrder="@ViewData["DateSortParm"]" asp-route-currentFilter ="@ViewData["CurrentFilter"]">Enrollment Date</a>
```

通过标记帮助程序显示分页按钮：

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

## <a name="create-an-about-page-that-shows-student-statistics"></a>创建关于页面来显示学生统计信息

在 Contoso 大学网站**About**页上，将显示每个课程有多少学生修读。 这要求在分组上再进行分组和简单计算。 要完成此操作，需要执行以下操作：

* 创建一个视图模型类，该视图类是需要传递到该视图的数据的抽象。

* 修改对 Home 控制器中的 About 方法。

* 修改关于视图。

### <a name="create-the-view-model"></a>创建视图模型

在*Model*文件夹中创建*SchoolViewModels*文件夹。

在新的文件夹中，添加*EnrollmentDateGroup.cs*类文件并将模板代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]

### <a name="modify-the-home-controller"></a>修改 Home 控制器

在*HomeController.cs*，在该文件的顶部添加以下 using 语句：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]

在类中，左左大括号后添加的数据库上下文类型的变量，并通过 ASP.NET Core 依赖注入获取上下文的实例：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]

将 `About` 方法的代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]

LINQ 语句将学生实体按修读日期分组，计算每个组中的实体数并将结果存储在`EnrollmentDateGroup`视图模型对象的集合中。
> [!NOTE] 
> 在 Entity Framework Core 1.0 版本中，整个结果集都会返回到客户端，并在客户端上进行分组。 在某些场景下，这会导致性能问题。 请务必使用用符合生产规模的数据来测试性能，如有必要使用原始 SQL 语句在服务器上进行分组。 有关如何使用原始的 SQL ，请参阅[本系列最后一个教程](advanced.md)。

### <a name="modify-the-about-view"></a>修改关于视图

将*Views/Home/About.cshtml*文件替换为以下代码：

[!code-html[](intro/samples/cu/Views/Home/About.cshtml)]

运行应用并转到关于页面。 表格中显示了每个修读日期的学生计数。

![有关页面](sort-filter-page/_static/about.png)

## <a name="summary"></a>摘要

在本教程中，你已了解如何执行排序、 筛选、 分页和分组。 在下一个的教程中，你将了解如何使用迁移来处理数据模型更改。

>[!div class="step-by-step"]
[上一页](crud.md)
[下一页](migrations.md)  
