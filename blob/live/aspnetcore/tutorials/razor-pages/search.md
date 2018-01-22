---
title: "将搜索添加到 ASP.NET Core Razor 页面"
author: rick-anderson
description: "演示如何将搜索添加到 ASP.NET Core Razor 页面"
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/razor-pages/search
ms.openlocfilehash: 2859d52e42d4430808e01739474df0598c07c805
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="adding-search-to-a-razor-pages-app"></a><span data-ttu-id="dcdb1-103">将搜索添加到 Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="dcdb1-103">Adding search to a Razor Pages app</span></span>

<span data-ttu-id="dcdb1-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dcdb1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="dcdb1-105">本文档中，将向索引页面添加搜索功能以实现按“流派”或“名称”搜索电影。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-105">In this document, search capability is added to the Index page that enables searching movies by *genre* or *name*.</span></span>

<span data-ttu-id="dcdb1-106">使用以下代码更新索引页面的 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-106">Update the Index page's `OnGetAsync` method with the following code:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

<span data-ttu-id="dcdb1-107">`OnGetAsync` 方法的第一行创建了 [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) 查询用于选择电影：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-107">The first line of the `OnGetAsync` method creates a [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="dcdb1-108">此时仅对查询进行了定义，它还不会针对数据库运行。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-108">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="dcdb1-109">如果 `searchString` 参数包含一个字符串，电影查询则会被修改为根据搜索字符串进行筛选：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-109">If the `searchString` parameter contains a string, the movies query is modified to filter on the search string:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

<span data-ttu-id="dcdb1-110">`s => s.Title.Contains()` 代码是 [Lambda 表达式](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-110">The `s => s.Title.Contains()` code is a [Lambda Expression](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="dcdb1-111">Lambda 在基于方法的 [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) 查询中用作标准查询运算符方法的参数，如 [Where](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 方法或 `Contains`（前面的代码中所使用的）。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-111">Lambdas are used in method-based [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) queries as arguments to standard query operator methods such as the [Where](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) method or `Contains` (used in the preceding code).</span></span> <span data-ttu-id="dcdb1-112">在对 LINQ 查询进行定义或通过调用方法（如  `Where`、`Contains` 或 `OrderBy`）进行修改后，此查询不会被执行。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-112">LINQ queries are not executed when they are defined or when they are modified by calling a method (such as `Where`, `Contains`  or `OrderBy`).</span></span> <span data-ttu-id="dcdb1-113">相反，会延迟执行查询。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-113">Rather, query execution is deferred.</span></span> <span data-ttu-id="dcdb1-114">这意味着表达式的计算会延迟，直到循环访问其实现的值或者调用 `ToListAsync` 方法为止。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-114">That means the evaluation of an expression is delayed until its realized value is iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="dcdb1-115">有关详细信息，请参阅 [Query Execution](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/query-execution)（查询执行）。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-115">See [Query Execution](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/query-execution) for more information.</span></span>

<span data-ttu-id="dcdb1-116">注意：[Contains](https://docs.microsoft.com//dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法在数据库中运行，而不是在 C# 代码中。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-116">**Note:** The [Contains](https://docs.microsoft.com//dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the C# code.</span></span> <span data-ttu-id="dcdb1-117">查询是否区分大小写取决于数据库和排序规则。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-117">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="dcdb1-118">在 SQL Server 上，`Contains` 映射到 [SQL LIKE](https://docs.microsoft.com/sql/t-sql/language-elements/like-transact-sql)，这是不区分大小写的。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-118">On SQL Server, `Contains` maps to [SQL LIKE](https://docs.microsoft.com/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="dcdb1-119">在 SQLite 中，由于使用了默认排序规则，因此需要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-119">In SQLite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="dcdb1-120">导航到电影页面，并向 URL追加一个如 `?searchString=Ghost` 的查询字符串（例如 `http://localhost:5000/Movies?searchString=Ghost`）。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-120">Navigate to the Movies page and append a query string such as `?searchString=Ghost` to the URL (for example, `http://localhost:5000/Movies?searchString=Ghost`).</span></span> <span data-ttu-id="dcdb1-121">筛选的电影将显示出来。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-121">The filtered movies are displayed.</span></span>

![索引视图](search/_static/ghost.png)

<span data-ttu-id="dcdb1-123">如果向索引页面添加了以下路由模板，搜索字符串则可作为 URL 段传递（例如 `http://localhost:5000/Movies/ghost`）。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-123">If the following route template is added to the Index page, the search string can be passed as a URL segment (for example, `http://localhost:5000/Movies/ghost`).</span></span>

```cshtml
@page "{searchString?}"
```

<span data-ttu-id="dcdb1-124">前面的路由约束允许按路由数据（URL 段）搜索标题，而不是按查询字符串值进行搜索。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-124">The preceding route constraint allows searching the title as route data (a URL segment) instead of as a query string value.</span></span>  <span data-ttu-id="dcdb1-125">`"{searchString?}"` 中的 `?` 表示这是可选路由参数。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-125">The `?` in `"{searchString?}"` means this is an optional route parameter.</span></span>

![索引视图，显示添加到 URL 的“ghost”一词以及返回的两部电影（Ghostbusters 和 Ghostbusters 2）的电影列表](search/_static/g2.png)

<span data-ttu-id="dcdb1-127">但是，不能指望用户修改 URL 来搜索电影。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-127">However, you can't expect users to modify the URL to search for a movie.</span></span> <span data-ttu-id="dcdb1-128">在此步骤中，会添加 UI 来筛选电影。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-128">In this step, UI is added to filter movies.</span></span> <span data-ttu-id="dcdb1-129">如果已添加路由约束 `"{searchString?}"`，请将它删除。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-129">If you added the route constraint `"{searchString?}"`, remove it.</span></span>

<span data-ttu-id="dcdb1-130">打开 Pages/Movies/Index.cshtml 文件，并添加以下代码中突出显示的 `<form>` 标记：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-130">Open the *Pages/Movies/Index.cshtml* file, and add the `<form>` markup highlighted in the following code:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

<span data-ttu-id="dcdb1-131">HTML `<form>` 标记使用[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-131">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="dcdb1-132">提交表单时，筛选器字符串将发送到 Pages/Movies/Index 页面。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-132">When the form is submitted, the filter string is sent to the *Pages/Movies/Index* page.</span></span> <span data-ttu-id="dcdb1-133">保存更改并测试筛选器。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-133">Save the changes and test the filter.</span></span>

![显示标题筛选器文本框中键入了 ghost 一词的索引视图](search/_static/filter.png)

## <a name="search-by-genre"></a><span data-ttu-id="dcdb1-135">按流派搜索</span><span class="sxs-lookup"><span data-stu-id="dcdb1-135">Search by genre</span></span>

<span data-ttu-id="dcdb1-136">将以下突出显示的属性添加到 Pages/Movies/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-136">Add the the following highlighted properties to *Pages/Movies/Index.cshtml.cs*:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-)]

<span data-ttu-id="dcdb1-137">`SelectList Genres` 包含流派列表。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-137">The `SelectList Genres` contains the list of genres.</span></span> <span data-ttu-id="dcdb1-138">这使用户能够从列表中选择一种流派。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-138">This allows the user to select a genre from the list.</span></span>

<span data-ttu-id="dcdb1-139">`MovieGenre` 属性包含用户选择的特定流派（例如“西部”）。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-139">The `MovieGenre` property contains the specific genre the user selects (for example, "Western").</span></span>

<span data-ttu-id="dcdb1-140">使用以下代码更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-140">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

<span data-ttu-id="dcdb1-141">下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-141">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

<span data-ttu-id="dcdb1-142">流派的 `SelectList` 是通过投影截然不同的流派创建的。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-142">The `SelectList` of genres is created by projecting the distinct genres.</span></span>

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There is no start line.

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a><span data-ttu-id="dcdb1-143">添加“按流派搜索”</span><span class="sxs-lookup"><span data-stu-id="dcdb1-143">Adding search by genre</span></span>

<span data-ttu-id="dcdb1-144">更新 Index.cshtml，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dcdb1-144">Update *Index.cshtml* as follows:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

<span data-ttu-id="dcdb1-145">通过按流派或/和电影标题搜索来测试应用。</span><span class="sxs-lookup"><span data-stu-id="dcdb1-145">Test the app by searching by genre, by movie title, and by both.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="dcdb1-146">[上一篇：更新页面](xref:tutorials/razor-pages/da1)
[下一篇：添加新字段](xref:tutorials/razor-pages/new-field)</span><span class="sxs-lookup"><span data-stu-id="dcdb1-146">[Previous: Updating the pages](xref:tutorials/razor-pages/da1)
[Next: Adding a new field](xref:tutorials/razor-pages/new-field)</span></span>
