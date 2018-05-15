# <a name="adding-search-to-a-razor-pages-app"></a><span data-ttu-id="cebac-101">将搜索添加到 Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="cebac-101">Adding search to a Razor Pages app</span></span>

<span data-ttu-id="cebac-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cebac-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cebac-103">本文档中，将向索引页面添加搜索功能以实现按“流派”或“名称”搜索电影。</span><span class="sxs-lookup"><span data-stu-id="cebac-103">In this document, search capability is added to the Index page that enables searching movies by *genre* or *name*.</span></span>

<span data-ttu-id="cebac-104">使用以下代码更新索引页面的 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="cebac-104">Update the Index page's `OnGetAsync` method with the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

<span data-ttu-id="cebac-105">`OnGetAsync` 方法的第一行创建了 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询用于选择电影：</span><span class="sxs-lookup"><span data-stu-id="cebac-105">The first line of the `OnGetAsync` method creates a [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="cebac-106">此时仅对查询进行了定义，它还不会针对数据库运行。</span><span class="sxs-lookup"><span data-stu-id="cebac-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="cebac-107">如果 `searchString` 参数包含一个字符串，电影查询则会被修改为根据搜索字符串进行筛选：</span><span class="sxs-lookup"><span data-stu-id="cebac-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the search string:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

<span data-ttu-id="cebac-108">`s => s.Title.Contains()` 代码是 [Lambda 表达式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="cebac-108">The `s => s.Title.Contains()` code is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="cebac-109">Lambda 在基于方法的 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询中用作标准查询运算符方法的参数，如 [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 方法或 `Contains`（前面的代码中所使用的）。</span><span class="sxs-lookup"><span data-stu-id="cebac-109">Lambdas are used in method-based [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) queries as arguments to standard query operator methods such as the [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) method or `Contains` (used in the preceding code).</span></span> <span data-ttu-id="cebac-110">在对 LINQ 查询进行定义或通过调用方法（如 `Where`、`Contains` 或 `OrderBy`）进行修改后，此查询不会被执行。</span><span class="sxs-lookup"><span data-stu-id="cebac-110">LINQ queries are not executed when they're defined or when they're modified by calling a method (such as `Where`, `Contains`  or `OrderBy`).</span></span> <span data-ttu-id="cebac-111">相反，会延迟执行查询。</span><span class="sxs-lookup"><span data-stu-id="cebac-111">Rather, query execution is deferred.</span></span> <span data-ttu-id="cebac-112">这意味着表达式的计算会延迟，直到循环访问其实现的值或者调用 `ToListAsync` 方法为止。</span><span class="sxs-lookup"><span data-stu-id="cebac-112">That means the evaluation of an expression is delayed until its realized value is iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="cebac-113">有关详细信息，请参阅 [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution)（查询执行）。</span><span class="sxs-lookup"><span data-stu-id="cebac-113">See [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution) for more information.</span></span>

<span data-ttu-id="cebac-114">注意：[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法在数据库中运行，而不是在 C# 代码中。</span><span class="sxs-lookup"><span data-stu-id="cebac-114">**Note:** The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the C# code.</span></span> <span data-ttu-id="cebac-115">查询是否区分大小写取决于数据库和排序规则。</span><span class="sxs-lookup"><span data-stu-id="cebac-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="cebac-116">在 SQL Server 上，`Contains` 映射到 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)，这是不区分大小写的。</span><span class="sxs-lookup"><span data-stu-id="cebac-116">On SQL Server, `Contains` maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="cebac-117">在 SQLite 中，由于使用了默认排序规则，因此需要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="cebac-117">In SQLite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="cebac-118">导航到电影页面，并向 URL追加一个如 `?searchString=Ghost` 的查询字符串（例如 `http://localhost:5000/Movies?searchString=Ghost`）。</span><span class="sxs-lookup"><span data-stu-id="cebac-118">Navigate to the Movies page and append a query string such as `?searchString=Ghost` to the URL (for example, `http://localhost:5000/Movies?searchString=Ghost`).</span></span> <span data-ttu-id="cebac-119">筛选的电影将显示出来。</span><span class="sxs-lookup"><span data-stu-id="cebac-119">The filtered movies are displayed.</span></span>

![索引视图](../../tutorials/razor-pages/search/_static/ghost.png)

<span data-ttu-id="cebac-121">如果向索引页面添加了以下路由模板，搜索字符串则可作为 URL 段传递（例如 `http://localhost:5000/Movies/ghost`）。</span><span class="sxs-lookup"><span data-stu-id="cebac-121">If the following route template is added to the Index page, the search string can be passed as a URL segment (for example, `http://localhost:5000/Movies/ghost`).</span></span>

```cshtml
@page "{searchString?}"
```

<span data-ttu-id="cebac-122">前面的路由约束允许按路由数据（URL 段）搜索标题，而不是按查询字符串值进行搜索。</span><span class="sxs-lookup"><span data-stu-id="cebac-122">The preceding route constraint allows searching the title as route data (a URL segment) instead of as a query string value.</span></span>  <span data-ttu-id="cebac-123">`"{searchString?}"` 中的 `?` 表示这是可选路由参数。</span><span class="sxs-lookup"><span data-stu-id="cebac-123">The `?` in `"{searchString?}"` means this is an optional route parameter.</span></span>

![索引视图，显示添加到 URL 的“ghost”一词以及返回的两部电影（Ghostbusters 和 Ghostbusters 2）的电影列表](../../tutorials/razor-pages/search/_static/g2.png)

<span data-ttu-id="cebac-125">但是，不能指望用户修改 URL 来搜索电影。</span><span class="sxs-lookup"><span data-stu-id="cebac-125">However, you can't expect users to modify the URL to search for a movie.</span></span> <span data-ttu-id="cebac-126">在此步骤中，会添加 UI 来筛选电影。</span><span class="sxs-lookup"><span data-stu-id="cebac-126">In this step, UI is added to filter movies.</span></span> <span data-ttu-id="cebac-127">如果已添加路由约束 `"{searchString?}"`，请将它删除。</span><span class="sxs-lookup"><span data-stu-id="cebac-127">If you added the route constraint `"{searchString?}"`, remove it.</span></span>

<span data-ttu-id="cebac-128">打开 Pages/Movies/Index.cshtml 文件，并添加以下代码中突出显示的 `<form>` 标记：</span><span class="sxs-lookup"><span data-stu-id="cebac-128">Open the *Pages/Movies/Index.cshtml* file, and add the `<form>` markup highlighted in the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

<span data-ttu-id="cebac-129">HTML `<form>` 标记使用[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="cebac-129">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="cebac-130">提交表单时，筛选器字符串将发送到 Pages/Movies/Index 页面。</span><span class="sxs-lookup"><span data-stu-id="cebac-130">When the form is submitted, the filter string is sent to the *Pages/Movies/Index* page.</span></span> <span data-ttu-id="cebac-131">保存更改并测试筛选器。</span><span class="sxs-lookup"><span data-stu-id="cebac-131">Save the changes and test the filter.</span></span>

![显示标题筛选器文本框中键入了 ghost 一词的索引视图](../../tutorials/razor-pages/search/_static/filter.png)

## <a name="search-by-genre"></a><span data-ttu-id="cebac-133">按流派搜索</span><span class="sxs-lookup"><span data-stu-id="cebac-133">Search by genre</span></span>

<span data-ttu-id="cebac-134">将以下突出显示的属性添加到 Pages/Movies/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="cebac-134">Add the following highlighted properties to *Pages/Movies/Index.cshtml.cs*:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

<span data-ttu-id="cebac-135">`SelectList Genres` 包含流派列表。</span><span class="sxs-lookup"><span data-stu-id="cebac-135">The `SelectList Genres` contains the list of genres.</span></span> <span data-ttu-id="cebac-136">这使用户能够从列表中选择一种流派。</span><span class="sxs-lookup"><span data-stu-id="cebac-136">This allows the user to select a genre from the list.</span></span>

<span data-ttu-id="cebac-137">`MovieGenre` 属性包含用户选择的特定流派（例如“西部”）。</span><span class="sxs-lookup"><span data-stu-id="cebac-137">The `MovieGenre` property contains the specific genre the user selects (for example, "Western").</span></span>

<span data-ttu-id="cebac-138">使用以下代码更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="cebac-138">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

<span data-ttu-id="cebac-139">下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="cebac-139">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

<span data-ttu-id="cebac-140">流派的 `SelectList` 是通过投影截然不同的流派创建的。</span><span class="sxs-lookup"><span data-stu-id="cebac-140">The `SelectList` of genres is created by projecting the distinct genres.</span></span>

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There's no start line.

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a><span data-ttu-id="cebac-141">添加“按流派搜索”</span><span class="sxs-lookup"><span data-stu-id="cebac-141">Adding search by genre</span></span>

<span data-ttu-id="cebac-142">更新 Index.cshtml，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cebac-142">Update *Index.cshtml* as follows:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

<span data-ttu-id="cebac-143">通过按流派或/和电影标题搜索来测试应用。</span><span class="sxs-lookup"><span data-stu-id="cebac-143">Test the app by searching by genre, by movie title, and by both.</span></span>
