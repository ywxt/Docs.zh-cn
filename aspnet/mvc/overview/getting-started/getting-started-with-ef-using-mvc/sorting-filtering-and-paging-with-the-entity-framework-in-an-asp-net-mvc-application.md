---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: "排序、 筛选和分页与实体框架中的 ASP.NET MVC 应用程序 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/01/2015
ms.topic: article
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d54c0e133bc2f6f2021821dc16cdf86cc23a5667
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="bbe4f-103">排序、 筛选和分页与实体框架中的 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="bbe4f-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="bbe4f-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bbe4f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="bbe4f-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="bbe4f-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="bbe4f-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="bbe4f-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="bbe4f-108">在前面的教程中实现一组有关的基本 CRUD 操作的 web 页面`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-108">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="bbe4f-109">在本教程中你将添加排序、 筛选和分页功能**学生**索引页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-109">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="bbe4f-110">你还将创建简单分组的页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-110">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="bbe4f-111">下图显示哪些页面将如下所示完成后。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-111">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="bbe4f-112">列标题是用户可以单击以按该列排序的链接。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-112">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="bbe4f-113">单击列标题反复将在升序和降序之间切换。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-113">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="bbe4f-115">将列排序链接添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="bbe4f-115">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="bbe4f-116">若要添加排序学生索引页，你将更改`Index`方法`Student`控制器并将代码添加到`Student`索引视图。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-116">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="bbe4f-117">添加排序功能向 Index 方法</span><span class="sxs-lookup"><span data-stu-id="bbe4f-117">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="bbe4f-118">在*Controllers\StudentController.cs*，替换`Index`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-118">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="bbe4f-119">此代码接收`sortOrder`从 URL 中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-119">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="bbe4f-120">ASP.NET MVC 提供查询字符串值作为参数传递给的操作方法。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-120">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="bbe4f-121">参数将为"Name"日期"，可以选择后跟下划线和字符串"desc"指定降序顺序的字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-121">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="bbe4f-122">默认排序顺序为升序。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-122">The default sort order is ascending.</span></span>

<span data-ttu-id="bbe4f-123">第一次请求索引页时，没有任何查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-123">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="bbe4f-124">升序排序依据显示学生`LastName`，这是默认设置，如回退通过用例中建立`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-124">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="bbe4f-125">当用户单击列标题超链接，相应`sortOrder`查询字符串中提供值。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-125">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="bbe4f-126">这两个`ViewBag`变量使用，以便该视图可以配置使用相应的查询字符串值的列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-126">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="bbe4f-127">这些是三元语句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-127">These are ternary statements.</span></span> <span data-ttu-id="bbe4f-128">第一个指定，如果`sortOrder`参数为 null 或为空，`ViewBag.NameSortParm`应设置为"名称\_desc"; 否则为它应设置为一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-128">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="bbe4f-129">这两个语句启用要设置列标题的超链接，如下所示的视图：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-129">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="bbe4f-130">当前的排序顺序</span><span class="sxs-lookup"><span data-stu-id="bbe4f-130">Current sort order</span></span> | <span data-ttu-id="bbe4f-131">最后一个名称超链接</span><span class="sxs-lookup"><span data-stu-id="bbe4f-131">Last Name Hyperlink</span></span> | <span data-ttu-id="bbe4f-132">日期超链接</span><span class="sxs-lookup"><span data-stu-id="bbe4f-132">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbe4f-133">上次名称升序排列</span><span class="sxs-lookup"><span data-stu-id="bbe4f-133">Last Name ascending</span></span> | <span data-ttu-id="bbe4f-134">descending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-134">descending</span></span> | <span data-ttu-id="bbe4f-135">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-135">ascending</span></span> |
| <span data-ttu-id="bbe4f-136">上次名称降序</span><span class="sxs-lookup"><span data-stu-id="bbe4f-136">Last Name descending</span></span> | <span data-ttu-id="bbe4f-137">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-137">ascending</span></span> | <span data-ttu-id="bbe4f-138">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-138">ascending</span></span> |
| <span data-ttu-id="bbe4f-139">升序的日期</span><span class="sxs-lookup"><span data-stu-id="bbe4f-139">Date ascending</span></span> | <span data-ttu-id="bbe4f-140">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-140">ascending</span></span> | <span data-ttu-id="bbe4f-141">descending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-141">descending</span></span> |
| <span data-ttu-id="bbe4f-142">日期降序</span><span class="sxs-lookup"><span data-stu-id="bbe4f-142">Date descending</span></span> | <span data-ttu-id="bbe4f-143">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-143">ascending</span></span> | <span data-ttu-id="bbe4f-144">ascending</span><span class="sxs-lookup"><span data-stu-id="bbe4f-144">ascending</span></span> |

<span data-ttu-id="bbe4f-145">该方法使用[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)指定要作为排序依据的列。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-145">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="bbe4f-146">该代码创建[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)变量之前`switch`语句，将修改在`switch`语句，并调用`ToList`方法之后`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-146">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="bbe4f-147">当你创建和修改`IQueryable`变量，没有查询发送到数据库。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-147">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="bbe4f-148">您将转换之前，不执行查询`IQueryable`到通过调用方法，如集合对象`ToList`。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-148">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="bbe4f-149">因此，此代码将导致直到不执行单个查询`return View`语句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-149">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="bbe4f-150">作为编写为每个排序顺序不同 LINQ 语句的替代方法，你可以动态创建 LINQ 语句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-150">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="bbe4f-151">有关动态 LINQ 的信息，请参阅[动态 LINQ](https://go.microsoft.com/fwlink/?LinkID=323957)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-151">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="bbe4f-152">添加列标题的学生索引视图的超链接</span><span class="sxs-lookup"><span data-stu-id="bbe4f-152">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="bbe4f-153">在*Views\Student\Index.cshtml*，替换`<tr>`和`<th>`具有突出显示的代码的标题行的元素：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-153">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="bbe4f-154">此代码使用中的信息`ViewBag`属性设置超链接与相应的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-154">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="bbe4f-155">运行页面并单击**姓氏**和**注册日期**列标题，以验证该排序工作原理。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-155">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="bbe4f-157">单击后**姓氏**标题下，按降序姓氏的顺序显示学生。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-157">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="bbe4f-158">将一个搜索框添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="bbe4f-158">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="bbe4f-159">若要添加到学生索引页过滤条件，将向视图添加一个文本框和提交按钮，并将中的相应更改`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-159">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="bbe4f-160">文本框中，你将输入要在名字和姓氏字段中搜索的字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-160">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="bbe4f-161">将筛选功能添加到索引方法</span><span class="sxs-lookup"><span data-stu-id="bbe4f-161">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="bbe4f-162">在*Controllers\StudentController.cs*，替换`Index`方法替换为以下代码 （突出显示所做的更改）：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-162">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="bbe4f-163">你已添加`searchString`参数`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-163">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="bbe4f-164">从将添加到索引视图的文本框中接收到搜索字符串值。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-164">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="bbe4f-165">你亦已添加到 LINQ 语句`where`选择仅学生的名字或姓氏包含搜索字符串的子句。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-165">You've also added to the LINQ statement a `where` clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="bbe4f-166">添加语句[其中](https://msdn.microsoft.com/library/bb535040.aspx)子句执行只有在要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-166">The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="bbe4f-167">在许多情况下你可以调用相同的方法，在实体框架实体集或作为扩展方法对内存中集合。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-167">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="bbe4f-168">结果通常都是相同，但在某些情况下可能会不同。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-168">The results are normally the same but in some cases may be different.</span></span>
> 
> <span data-ttu-id="bbe4f-169">例如，.NET Framework 实现的`Contains`方法将返回所有行，将一个空字符串传递给它，而 SQL Server Compact 4.0 的实体框架提供程序都返回空字符串零行。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-169">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="bbe4f-170">因此该示例中的代码 (将`Where`内的语句`if`语句) 可确保对于所有版本的 SQL Server 获得相同的结果。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-170">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="bbe4f-171">此外，.NET Framework 实现的`Contains`方法默认情况下，执行区分大小写的比较，但在实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-171">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="bbe4f-172">因此，调用`ToUpper`来进行测试显式不区分大小写的方法可确保在更改代码更高版本以使用一个存储库，它将返回时，结果不会发生更改`IEnumerable`而不是集合`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-172">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="bbe4f-173">(当你调用`Contains`方法`IEnumerable`集合，你将获取.NET Framework 实现; 当上调用它`IQueryable`对象，则会出现的数据库提供程序实现。)</span><span class="sxs-lookup"><span data-stu-id="bbe4f-173">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
> 
> <span data-ttu-id="bbe4f-174">Null 处理可能也会不同的数据库提供程序，或者在使用不同`IQueryable`使用时，对象相比`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-174">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="bbe4f-175">例如，在某些情况下`Where`如条件`table.Column != 0`可能不会返回具有列`null`作为值。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-175">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="bbe4f-176">有关详细信息，请参阅['where' 子句中的 null 变量的不正确处理](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-176">For more information, see [Incorrect handling of null variables in 'where' clause](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl).</span></span>


### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="bbe4f-177">将一个搜索框添加到学生索引视图</span><span class="sxs-lookup"><span data-stu-id="bbe4f-177">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="bbe4f-178">在*Views\Student\Index.cshtml*，添加突出显示的代码在打开之前立即`table`才能创建标题，文本框中，标记和**搜索**按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-178">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="bbe4f-179">运行页面，输入搜索字符串，然后单击**搜索**以验证筛选是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-179">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="bbe4f-181">请注意 URL 不包含""搜索字符串，这意味着，如果此页加入书签，你不会获得的筛选的列表，当你使用书签。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-181">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="bbe4f-182">这还适用于列的排序链接，因为它们将对整个列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-182">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="bbe4f-183">你将更改**搜索**按钮以更高版本在本教程中使用 for 筛选条件的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-183">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="bbe4f-184">将分页添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="bbe4f-184">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="bbe4f-185">若要将分页添加到学生索引页，你将首先安装**PagedList.Mvc** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-185">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="bbe4f-186">然后你将使中的其他更改`Index`方法和分页将链接添加到`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-186">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="bbe4f-187">**PagedList.Mvc**是许多良好分页和 ASP.NET MVC 的排序包之一，它在本文中的使用应仅作为示例，不是相对于其他选择为其建议。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-187">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="bbe4f-188">下图显示分页链接。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-188">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="bbe4f-190">安装 PagedList.MVC NuGet 包</span><span class="sxs-lookup"><span data-stu-id="bbe4f-190">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="bbe4f-191">NuGet **PagedList.Mvc**包会自动安装**PagedList**作为依赖项包。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="bbe4f-192">**PagedList**包安装`PagedList`集合类型和扩展方法`IQueryable`和`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="bbe4f-193">扩展方法创建一个页面中的数据中`PagedList`集合外的你`IQueryable`或`IEnumerable`，和`PagedList`集合提供了一些属性和方法，以方便分页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="bbe4f-194">**PagedList.Mvc**程序包将安装的分页的帮助程序显示分页按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="bbe4f-195">从**工具**菜单上，选择**库程序包管理器**然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-195">From the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>

<span data-ttu-id="bbe4f-196">在**程序包管理器控制台**窗口中，请确保**包源**是**nuget.org**和**默认项目**是**ContosoUniversity**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

`Install-Package PagedList.Mvc`

![Install PagedList.Mvc](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="bbe4f-198">生成项目。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-198">Build the project.</span></span> 

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="bbe4f-199">将分页功能添加到索引方法</span><span class="sxs-lookup"><span data-stu-id="bbe4f-199">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="bbe4f-200">在*Controllers\StudentController.cs*，添加`using`语句`PagedList`命名空间：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-200">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="bbe4f-201">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-201">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

<span data-ttu-id="bbe4f-202">此代码将添加`page`参数、 当前的排序顺序参数和向方法签名的当前筛选器参数：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-202">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="bbe4f-203">第一次显示页面，或如果用户未单击分页或排序链接，则所有参数将都为 null。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-203">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="bbe4f-204">如果单击的分页链接，`page`变量将包含要显示的页码。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-204">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="bbe4f-205">A`ViewBag`属性提供了与当前的排序顺序中，视图，因为这必须包含在分页链接以保持排序顺序分页时相同：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-205">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="bbe4f-206">另一个属性， `ViewBag.CurrentFilter`，与当前的筛选器字符串中提供的视图。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-206">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="bbe4f-207">若要分页，过程维护的筛选器设置情况下，此值必须包括在分页链接，必须还原到文本框中时重新显示页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-207">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="bbe4f-208">如果分页期间更改搜索字符串，页将显示被重置为 1，因为新的筛选器可能会导致不同的数据，以显示。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-208">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="bbe4f-209">在文本框中输入了值，按下提交按钮，则会更改搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-209">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="bbe4f-210">在这种情况下，`searchString`参数不为 null。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-210">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="bbe4f-211">该方法的末尾`ToPagedList`上学生的扩展方法`IQueryable`对象将学生查询转换为支持分页的集合类型中的学生的单页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-211">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="bbe4f-212">学生的单个页面然后传递给视图：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-212">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="bbe4f-213">`ToPagedList`方法采用页号。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-213">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="bbe4f-214">两个问号表示[null 合并运算符](https://msdn.microsoft.com/library/ms173224.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-214">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="bbe4f-215">Null 合并运算符定义可以为 null 的类型; 默认值表达式`(page ?? 1)`意味着返回的值`page`如果它具有一个值，或返回 1，如果`page`为 null。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-215">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="bbe4f-216">将分页链接添加到学生索引视图</span><span class="sxs-lookup"><span data-stu-id="bbe4f-216">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="bbe4f-217">在*Views\Student\Index.cshtml*，替换为以下代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-217">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="bbe4f-218">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-218">The changes are highlighted.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

<span data-ttu-id="bbe4f-219">`@model`页顶部的语句指定视图现在获取`PagedList`对象而不是`List`对象。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-219">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="bbe4f-220">`using`语句`PagedList.Mvc`分页按钮访问的 MVC 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-220">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="bbe4f-221">该代码使用的重载[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) ，它指定允许[FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-221">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="bbe4f-222">默认值[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)提交表单 post，这意味着，参数将在 HTTP 消息正文中，不能在 URL 作为查询字符串传递的数据。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-222">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="bbe4f-223">指定 HTTP GET 时，窗体数据是在 URL 中作为查询字符串传递，这使得用户能够创建 URL 的书签。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-223">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="bbe4f-224">[使用 HTTP GET 的 W3C 准则](http://www.w3.org/2001/tag/doc/whenToUseGet.html)建议的操作未导致更新时，你应使用 GET。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-224">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="bbe4f-225">因此，当你单击一个新页你可以看到当前的搜索字符串，将使用当前的搜索字符串初始化文本框。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-225">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="bbe4f-226">列标题链接使用查询字符串将当前的搜索字符串传递到控制器，以便用户可以在筛选器的结果中进行排序：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-226">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="bbe4f-227">显示当前页和总页数。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-227">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="bbe4f-228">如果不没有显示任何页，将显示"页 0 0"。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-228">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="bbe4f-229">(在这种情况下页号大于页计数因为`Model.PageNumber`为 1，和`Model.PageCount`为 0。)</span><span class="sxs-lookup"><span data-stu-id="bbe4f-229">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="bbe4f-230">分页按钮显示通过`PagedListPager`帮助器：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-230">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="bbe4f-231">`PagedListPager`帮助器提供了多种你可以自定义，包括 Url 和样式的选项。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-231">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="bbe4f-232">有关详细信息，请参阅[TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 站点上。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-232">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="bbe4f-233">运行页面。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-233">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="bbe4f-235">单击以确保分页工作原理的不同的排序顺序中的分页链接。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-235">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="bbe4f-236">然后输入搜索字符串，然后重试以验证分页还适用正确使用排序和筛选的分页。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-236">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="bbe4f-237">创建有关显示学生统计信息的页面</span><span class="sxs-lookup"><span data-stu-id="bbe4f-237">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="bbe4f-238">Contoso 大学网站的有关页面，将显示如何很多学生已注册的每个注册日期。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-238">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="bbe4f-239">这要求在组上的分组和简单计算。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-239">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="bbe4f-240">要完成此操作，将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-240">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="bbe4f-241">创建一个视图模型类，你需要将传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-241">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="bbe4f-242">修改`About`中的方法`Home`控制器。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-242">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="bbe4f-243">修改`About`视图。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-243">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="bbe4f-244">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="bbe4f-244">Create the View Model</span></span>

<span data-ttu-id="bbe4f-245">创建*Viewmodel*项目文件夹中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-245">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="bbe4f-246">在该文件夹中，将类文件添加*EnrollmentDateGroup.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-246">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="bbe4f-247">修改主控制器</span><span class="sxs-lookup"><span data-stu-id="bbe4f-247">Modify the Home Controller</span></span>

<span data-ttu-id="bbe4f-248">在*HomeController.cs*，添加以下`using`语句文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-248">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="bbe4f-249">类的左大括号后立即添加的数据库上下文的类变量：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-249">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="bbe4f-250">将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-250">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="bbe4f-251">LINQ 语句学生实体分组按注册日期，计算每个组中的实体数并将结果存储在集合中的`EnrollmentDateGroup`查看模型对象。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-251">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="bbe4f-252">添加`Dispose`方法：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-252">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="bbe4f-253">修改有关视图</span><span class="sxs-lookup"><span data-stu-id="bbe4f-253">Modify the About View</span></span>

<span data-ttu-id="bbe4f-254">中的代码替换*Views\Home\About.cshtml*文件替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bbe4f-254">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="bbe4f-255">运行应用并单击**有关**链接。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-255">Run the app and click the **About** link.</span></span> <span data-ttu-id="bbe4f-256">每个注册日期的学生计数显示在表格中。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-256">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="bbe4f-258">摘要</span><span class="sxs-lookup"><span data-stu-id="bbe4f-258">Summary</span></span>

<span data-ttu-id="bbe4f-259">在本教程中，你已了解如何创建数据模型和实现基本的 CRUD，排序、 筛选、 分页和分组功能。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-259">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="bbe4f-260">在下一教程将首先通过展开数据模型来查看更高级的主题。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-260">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="bbe4f-261">请在如何喜欢本教程的方式，我们可以提高上，留下反馈。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-261">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="bbe4f-262">你还可以请求新主题[教我编写代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-262">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="bbe4f-263">在找不到其他实体框架资源的链接[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="bbe4f-263">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="bbe4f-264">[上一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[下一页](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="bbe4f-264">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
