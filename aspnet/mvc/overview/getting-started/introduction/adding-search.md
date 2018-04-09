---
uid: mvc/overview/getting-started/introduction/adding-search
title: 搜索 |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: 8afa72d4dbc4695e7d26c6ef4052be08a7c69080
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="search"></a><span data-ttu-id="d7c14-102">搜索</span><span class="sxs-lookup"><span data-stu-id="d7c14-102">Search</span></span>
====================
<span data-ttu-id="d7c14-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d7c14-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="d7c14-104">添加搜索方法和搜索视图</span><span class="sxs-lookup"><span data-stu-id="d7c14-104">Adding a Search Method and Search View</span></span>

<span data-ttu-id="d7c14-105">在本部分中，你将添加到搜索功能`Index`操作方法，可使你搜索电影按风格或名称。</span><span class="sxs-lookup"><span data-stu-id="d7c14-105">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="updating-the-index-form"></a><span data-ttu-id="d7c14-106">更新索引窗体</span><span class="sxs-lookup"><span data-stu-id="d7c14-106">Updating the Index Form</span></span>

<span data-ttu-id="d7c14-107">通过更新开始`Index`到现有的操作方法`MoviesController`类。</span><span class="sxs-lookup"><span data-stu-id="d7c14-107">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="d7c14-108">以下是代码：</span><span class="sxs-lookup"><span data-stu-id="d7c14-108">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="d7c14-109">第一行`Index`方法中创建以下[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询，以便选择电影：</span><span class="sxs-lookup"><span data-stu-id="d7c14-109">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="d7c14-110">查询在这种情况下，定义，但尚未尚未对数据库运行。</span><span class="sxs-lookup"><span data-stu-id="d7c14-110">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="d7c14-111">如果`searchString`参数包含一个字符串，将修改电影查询要作为筛选依据的搜索字符串，使用下面的代码的值：</span><span class="sxs-lookup"><span data-stu-id="d7c14-111">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="d7c14-112">上面的 `s => s.Title` 代码是 [Lambda 表达式](https://msdn.microsoft.com/library/bb397687.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d7c14-112">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="d7c14-113">Lambda 在基于方法的使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)如查询中用作标准查询运算符方法的自变量[其中](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)在上面的代码中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-113">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="d7c14-114">在定义后或通过调用方法，如对其进行修改时，将不会执行 LINQ 查询`Where`或`OrderBy`。</span><span class="sxs-lookup"><span data-stu-id="d7c14-114">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="d7c14-115">相反，延迟查询执行，这意味着表达式的计算延迟，直到它已实现的值实际上循环访问或[ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx)调用方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-115">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="d7c14-116">在`Search`示例中，在执行查询*Index.cshtml*视图。</span><span class="sxs-lookup"><span data-stu-id="d7c14-116">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="d7c14-117">有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。</span><span class="sxs-lookup"><span data-stu-id="d7c14-117">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d7c14-118">[Contains](https://msdn.microsoft.com/library/bb155125.aspx)方法运行在数据库中，不是 c# 代码上面。</span><span class="sxs-lookup"><span data-stu-id="d7c14-118">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="d7c14-119">在数据库中， [Contains](https://msdn.microsoft.com/library/bb155125.aspx)映射到[SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx)，这是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="d7c14-119">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="d7c14-120">现在你可以更新`Index`将向用户显示该窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="d7c14-120">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="d7c14-121">运行应用程序并导航到*/电影/索引*。</span><span class="sxs-lookup"><span data-stu-id="d7c14-121">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="d7c14-122">将查询字符串（如 `?searchString=ghost`）追加到 URL。</span><span class="sxs-lookup"><span data-stu-id="d7c14-122">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="d7c14-123">筛选的电影将显示出来。</span><span class="sxs-lookup"><span data-stu-id="d7c14-123">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="d7c14-125">如果你更改的签名`Index`方法都具有一个名为参数`id`、`id`参数将匹配`{id}`默认的占位符将路由中的组*应用\_用户RouteConfig.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="d7c14-125">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="d7c14-126">原始`Index`方法如下所示::</span><span class="sxs-lookup"><span data-stu-id="d7c14-126">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="d7c14-127">已修改`Index`方法如下，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d7c14-127">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="d7c14-128">现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。</span><span class="sxs-lookup"><span data-stu-id="d7c14-128">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="d7c14-129">但是，不能指望用户在每次要搜索电影时都修改 URL。</span><span class="sxs-lookup"><span data-stu-id="d7c14-129">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="d7c14-130">至此，你将添加 UI，以帮助它们筛选电影。</span><span class="sxs-lookup"><span data-stu-id="d7c14-130">So now you you'll add UI to help them filter movies.</span></span> <span data-ttu-id="d7c14-131">如果你更改的签名`Index`方法来测试如何将传递路由绑定 ID 参数，将其更改回来，以使你`Index`方法采用字符串参数名为`searchString`:</span><span class="sxs-lookup"><span data-stu-id="d7c14-131">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="d7c14-132">打开*Views\Movies\Index.cshtml*文件中，并紧后面`@Html.ActionLink("Create New", "Create")`，添加以下突出显示的窗体标记：</span><span class="sxs-lookup"><span data-stu-id="d7c14-132">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="d7c14-133">`Html.BeginForm`帮助器创建开始`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="d7c14-133">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="d7c14-134">`Html.BeginForm`帮助程序使窗体时在用户通过单击提交窗体发布到其自身**筛选器**按钮。</span><span class="sxs-lookup"><span data-stu-id="d7c14-134">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="d7c14-135">Visual Studio 2013 具有良好的改善时显示和编辑视图文件。</span><span class="sxs-lookup"><span data-stu-id="d7c14-135">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="d7c14-136">使用运行时应用程序视图文件打开，Visual Studio 2013 时，将调用以显示视图的正确的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-136">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="d7c14-137">索引视图 （如在上图中所示），在 Visual Studio 中打开，点击 Ctr F5 运行应用程序，然后再尝试搜索一部电影。</span><span class="sxs-lookup"><span data-stu-id="d7c14-137">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="d7c14-138">没有任何`HttpPost`重载`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-138">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="d7c14-139">你不需要它，因为该方法不更改状态的应用程序，只需筛选数据。</span><span class="sxs-lookup"><span data-stu-id="d7c14-139">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="d7c14-140">可添加以下 `HttpPost Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-140">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="d7c14-141">在这种情况下，将匹配操作调用程序`HttpPost Index`方法，与`HttpPost Index`方法将运行下图中所示。</span><span class="sxs-lookup"><span data-stu-id="d7c14-141">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="d7c14-143">但是，即使添加 `Index` 方法的 `HttpPost` 版本，其实现方式也受到限制。</span><span class="sxs-lookup"><span data-stu-id="d7c14-143">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="d7c14-144">假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。</span><span class="sxs-lookup"><span data-stu-id="d7c14-144">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="d7c14-145">请注意，HTTP POST 请求的 URL 是 GET 请求中 （localhost:xxxxx/电影/索引） 的 URL 相同-没有在 URL 本身搜索信息。</span><span class="sxs-lookup"><span data-stu-id="d7c14-145">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="d7c14-146">右现在，搜索字符串信息发送到服务器作为窗体字段值。</span><span class="sxs-lookup"><span data-stu-id="d7c14-146">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="d7c14-147">这意味着你无法捕获该搜索信息来添加书签或将发送到 URL 中的友元。</span><span class="sxs-lookup"><span data-stu-id="d7c14-147">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="d7c14-148">解决方案是使用的重载`BeginForm`指定 POST 请求，应将搜索信息添加到 URL，并且它应将路由到`HttpGet`版本`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-148">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="d7c14-149">将现有无参数`BeginForm`方法替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="d7c14-149">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="d7c14-151">现在当你提交搜索时，该 URL 将包含搜索查询字符串。</span><span class="sxs-lookup"><span data-stu-id="d7c14-151">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="d7c14-152">即使具备 `HttpPost Index` 方法，搜索也将转到 `HttpGet Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-152">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="d7c14-154">添加按风格的搜索</span><span class="sxs-lookup"><span data-stu-id="d7c14-154">Adding Search by Genre</span></span>

<span data-ttu-id="d7c14-155">如果你添加`HttpPost`版本`Index`方法，现在将其删除。</span><span class="sxs-lookup"><span data-stu-id="d7c14-155">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="d7c14-156">接下来，你将添加一项功能，以便按风格搜索电影的用户。</span><span class="sxs-lookup"><span data-stu-id="d7c14-156">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="d7c14-157">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="d7c14-157">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="d7c14-158">此版本的`Index`方法采用附加参数，即`movieGenre`。</span><span class="sxs-lookup"><span data-stu-id="d7c14-158">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="d7c14-159">代码的前几行创建`List`对象以保存从数据库的电影风格。</span><span class="sxs-lookup"><span data-stu-id="d7c14-159">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="d7c14-160">下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="d7c14-160">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="d7c14-161">该代码使用`AddRange`方法的泛型`List`集合，以便添加到列表的所有非重复的风格。</span><span class="sxs-lookup"><span data-stu-id="d7c14-161">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="d7c14-162">(而无需`Distinct`修饰符，将添加重复的风格 — 例如，将在我们的示例中两次添加喜剧)。</span><span class="sxs-lookup"><span data-stu-id="d7c14-162">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="d7c14-163">代码然后将存储的列表中的风格`ViewBag.MovieGenre`对象。</span><span class="sxs-lookup"><span data-stu-id="d7c14-163">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="d7c14-164">存储类别数据 （此类电影风格的） 作为[此时](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx)对象在`ViewBag`，则访问一个下拉列表框中的类别数据是典型的 MVC 应用程序的方法。</span><span class="sxs-lookup"><span data-stu-id="d7c14-164">Storing category data (such a movie genre's) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="d7c14-165">下面的代码演示如何检查`movieGenre`参数。</span><span class="sxs-lookup"><span data-stu-id="d7c14-165">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="d7c14-166">如果不为空，则进一步对代码约束电影查询，以限制到指定的流派所选的影片。</span><span class="sxs-lookup"><span data-stu-id="d7c14-166">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="d7c14-167">如前面所述，运行查询时未对数据基础直到影片列表循环访问 (这发生在视图中之后,`Index`操作方法会返回)。</span><span class="sxs-lookup"><span data-stu-id="d7c14-167">As stated previously, the query is not run on the data base until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="d7c14-168">将标记添加到索引视图，用于支持按风格的搜索</span><span class="sxs-lookup"><span data-stu-id="d7c14-168">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="d7c14-169">添加`Html.DropDownList`到帮助程序*Views\Movies\Index.cshtml*文件，之前`TextBox`帮助器。</span><span class="sxs-lookup"><span data-stu-id="d7c14-169">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="d7c14-170">已完成的标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="d7c14-170">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="d7c14-171">在下面的代码：</span><span class="sxs-lookup"><span data-stu-id="d7c14-171">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="d7c14-172">参数"MovieGenre"提供的密钥`DropDownList`用于查找帮助`IEnumerable<SelectListItem>`中`ViewBag`。</span><span class="sxs-lookup"><span data-stu-id="d7c14-172">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="d7c14-173">`ViewBag`已填充的操作方法中：</span><span class="sxs-lookup"><span data-stu-id="d7c14-173">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="d7c14-174">"全部"提供的选项标签参数。</span><span class="sxs-lookup"><span data-stu-id="d7c14-174">The parameter "All" provides an option label.</span></span> <span data-ttu-id="d7c14-175">如果您在浏览器中检查该选择，你将看到其"value"属性为空。</span><span class="sxs-lookup"><span data-stu-id="d7c14-175">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="d7c14-176">由于我们控制器仅筛选`if`字符串不是`null`或该表为空，提交空值的`movieGenre`显示所有风格。</span><span class="sxs-lookup"><span data-stu-id="d7c14-176">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="d7c14-177">你还可以设置一个选项以默认处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="d7c14-177">You can also set an option to be selected by default.</span></span> <span data-ttu-id="d7c14-178">如果你想"喜剧"作为默认选项，则可以更改在控制器中的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="d7c14-178">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="d7c14-179">运行应用程序，并浏览到*/电影/索引*。</span><span class="sxs-lookup"><span data-stu-id="d7c14-179">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="d7c14-180">按风格、 电影名称，以及这两个条件，请尝试搜索。</span><span class="sxs-lookup"><span data-stu-id="d7c14-180">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="d7c14-181">在本部分中创建的搜索操作方法和视图，以让用户通过影片标题和风格搜索。</span><span class="sxs-lookup"><span data-stu-id="d7c14-181">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="d7c14-182">在下一步的部分中，你将了解如何将属性添加到`Movie`模型以及如何添加初始值设定项将自动创建一个测试数据库。</span><span class="sxs-lookup"><span data-stu-id="d7c14-182">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7c14-183">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="d7c14-183">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
