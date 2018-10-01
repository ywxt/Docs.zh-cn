---
title: 将搜索添加到 ASP.NET Core Razor 页面
author: rick-anderson
description: 演示如何将搜索添加到 ASP.NET Core Razor 页面
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/search
ms.openlocfilehash: 9608f454c2c4ae0f4db1e71200b0ca98fe2cd2ad
ms.sourcegitcommit: 32f5ee0690604d451f61e9a5c28881c9fcf85738
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454708"
---
# <a name="add-search-to-aspnet-core-razor-pages"></a>将搜索添加到 ASP.NET Core Razor 页面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本文档中，将向索引页面添加搜索功能以实现按“流派”或“名称”搜索电影。

使用以下代码更新索引页面的 `OnGetAsync` 方法：

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

`OnGetAsync` 方法的第一行创建了 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询用于选择电影：

```csharp
// using System.Linq;
var movies = from m in _context.Movie
             select m;
```

此时仅对查询进行了定义，它还不会针对数据库运行。

如果 `searchString` 参数包含一个字符串，电影查询则会被修改为根据搜索字符串进行筛选：

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

`s => s.Title.Contains()` 代码是 [Lambda 表达式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。 Lambda 在基于方法的 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询中用作标准查询运算符方法的参数，如 [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 方法或 `Contains`（前面的代码中所使用的）。 在对 LINQ 查询进行定义或通过调用方法（如 `Where`、`Contains` 或 `OrderBy`）进行修改后，此查询不会被执行。 相反，会延迟执行查询。 这意味着表达式的计算会延迟，直到循环访问其实现的值或者调用 `ToListAsync` 方法为止。 有关详细信息，请参阅 [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution)（查询执行）。

注意：[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法在数据库中运行，而不是在 C# 代码中。 查询是否区分大小写取决于数据库和排序规则。 在 SQL Server 上，`Contains` 映射到 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)，这是不区分大小写的。 在 SQLite 中，由于使用了默认排序规则，因此需要区分大小写。

导航到电影页面，并向 URL追加一个如 `?searchString=Ghost` 的查询字符串（例如 `http://localhost:5000/Movies?searchString=Ghost`）。 筛选的电影将显示出来。

![索引视图](search/_static/ghost.png)

如果向索引页面添加了以下路由模板，搜索字符串则可作为 URL 段传递（例如 `http://localhost:5000/Movies/Ghost`）。

```cshtml
@page "{searchString?}"
```

前面的路由约束允许按路由数据（URL 段）搜索标题，而不是按查询字符串值进行搜索。  `"{searchString?}"` 中的 `?` 表示这是可选路由参数。

![索引视图，显示添加到 URL 的“ghost”一词以及返回的两部电影（Ghostbusters 和 Ghostbusters 2）的电影列表](search/_static/g2.png)

但是，不能指望用户修改 URL 来搜索电影。 在此步骤中，会添加 UI 来筛选电影。 如果已添加路由约束 `"{searchString?}"`，请将它删除。

打开 Pages/Movies/Index.cshtml 文件，并添加以下代码中突出显示的 `<form>` 标记：

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

HTML `<form>` 标记使用[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)。 提交表单时，筛选器字符串将发送到 Pages/Movies/Index 页面。 保存更改并测试筛选器。

![显示标题筛选器文本框中键入了 ghost 一词的索引视图](search/_static/filter.png)

## <a name="search-by-genre"></a>按流派搜索

将以下突出显示的属性添加到 Pages/Movies/Index.cshtml.cs：

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

::: moniker-end


`SelectList Genres` 包含流派列表。 这使用户能够从列表中选择一种流派。

`MovieGenre` 属性包含用户选择的特定流派（例如“西部”）。

使用以下代码更新 `OnGetAsync` 方法：

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

流派的 `SelectList` 是通过投影截然不同的流派创建的。

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There's no start line.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a>添加“按流派搜索”

更新 Index.cshtml，如下所示：

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

通过按流派或/和电影标题搜索来测试应用。

> [!div class="step-by-step"]
> [上一篇：更新页面](xref:tutorials/razor-pages/da1)
> [下一篇：添加新字段](xref:tutorials/razor-pages/new-field)
