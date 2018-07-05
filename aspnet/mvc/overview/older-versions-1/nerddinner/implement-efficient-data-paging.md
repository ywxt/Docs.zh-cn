---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效数据分页 |Microsoft Docs
author: microsoft
description: 步骤 8 显示了如何将分页支持添加到我们 /Dinners URL，以便而不是显示数千次 dinners，我们将仅显示在 10 个即将推出 dinners...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: e6347c817c7518ef96ffbbf83cf98dd4dc6c011e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372444"
---
<a name="implement-efficient-data-paging"></a><span data-ttu-id="13a40-103">实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="13a40-103">Implement Efficient Data Paging</span></span>
====================
<span data-ttu-id="13a40-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="13a40-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="13a40-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="13a40-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="13a40-106">这是一种免费的步骤 8 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a40-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="13a40-107">步骤 8 显示了如何将分页支持添加到我们 /Dinners URL，以便而不是显示数千次 dinners，我们将仅显示一次-10 即将推出 dinners 并允许最终用户返回页和向前浏览整个列表以 SEO 友好的方式。</span><span class="sxs-lookup"><span data-stu-id="13a40-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="13a40-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="13a40-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="13a40-109">NerdDinner 步骤 8： 分页支持</span><span class="sxs-lookup"><span data-stu-id="13a40-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="13a40-110">如果我们的站点成功，它将具有数千个即将推出 dinners。</span><span class="sxs-lookup"><span data-stu-id="13a40-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="13a40-111">我们需要确保我们的 UI 可进行缩放以处理所有这些 dinners，并允许用户对其进行浏览。</span><span class="sxs-lookup"><span data-stu-id="13a40-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="13a40-112">若要启用此功能，我们将添加到的分页支持我们 */Dinners* URL 以代替的 dinners 的 1000 次为单位显示在一次，我们将仅一次-显示 10 个即将推出 dinners 和允许最终用户页后和向前浏览整个列表中SEO 友好的方式。</span><span class="sxs-lookup"><span data-stu-id="13a40-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="13a40-113">Index （） 操作方法回顾</span><span class="sxs-lookup"><span data-stu-id="13a40-113">Index() Action Method Recap</span></span>

<span data-ttu-id="13a40-114">Index （） 操作方法中我们 DinnersController 类目前看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="13a40-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="13a40-115">当请求 */Dinners* URL，它检索所有即将推出 dinners 的列表，然后呈现出所有的列表：</span><span class="sxs-lookup"><span data-stu-id="13a40-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a><span data-ttu-id="13a40-116">了解 IQuerable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="13a40-116">Understanding IQuerable&lt;T&gt;</span></span>

<span data-ttu-id="13a40-117">*IQueryable&lt;T&gt;* 是作为.NET 3.5 的一部分引入了 LINQ 的接口。</span><span class="sxs-lookup"><span data-stu-id="13a40-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="13a40-118">这样，我们可以充分利用实现分页支持的功能强大的"延迟执行"方案。</span><span class="sxs-lookup"><span data-stu-id="13a40-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="13a40-119">在我们 DinnerRepository 中我们要返回 IQueryable&lt;Dinner&gt;序列从我们 FindUpcomingDinners() 方法：</span><span class="sxs-lookup"><span data-stu-id="13a40-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="13a40-120">IQueryable&lt;Dinner&gt;我们 FindUpcomingDinners() 方法返回的对象将封装查询以从我们使用 LINQ to SQL 的数据库中检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="13a40-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="13a40-121">重要的是，它不会执行对数据库进行查询，直到我们尝试访问/遍历数据，在查询中，或者我们对其调用 tolist （） 方法。</span><span class="sxs-lookup"><span data-stu-id="13a40-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="13a40-122">调用我们 FindUpcomingDinners() 方法的代码可以选择性地将更多"链接"操作/筛选器添加到 IQueryable&lt;Dinner&gt;执行查询前的对象。</span><span class="sxs-lookup"><span data-stu-id="13a40-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="13a40-123">然后，LINQ to SQL 是智能，它能够组合针对数据库执行查询时所请求的数据。</span><span class="sxs-lookup"><span data-stu-id="13a40-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="13a40-124">若要实现分页逻辑我们可以更新我们 DinnersController index （） 操作方法，以便它将额外的"跳过"和"Take"运算符应用于返回 IQueryable&lt;Dinner&gt;之前对其调用 tolist （） 的序列：</span><span class="sxs-lookup"><span data-stu-id="13a40-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="13a40-125">上面的代码通过在数据库中，前 10 个即将推出 dinners 跳过，然后返回 20 dinners。</span><span class="sxs-lookup"><span data-stu-id="13a40-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="13a40-126">LINQ to SQL 是不够智能，无法构造执行此跳过逻辑 SQL 数据库-中并不在 web 服务器的优化的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="13a40-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="13a40-127">这意味着，即使我们在数据库中具有数以百万计的即将推出 Dinners，我们想要的 10 将检索 （使其成为高效、 可缩放） 此请求的一部分。</span><span class="sxs-lookup"><span data-stu-id="13a40-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="13a40-128">向 URL 添加一个"page"值</span><span class="sxs-lookup"><span data-stu-id="13a40-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="13a40-129">而不是硬编码的特定页范围，我们需要我们 Url 以包含一个"page"参数，指示用户正在请求哪个 Dinner 范围。</span><span class="sxs-lookup"><span data-stu-id="13a40-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="13a40-130">使用查询字符串值</span><span class="sxs-lookup"><span data-stu-id="13a40-130">Using a Querystring value</span></span>

<span data-ttu-id="13a40-131">下面的代码演示，我们可以如何更新以支持查询字符串参数并启用 Url 等我们 index （） 操作方法 */Dinners？ 页 = 2*:</span><span class="sxs-lookup"><span data-stu-id="13a40-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="13a40-132">上面的 index （） 操作方法具有一个名为"page"参数。</span><span class="sxs-lookup"><span data-stu-id="13a40-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="13a40-133">参数声明为可为 null 的整数 (这是什么 int？ 指示)。</span><span class="sxs-lookup"><span data-stu-id="13a40-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="13a40-134">这意味着 */Dinners？ 页 = 2* URL 将导致"2"作为参数值传递的值。</span><span class="sxs-lookup"><span data-stu-id="13a40-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="13a40-135">*/Dinners* URL （不带查询字符串值） 将导致传递的 null 值。</span><span class="sxs-lookup"><span data-stu-id="13a40-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="13a40-136">我们按页大小 （在这种情况下 10 行） 乘以页值，以确定多少 dinners，若要跳过。</span><span class="sxs-lookup"><span data-stu-id="13a40-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="13a40-137">我们将使用[C# null"合并"运算符 （？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)处理可以为 null 的类型时，这很有用。</span><span class="sxs-lookup"><span data-stu-id="13a40-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="13a40-138">如果页参数为 null，上面的代码将页分配的值为 0。</span><span class="sxs-lookup"><span data-stu-id="13a40-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="13a40-139">使用嵌入 URL 值</span><span class="sxs-lookup"><span data-stu-id="13a40-139">Using Embedded URL values</span></span>

<span data-ttu-id="13a40-140">使用查询字符串值的替代方法是嵌入的实际 URL 本身中的页参数。</span><span class="sxs-lookup"><span data-stu-id="13a40-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="13a40-141">例如： */Dinners/Page/2*或 */Dinners/2*。</span><span class="sxs-lookup"><span data-stu-id="13a40-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="13a40-142">ASP.NET MVC 包括了功能强大的 URL 路由引擎，它可以更轻松地支持此类方案。</span><span class="sxs-lookup"><span data-stu-id="13a40-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="13a40-143">我们可以注册自定义的路由规则对我们想要任何控制器类或操作方法的任何传入的 URL 或 URL 格式的映射。</span><span class="sxs-lookup"><span data-stu-id="13a40-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="13a40-144">我们需要待办事项，只需打开我们的项目中的 Global.asax 文件：</span><span class="sxs-lookup"><span data-stu-id="13a40-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="13a40-145">然后再注册新的映射规则使用 MapRoute() 帮助器方法，如首次调用的路由。MapRoute() 下面：</span><span class="sxs-lookup"><span data-stu-id="13a40-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="13a40-146">更高版本，我们将注册一个名为"UpcomingDinners"的新路由规则。</span><span class="sxs-lookup"><span data-stu-id="13a40-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="13a40-147">我们要指出它具有 URL 格式"Dinners/页 / {页}"– 其中 {page} 是嵌入在 URL 中的参数值。</span><span class="sxs-lookup"><span data-stu-id="13a40-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="13a40-148">MapRoute() 方法的第三个参数指示我们应将采用这种格式向 DinnersController 类上的 index （） 操作方法的 Url 映射。</span><span class="sxs-lookup"><span data-stu-id="13a40-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="13a40-149">我们可以使用我们已经有了之前使用我们的查询字符串方案 – 但现在我们"page"参数将来自的 URL，并且不在查询字符串完全相同的 index （） 代码：</span><span class="sxs-lookup"><span data-stu-id="13a40-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="13a40-150">现在我们运行该应用程序并在键入 */Dinners*我们将要看到的前 10 个即将推出 dinners:</span><span class="sxs-lookup"><span data-stu-id="13a40-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="13a40-151">当我们键入 */Dinners/Page/1*我们将看到 dinners 的下一页面：</span><span class="sxs-lookup"><span data-stu-id="13a40-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="13a40-152">添加页导航用户界面</span><span class="sxs-lookup"><span data-stu-id="13a40-152">Adding page navigation UI</span></span>

<span data-ttu-id="13a40-153">若要完成我们分页方案的最后一步将是实现"下一步"和"早期/之前"中的导航 UI 视图模板以使用户能够轻松地跳过 Dinner 数据。</span><span class="sxs-lookup"><span data-stu-id="13a40-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="13a40-154">若要正确实现此操作，我们需要知道 Dinners 的总数在数据库中，以及如何多页数据这会转换为。</span><span class="sxs-lookup"><span data-stu-id="13a40-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="13a40-155">然后，我们将需要以计算当前请求"页"的值是否开头或结尾的数据，以及显示或隐藏"上一个"和"下一步"UI 相应地。</span><span class="sxs-lookup"><span data-stu-id="13a40-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="13a40-156">我们 index （） 操作方法中，我们可以实现此逻辑。</span><span class="sxs-lookup"><span data-stu-id="13a40-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="13a40-157">或者我们可以向我们的更多重复使用的方式封装此逻辑的项目添加一个帮助器类。</span><span class="sxs-lookup"><span data-stu-id="13a40-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="13a40-158">下面是一个简单的"PaginatedList"帮助程序类派生自列表&lt;T&gt;集合类内置于.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="13a40-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="13a40-159">它实现了可用于对任何的 IQueryable 数据序列进行分页的可重用集合类。</span><span class="sxs-lookup"><span data-stu-id="13a40-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="13a40-160">NerdDinner 应用程序中我们将它的工作通过 IQueryable&lt;Dinner&gt;的结果，但它可以很容易地对使用 IQueryable&lt;产品&gt;或 IQueryable&lt;客户&gt;导致其他应用程序方案：</span><span class="sxs-lookup"><span data-stu-id="13a40-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="13a40-161">请注意上面如何计算，然后公开属性，例如"PageIndex"、"PageSize"、"TotalCount"和"TotalPages"。</span><span class="sxs-lookup"><span data-stu-id="13a40-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="13a40-162">它还公开两个帮助程序属性"HasPreviousPage"和"HasNextPage"，指示集合中的数据页的开头或原始序列的末尾。</span><span class="sxs-lookup"><span data-stu-id="13a40-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="13a40-163">上面的代码将导致两个 SQL 查询要运行的第一个要检索的 Dinner 对象总数的计数 （这不会返回的对象 – 它而是执行返回一个整数的"SELECT COUNT"语句），第二个要检索的行只是我们需要从我们的数据的当前页的数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="13a40-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="13a40-164">然后，我们可以更新我们 DinnersController.Index() helper 方法来创建 PaginatedList&lt;Dinner&gt;从我们 DinnerRepository.FindUpcomingDinners()，并将其传递给视图模板：</span><span class="sxs-lookup"><span data-stu-id="13a40-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="13a40-165">我们然后可以更新 \Views\Dinners\Index.aspx 视图模板继承 ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt;而不是 ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;，然后将以下代码添加到我们视图模板来显示或隐藏下一页和上一页导航用户界面的底部：</span><span class="sxs-lookup"><span data-stu-id="13a40-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="13a40-166">请注意上面如何我们正在使用 Html.RouteLink() 帮助器方法来生成我们的超链接。</span><span class="sxs-lookup"><span data-stu-id="13a40-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="13a40-167">此方法非常类似于我们以前已使用的 Html.ActionLink() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="13a40-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="13a40-168">不同之处在于，我们要生成使用"UpcomingDinners"路由规则，我们在我们的 Global.asax 文件中设置的 URL。</span><span class="sxs-lookup"><span data-stu-id="13a40-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="13a40-169">这可确保我们将对具有格式我们 index （） 操作方法生成 Url: */Dinners/页 / {page}* – 其中 {page} 值是我们要提供上述基于当前 PageIndex 的变量。</span><span class="sxs-lookup"><span data-stu-id="13a40-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="13a40-170">现在当我们运行我们的应用程序时再次我们将看到一次 10 个 dinners 我们浏览器中：</span><span class="sxs-lookup"><span data-stu-id="13a40-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="13a40-171">我们还有&lt; &lt; &lt;并&gt; &gt; &gt;导航用户界面底部的页，可用于跳过向前和向后通过我们的数据使用搜索引擎可访问的 Url:</span><span class="sxs-lookup"><span data-stu-id="13a40-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="13a40-172">**端主题： 了解 IQueryable 的含义&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="13a40-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="13a40-173">IQueryable&lt;T&gt;是一个非常强大的功能，使各种有趣的延迟的执行方案 （例如分页和组合基于查询）。</span><span class="sxs-lookup"><span data-stu-id="13a40-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="13a40-174">为所有强大功能，你想要谨慎使用如何使用它并确保不被滥用。</span><span class="sxs-lookup"><span data-stu-id="13a40-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="13a40-175">务必要识别该返回 IQueryable&lt;T&gt;从你的存储库的结果使调用代码能够以附加链接的运算符方法，并使参与 ultimate 查询执行。</span><span class="sxs-lookup"><span data-stu-id="13a40-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="13a40-176">如果你不想要提供此功能的调用代码，则应返回返回 IList&lt;T&gt;或 IEnumerable&lt;T&gt;结果-包含已执行查询的结果。</span><span class="sxs-lookup"><span data-stu-id="13a40-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="13a40-177">为分页方案中，这将要求你将推送到存储库方法被调用的实际数据的分页逻辑。</span><span class="sxs-lookup"><span data-stu-id="13a40-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="13a40-178">在此方案中，我们可能会更新我们 FindUpcomingDinners() finder 方法，以使任何一个返回 PaginatedList 的签名： PaginatedList&lt; Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或返回 IList&lt;Dinner&gt;，并使用"totalCount"out 参数返回 Dinners 的总计数： IList&lt;Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize 出 int totalCount） {}</span><span class="sxs-lookup"><span data-stu-id="13a40-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="13a40-179">下一步</span><span class="sxs-lookup"><span data-stu-id="13a40-179">Next Step</span></span>

<span data-ttu-id="13a40-180">让我们现在看看如何我们可以将身份验证和授权支持添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a40-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="13a40-181">[上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="13a40-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
