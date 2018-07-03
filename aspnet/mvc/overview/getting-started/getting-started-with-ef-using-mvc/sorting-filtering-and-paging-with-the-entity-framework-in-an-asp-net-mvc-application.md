---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 排序、 筛选和分页与实体框架中的 ASP.NET MVC 应用程序 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/01/2015
ms.topic: article
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 3cd7d5e7ea97dd4defa5e609de70beda7dfccf77
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375407"
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="62553-103">排序、 筛选和分页与 ASP.NET MVC 应用程序中的实体框架</span><span class="sxs-lookup"><span data-stu-id="62553-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="62553-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="62553-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="62553-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="62553-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="62553-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="62553-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="62553-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="62553-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="62553-108">上一教程中实现一组基本的 CRUD 操作执行的 web 页面`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="62553-108">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="62553-109">在本教程将添加排序、 筛选和分页功能**学生**索引页。</span><span class="sxs-lookup"><span data-stu-id="62553-109">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="62553-110">同时，还将创建一个执行简单分组的页面。</span><span class="sxs-lookup"><span data-stu-id="62553-110">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="62553-111">下图展示了完成操作后的页面外观。</span><span class="sxs-lookup"><span data-stu-id="62553-111">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="62553-112">列标题是用户可以单击以按该列排序的链接。</span><span class="sxs-lookup"><span data-stu-id="62553-112">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="62553-113">重复单击列标题可在升降排序顺序之间切换。</span><span class="sxs-lookup"><span data-stu-id="62553-113">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="62553-115">向学生索引页添加列排序链接</span><span class="sxs-lookup"><span data-stu-id="62553-115">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="62553-116">若要添加到学生索引页进行排序，你将更改`Index`方法`Student`控制器并将代码添加到`Student`索引视图。</span><span class="sxs-lookup"><span data-stu-id="62553-116">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="62553-117">添加排序功能，到 Index 方法</span><span class="sxs-lookup"><span data-stu-id="62553-117">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="62553-118">在中*Controllers\StudentController.cs*，将为`Index`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="62553-118">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="62553-119">此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。</span><span class="sxs-lookup"><span data-stu-id="62553-119">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="62553-120">ASP.NET MVC 提供查询字符串值作为操作方法的参数。</span><span class="sxs-lookup"><span data-stu-id="62553-120">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="62553-121">该参数将是一个字符串，可为“Name”或“Date”，可选择后跟下划线和字符串“desc”来指定降序。</span><span class="sxs-lookup"><span data-stu-id="62553-121">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="62553-122">默认排序顺序为升序。</span><span class="sxs-lookup"><span data-stu-id="62553-122">The default sort order is ascending.</span></span>

<span data-ttu-id="62553-123">首次请求索引页时，没有任何查询字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-123">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="62553-124">学生显示按升序排序依据`LastName`，这是默认设置，如在 fall-through 事例所建立`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="62553-124">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="62553-125">当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。</span><span class="sxs-lookup"><span data-stu-id="62553-125">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="62553-126">这两个`ViewBag`使用变量，以便该视图可以配置与相应的查询字符串值的列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="62553-126">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="62553-127">这些是三元语句。</span><span class="sxs-lookup"><span data-stu-id="62553-127">These are ternary statements.</span></span> <span data-ttu-id="62553-128">第一个指定，如果`sortOrder`参数为 null 或为空，`ViewBag.NameSortParm`应设置为"名称\_desc"; 否则为它应设置为空字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-128">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="62553-129">通过这两个语句，视图可如下设置列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="62553-129">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="62553-130">当前排序顺序</span><span class="sxs-lookup"><span data-stu-id="62553-130">Current sort order</span></span> | <span data-ttu-id="62553-131">姓氏超链接</span><span class="sxs-lookup"><span data-stu-id="62553-131">Last Name Hyperlink</span></span> | <span data-ttu-id="62553-132">日期超链接</span><span class="sxs-lookup"><span data-stu-id="62553-132">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62553-133">姓氏升序</span><span class="sxs-lookup"><span data-stu-id="62553-133">Last Name ascending</span></span> | <span data-ttu-id="62553-134">descending</span><span class="sxs-lookup"><span data-stu-id="62553-134">descending</span></span> | <span data-ttu-id="62553-135">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-135">ascending</span></span> |
| <span data-ttu-id="62553-136">姓氏降序</span><span class="sxs-lookup"><span data-stu-id="62553-136">Last Name descending</span></span> | <span data-ttu-id="62553-137">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-137">ascending</span></span> | <span data-ttu-id="62553-138">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-138">ascending</span></span> |
| <span data-ttu-id="62553-139">日期升序</span><span class="sxs-lookup"><span data-stu-id="62553-139">Date ascending</span></span> | <span data-ttu-id="62553-140">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-140">ascending</span></span> | <span data-ttu-id="62553-141">descending</span><span class="sxs-lookup"><span data-stu-id="62553-141">descending</span></span> |
| <span data-ttu-id="62553-142">日期降序</span><span class="sxs-lookup"><span data-stu-id="62553-142">Date descending</span></span> | <span data-ttu-id="62553-143">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-143">ascending</span></span> | <span data-ttu-id="62553-144">ascending</span><span class="sxs-lookup"><span data-stu-id="62553-144">ascending</span></span> |

<span data-ttu-id="62553-145">该方法使用[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)指定要作为排序依据的列。</span><span class="sxs-lookup"><span data-stu-id="62553-145">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="62553-146">该代码会创建[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)变量之前`switch`语句，将修改在`switch`语句，并调用`ToList`方法之后`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="62553-146">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="62553-147">当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。</span><span class="sxs-lookup"><span data-stu-id="62553-147">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="62553-148">您将转换之前未执行查询`IQueryable`对象通过调用一个方法，如集合`ToList`。</span><span class="sxs-lookup"><span data-stu-id="62553-148">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="62553-149">因此，此代码导致直到才执行单个查询`return View`语句。</span><span class="sxs-lookup"><span data-stu-id="62553-149">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="62553-150">编写每个排序顺序不同的 LINQ 语句的替代方法，可以动态创建的 LINQ 语句。</span><span class="sxs-lookup"><span data-stu-id="62553-150">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="62553-151">有关动态 LINQ 的信息，请参阅[动态 LINQ](https://go.microsoft.com/fwlink/?LinkID=323957)。</span><span class="sxs-lookup"><span data-stu-id="62553-151">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="62553-152">添加列标题超链接到学生索引视图</span><span class="sxs-lookup"><span data-stu-id="62553-152">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="62553-153">在中*Views\Student\Index.cshtml*，替换`<tr>`和`<th>`的标题行的突出显示的代码元素：</span><span class="sxs-lookup"><span data-stu-id="62553-153">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="62553-154">此代码使用中的信息`ViewBag`属性具有相应查询的超链接设置字符串值。</span><span class="sxs-lookup"><span data-stu-id="62553-154">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="62553-155">运行页面，然后单击**姓氏**并**注册日期**列标题以验证排序是否工作。</span><span class="sxs-lookup"><span data-stu-id="62553-155">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="62553-157">单击后**姓氏**标题下方，学生显示按降序姓氏的顺序。</span><span class="sxs-lookup"><span data-stu-id="62553-157">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="62553-158">向学生索引页添加搜索框</span><span class="sxs-lookup"><span data-stu-id="62553-158">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="62553-159">要向学生索引页添加筛选功能，需将文本框和提交按钮添加到视图，并在 `Index` 方法中做出相应的更改。</span><span class="sxs-lookup"><span data-stu-id="62553-159">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="62553-160">在文本框中输入一个字符串以在名字和姓氏字段中进行搜索。</span><span class="sxs-lookup"><span data-stu-id="62553-160">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="62553-161">向 Index 方法添加筛选功能</span><span class="sxs-lookup"><span data-stu-id="62553-161">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="62553-162">在中*Controllers\StudentController.cs*，将为`Index`用下面的代码 （所做的更改会突出显示） 的方法：</span><span class="sxs-lookup"><span data-stu-id="62553-162">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="62553-163">已向 `Index` 方法添加 `searchString` 参数。</span><span class="sxs-lookup"><span data-stu-id="62553-163">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="62553-164">从要添加到索引视图的文本框中接收搜索字符串值。</span><span class="sxs-lookup"><span data-stu-id="62553-164">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="62553-165">你还向 LINQ 语句添加`where`子句仅选择的学生的名字或姓氏中包含搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-165">You've also added to the LINQ statement a `where` clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="62553-166">添加的语句[其中](https://msdn.microsoft.com/library/bb535040.aspx)子句执行仅当没有要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="62553-166">The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="62553-167">在许多情况下可以对实体框架实体集或作为内存中集合上的扩展方法调用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="62553-167">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="62553-168">结果通常都是相同，但在某些情况下可能会不同。</span><span class="sxs-lookup"><span data-stu-id="62553-168">The results are normally the same but in some cases may be different.</span></span>
> 
> <span data-ttu-id="62553-169">例如，.NET Framework 实现`Contains`方法将空字符串传递给它，而 SQL Server Compact 4.0 的实体框架提供程序返回空字符串零行，则返回所有行。</span><span class="sxs-lookup"><span data-stu-id="62553-169">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="62553-170">因此该示例中的代码 (将放`Where`内的语句`if`语句) 可确保对于所有版本的 SQL Server 获得相同的结果。</span><span class="sxs-lookup"><span data-stu-id="62553-170">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="62553-171">此外，.NET Framework 实现`Contains`方法默认情况下，执行区分大小写比较，但实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="62553-171">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="62553-172">因此，调用`ToUpper`使测试显式不区分大小写的方法可确保结果不更改时更改代码更高版本以使用存储库，它将返回`IEnumerable`而不是集合`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="62553-172">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="62553-173">（在 `IEnumerable` 集合上调用 `Contains` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）</span><span class="sxs-lookup"><span data-stu-id="62553-173">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
> 
> <span data-ttu-id="62553-174">Null 处理也可能会因不同的数据库提供程序，或者在使用`IQueryable`使用时，对象相比`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="62553-174">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="62553-175">例如，在某些情况下`Where`如条件`table.Column != 0`可能不会返回具有列`null`作为值。</span><span class="sxs-lookup"><span data-stu-id="62553-175">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="62553-176">有关详细信息，请参阅[的 where 子句中的 null 变量不正确处理](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl)。</span><span class="sxs-lookup"><span data-stu-id="62553-176">For more information, see [Incorrect handling of null variables in 'where' clause](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl).</span></span>


### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="62553-177">向“学生索引”视图添加搜索框</span><span class="sxs-lookup"><span data-stu-id="62553-177">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="62553-178">在中*Views\Student\Index.cshtml*，添加打开之前立即突出显示的代码`table`若要创建标题栏、 文本框中，标记和一个**搜索**按钮。</span><span class="sxs-lookup"><span data-stu-id="62553-178">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="62553-179">运行页上，输入搜索字符串，然后单击**搜索**以验证筛选是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="62553-179">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="62553-181">请注意，URL 不包含"an"搜索字符串，这意味着，如果此页加入书签，您不会获得筛选的列表，当您使用书签。</span><span class="sxs-lookup"><span data-stu-id="62553-181">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="62553-182">这同样适用于列排序链接，因为它们将对整个列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="62553-182">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="62553-183">将更改**搜索**按钮，本教程的后面使用筛选器条件的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-183">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="62553-184">向学生索引页添加分页</span><span class="sxs-lookup"><span data-stu-id="62553-184">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="62553-185">若要向学生索引页添加分页，首先你将安装**PagedList.Mvc** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="62553-185">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="62553-186">然后你将进行中的其他更改`Index`方法并添加分页链接到`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="62553-186">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="62553-187">**PagedList.Mvc**是许多很好的分页和排序的 ASP.NET MVC 中，包之一，此处使用旨在仅作为示例，不为相对于其他选择为其建议。</span><span class="sxs-lookup"><span data-stu-id="62553-187">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="62553-188">下图显示了分页链接。</span><span class="sxs-lookup"><span data-stu-id="62553-188">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="62553-190">安装 PagedList.MVC NuGet 包</span><span class="sxs-lookup"><span data-stu-id="62553-190">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="62553-191">NuGet **PagedList.Mvc**会自动安装包**PagedList**包作为依赖项。</span><span class="sxs-lookup"><span data-stu-id="62553-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="62553-192">**PagedList**打包安装`PagedList`的集合类型和扩展方法`IQueryable`和`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="62553-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="62553-193">扩展方法创建单个页面中的数据`PagedList`共集合您`IQueryable`或`IEnumerable`，和`PagedList`集合提供了一些属性和方法的简化分页。</span><span class="sxs-lookup"><span data-stu-id="62553-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="62553-194">**PagedList.Mvc**包将安装的分页帮助器显示分页按钮。</span><span class="sxs-lookup"><span data-stu-id="62553-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="62553-195">从**工具**菜单中，选择**库程序包管理器**，然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="62553-195">From the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>

<span data-ttu-id="62553-196">在中**程序包管理器控制台**窗口中，请确保**包源**是**nuget.org**并**默认项目**是**ContosoUniversity**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="62553-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

`Install-Package PagedList.Mvc`

![安装 PagedList.Mvc](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="62553-198">生成项目。</span><span class="sxs-lookup"><span data-stu-id="62553-198">Build the project.</span></span> 

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="62553-199">向 Index 方法添加分页功能</span><span class="sxs-lookup"><span data-stu-id="62553-199">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="62553-200">在中*Controllers\StudentController.cs*，添加`using`语句`PagedList`命名空间：</span><span class="sxs-lookup"><span data-stu-id="62553-200">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="62553-201">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62553-201">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

<span data-ttu-id="62553-202">此代码将添加`page`参数、 当前的排序顺序参数和当前的筛选器参数向方法签名：</span><span class="sxs-lookup"><span data-stu-id="62553-202">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="62553-203">第一次显示页面时，或者如果用户没有单击分页或排序链接，所有参数都将为 NULL。</span><span class="sxs-lookup"><span data-stu-id="62553-203">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="62553-204">如果单击分页链接后，`page`变量将包含要显示的页码。</span><span class="sxs-lookup"><span data-stu-id="62553-204">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="62553-205">一个`ViewBag`属性提供了与当前的排序顺序中，视图，因为此值必须包含在分页链接为了保持排序顺序都分页时相同：</span><span class="sxs-lookup"><span data-stu-id="62553-205">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="62553-206">另一个属性， `ViewBag.CurrentFilter`，视图提供当前筛选器字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-206">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="62553-207">此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。</span><span class="sxs-lookup"><span data-stu-id="62553-207">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="62553-208">如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。</span><span class="sxs-lookup"><span data-stu-id="62553-208">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="62553-209">在文本框中输入值并按下提交按钮，则会更改搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="62553-209">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="62553-210">在这种情况下，`searchString`参数不为 null。</span><span class="sxs-lookup"><span data-stu-id="62553-210">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="62553-211">该方法的末尾`ToPagedList`学生的扩展方法`IQueryable`对象将学生查询转换为支持分页的集合类型中的学生的单个页。</span><span class="sxs-lookup"><span data-stu-id="62553-211">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="62553-212">该单个学生页面然后传递给视图：</span><span class="sxs-lookup"><span data-stu-id="62553-212">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="62553-213">`ToPagedList` 方法需要一个页码。</span><span class="sxs-lookup"><span data-stu-id="62553-213">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="62553-214">两个问号表示[null 合并运算符](https://msdn.microsoft.com/library/ms173224.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62553-214">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="62553-215">NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。</span><span class="sxs-lookup"><span data-stu-id="62553-215">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="62553-216">向学生索引视图添加分页链接</span><span class="sxs-lookup"><span data-stu-id="62553-216">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="62553-217">在中*Views\Student\Index.cshtml*，现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="62553-217">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="62553-218">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="62553-218">The changes are highlighted.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

<span data-ttu-id="62553-219">页面顶部的 `@model` 语句指定视图现在获取的是 `PagedList` 对象，而不是 `List` 对象。</span><span class="sxs-lookup"><span data-stu-id="62553-219">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="62553-220">`using`语句`PagedList.Mvc`，访问 MVC 帮助程序的分页按钮。</span><span class="sxs-lookup"><span data-stu-id="62553-220">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="62553-221">该代码使用的重载[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) ，它指定允许[FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。</span><span class="sxs-lookup"><span data-stu-id="62553-221">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="62553-222">默认值[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)提交表单数据对于 POST，这意味着，参数将 HTTP 消息正文中而不是在 URL 作为查询字符串传递。</span><span class="sxs-lookup"><span data-stu-id="62553-222">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="62553-223">当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。</span><span class="sxs-lookup"><span data-stu-id="62553-223">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="62553-224">[使用 HTTP GET 的 W3C 指南](http://www.w3.org/2001/tag/doc/whenToUseGet.html)建议操作不会导致更新时应使用 GET。</span><span class="sxs-lookup"><span data-stu-id="62553-224">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="62553-225">单击新页面时可以看到当前的搜索字符串，将使用当前搜索字符串初始化文本框。</span><span class="sxs-lookup"><span data-stu-id="62553-225">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="62553-226">列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：</span><span class="sxs-lookup"><span data-stu-id="62553-226">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="62553-227">显示当前页和总页数。</span><span class="sxs-lookup"><span data-stu-id="62553-227">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="62553-228">如果没有要显示的页面，会显示"的 0 页 0"。</span><span class="sxs-lookup"><span data-stu-id="62553-228">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="62553-229">(在这种情况下页面数大于页计数因为`Model.PageNumber`为 1，和`Model.PageCount`为 0。)</span><span class="sxs-lookup"><span data-stu-id="62553-229">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="62553-230">通过显示分页按钮`PagedListPager`帮助程序：</span><span class="sxs-lookup"><span data-stu-id="62553-230">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="62553-231">`PagedListPager`帮助器提供多种可自定义，包括 Url 和样式设置的选项。</span><span class="sxs-lookup"><span data-stu-id="62553-231">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="62553-232">有关详细信息，请参阅[TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 站点上。</span><span class="sxs-lookup"><span data-stu-id="62553-232">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="62553-233">运行页。</span><span class="sxs-lookup"><span data-stu-id="62553-233">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="62553-235">单击不同排序顺序的分页链接，以确保分页正常工作。</span><span class="sxs-lookup"><span data-stu-id="62553-235">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="62553-236">然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。</span><span class="sxs-lookup"><span data-stu-id="62553-236">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="62553-237">创建有关页面，其中显示学生统计信息</span><span class="sxs-lookup"><span data-stu-id="62553-237">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="62553-238">对于 Contoso 大学网站的一页，将显示每个注册日期注册学生的数量。</span><span class="sxs-lookup"><span data-stu-id="62553-238">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="62553-239">这需要对组进行分组和简单计算。</span><span class="sxs-lookup"><span data-stu-id="62553-239">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="62553-240">若要完成此操作，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="62553-240">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="62553-241">为需要传递给视图的数据创建一个视图模型类。</span><span class="sxs-lookup"><span data-stu-id="62553-241">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="62553-242">修改`About`中的方法`Home`控制器。</span><span class="sxs-lookup"><span data-stu-id="62553-242">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="62553-243">修改`About`视图。</span><span class="sxs-lookup"><span data-stu-id="62553-243">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="62553-244">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="62553-244">Create the View Model</span></span>

<span data-ttu-id="62553-245">创建*Viewmodel*项目文件夹中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="62553-245">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="62553-246">在该文件夹中，将类文件添加*EnrollmentDateGroup.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62553-246">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="62553-247">修改主控制器</span><span class="sxs-lookup"><span data-stu-id="62553-247">Modify the Home Controller</span></span>

<span data-ttu-id="62553-248">在中*HomeController.cs*，添加以下`using`语句的文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="62553-248">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="62553-249">类的左大括号后立即添加数据库上下文的类变量：</span><span class="sxs-lookup"><span data-stu-id="62553-249">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="62553-250">将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62553-250">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="62553-251">LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。</span><span class="sxs-lookup"><span data-stu-id="62553-251">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="62553-252">添加`Dispose`方法：</span><span class="sxs-lookup"><span data-stu-id="62553-252">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="62553-253">修改“关于”视图</span><span class="sxs-lookup"><span data-stu-id="62553-253">Modify the About View</span></span>

<span data-ttu-id="62553-254">中的代码替换*Views\Home\About.cshtml*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="62553-254">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="62553-255">运行应用并单击**有关**链接。</span><span class="sxs-lookup"><span data-stu-id="62553-255">Run the app and click the **About** link.</span></span> <span data-ttu-id="62553-256">表格中会显示每个注册日期的学生计数。</span><span class="sxs-lookup"><span data-stu-id="62553-256">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="62553-258">总结</span><span class="sxs-lookup"><span data-stu-id="62553-258">Summary</span></span>

<span data-ttu-id="62553-259">在本教程中已了解如何创建数据模型并实现基本的 CRUD，排序、 筛选、 分页和分组功能。</span><span class="sxs-lookup"><span data-stu-id="62553-259">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="62553-260">在下一教程将开始通过展开数据模型来查看更高级的主题。</span><span class="sxs-lookup"><span data-stu-id="62553-260">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="62553-261">请在你喜欢本教程的内容，我们可以提高上留下反馈。</span><span class="sxs-lookup"><span data-stu-id="62553-261">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="62553-262">此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="62553-262">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="62553-263">其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="62553-263">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62553-264">[上一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [下一页](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="62553-264">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
