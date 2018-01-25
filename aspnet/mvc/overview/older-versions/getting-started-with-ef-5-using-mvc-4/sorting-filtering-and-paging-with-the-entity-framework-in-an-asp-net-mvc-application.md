---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: "排序、 筛选和分页与实体框架中的 ASP.NET MVC 应用程序 (3 的 10) |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f9b68abeba19561a327bad5ee4be80d79af1a550
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a><span data-ttu-id="08286-103">排序、 筛选和分页与实体框架中的 ASP.NET MVC 应用程序 (3 的 10)</span><span class="sxs-lookup"><span data-stu-id="08286-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application (3 of 10)</span></span>
====================
<span data-ttu-id="08286-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="08286-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="08286-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="08286-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="08286-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="08286-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="08286-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="08286-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="08286-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="08286-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="08286-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="08286-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="08286-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="08286-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="08286-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="08286-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="08286-112">在前面的教程中实现一组有关的基本 CRUD 操作的 web 页面`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="08286-112">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="08286-113">在本教程中你将添加排序、 筛选和分页功能**学生**索引页。</span><span class="sxs-lookup"><span data-stu-id="08286-113">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="08286-114">你还将创建简单分组的页。</span><span class="sxs-lookup"><span data-stu-id="08286-114">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="08286-115">下图显示哪些页面将如下所示完成后。</span><span class="sxs-lookup"><span data-stu-id="08286-115">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="08286-116">列标题是用户可以单击以按该列排序的链接。</span><span class="sxs-lookup"><span data-stu-id="08286-116">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="08286-117">单击列标题反复将在升序和降序之间切换。</span><span class="sxs-lookup"><span data-stu-id="08286-117">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="08286-119">将列排序链接添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="08286-119">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="08286-120">若要添加排序学生索引页，你将更改`Index`方法`Student`控制器并将代码添加到`Student`索引视图。</span><span class="sxs-lookup"><span data-stu-id="08286-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="08286-121">添加排序功能向 Index 方法</span><span class="sxs-lookup"><span data-stu-id="08286-121">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="08286-122">在*Controllers\StudentController.cs*，替换`Index`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="08286-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="08286-123">此代码接收`sortOrder`从 URL 中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="08286-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="08286-124">ASP.NET MVC 提供查询字符串值作为参数传递给的操作方法。</span><span class="sxs-lookup"><span data-stu-id="08286-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="08286-125">参数将为"Name"日期"，可以选择后跟下划线和字符串"desc"指定降序顺序的字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-125">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="08286-126">默认排序顺序为升序。</span><span class="sxs-lookup"><span data-stu-id="08286-126">The default sort order is ascending.</span></span>

<span data-ttu-id="08286-127">第一次请求索引页时，没有任何查询字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="08286-128">升序排序依据显示学生`LastName`，这是默认设置，如回退通过用例中建立`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="08286-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="08286-129">当用户单击列标题超链接，相应`sortOrder`查询字符串中提供值。</span><span class="sxs-lookup"><span data-stu-id="08286-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="08286-130">这两个`ViewBag`变量使用，以便该视图可以配置使用相应的查询字符串值的列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="08286-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="08286-131">这些是三元语句。</span><span class="sxs-lookup"><span data-stu-id="08286-131">These are ternary statements.</span></span> <span data-ttu-id="08286-132">第一个指定，如果`sortOrder`参数为 null 或为空，`ViewBag.NameSortParm`应设置为"名称\_desc"; 否则为它应设置为一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="08286-133">这两个语句启用要设置列标题的超链接，如下所示的视图：</span><span class="sxs-lookup"><span data-stu-id="08286-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="08286-134">当前的排序顺序</span><span class="sxs-lookup"><span data-stu-id="08286-134">Current sort order</span></span> | <span data-ttu-id="08286-135">最后一个名称超链接</span><span class="sxs-lookup"><span data-stu-id="08286-135">Last Name Hyperlink</span></span> | <span data-ttu-id="08286-136">日期超链接</span><span class="sxs-lookup"><span data-stu-id="08286-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08286-137">上次名称升序排列</span><span class="sxs-lookup"><span data-stu-id="08286-137">Last Name ascending</span></span> | <span data-ttu-id="08286-138">descending</span><span class="sxs-lookup"><span data-stu-id="08286-138">descending</span></span> | <span data-ttu-id="08286-139">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-139">ascending</span></span> |
| <span data-ttu-id="08286-140">上次名称降序</span><span class="sxs-lookup"><span data-stu-id="08286-140">Last Name descending</span></span> | <span data-ttu-id="08286-141">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-141">ascending</span></span> | <span data-ttu-id="08286-142">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-142">ascending</span></span> |
| <span data-ttu-id="08286-143">升序的日期</span><span class="sxs-lookup"><span data-stu-id="08286-143">Date ascending</span></span> | <span data-ttu-id="08286-144">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-144">ascending</span></span> | <span data-ttu-id="08286-145">descending</span><span class="sxs-lookup"><span data-stu-id="08286-145">descending</span></span> |
| <span data-ttu-id="08286-146">日期降序</span><span class="sxs-lookup"><span data-stu-id="08286-146">Date descending</span></span> | <span data-ttu-id="08286-147">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-147">ascending</span></span> | <span data-ttu-id="08286-148">ascending</span><span class="sxs-lookup"><span data-stu-id="08286-148">ascending</span></span> |

<span data-ttu-id="08286-149">该方法使用[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)指定要作为排序依据的列。</span><span class="sxs-lookup"><span data-stu-id="08286-149">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="08286-150">该代码创建[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)变量之前`switch`语句，将修改在`switch`语句，并调用`ToList`方法之后`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="08286-150">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="08286-151">当你创建和修改`IQueryable`变量，没有查询发送到数据库。</span><span class="sxs-lookup"><span data-stu-id="08286-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="08286-152">您将转换之前，不执行查询`IQueryable`到通过调用方法，如集合对象`ToList`。</span><span class="sxs-lookup"><span data-stu-id="08286-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="08286-153">因此，此代码将导致直到不执行单个查询`return View`语句。</span><span class="sxs-lookup"><span data-stu-id="08286-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="08286-154">添加列标题的学生索引视图的超链接</span><span class="sxs-lookup"><span data-stu-id="08286-154">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="08286-155">在*Views\Student\Index.cshtml*，替换`<tr>`和`<th>`具有突出显示的代码的标题行的元素：</span><span class="sxs-lookup"><span data-stu-id="08286-155">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="08286-156">此代码使用中的信息`ViewBag`属性设置超链接与相应的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="08286-156">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="08286-157">运行页面并单击**姓氏**和**注册日期**列标题，以验证该排序工作原理。</span><span class="sxs-lookup"><span data-stu-id="08286-157">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="08286-159">单击后**姓氏**标题下，按降序姓氏的顺序显示学生。</span><span class="sxs-lookup"><span data-stu-id="08286-159">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="08286-160">将一个搜索框添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="08286-160">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="08286-161">若要添加到学生索引页过滤条件，将向视图添加一个文本框和提交按钮，并将中的相应更改`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="08286-161">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="08286-162">文本框中，你将输入要在名字和姓氏字段中搜索的字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-162">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="08286-163">将筛选功能添加到索引方法</span><span class="sxs-lookup"><span data-stu-id="08286-163">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="08286-164">在*Controllers\StudentController.cs*，替换`Index`方法替换为以下代码 （突出显示所做的更改）：</span><span class="sxs-lookup"><span data-stu-id="08286-164">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="08286-165">你已添加`searchString`参数`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="08286-165">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="08286-166">你亦已添加到 LINQ 语句`where`clausethat 选择仅学生的名字或姓氏包含搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-166">You've also added to the LINQ statement a `where` clausethat selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="08286-167">从将添加到索引视图的文本框中接收到搜索字符串值。添加语句[其中](https://msdn.microsoft.com/library/bb535040.aspx)子句执行只有在要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="08286-167">The search string value is received from a text box that you'll add to the Index view.The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="08286-168">在许多情况下你可以调用相同的方法，在实体框架实体集或作为扩展方法对内存中集合。</span><span class="sxs-lookup"><span data-stu-id="08286-168">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="08286-169">结果通常都是相同，但在某些情况下可能会不同。</span><span class="sxs-lookup"><span data-stu-id="08286-169">The results are normally the same but in some cases may be different.</span></span> <span data-ttu-id="08286-170">例如，.NET Framework 实现的`Contains`方法将返回所有行，将一个空字符串传递给它，而 SQL Server Compact 4.0 的实体框架提供程序都返回空字符串零行。</span><span class="sxs-lookup"><span data-stu-id="08286-170">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="08286-171">因此该示例中的代码 (将`Where`内的语句`if`语句) 可确保对于所有版本的 SQL Server 获得相同的结果。</span><span class="sxs-lookup"><span data-stu-id="08286-171">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="08286-172">此外，.NET Framework 实现的`Contains`方法默认情况下，执行区分大小写的比较，但在实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="08286-172">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="08286-173">因此，调用`ToUpper`来进行测试显式不区分大小写的方法可确保在更改代码更高版本以使用一个存储库，它将返回时，结果不会发生更改`IEnumerable`而不是集合`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="08286-173">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="08286-174">(当你调用`Contains`方法`IEnumerable`集合，你将获取.NET Framework 实现; 当上调用它`IQueryable`对象，则会出现的数据库提供程序实现。)</span><span class="sxs-lookup"><span data-stu-id="08286-174">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>


### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="08286-175">将一个搜索框添加到学生索引视图</span><span class="sxs-lookup"><span data-stu-id="08286-175">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="08286-176">在*Views\Student\Index.cshtml*，添加突出显示的代码在打开之前立即`table`才能创建标题，文本框中，标记和**搜索**按钮。</span><span class="sxs-lookup"><span data-stu-id="08286-176">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="08286-177">运行页面，输入搜索字符串，然后单击**搜索**以验证筛选是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="08286-177">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="08286-179">请注意 URL 不包含""搜索字符串，这意味着，如果此页加入书签，你不会获得的筛选的列表，当你使用书签。</span><span class="sxs-lookup"><span data-stu-id="08286-179">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="08286-180">你将更改**搜索**按钮以更高版本在本教程中使用 for 筛选条件的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-180">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="08286-181">将分页添加到学生索引页</span><span class="sxs-lookup"><span data-stu-id="08286-181">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="08286-182">若要将分页添加到学生索引页，你将首先安装**PagedList.Mvc** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="08286-182">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="08286-183">然后你将使中的其他更改`Index`方法和分页将链接添加到`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="08286-183">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="08286-184">**PagedList.Mvc**是许多良好分页和 ASP.NET MVC 的排序包之一，它在本文中的使用应仅作为示例，不是相对于其他选择为其建议。</span><span class="sxs-lookup"><span data-stu-id="08286-184">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="08286-185">下图显示分页链接。</span><span class="sxs-lookup"><span data-stu-id="08286-185">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="08286-187">安装 PagedList.MVC NuGet 包</span><span class="sxs-lookup"><span data-stu-id="08286-187">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="08286-188">NuGet **PagedList.Mvc**包会自动安装**PagedList**作为依赖项包。</span><span class="sxs-lookup"><span data-stu-id="08286-188">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="08286-189">**PagedList**包安装`PagedList`集合类型和扩展方法`IQueryable`和`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="08286-189">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="08286-190">扩展方法创建一个页面中的数据中`PagedList`集合外的你`IQueryable`或`IEnumerable`，和`PagedList`集合提供了一些属性和方法，以方便分页。</span><span class="sxs-lookup"><span data-stu-id="08286-190">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="08286-191">**PagedList.Mvc**程序包将安装的分页的帮助程序显示分页按钮。</span><span class="sxs-lookup"><span data-stu-id="08286-191">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="08286-192">从**工具**菜单上，选择**库程序包管理器**然后**管理解决方案的 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="08286-192">From the **Tools** menu, select **Library Package Manager** and then **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="08286-193">在**管理 NuGet 包**对话框中，单击**联机**在左侧选项卡，然后在搜索框中输入"分页"。</span><span class="sxs-lookup"><span data-stu-id="08286-193">In the **Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter "paged" in the search box.</span></span> <span data-ttu-id="08286-194">当你看到**PagedList.Mvc**包、 单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="08286-194">When you see the **PagedList.Mvc** package, click **Install**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="08286-195">在**选择项目**框中，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="08286-195">In the **Select Projects** box, click **OK**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="08286-196">将分页功能添加到索引方法</span><span class="sxs-lookup"><span data-stu-id="08286-196">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="08286-197">在*Controllers\StudentController.cs*，添加`using`语句`PagedList`命名空间：</span><span class="sxs-lookup"><span data-stu-id="08286-197">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="08286-198">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="08286-198">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="08286-199">此代码将添加`page`参数、 当前的排序顺序参数和当前筛选器参数传递给方法的签名，如下所示：</span><span class="sxs-lookup"><span data-stu-id="08286-199">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature, as shown here:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="08286-200">第一次显示页面，或如果用户未单击分页或排序链接，则所有参数将都为 null。</span><span class="sxs-lookup"><span data-stu-id="08286-200">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="08286-201">如果单击的分页链接，`page`变量将包含要显示的页码。</span><span class="sxs-lookup"><span data-stu-id="08286-201">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="08286-202">`A ViewBag`属性提供的视图具有当前的排序顺序，因为这必须包含在分页链接以保持排序顺序分页时相同：</span><span class="sxs-lookup"><span data-stu-id="08286-202">`A ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="08286-203">另一个属性， `ViewBag.CurrentFilter`，与当前的筛选器字符串中提供的视图。</span><span class="sxs-lookup"><span data-stu-id="08286-203">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="08286-204">若要分页，过程维护的筛选器设置情况下，此值必须包括在分页链接，必须还原到文本框中时重新显示页。</span><span class="sxs-lookup"><span data-stu-id="08286-204">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="08286-205">如果分页期间更改搜索字符串，页将显示被重置为 1，因为新的筛选器可能会导致不同的数据，以显示。</span><span class="sxs-lookup"><span data-stu-id="08286-205">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="08286-206">在文本框中输入了值，按下提交按钮，则会更改搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-206">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="08286-207">在这种情况下，`searchString`参数不为 null。</span><span class="sxs-lookup"><span data-stu-id="08286-207">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="08286-208">该方法的末尾`ToPagedList`上学生的扩展方法`IQueryable`对象将学生查询转换为支持分页的集合类型中的学生的单页。</span><span class="sxs-lookup"><span data-stu-id="08286-208">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="08286-209">学生的单个页面然后传递给视图：</span><span class="sxs-lookup"><span data-stu-id="08286-209">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="08286-210">`ToPagedList`方法采用页号。</span><span class="sxs-lookup"><span data-stu-id="08286-210">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="08286-211">两个问号表示[null 合并运算符](https://msdn.microsoft.com/library/ms173224.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08286-211">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="08286-212">Null 合并运算符定义可以为 null 的类型; 默认值表达式`(page ?? 1)`意味着返回的值`page`如果它具有一个值，或返回 1，如果`page`为 null。</span><span class="sxs-lookup"><span data-stu-id="08286-212">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="08286-213">将分页链接添加到学生索引视图</span><span class="sxs-lookup"><span data-stu-id="08286-213">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="08286-214">在*Views\Student\Index.cshtml*，将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="08286-214">In *Views\Student\Index.cshtml*, replace the existing code with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

<span data-ttu-id="08286-215">`@model`页顶部的语句指定视图现在获取`PagedList`对象而不是`List`对象。</span><span class="sxs-lookup"><span data-stu-id="08286-215">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="08286-216">`using`语句`PagedList.Mvc`分页按钮访问的 MVC 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="08286-216">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="08286-217">该代码使用的重载[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) ，它指定允许[FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。</span><span class="sxs-lookup"><span data-stu-id="08286-217">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="08286-218">默认值[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)提交表单 post，这意味着，参数将在 HTTP 消息正文中，不能在 URL 作为查询字符串传递的数据。</span><span class="sxs-lookup"><span data-stu-id="08286-218">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="08286-219">指定 HTTP GET 时，窗体数据是在 URL 中作为查询字符串传递，这使得用户能够创建 URL 的书签。</span><span class="sxs-lookup"><span data-stu-id="08286-219">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="08286-220">[使用 HTTP GET 的 W3C 准则](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定当操作未导致更新时应使用 GET。</span><span class="sxs-lookup"><span data-stu-id="08286-220">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) specify that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="08286-221">因此，当你单击一个新页你可以看到当前的搜索字符串，将使用当前的搜索字符串初始化文本框。</span><span class="sxs-lookup"><span data-stu-id="08286-221">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="08286-222">列标题链接使用查询字符串将当前的搜索字符串传递到控制器，以便用户可以在筛选器的结果中进行排序：</span><span class="sxs-lookup"><span data-stu-id="08286-222">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="08286-223">显示当前页和总页数。</span><span class="sxs-lookup"><span data-stu-id="08286-223">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="08286-224">如果不没有显示任何页，将显示"页 0 0"。</span><span class="sxs-lookup"><span data-stu-id="08286-224">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="08286-225">(在这种情况下页号大于页计数因为`Model.PageNumber`为 1，和`Model.PageCount`为 0。)</span><span class="sxs-lookup"><span data-stu-id="08286-225">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="08286-226">分页按钮显示通过`PagedListPager`帮助器：</span><span class="sxs-lookup"><span data-stu-id="08286-226">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="08286-227">`PagedListPager`帮助器提供了多种你可以自定义，包括 Url 和样式的选项。</span><span class="sxs-lookup"><span data-stu-id="08286-227">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="08286-228">有关详细信息，请参阅[TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 站点上。</span><span class="sxs-lookup"><span data-stu-id="08286-228">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="08286-229">运行页面。</span><span class="sxs-lookup"><span data-stu-id="08286-229">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="08286-231">单击以确保分页工作原理的不同的排序顺序中的分页链接。</span><span class="sxs-lookup"><span data-stu-id="08286-231">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="08286-232">然后输入搜索字符串，然后重试以验证分页还适用正确使用排序和筛选的分页。</span><span class="sxs-lookup"><span data-stu-id="08286-232">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="08286-233">创建有关显示学生统计信息的页面</span><span class="sxs-lookup"><span data-stu-id="08286-233">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="08286-234">Contoso 大学网站的有关页面，将显示如何很多学生已注册的每个注册日期。</span><span class="sxs-lookup"><span data-stu-id="08286-234">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="08286-235">这要求在组上的分组和简单计算。</span><span class="sxs-lookup"><span data-stu-id="08286-235">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="08286-236">要完成此操作，将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="08286-236">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="08286-237">创建一个视图模型类，你需要将传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="08286-237">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="08286-238">修改`About`中的方法`Home`控制器。</span><span class="sxs-lookup"><span data-stu-id="08286-238">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="08286-239">修改`About`视图。</span><span class="sxs-lookup"><span data-stu-id="08286-239">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="08286-240">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="08286-240">Create the View Model</span></span>

<span data-ttu-id="08286-241">创建*Viewmodel*文件夹。</span><span class="sxs-lookup"><span data-stu-id="08286-241">Create a *ViewModels* folder.</span></span> <span data-ttu-id="08286-242">在该文件夹中，将类文件添加*EnrollmentDateGroup.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="08286-242">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="08286-243">修改主控制器</span><span class="sxs-lookup"><span data-stu-id="08286-243">Modify the Home Controller</span></span>

<span data-ttu-id="08286-244">在*HomeController.cs*，添加以下`using`语句文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="08286-244">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="08286-245">类的左大括号后立即添加的数据库上下文的类变量：</span><span class="sxs-lookup"><span data-stu-id="08286-245">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="08286-246">将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="08286-246">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="08286-247">LINQ 语句学生实体分组按注册日期，计算每个组中的实体数并将结果存储在集合中的`EnrollmentDateGroup`查看模型对象。</span><span class="sxs-lookup"><span data-stu-id="08286-247">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="08286-248">添加`Dispose`方法：</span><span class="sxs-lookup"><span data-stu-id="08286-248">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="08286-249">修改有关视图</span><span class="sxs-lookup"><span data-stu-id="08286-249">Modify the About View</span></span>

<span data-ttu-id="08286-250">中的代码替换*Views\Home\About.cshtml*文件替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="08286-250">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="08286-251">运行应用并单击**有关**链接。</span><span class="sxs-lookup"><span data-stu-id="08286-251">Run the app and click the **About** link.</span></span> <span data-ttu-id="08286-252">每个注册日期的学生计数显示在表格中。</span><span class="sxs-lookup"><span data-stu-id="08286-252">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a><span data-ttu-id="08286-254">可选： 将应用部署到 Windows Azure</span><span class="sxs-lookup"><span data-stu-id="08286-254">Optional: Deploy the app to Windows Azure</span></span>

<span data-ttu-id="08286-255">到目前为止您的应用程序已经运行本地 IIS Express 在开发计算机上。</span><span class="sxs-lookup"><span data-stu-id="08286-255">So far your application has been running locally in IIS Express on your development computer.</span></span> <span data-ttu-id="08286-256">若要使其可供其他人通过 Internet 使用，必须将其部署到 web 宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="08286-256">To make it available for other people to use over the Internet, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="08286-257">在本教程的这个可选部分将将其部署到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="08286-257">In this optional section of the tutorial you'll deploy it to a Windows Azure Web Site.</span></span>

### <a name="using-code-first-migrations-to-deploy-the-database"></a><span data-ttu-id="08286-258">使用 Code First 迁移将数据库部署</span><span class="sxs-lookup"><span data-stu-id="08286-258">Using Code First Migrations to Deploy the Database</span></span>

<span data-ttu-id="08286-259">若要将数据库部署将使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="08286-259">To deploy the database you'll use Code First Migrations.</span></span> <span data-ttu-id="08286-260">在创建使用从 Visual Studio 部署的配置设置的发布配置文件时，你将选择一个复选框，标记为**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="08286-260">When you create the publish profile that you use to configure settings for deploying from Visual Studio, you'll select a check box that is labeled **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="08286-261">此设置会导致自动配置应用程序的部署过程*Web.config*文件在目标服务器上，以便代码优先使用`MigrateDatabaseToLatestVersion`初始值设定项类。</span><span class="sxs-lookup"><span data-stu-id="08286-261">This setting causes the deployment process to automatically configure the application *Web.config* file on the destination server so that Code First uses the `MigrateDatabaseToLatestVersion` initializer class.</span></span>

<span data-ttu-id="08286-262">Visual Studio 不执行任何与数据库在部署过程。</span><span class="sxs-lookup"><span data-stu-id="08286-262">Visual Studio does not do anything with the database during the deployment process.</span></span> <span data-ttu-id="08286-263">当部署的应用程序部署后首次访问数据库时，Code First 自动创建数据库或数据库架构更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="08286-263">When the deployed application accesses the database for the first time after deployment, Code First automatically creates the database or updates the database schema to the latest version.</span></span> <span data-ttu-id="08286-264">如果应用程序实施迁移`Seed`方法，创建数据库或架构更新后的方法运行。</span><span class="sxs-lookup"><span data-stu-id="08286-264">If the application implements a Migrations `Seed` method, the method runs after the database is created or the schema is updated.</span></span>

<span data-ttu-id="08286-265">迁移过程`Seed`方法插入测试数据。</span><span class="sxs-lookup"><span data-stu-id="08286-265">Your Migrations `Seed` method inserts test data.</span></span> <span data-ttu-id="08286-266">如果你在部署到生产环境，你将必须更改`Seed`方法，以便它只会将你想要插入到你的生产数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="08286-266">If you were deploying to a production environment, you would have to change the `Seed` method so that it only inserts data that you want to be inserted into your production database.</span></span> <span data-ttu-id="08286-267">例如，当前数据模型中你可能想要开发数据库中具有真实课程但虚构学生。</span><span class="sxs-lookup"><span data-stu-id="08286-267">For example, in your current data model you might want to have real courses but fictional students in the development database.</span></span> <span data-ttu-id="08286-268">你可以编写`Seed`加载同时在开发中，并在部署到生产环境之前然后注释虚构学生方法。</span><span class="sxs-lookup"><span data-stu-id="08286-268">You can write a `Seed` method to load both in development, and then comment out the fictional students before you deploy to production.</span></span> <span data-ttu-id="08286-269">也可以编写`Seed`加载仅课程，并使用应用程序的用户界面手动测试数据库中输入虚构学生方法。</span><span class="sxs-lookup"><span data-stu-id="08286-269">Or you can write a `Seed` method to load only courses, and enter the fictional students in the test database manually by using the application's UI.</span></span>

### <a name="get-a-windows-azure-account"></a><span data-ttu-id="08286-270">获取 Windows Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="08286-270">Get a Windows Azure account</span></span>

<span data-ttu-id="08286-271">你将需要 Windows Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="08286-271">You'll need a Windows Azure account.</span></span> <span data-ttu-id="08286-272">如果你还没有一个，可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="08286-272">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="08286-273">有关详细信息，请参阅[Windows Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="08286-273">For details, see [Windows Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a><span data-ttu-id="08286-274">在 Windows Azure 中创建网站和 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="08286-274">Create a web site and a SQL database in Windows Azure</span></span>

<span data-ttu-id="08286-275">Windows Azure 网站将运行在共享宿主环境中，这意味着它与其他 Windows Azure 客户端共享的虚拟机 (Vm) 上运行。</span><span class="sxs-lookup"><span data-stu-id="08286-275">Your Windows Azure Web Site will run in a shared hosting environment, which means it runs on virtual machines (VMs) that are shared with other Windows Azure clients.</span></span> <span data-ttu-id="08286-276">共享宿主环境是在云中开始低成本方法。</span><span class="sxs-lookup"><span data-stu-id="08286-276">A shared hosting environment is a low-cost way to get started in the cloud.</span></span> <span data-ttu-id="08286-277">更高版本，如果你的 web 流量增加，应用程序可以缩放以满足需要通过在专用 Vm 上运行。</span><span class="sxs-lookup"><span data-stu-id="08286-277">Later, if your web traffic increases, the application can scale to meet the need by running on dedicated VMs.</span></span> <span data-ttu-id="08286-278">如果你需要更复杂的体系结构，你可以将其迁移到 Windows Azure 云服务。</span><span class="sxs-lookup"><span data-stu-id="08286-278">If you need a more complex architecture, you can migrate to a Windows Azure Cloud Service.</span></span> <span data-ttu-id="08286-279">在你可以根据需要配置的专用 Vm 上运行云服务。</span><span class="sxs-lookup"><span data-stu-id="08286-279">Cloud services run on dedicated VMs that you can configure according to your needs.</span></span>

<span data-ttu-id="08286-280">Windows Azure SQL 数据库是根据 SQL Server 技术构建的基于云的关系数据库服务。</span><span class="sxs-lookup"><span data-stu-id="08286-280">Windows Azure SQL Database is a cloud-based relational database service that is built on SQL Server technologies.</span></span> <span data-ttu-id="08286-281">工具和应用程序使用 SQL Server 还处理 SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="08286-281">Tools and applications that work with SQL Server also work with SQL Database.</span></span>

1. <span data-ttu-id="08286-282">在[Windows Azure 管理门户](https://manage.windowsazure.com/)，单击**网站**在左侧选项卡，然后单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="08286-282">In the [Windows Azure Management Portal](https://manage.windowsazure.com/), click **Web Sites** in the left tab, and then click **New**.</span></span>

    ![在管理门户中的新按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. <span data-ttu-id="08286-284">单击**自定义创建**。</span><span class="sxs-lookup"><span data-stu-id="08286-284">Click **CUSTOM CREATE**.</span></span>

    ![创建包含在管理门户中的数据库链接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

 <span data-ttu-id="08286-286">**新建网站-自定义创建**向导随即打开。</span><span class="sxs-lookup"><span data-stu-id="08286-286">The **New Web Site - Custom Create** wizard opens.</span></span>
3. <span data-ttu-id="08286-287">在**新网站**步骤的向导中，输入中的字符串**URL**框，以用作你的应用程序的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="08286-287">In the **New Web Site** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application.</span></span> <span data-ttu-id="08286-288">完整的 URL 将包含的你在此处输入和文本框旁边看到的后缀。</span><span class="sxs-lookup"><span data-stu-id="08286-288">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span> <span data-ttu-id="08286-289">图中显示"ConU"，但该 URL 是可能因此必须另外选择一个。</span><span class="sxs-lookup"><span data-stu-id="08286-289">The illustration shows "ConU", but that URL is probably taken so you will have to choose a different one.</span></span>

    ![创建包含在管理门户中的数据库链接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. <span data-ttu-id="08286-291">在**区域**下拉列表中，选择靠近你的区域。</span><span class="sxs-lookup"><span data-stu-id="08286-291">In the **Region** drop-down list, choose a region close to you.</span></span> <span data-ttu-id="08286-292">此设置指定您的网站将运行在哪个数据中心。</span><span class="sxs-lookup"><span data-stu-id="08286-292">This setting specifies which data center your web site will run in.</span></span>
5. <span data-ttu-id="08286-293">在**数据库**下拉列表中，选择**创建免费的 20 MB SQL 数据库**。</span><span class="sxs-lookup"><span data-stu-id="08286-293">In the **Database** drop-down list, choose **Create a free 20 MB SQL database**.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. <span data-ttu-id="08286-294">在**数据库连接字符串名称**，输入*SchoolContext*。</span><span class="sxs-lookup"><span data-stu-id="08286-294">In the **DB CONNECTION STRING NAME**, enter *SchoolContext*.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. <span data-ttu-id="08286-295">单击框底部右侧箭头。</span><span class="sxs-lookup"><span data-stu-id="08286-295">Click the arrow that points to the right at the bottom of the box.</span></span> <span data-ttu-id="08286-296">向导将前进到**数据库设置**步骤。</span><span class="sxs-lookup"><span data-stu-id="08286-296">The wizard advances to the **Database Settings** step.</span></span>
8. <span data-ttu-id="08286-297">在**名称**框中，输入*ContosoUniversityDB*。</span><span class="sxs-lookup"><span data-stu-id="08286-297">In the **Name** box, enter *ContosoUniversityDB*.</span></span>
9. <span data-ttu-id="08286-298">在**服务器**框中，选择**新建 SQL 数据库服务器**。</span><span class="sxs-lookup"><span data-stu-id="08286-298">In the **Server** box, select **New SQL Database server**.</span></span> <span data-ttu-id="08286-299">或者，如果你以前创建的服务器，你可以从下拉列表中选择该服务器。</span><span class="sxs-lookup"><span data-stu-id="08286-299">Alternatively, if you previously created a server, you can select that server from the drop-down list.</span></span>
10. <span data-ttu-id="08286-300">输入管理员**登录名**和**密码**。</span><span class="sxs-lookup"><span data-stu-id="08286-300">Enter an administrator **LOGIN NAME** and **PASSWORD**.</span></span> <span data-ttu-id="08286-301">如果你选择**新建 SQL 数据库服务器**不要输入现有名称和密码在此处，你应输入新名称和密码，你现在定义以后访问数据库时使用。</span><span class="sxs-lookup"><span data-stu-id="08286-301">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="08286-302">如果你选择你之前创建的服务器，你将为该服务器输入凭据。</span><span class="sxs-lookup"><span data-stu-id="08286-302">If you selected a server that you created previously, you'll enter credentials for that server.</span></span> <span data-ttu-id="08286-303">对于本教程，你将不会选择***高级***复选框。</span><span class="sxs-lookup"><span data-stu-id="08286-303">For this tutorial, you won't select the ***Advanced*** check box.</span></span> <span data-ttu-id="08286-304">***高级***选项使您可以将数据库设置[排序规则](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="08286-304">The ***Advanced*** options enable you to set the database [collation](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx).</span></span>
11. <span data-ttu-id="08286-305">选择相同**区域**与你为网站选择。</span><span class="sxs-lookup"><span data-stu-id="08286-305">Choose the same **Region** that you chose for the web site.</span></span>
12. <span data-ttu-id="08286-306">单击右下角的框以指示你已完成的复选标记。</span><span class="sxs-lookup"><span data-stu-id="08286-306">Click the check mark at the bottom right of the box to indicate that you're finished.</span></span>   
  
    ![数据库设置步骤使用数据库向导创建的新网站-](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

 <span data-ttu-id="08286-308">下图显示了使用现有 SQL Server 和登录名。</span><span class="sxs-lookup"><span data-stu-id="08286-308">The following image shows using an existing SQL Server and Login.</span></span>   
  
    ![数据库设置步骤使用数据库向导创建的新网站-](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
 <span data-ttu-id="08286-310">管理门户返回到网站页中，与**状态**列显示正在创建网站。</span><span class="sxs-lookup"><span data-stu-id="08286-310">The Management Portal returns to the Web Sites page, and the **Status** column shows that the site is being created.</span></span> <span data-ttu-id="08286-311">（通常小于一分钟），一段时间后**状态**列显示已成功创建网站。</span><span class="sxs-lookup"><span data-stu-id="08286-311">After a while (typically less than a minute), the **Status** column shows that the site was successfully created.</span></span> <span data-ttu-id="08286-312">在左侧导航栏中，必须在你的帐户中的站点数旁边将出现**网站**旁边显示图标和数据库的数目**SQL 数据库**图标。</span><span class="sxs-lookup"><span data-stu-id="08286-312">In the navigation bar at the left, the number of sites you have in your account appears next to the **Web Sites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="08286-313">部署到 Windows Azure 应用程序</span><span class="sxs-lookup"><span data-stu-id="08286-313">Deploy the application to Windows Azure</span></span>

1. <span data-ttu-id="08286-314">在 Visual Studio 中，右键单击中的项目**解决方案资源管理器**和选择**发布**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="08286-314">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>  
  
    ![在项目上下文菜单中发布](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. <span data-ttu-id="08286-316">在**配置文件**选项卡**发布 Web**向导中，单击**导入**。</span><span class="sxs-lookup"><span data-stu-id="08286-316">In the **Profile** tab of the **Publish Web** wizard, click **Import**.</span></span>  
  
    ![导入发布设置](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. <span data-ttu-id="08286-318">如果之前未添加 Windows Azure 订阅在 Visual Studio 中，执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="08286-318">If you have not previously added your Windows Azure subscription in Visual Studio, perform the following steps.</span></span> <span data-ttu-id="08286-319">在这些步骤中添加你的订阅，以便下拉列表下**从 Windows Azure 网站导入**将包括您的网站。</span><span class="sxs-lookup"><span data-stu-id="08286-319">In these steps you add your subscription so that the drop-down list under **Import from a Windows Azure web site** will include your web site.</span></span>

    <span data-ttu-id="08286-320">a.</span><span class="sxs-lookup"><span data-stu-id="08286-320">a.</span></span> <span data-ttu-id="08286-321">在**导入发布配置文件**对话框中，单击**从 Windows Azure 网站导入**，然后单击**添加 Windows Azure 订阅**。</span><span class="sxs-lookup"><span data-stu-id="08286-321">In the **Import Publish Profile** dialog box, click **Import from a Windows Azure web site**, and then click **Add Windows Azure subscription**.</span></span>

    ![添加 Windows Azure 订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    <span data-ttu-id="08286-323">b.</span><span class="sxs-lookup"><span data-stu-id="08286-323">b.</span></span> <span data-ttu-id="08286-324">在**导入 Windows Azure 订阅**对话框中，单击**下载订阅文件**。</span><span class="sxs-lookup"><span data-stu-id="08286-324">In the **Import Windows Azure Subscriptions** dialog box, click **Download subscription file**.</span></span>

    ![下载订阅文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    <span data-ttu-id="08286-326">c.</span><span class="sxs-lookup"><span data-stu-id="08286-326">c.</span></span> <span data-ttu-id="08286-327">在浏览器窗口中，保存*.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="08286-327">In your browser window, save the *.publishsettings* file.</span></span>

    ![下载的.publishsettings 文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > <span data-ttu-id="08286-329">安全- *publishsettings*文件包含你用于管理你的 Windows Azure 订阅和服务的凭据 （未编码）。</span><span class="sxs-lookup"><span data-stu-id="08286-329">Security - The *publishsettings* file contains your credentials (unencoded) that are used to administer your Windows Azure subscriptions and services.</span></span> <span data-ttu-id="08286-330">此文件的最佳安全方案是将其暂时存储源目录以外 (例如在*Libraries\Documents*文件夹)，然后将其导入完毕后删除。</span><span class="sxs-lookup"><span data-stu-id="08286-330">The security best practice for this file is to store it temporarily outside your source directories (for example in the *Libraries\Documents* folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="08286-331">恶意用户获得访问权`.publishsettings`文件可以编辑、 创建和删除 Windows Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="08286-331">A malicious user who gains access to the `.publishsettings` file can edit, create, and delete your Windows Azure services.</span></span>

    <span data-ttu-id="08286-332">d.</span><span class="sxs-lookup"><span data-stu-id="08286-332">d.</span></span> <span data-ttu-id="08286-333">在**导入 Windows Azure 订阅**对话框中，单击**浏览**并导航到*.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="08286-333">In the **Import Windows Azure Subscriptions** dialog box, click **Browse** and navigate to the *.publishsettings* file.</span></span>

    ![下载订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    <span data-ttu-id="08286-335">e.</span><span class="sxs-lookup"><span data-stu-id="08286-335">e.</span></span> <span data-ttu-id="08286-336">单击“导入” 。</span><span class="sxs-lookup"><span data-stu-id="08286-336">Click **Import**.</span></span>

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. <span data-ttu-id="08286-338">在**导入发布配置文件**对话框中，选择**从 Windows Azure 网站导入**，从下拉列表中，选择您的网站，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="08286-338">In the **Import Publish Profile** dialog box, select **Import from a Windows Azure web site**, select your web site from the drop-down list, and then click **OK**.</span></span>  
  
    ![导入发布配置文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. <span data-ttu-id="08286-340">在**连接**选项卡上，单击**验证连接**若要确保设置正确无误。</span><span class="sxs-lookup"><span data-stu-id="08286-340">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>  
  
    ![验证连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. <span data-ttu-id="08286-342">在验证连接后，旁边出现一个绿色的复选标记**验证连接**按钮。</span><span class="sxs-lookup"><span data-stu-id="08286-342">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span> <span data-ttu-id="08286-343">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="08286-343">Click **Next**.</span></span>  
  
    ![已成功验证的连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. <span data-ttu-id="08286-345">打开**远程连接字符串**下的下拉列表**SchoolContext** ，然后选择你创建的数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-345">Open the **Remote connection string** drop-down list under **SchoolContext** and select the connection string for the database you created.</span></span>
8. <span data-ttu-id="08286-346">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="08286-346">Select **Execute Code First Migrations (runs on application start)**.</span></span>
9. <span data-ttu-id="08286-347">取消选中**在运行时使用此连接字符串**为**上下文 (DefaultConnection)**，因为此应用程序不使用成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="08286-347">Uncheck **Use this connection string at runtime** for the **UserContext (DefaultConnection)**, since this application is not using the membership database.</span></span>   
  
    ![设置选项卡](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. <span data-ttu-id="08286-349">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="08286-349">Click **Next**.</span></span>
11. <span data-ttu-id="08286-350">在**预览**选项卡上，单击**开始预览**。</span><span class="sxs-lookup"><span data-stu-id="08286-350">In the **Preview** tab, click **Start Preview**.</span></span>  
  
    ![预览选项卡中的开始预览按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
 <span data-ttu-id="08286-352">选项卡显示将复制到服务器的文件列表。</span><span class="sxs-lookup"><span data-stu-id="08286-352">The tab displays a list of the files that will be copied to the server.</span></span> <span data-ttu-id="08286-353">显示预览不需要发布应用程序但有用的功能，需要注意。</span><span class="sxs-lookup"><span data-stu-id="08286-353">Displaying the preview isn't required to publish the application but is a useful function to be aware of.</span></span> <span data-ttu-id="08286-354">在这种情况下，你不必使用显示的文件列表执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="08286-354">In this case, you don't need to do anything with the list of files that is displayed.</span></span> <span data-ttu-id="08286-355">下次部署此应用程序，仅将已更改的文件将在此列表中。</span><span class="sxs-lookup"><span data-stu-id="08286-355">The next time you deploy this application, only the files that have changed will be in this list.</span></span>  
  
    ![开始预览文件输出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. <span data-ttu-id="08286-357">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="08286-357">Click **Publish**.</span></span>  
 <span data-ttu-id="08286-358">Visual Studio 开始将文件复制到 Windows Azure 服务器的过程。</span><span class="sxs-lookup"><span data-stu-id="08286-358">Visual Studio begins the process of copying the files to the Windows Azure server.</span></span>
13. <span data-ttu-id="08286-359">**输出**窗口将显示已执行的部署操作并报告已成功完成的部署。</span><span class="sxs-lookup"><span data-stu-id="08286-359">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>  
  
    ![输出窗口报告部署成功](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. <span data-ttu-id="08286-361">成功部署后，默认浏览器自动打开指向已部署的 web 站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="08286-361">Upon successful deployment, the default browser automatically opens to the URL of the deployed web site.</span></span>  
 <span data-ttu-id="08286-362">你创建的应用程序现在在云中运行。</span><span class="sxs-lookup"><span data-stu-id="08286-362">The application you created is now running in the cloud.</span></span> <span data-ttu-id="08286-363">单击学生选项卡。</span><span class="sxs-lookup"><span data-stu-id="08286-363">Click the Students tab.</span></span>  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

<span data-ttu-id="08286-365">此时你*SchoolContext*已在 Windows Azure SQL 数据库中创建了数据库由于你选择了**执行 Code First 迁移 （在应用启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="08286-365">At this point your *SchoolContext* database has been created in the Windows Azure SQL Database because you selected **Execute Code First Migrations (runs on app start)**.</span></span> <span data-ttu-id="08286-366">*Web.config*已部署的 web 站点中的文件已更改，以便[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项将运行你的代码读取或写入数据库中的数据的第一个时间 (所选时发生**学生**选项卡上):</span><span class="sxs-lookup"><span data-stu-id="08286-366">The *Web.config* file in the deployed web site has been changed so that the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer would run the first time your code reads or writes data in the database (which happened when you selected the **Students** tab):</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

<span data-ttu-id="08286-367">在部署过程还创建新的连接字符串*(SchoolContext\_DatabasePublish*) 的代码优先迁移来用于更新数据库架构和数据库进行种子设定。</span><span class="sxs-lookup"><span data-stu-id="08286-367">The deployment process also created a new connection string *(SchoolContext\_DatabasePublish*) for Code First Migrations to use for updating the database schema and seeding the database.</span></span>

![Database_Publish 连接字符串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

<span data-ttu-id="08286-369">*DefaultConnection*连接字符串用于成员资格数据库 （其中我们不使用在本教程中）。</span><span class="sxs-lookup"><span data-stu-id="08286-369">The *DefaultConnection* connection string is for the membership database (which we are not using in this tutorial).</span></span> <span data-ttu-id="08286-370">*SchoolContext* ContosoUniversity 数据库是连接字符串。</span><span class="sxs-lookup"><span data-stu-id="08286-370">The *SchoolContext* connection string is for the ContosoUniversity database.</span></span>

<span data-ttu-id="08286-371">您可以找到在你自己的计算机上的 Web.config 文件的已部署的版本*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*。你可以访问部署*Web.config*文件本身通过使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="08286-371">You can find the deployed version of the Web.config file on your own computer in *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. You can access the deployed *Web.config* file itself by using FTP.</span></span> <span data-ttu-id="08286-372">有关说明，请参阅[使用 Visual Studio 的 ASP.NET Web 部署： 部署某一代码更新](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。</span><span class="sxs-lookup"><span data-stu-id="08286-372">For instructions, see [ASP.NET Web Deployment using Visual Studio: Deploying a Code Update](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md).</span></span> <span data-ttu-id="08286-373">按照以开头的说明"若要使用 FTP 工具，需要以下三项： 的 FTP URL、 用户名和密码。"</span><span class="sxs-lookup"><span data-stu-id="08286-373">Follow the instructions that start with "To use an FTP tool, you need three things: the FTP URL, the user name, and the password."</span></span>

> [!NOTE]
> <span data-ttu-id="08286-374">Web 应用未实现安全，因此任何找到的 URL 的人都可以更改的数据。</span><span class="sxs-lookup"><span data-stu-id="08286-374">The web app doesn't implement security, so anyone who finds the URL can change the data.</span></span> <span data-ttu-id="08286-375">有关如何确保网站的安全的说明，请参阅[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用程序部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="08286-375">For instructions on how to secure the web site, see [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="08286-376">可以通过使用 Windows Azure 管理门户中使用该站点中阻止其他人或**服务器资源管理器**Visual Studio 停止该站点中。</span><span class="sxs-lookup"><span data-stu-id="08286-376">You can prevent other people from using the site by using the Windows Azure Management Portal or **Server Explorer** in Visual Studio to stop the site.</span></span>


![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a><span data-ttu-id="08286-377">代码 First 初始值设定项</span><span class="sxs-lookup"><span data-stu-id="08286-377">Code First Initializers</span></span>

<span data-ttu-id="08286-378">在部署部分你已看到[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)正在使用的初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="08286-378">In the deployment section you saw the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer being used.</span></span> <span data-ttu-id="08286-379">代码首先还提供您可以使用，其中包括其他初始值设定项[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （默认值）、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx)和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。</span><span class="sxs-lookup"><span data-stu-id="08286-379">Code First also provides other initializers that you can use, including [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (the default), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) and [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx).</span></span> <span data-ttu-id="08286-380">`DropCreateAlways`初始值设定项可用于设置单元测试的条件。</span><span class="sxs-lookup"><span data-stu-id="08286-380">The `DropCreateAlways` initializer can be useful for setting up conditions for unit tests.</span></span> <span data-ttu-id="08286-381">你还可以编写你自己初始值设定项，并且如果不想等待，直到应用程序从读取或写入数据库，你可以显式调用初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="08286-381">You can also write your own initializers, and you can call an initializer explicitly if you don't want to wait until the application reads from or writes to the database.</span></span> <span data-ttu-id="08286-382">初始值设定项的完整说明，请参阅书籍的第 6 章[编程实体框架： Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan Miller。</span><span class="sxs-lookup"><span data-stu-id="08286-382">For a comprehensive explanation of initializers, see chapter 6 of the book [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) by Julie Lerman and Rowan Miller.</span></span>

## <a name="summary"></a><span data-ttu-id="08286-383">摘要</span><span class="sxs-lookup"><span data-stu-id="08286-383">Summary</span></span>

<span data-ttu-id="08286-384">在本教程中，你已了解如何创建数据模型和实现基本的 CRUD，排序、 筛选、 分页和分组功能。</span><span class="sxs-lookup"><span data-stu-id="08286-384">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="08286-385">在下一教程将首先通过展开数据模型来查看更高级的主题。</span><span class="sxs-lookup"><span data-stu-id="08286-385">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="08286-386">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="08286-386">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="08286-387">[上一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[下一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="08286-387">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span></span>
