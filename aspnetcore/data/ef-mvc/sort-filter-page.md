---
title: ASP.NET Core MVC 和 EF Core - 排序、筛选、分页 - 第 3 个教程，共 10 个教程
author: rick-anderson
description: 本教程将使用 ASP.NET Core 和 Entity Framework Core 向页面添加排序、筛选和分页功能。
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/sort-filter-page
ms.openlocfilehash: 344e3a1806ff21d8ce335b2b407a8a93baf72c1b
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
---
# <a name="aspnet-core-mvc-with-ef-core---sort-filter-paging---3-of-10"></a><span data-ttu-id="b40b6-103">ASP.NET Core MVC 和 EF Core - 排序、筛选、分页 - 第 3 个教程，共 10 个教程</span><span class="sxs-lookup"><span data-stu-id="b40b6-103">ASP.NET Core MVC with EF Core - Sort, Filter, Paging - 3 of 10</span></span>

<span data-ttu-id="b40b6-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b40b6-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b40b6-105">Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b40b6-105">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="b40b6-106">若要了解教程系列，请参阅[本系列中的第一个教程](intro.md)。</span><span class="sxs-lookup"><span data-stu-id="b40b6-106">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="b40b6-107">在上一个教程中，已为 Student 实体实现了一组网页用于执行基本的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="b40b6-107">In the previous tutorial, you implemented a set of web pages for basic CRUD operations for Student entities.</span></span> <span data-ttu-id="b40b6-108">在本教程中，将向学生索引页添加排序、筛选和分页功能。</span><span class="sxs-lookup"><span data-stu-id="b40b6-108">In this tutorial you'll add sorting, filtering, and paging functionality to the Students Index page.</span></span> <span data-ttu-id="b40b6-109">同时，还将创建一个执行简单分组的页面。</span><span class="sxs-lookup"><span data-stu-id="b40b6-109">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="b40b6-110">下图展示了完成操作后的页面外观。</span><span class="sxs-lookup"><span data-stu-id="b40b6-110">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="b40b6-111">列标题是用户可以单击以按该列排序的链接。</span><span class="sxs-lookup"><span data-stu-id="b40b6-111">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="b40b6-112">重复单击列标题可在升降排序顺序之间切换。</span><span class="sxs-lookup"><span data-stu-id="b40b6-112">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![“学生索引”页](sort-filter-page/_static/paging.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="b40b6-114">向学生索引页添加列排序链接</span><span class="sxs-lookup"><span data-stu-id="b40b6-114">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="b40b6-115">要向学生索引页添加排序功能，需更改学生控制器的 `Index` 方法并将代码添加到学生索引视图。</span><span class="sxs-lookup"><span data-stu-id="b40b6-115">To add sorting to the Student Index page, you'll change the `Index` method of the Students controller and add code to the Student Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="b40b6-116">向 Index 方法添加排序功能</span><span class="sxs-lookup"><span data-stu-id="b40b6-116">Add sorting Functionality to the Index method</span></span>

<span data-ttu-id="b40b6-117">在 StudentsController.cs 中，将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b40b6-117">In *StudentsController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly)]

<span data-ttu-id="b40b6-118">此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-118">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="b40b6-119">查询字符串值由 ASP.NET Core MVC 提供，作为操作方法的参数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-119">The query string value is provided by ASP.NET Core MVC as a parameter to the action method.</span></span> <span data-ttu-id="b40b6-120">该参数将是一个字符串，可为“Name”或“Date”，可选择后跟下划线和字符串“desc”来指定降序。</span><span class="sxs-lookup"><span data-stu-id="b40b6-120">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="b40b6-121">默认排序顺序为升序。</span><span class="sxs-lookup"><span data-stu-id="b40b6-121">The default sort order is ascending.</span></span>

<span data-ttu-id="b40b6-122">首次请求索引页时，没有任何查询字符串。</span><span class="sxs-lookup"><span data-stu-id="b40b6-122">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="b40b6-123">学生按照姓氏升序显示，这是 `switch` 语句中的 fall-through 事例所建立的默认值。</span><span class="sxs-lookup"><span data-stu-id="b40b6-123">The students are displayed in ascending order by last name, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="b40b6-124">当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。</span><span class="sxs-lookup"><span data-stu-id="b40b6-124">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="b40b6-125">视图使用两个 `ViewData` 元素（NameSortParm 和 DateSortParm）来为列标题超链接配置相应的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="b40b6-125">The two `ViewData` elements (NameSortParm and DateSortParm) are used by the view to configure the column heading hyperlinks with the appropriate query string values.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortOnly&highlight=3-4)]

<span data-ttu-id="b40b6-126">这些是三元语句。</span><span class="sxs-lookup"><span data-stu-id="b40b6-126">These are ternary statements.</span></span> <span data-ttu-id="b40b6-127">第一个指定如果 `sortOrder` 参数为 NULL 或空，则应将 NameSortParm 设置为“name_desc”；否则，应将其设置为空字符串。</span><span class="sxs-lookup"><span data-stu-id="b40b6-127">The first one specifies that if the `sortOrder` parameter is null or empty, NameSortParm should be set to "name_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="b40b6-128">通过这两个语句，视图可如下设置列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="b40b6-128">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

|  <span data-ttu-id="b40b6-129">当前排序顺序</span><span class="sxs-lookup"><span data-stu-id="b40b6-129">Current sort order</span></span>  | <span data-ttu-id="b40b6-130">姓氏超链接</span><span class="sxs-lookup"><span data-stu-id="b40b6-130">Last Name Hyperlink</span></span> | <span data-ttu-id="b40b6-131">日期超链接</span><span class="sxs-lookup"><span data-stu-id="b40b6-131">Date Hyperlink</span></span> |
|:--------------------:|:-------------------:|:--------------:|
| <span data-ttu-id="b40b6-132">姓氏升序</span><span class="sxs-lookup"><span data-stu-id="b40b6-132">Last Name ascending</span></span>  | <span data-ttu-id="b40b6-133">descending</span><span class="sxs-lookup"><span data-stu-id="b40b6-133">descending</span></span>          | <span data-ttu-id="b40b6-134">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-134">ascending</span></span>      |
| <span data-ttu-id="b40b6-135">姓氏降序</span><span class="sxs-lookup"><span data-stu-id="b40b6-135">Last Name descending</span></span> | <span data-ttu-id="b40b6-136">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-136">ascending</span></span>           | <span data-ttu-id="b40b6-137">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-137">ascending</span></span>      |
| <span data-ttu-id="b40b6-138">日期升序</span><span class="sxs-lookup"><span data-stu-id="b40b6-138">Date ascending</span></span>       | <span data-ttu-id="b40b6-139">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-139">ascending</span></span>           | <span data-ttu-id="b40b6-140">descending</span><span class="sxs-lookup"><span data-stu-id="b40b6-140">descending</span></span>     |
| <span data-ttu-id="b40b6-141">日期降序</span><span class="sxs-lookup"><span data-stu-id="b40b6-141">Date descending</span></span>      | <span data-ttu-id="b40b6-142">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-142">ascending</span></span>           | <span data-ttu-id="b40b6-143">ascending</span><span class="sxs-lookup"><span data-stu-id="b40b6-143">ascending</span></span>      |

<span data-ttu-id="b40b6-144">该方法使用 LINQ to Entities 指定要作为排序依据的列。</span><span class="sxs-lookup"><span data-stu-id="b40b6-144">The method uses LINQ to Entities to specify the column to sort by.</span></span> <span data-ttu-id="b40b6-145">该代码在 switch 语句之前创建一个 `IQueryable` 变量，在 switch 语句中对其进行修改，并在 `switch` 语句后调用 `ToListAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="b40b6-145">The code creates an `IQueryable` variable before the switch statement, modifies it in the switch statement, and calls the `ToListAsync` method after the `switch` statement.</span></span> <span data-ttu-id="b40b6-146">当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。</span><span class="sxs-lookup"><span data-stu-id="b40b6-146">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="b40b6-147">只有通过调用 `ToListAsync` 之类的方法将 `IQueryable` 对象转换为集合，查询才会执行。</span><span class="sxs-lookup"><span data-stu-id="b40b6-147">The query isn't executed until you convert the `IQueryable` object into a collection by calling a method such as `ToListAsync`.</span></span> <span data-ttu-id="b40b6-148">因此，此代码导致直到 `return View` 语句才会执行单个查询。</span><span class="sxs-lookup"><span data-stu-id="b40b6-148">Therefore, this code results in a single query that's not executed until the `return View` statement.</span></span>

<span data-ttu-id="b40b6-149">此代码可能获得包含大量列的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b40b6-149">This code could get verbose with a large number of columns.</span></span> <span data-ttu-id="b40b6-150">[本系列的最后一个教程](advanced.md#dynamic-linq)演示了如何编写在字符串变量中传递 `OrderBy` 列名的代码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-150">[The last tutorial in this series](advanced.md#dynamic-linq) shows how to write code that lets you pass the name of the `OrderBy` column in a string variable.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="b40b6-151">向“学生索引”视图添加列标题超链接</span><span class="sxs-lookup"><span data-stu-id="b40b6-151">Add column heading hyperlinks to the Student Index view</span></span>

<span data-ttu-id="b40b6-152">将 Views / Students / Index.cshtml 中的代码替换为以下代码，以添加列标题超链接。</span><span class="sxs-lookup"><span data-stu-id="b40b6-152">Replace the code in *Views/Students/Index.cshtml*, with the following code to add column heading hyperlinks.</span></span> <span data-ttu-id="b40b6-153">已更改的行为突出显示状态。</span><span class="sxs-lookup"><span data-stu-id="b40b6-153">The changed lines are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index2.cshtml?highlight=16,22)]

<span data-ttu-id="b40b6-154">此代码使用 `ViewData` 属性中的信息来设置具有相应查询字符串值的超链接。</span><span class="sxs-lookup"><span data-stu-id="b40b6-154">This code uses the information in `ViewData` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="b40b6-155">运行应用，选择“学生”选项卡，然后单击“姓氏”和“注册日期”列标题以验证排序是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b40b6-155">Run the app, select the **Students** tab, and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![按姓名顺序的学生索引页](sort-filter-page/_static/name-order.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="b40b6-157">向“学生索引”页添加搜索框</span><span class="sxs-lookup"><span data-stu-id="b40b6-157">Add a Search Box to the Students Index page</span></span>

<span data-ttu-id="b40b6-158">要向学生索引页添加筛选功能，需将文本框和提交按钮添加到视图，并在 `Index` 方法中做出相应的更改。</span><span class="sxs-lookup"><span data-stu-id="b40b6-158">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="b40b6-159">在文本框中输入一个字符串以在名字和姓氏字段中进行搜索。</span><span class="sxs-lookup"><span data-stu-id="b40b6-159">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="b40b6-160">向 Index 方法添加筛选功能</span><span class="sxs-lookup"><span data-stu-id="b40b6-160">Add filtering functionality to the Index method</span></span>

<span data-ttu-id="b40b6-161">在 StudentsController.cs 中，将 `Index` 方法替换为以下代码（所做的更改为突出显示状态）。</span><span class="sxs-lookup"><span data-stu-id="b40b6-161">In *StudentsController.cs*, replace the `Index` method with the following code (the changes are highlighted).</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilter&highlight=1,5,9-13)]

<span data-ttu-id="b40b6-162">已向 `Index` 方法添加 `searchString` 参数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-162">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="b40b6-163">从要添加到索引视图的文本框中接收搜索字符串值。</span><span class="sxs-lookup"><span data-stu-id="b40b6-163">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="b40b6-164">并且，还向 LINQ 语句添加了 where 子句，该子句仅选择名字或姓氏中包含搜索字符串的学生。</span><span class="sxs-lookup"><span data-stu-id="b40b6-164">You've also added to the LINQ statement a where clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="b40b6-165">只有在有搜索值的情况下，才会执行添加了 where 子句的语句。</span><span class="sxs-lookup"><span data-stu-id="b40b6-165">The statement that adds the where clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="b40b6-166">此处正在调用 `IQueryable` 对象上的 `Where` 方法，并且将在服务器上处理该筛选器。</span><span class="sxs-lookup"><span data-stu-id="b40b6-166">Here you are calling the `Where` method on an `IQueryable` object, and the filter will be processed on the server.</span></span> <span data-ttu-id="b40b6-167">在某些情况下，可能会将 `Where` 方法作为内存中集合上的扩展方法进行调用。</span><span class="sxs-lookup"><span data-stu-id="b40b6-167">In some scenarios you might be calling the `Where` method as an extension method on an in-memory collection.</span></span> <span data-ttu-id="b40b6-168">（例如，假设将引用更改为 `_context.Students`，这样它引用的不再是 EF `DbSet`，而是一个返回 `IEnumerable` 集合的存储库方法。）结果通常是相同的，但在某些情况下可能不同。</span><span class="sxs-lookup"><span data-stu-id="b40b6-168">(For example, suppose you change the reference to `_context.Students` so that instead of an EF `DbSet` it references a repository method that returns an `IEnumerable` collection.) The result would normally be the same but in some cases may be different.</span></span>
>
><span data-ttu-id="b40b6-169">例如，`Contains` 方法的 .NET Framework 实现在默认情况下执行区分大小写比较，但在 SQL Server 中，这由 SQL Server 实例的排序规则设置决定。</span><span class="sxs-lookup"><span data-stu-id="b40b6-169">For example, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but in SQL Server this is determined by the collation setting of the SQL Server instance.</span></span> <span data-ttu-id="b40b6-170">该设置默认为不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b40b6-170">That setting defaults to case-insensitive.</span></span> <span data-ttu-id="b40b6-171">可调用 `ToUpper` 方法使测试显式不区分大小写：Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())。</span><span class="sxs-lookup"><span data-stu-id="b40b6-171">You could call the `ToUpper` method to make the test explicitly case-insensitive:  *Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())*.</span></span> <span data-ttu-id="b40b6-172">如果稍后更改代码以使用返回 `IEnumerable` 集合而不是 `IQueryable` 对象的存储库，则可确保结果保持不变。</span><span class="sxs-lookup"><span data-stu-id="b40b6-172">That would ensure that results stay the same if you change the code later to use a repository which returns   an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="b40b6-173">（在 `IEnumerable` 集合上调用 `Contains` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）但是，此解决方案会降低性能。</span><span class="sxs-lookup"><span data-stu-id="b40b6-173">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.) However, there's a performance penalty for this solution.</span></span> <span data-ttu-id="b40b6-174">`ToUpper` 代码将在 TSQL SELECT 语句的 WHERE 子句中放置一个函数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-174">The `ToUpper` code would put a function in the WHERE clause of the TSQL SELECT statement.</span></span> <span data-ttu-id="b40b6-175">这将阻止优化器使用索引。</span><span class="sxs-lookup"><span data-stu-id="b40b6-175">That would prevent the optimizer from using an index.</span></span> <span data-ttu-id="b40b6-176">鉴于 SQL 主要安装为不区分大小写，在迁移到区分大小写的数据存储之前，最好避免使用 `ToUpper` 代码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-176">Given that SQL is mostly installed as case-insensitive, it's best to avoid the `ToUpper` code until you migrate to a case-sensitive data store.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="b40b6-177">向“学生索引”视图添加搜索框</span><span class="sxs-lookup"><span data-stu-id="b40b6-177">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="b40b6-178">在 Views/Student/Index.cshtml 中，请在打开表格标签之前立即添加突出显示的代码，以创建标题栏、文本框和搜索按钮。</span><span class="sxs-lookup"><span data-stu-id="b40b6-178">In *Views/Student/Index.cshtml*, add the highlighted code immediately before the opening table tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index3.cshtml?range=9-23&highlight=5-13)]

<span data-ttu-id="b40b6-179">此代码使用 `<form>` [标记帮助器](xref:mvc/views/tag-helpers/intro)添加搜索文本框和按钮。</span><span class="sxs-lookup"><span data-stu-id="b40b6-179">This code uses the `<form>` [tag helper](xref:mvc/views/tag-helpers/intro) to add the search text box and button.</span></span> <span data-ttu-id="b40b6-180">默认情况下，`<form>` 标记帮助器使用 POST 提交表单数据，这意味着参数在 HTTP 消息正文中传递，而不是作为查询字符串在 URL 中传递。</span><span class="sxs-lookup"><span data-stu-id="b40b6-180">By default, the `<form>` tag helper submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="b40b6-181">当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。</span><span class="sxs-lookup"><span data-stu-id="b40b6-181">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="b40b6-182">W3C 指南建议在操作不会导致更新时使用 GET。</span><span class="sxs-lookup"><span data-stu-id="b40b6-182">The W3C guidelines recommend that you should use GET when the action doesn't result in an update.</span></span>

<span data-ttu-id="b40b6-183">运行应用，选择“学生”选项卡，输入搜索字符串，然后单击“搜索”以验证筛选是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b40b6-183">Run the app, select the **Students** tab, enter a search string, and click Search to verify that filtering is working.</span></span>

![带有筛选功能的学生索引页](sort-filter-page/_static/filtering.png)

<span data-ttu-id="b40b6-185">请注意，该 URL 包含搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="b40b6-185">Notice that the URL contains the search string.</span></span>

```html
http://localhost:5813/Students?SearchString=an
```

<span data-ttu-id="b40b6-186">如果将此页加入书签，当使用书签时，将获得已筛选的列表。</span><span class="sxs-lookup"><span data-stu-id="b40b6-186">If you bookmark this page, you'll get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="b40b6-187">向 `form` 标记添加 `method="get"` 是导致生成查询字符串的原因。</span><span class="sxs-lookup"><span data-stu-id="b40b6-187">Adding `method="get"` to the `form` tag is what caused the query string to be generated.</span></span>

<span data-ttu-id="b40b6-188">在此阶段，如果单击列标题排序链接，则会丢失已在“搜索”框中输入的筛选器值。</span><span class="sxs-lookup"><span data-stu-id="b40b6-188">At this stage, if you click a column heading sort link you'll lose the filter value that you entered in the **Search** box.</span></span> <span data-ttu-id="b40b6-189">此问题将在下一部分得以解决。</span><span class="sxs-lookup"><span data-stu-id="b40b6-189">You'll fix that in the next section.</span></span>

## <a name="add-paging-functionality-to-the-students-index-page"></a><span data-ttu-id="b40b6-190">向“学生索引”页添加分页功能</span><span class="sxs-lookup"><span data-stu-id="b40b6-190">Add paging functionality to the Students Index page</span></span>

<span data-ttu-id="b40b6-191">要向学生索引页添加分页功能，需创建一个使用 `Skip` 和 `Take` 语句的 `PaginatedList` 类来筛选服务器上的数据，而不总是对表中的所有行进行检索。</span><span class="sxs-lookup"><span data-stu-id="b40b6-191">To add paging to the Students Index page, you'll create a `PaginatedList` class that uses `Skip` and `Take` statements to filter data on the server instead of always retrieving all rows of the table.</span></span> <span data-ttu-id="b40b6-192">然后在 `Index` 方法中进行其他更改，并将分页按钮添加到 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="b40b6-192">Then you'll make additional changes in the `Index` method and add paging buttons to the `Index` view.</span></span> <span data-ttu-id="b40b6-193">下图显示了分页按钮。</span><span class="sxs-lookup"><span data-stu-id="b40b6-193">The following illustration shows the paging buttons.</span></span>

![带有分页链接的“学生索引”页](sort-filter-page/_static/paging.png)

<span data-ttu-id="b40b6-195">在项目文件夹中，创建 `PaginatedList.cs`，然后用以下代码替换模板代码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-195">In the project folder, create `PaginatedList.cs`, and then replace the template code with the following code.</span></span>

[!code-csharp[](intro/samples/cu/PaginatedList.cs)]

<span data-ttu-id="b40b6-196">此代码中的 `CreateAsync` 方法将提取页面大小和页码，并将相应的 `Skip` 和 `Take` 语句应用于 `IQueryable`。</span><span class="sxs-lookup"><span data-stu-id="b40b6-196">The `CreateAsync` method in this code takes page size and page number and applies the appropriate `Skip` and `Take` statements to the `IQueryable`.</span></span> <span data-ttu-id="b40b6-197">当在 `IQueryable` 上调用 `ToListAsync` 时，它将返回仅包含请求页的列表。</span><span class="sxs-lookup"><span data-stu-id="b40b6-197">When `ToListAsync` is called on the `IQueryable`, it will return a List containing only the requested page.</span></span> <span data-ttu-id="b40b6-198">属性 `HasPreviousPage` 和 `HasNextPage` 可用于启用或禁用“上一页”和“下一页”的分页按钮。</span><span class="sxs-lookup"><span data-stu-id="b40b6-198">The properties `HasPreviousPage` and `HasNextPage` can be used to enable or disable **Previous** and **Next** paging buttons.</span></span>

<span data-ttu-id="b40b6-199">由于构造函数不能运行异步代码，因此使用 `CreateAsync` 方法来创建 `PaginatedList<T>` 对象，而非构造函数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-199">A `CreateAsync` method is used instead of a constructor to create the `PaginatedList<T>` object because constructors can't run asynchronous code.</span></span>

## <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="b40b6-200">向 Index 方法添加分页功能</span><span class="sxs-lookup"><span data-stu-id="b40b6-200">Add paging functionality to the Index method</span></span>

<span data-ttu-id="b40b6-201">在 StudentsController.cs 中，将 `Index` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-201">In *StudentsController.cs*, replace the `Index` method with the following code.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_SortFilterPage&highlight=1-5,7,11-18,45-46)]

<span data-ttu-id="b40b6-202">该代码向方法签名中添加一个页码参数、一个当前排序顺序参数和一个当前筛选器参数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-202">This code adds a page number parameter, a current sort order parameter, and a current filter parameter to the method signature.</span></span>

```csharp
public async Task<IActionResult> Index(
    string sortOrder,
    string currentFilter,
    string searchString,
    int? page)
```

<span data-ttu-id="b40b6-203">第一次显示页面时，或者如果用户没有单击分页或排序链接，所有参数都将为 NULL。</span><span class="sxs-lookup"><span data-stu-id="b40b6-203">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span>  <span data-ttu-id="b40b6-204">如果单击了分页链接，页面变量将包含要显示的页码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-204">If a paging link is clicked, the page variable will contain the page number to display.</span></span>

<span data-ttu-id="b40b6-205">名为 CurrentSort 的 `ViewData` 元素为视图提供当前排序顺序，因为此值必须包含在分页链接中，以便在分页时保持排序顺序相同。</span><span class="sxs-lookup"><span data-stu-id="b40b6-205">The `ViewData` element named CurrentSort provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging.</span></span>

<span data-ttu-id="b40b6-206">名为 CurrentFilter 的 `ViewData` 元素为视图提供当前筛选器字符串。</span><span class="sxs-lookup"><span data-stu-id="b40b6-206">The `ViewData` element named CurrentFilter provides the view with the current filter string.</span></span> <span data-ttu-id="b40b6-207">此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。</span><span class="sxs-lookup"><span data-stu-id="b40b6-207">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span>

<span data-ttu-id="b40b6-208">如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。</span><span class="sxs-lookup"><span data-stu-id="b40b6-208">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="b40b6-209">在文本框中输入值并按下“提交”按钮时，搜索字符串将被更改。</span><span class="sxs-lookup"><span data-stu-id="b40b6-209">The search string is changed when a value is entered in the text box and the Submit button is pressed.</span></span> <span data-ttu-id="b40b6-210">在这种情况下，`searchString` 参数不为 NULL。</span><span class="sxs-lookup"><span data-stu-id="b40b6-210">In that case, the `searchString` parameter isn't null.</span></span>

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

<span data-ttu-id="b40b6-211">在 `Index` 方法最后，`PaginatedList.CreateAsync` 方法会将学生查询转换为支持分页的集合类型中的学生的单个页面。</span><span class="sxs-lookup"><span data-stu-id="b40b6-211">At the end of the `Index` method, the `PaginatedList.CreateAsync` method converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="b40b6-212">然后将学生的单个页面传递给视图。</span><span class="sxs-lookup"><span data-stu-id="b40b6-212">That single page of students is then passed to the view.</span></span>

```csharp
return View(await PaginatedList<Student>.CreateAsync(students.AsNoTracking(), page ?? 1, pageSize));
```

<span data-ttu-id="b40b6-213">`PaginatedList.CreateAsync` 方法需要一个页码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-213">The `PaginatedList.CreateAsync` method takes a page number.</span></span> <span data-ttu-id="b40b6-214">两个问号表示 NULL 合并运算符。</span><span class="sxs-lookup"><span data-stu-id="b40b6-214">The two question marks represent the null-coalescing operator.</span></span> <span data-ttu-id="b40b6-215">NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。</span><span class="sxs-lookup"><span data-stu-id="b40b6-215">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

## <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="b40b6-216">向学生索引视图添加分页链接</span><span class="sxs-lookup"><span data-stu-id="b40b6-216">Add paging links to the Student Index view</span></span>

<span data-ttu-id="b40b6-217">在 Views/Students/Index.cshtml 中，将现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="b40b6-217">In *Views/Students/Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="b40b6-218">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="b40b6-218">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index.cshtml?highlight=1,27,30,33,61-79)]

<span data-ttu-id="b40b6-219">页面顶部的 `@model` 语句指定视图现在获取的是 `PaginatedList<T>` 对象，而不是 `List<T>` 对象。</span><span class="sxs-lookup"><span data-stu-id="b40b6-219">The `@model` statement at the top of the page specifies that the view now gets a `PaginatedList<T>` object instead of a `List<T>` object.</span></span>

<span data-ttu-id="b40b6-220">列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：</span><span class="sxs-lookup"><span data-stu-id="b40b6-220">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

```html
<a asp-action="Index" asp-route-sortOrder="@ViewData["DateSortParm"]" asp-route-currentFilter ="@ViewData["CurrentFilter"]">Enrollment Date</a>
```

<span data-ttu-id="b40b6-221">分页按钮由标记帮助器显示：</span><span class="sxs-lookup"><span data-stu-id="b40b6-221">The paging buttons are displayed by tag helpers:</span></span>

```html
<a asp-action="Index"
   asp-route-sortOrder="@ViewData["CurrentSort"]"
   asp-route-page="@(Model.PageIndex - 1)"
   asp-route-currentFilter="@ViewData["CurrentFilter"]"
   class="btn btn-default @prevDisabled">
   Previous
</a>
```

<span data-ttu-id="b40b6-222">运行应用并转到“学生”页。</span><span class="sxs-lookup"><span data-stu-id="b40b6-222">Run the app and go to the Students page.</span></span>

![带有分页链接的“学生索引”页](sort-filter-page/_static/paging.png)

<span data-ttu-id="b40b6-224">单击不同排序顺序的分页链接，以确保分页正常工作。</span><span class="sxs-lookup"><span data-stu-id="b40b6-224">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="b40b6-225">然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。</span><span class="sxs-lookup"><span data-stu-id="b40b6-225">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="b40b6-226">创建显示学生统计信息的“关于”页</span><span class="sxs-lookup"><span data-stu-id="b40b6-226">Create an About page that shows Student statistics</span></span>

<span data-ttu-id="b40b6-227">对于 Contoso 大学网站的“关于”页，将显示每个注册日期注册了多少名学生。</span><span class="sxs-lookup"><span data-stu-id="b40b6-227">For the Contoso University website's **About** page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="b40b6-228">这需要对组进行分组和简单计算。</span><span class="sxs-lookup"><span data-stu-id="b40b6-228">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="b40b6-229">若要完成此操作，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="b40b6-229">To accomplish this, you'll do the following:</span></span>

* <span data-ttu-id="b40b6-230">为需要传递给视图的数据创建一个视图模型类。</span><span class="sxs-lookup"><span data-stu-id="b40b6-230">Create a view model class for the data that you need to pass to the view.</span></span>

* <span data-ttu-id="b40b6-231">修改主控制器中的“关于”方法。</span><span class="sxs-lookup"><span data-stu-id="b40b6-231">Modify the About method in the Home controller.</span></span>

* <span data-ttu-id="b40b6-232">修改“关于”视图。</span><span class="sxs-lookup"><span data-stu-id="b40b6-232">Modify the About view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="b40b6-233">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="b40b6-233">Create the view model</span></span>

<span data-ttu-id="b40b6-234">在 Models 文件夹中创建一个 SchoolViewModels 文件夹。</span><span class="sxs-lookup"><span data-stu-id="b40b6-234">Create a *SchoolViewModels* folder in the *Models* folder.</span></span>

<span data-ttu-id="b40b6-235">在新文件夹中，添加一个类文件 EnrollmentDateGroup.cs，并用以下代码替换模板代码：</span><span class="sxs-lookup"><span data-stu-id="b40b6-235">In the new folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="b40b6-236">修改主控制器</span><span class="sxs-lookup"><span data-stu-id="b40b6-236">Modify the Home Controller</span></span>

<span data-ttu-id="b40b6-237">在 HomeController.cs 中，使用文件顶部的语句添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="b40b6-237">In *HomeController.cs*, add the following using statements at the top of the file:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings1)]

<span data-ttu-id="b40b6-238">在类的左大括号之后立即为数据库上下文添加一个类变量，并从 ASP.NET Core DI 获取上下文的实例：</span><span class="sxs-lookup"><span data-stu-id="b40b6-238">Add a class variable for the database context immediately after the opening curly brace for the class, and get an instance of the context from ASP.NET Core DI:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_AddContext&highlight=3,5,7)]

<span data-ttu-id="b40b6-239">将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b40b6-239">Replace the `About` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseDbSet)]

<span data-ttu-id="b40b6-240">LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。</span><span class="sxs-lookup"><span data-stu-id="b40b6-240">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>
> [!NOTE] 
> <span data-ttu-id="b40b6-241">在 1.0 版 Entity Framework Core 中，整个结果集被返回给客户端，并在客户端上完成分组。</span><span class="sxs-lookup"><span data-stu-id="b40b6-241">In the 1.0 version of Entity Framework Core, the entire result set is returned to the client, and grouping is done on the client.</span></span> <span data-ttu-id="b40b6-242">在某些情况下，这可能会造成性能问题。</span><span class="sxs-lookup"><span data-stu-id="b40b6-242">In some scenarios this could create performance problems.</span></span> <span data-ttu-id="b40b6-243">请务必使用生产数据量测试性能，必要时请使用原始 SQL 在服务器上进行分组。</span><span class="sxs-lookup"><span data-stu-id="b40b6-243">Be sure to test performance with production volumes of data, and if necessary use raw SQL to do the grouping on the server.</span></span> <span data-ttu-id="b40b6-244">有关如何使用原始 SQL 的信息，请参阅[本系列中的最后一个教程](advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="b40b6-244">For information about how to use raw SQL, see [the last tutorial in this series](advanced.md).</span></span>

### <a name="modify-the-about-view"></a><span data-ttu-id="b40b6-245">修改“关于”视图</span><span class="sxs-lookup"><span data-stu-id="b40b6-245">Modify the About View</span></span>

<span data-ttu-id="b40b6-246">将 Views/Home/About.cshtml 文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b40b6-246">Replace the code in the *Views/Home/About.cshtml* file with the following code:</span></span>

[!code-html[](intro/samples/cu/Views/Home/About.cshtml)]

<span data-ttu-id="b40b6-247">运行应用并转到“关于”页。</span><span class="sxs-lookup"><span data-stu-id="b40b6-247">Run the app and go to the About page.</span></span> <span data-ttu-id="b40b6-248">表格中会显示每个注册日期的学生计数。</span><span class="sxs-lookup"><span data-stu-id="b40b6-248">The count of students for each enrollment date is displayed in a table.</span></span>

![“关于”页面](sort-filter-page/_static/about.png)

## <a name="summary"></a><span data-ttu-id="b40b6-250">总结</span><span class="sxs-lookup"><span data-stu-id="b40b6-250">Summary</span></span>

<span data-ttu-id="b40b6-251">在本教程中，你已了解了如何执行排序、筛选、分页和分组。</span><span class="sxs-lookup"><span data-stu-id="b40b6-251">In this tutorial, you've seen how to perform sorting, filtering, paging, and grouping.</span></span> <span data-ttu-id="b40b6-252">在下一个教程中，你将了解如何使用迁移来处理数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="b40b6-252">In the next tutorial, you'll learn how to handle data model changes by using migrations.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b40b6-253">[上一页](crud.md)
> [下一页](migrations.md)</span><span class="sxs-lookup"><span data-stu-id="b40b6-253">[Previous](crud.md)
[Next](migrations.md)</span></span>  
