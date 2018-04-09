---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效数据分页 |Microsoft 文档
author: microsoft
description: 步骤 8 演示如何将分页支持添加到我们 /Dinners URL，以便而不是显示的一次晚餐 1000 秒内，我们将仅显示在 10 即将到来晚餐...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 0188e21438820adf2adbe05b047fdb772540e1a0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="implement-efficient-data-paging"></a><span data-ttu-id="7355e-103">实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="7355e-103">Implement Efficient Data Paging</span></span>
====================
<span data-ttu-id="7355e-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7355e-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7355e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="7355e-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7355e-106">这是一个免费的步骤 8 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7355e-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="7355e-107">步骤 8 演示如何将分页支持添加到我们 /Dinners URL，以便而不是显示的一次晚餐 1000 秒内，我们将仅显示一次-10 即将到来晚餐并允许最终用户返回页面和 SEO 友好方式向前移动整个列表。</span><span class="sxs-lookup"><span data-stu-id="7355e-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="7355e-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="7355e-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="7355e-109">NerdDinner 步骤 8： 分页支持</span><span class="sxs-lookup"><span data-stu-id="7355e-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="7355e-110">如果我们的站点操作成功，将会有数千个即将到来的晚餐。</span><span class="sxs-lookup"><span data-stu-id="7355e-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="7355e-111">我们需要确保我们的 UI 进行缩放以处理所有这些晚餐，并允许用户对其进行浏览。</span><span class="sxs-lookup"><span data-stu-id="7355e-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="7355e-112">若要启用此功能，我们将添加到的分页支持我们*/Dinners* URL，因此的晚餐 1000 秒内显示在一次，我们将仅显示一次-10 即将到来晚餐和允许最终用户页后和向前移动的完整列表SEO 友好的方式。</span><span class="sxs-lookup"><span data-stu-id="7355e-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="7355e-113">Index （） 操作方法概述</span><span class="sxs-lookup"><span data-stu-id="7355e-113">Index() Action Method Recap</span></span>

<span data-ttu-id="7355e-114">我们 DinnersController 类中的 index （） 操作方法当前看起来像下面：</span><span class="sxs-lookup"><span data-stu-id="7355e-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="7355e-115">当请求*/Dinners* URL，它将检索所有即将发布晚餐的列表，然后呈现所有的效果的列表：</span><span class="sxs-lookup"><span data-stu-id="7355e-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a><span data-ttu-id="7355e-116">了解 IQuerable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="7355e-116">Understanding IQuerable&lt;T&gt;</span></span>

<span data-ttu-id="7355e-117">*IQueryable&lt;T&gt;* 是作为.NET 3.5 的一部分引入了 LINQ 的接口。</span><span class="sxs-lookup"><span data-stu-id="7355e-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="7355e-118">它使我们可以充分利用实现分页支持的功能强大的"延迟执行"方案。</span><span class="sxs-lookup"><span data-stu-id="7355e-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="7355e-119">在我们 DinnerRepository 我们要返回 IQueryable&lt;Dinner&gt;从我们 FindUpcomingDinners() 方法的序列：</span><span class="sxs-lookup"><span data-stu-id="7355e-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="7355e-120">IQueryable&lt;Dinner&gt;我们 FindUpcomingDinners() 方法返回的对象所封装查询以从我们使用 LINQ to SQL 的数据库中检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="7355e-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="7355e-121">重要的是，它不会执行对数据库的查询，直到我们尝试访问/循环访问的数据在查询中，或直到我们对其调用 tolist （） 方法。</span><span class="sxs-lookup"><span data-stu-id="7355e-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="7355e-122">调用我们 FindUpcomingDinners() 方法的代码可以根据需要选择将更多"链接"操作/筛选器添加到 IQueryable&lt;Dinner&gt;之前执行查询的对象。</span><span class="sxs-lookup"><span data-stu-id="7355e-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="7355e-123">LINQ to SQL 是然后足够智能，可执行对数据库的组合的查询请求数据时。</span><span class="sxs-lookup"><span data-stu-id="7355e-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="7355e-124">若要实现分页逻辑我们可以更新我们 DinnersController index （） 操作方法，以便它将其他"Skip"和"使用"运算符应用于返回 IQueryable&lt;Dinner&gt;之前对其调用 tolist （） 的序列：</span><span class="sxs-lookup"><span data-stu-id="7355e-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="7355e-125">上面的代码会跳过前 10 的即将到来晚餐在数据库中，并返回然后 20 晚餐。</span><span class="sxs-lookup"><span data-stu-id="7355e-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="7355e-126">LINQ to SQL 是足够智能，可构造执行此跳过逻辑 SQL 数据库 – 中，不能在 web 服务器的优化的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="7355e-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="7355e-127">这意味着，即使在数据库中具有数以百万计的即将到来的晚餐我们，我们希望的 10 将检索 （使其成为高效且可伸缩） 此请求的一部分。</span><span class="sxs-lookup"><span data-stu-id="7355e-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="7355e-128">将"页"值添加到 URL</span><span class="sxs-lookup"><span data-stu-id="7355e-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="7355e-129">而不是硬编码的特定页范围，我们将需要我们 Url 以包括"页"参数，该值指示用户正在请求的 Dinner 范围。</span><span class="sxs-lookup"><span data-stu-id="7355e-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="7355e-130">使用查询字符串值</span><span class="sxs-lookup"><span data-stu-id="7355e-130">Using a Querystring value</span></span>

<span data-ttu-id="7355e-131">下面的代码演示如何更新我们 index （） 的操作方法中支持的查询字符串参数和实现类似的 Url */Dinners？ 页 = 2*:</span><span class="sxs-lookup"><span data-stu-id="7355e-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="7355e-132">上面的 index （） 操作方法具有一个名为"页"参数。</span><span class="sxs-lookup"><span data-stu-id="7355e-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="7355e-133">参数声明为可以为 null 的整数 (这是什么 int？ 指示)。</span><span class="sxs-lookup"><span data-stu-id="7355e-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="7355e-134">这意味着， */Dinners？ 页 = 2* URL 将会导致"2"作为参数值传递值。</span><span class="sxs-lookup"><span data-stu-id="7355e-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="7355e-135">*/Dinners* URL （不带查询字符串值） 将导致将传递 null 值。</span><span class="sxs-lookup"><span data-stu-id="7355e-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="7355e-136">我们将乘以页值 （在这种情况下 10 行） 的页大小来确定多少晚餐跳过。</span><span class="sxs-lookup"><span data-stu-id="7355e-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="7355e-137">我们将使用[C# null"合并"运算符 （？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)处理可以为 null 的类型时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="7355e-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="7355e-138">如果页参数为 null，上面的代码将页分配值为 0。</span><span class="sxs-lookup"><span data-stu-id="7355e-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="7355e-139">使用嵌入的 URL 值</span><span class="sxs-lookup"><span data-stu-id="7355e-139">Using Embedded URL values</span></span>

<span data-ttu-id="7355e-140">使用查询字符串值的替代方法是嵌入的实际 URL 本身中的页参数。</span><span class="sxs-lookup"><span data-stu-id="7355e-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="7355e-141">例如： */Dinners/Page/2*或*/晚餐/2*。</span><span class="sxs-lookup"><span data-stu-id="7355e-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="7355e-142">ASP.NET MVC 包括一个功能强大的 URL 路由引擎，可以轻松地支持与此类似的方案。</span><span class="sxs-lookup"><span data-stu-id="7355e-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="7355e-143">我们可以注册自定义的路由规则的映射任何传入的 URL 或 URL 格式，我们想要任何控制器类或操作方法。</span><span class="sxs-lookup"><span data-stu-id="7355e-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="7355e-144">我们只需待办事项是打开我们项目中的 Global.asax 文件：</span><span class="sxs-lookup"><span data-stu-id="7355e-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="7355e-145">然后再注册新的映射规则使用如路由首次调用的 MapRoute() 帮助器方法。MapRoute() 下面：</span><span class="sxs-lookup"><span data-stu-id="7355e-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="7355e-146">更高版本，我们将注册一个名为"UpcomingDinners"的新路由规则。</span><span class="sxs-lookup"><span data-stu-id="7355e-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="7355e-147">我们将它具有以下 URL 格式，表示"晚餐/页 / {页}"– 其中 {page} 是在 URL 中嵌入一个参数值。</span><span class="sxs-lookup"><span data-stu-id="7355e-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="7355e-148">MapRoute() 方法的第三个参数指示我们应映射匹配到 DinnersController 类上的 index （） 操作方法的这种格式的 Url。</span><span class="sxs-lookup"><span data-stu-id="7355e-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="7355e-149">我们可以使用我们在之前我们查询字符串的方案 – 但现在我们"页"参数将来自的 URL 和查询字符串不完全相同的 index （） 代码：</span><span class="sxs-lookup"><span data-stu-id="7355e-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="7355e-150">现在我们运行应用程序并在键入*/Dinners*我们将看到前 10 个即将到来晚餐：</span><span class="sxs-lookup"><span data-stu-id="7355e-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="7355e-151">当我们键入*/Dinners/Page/1*我们将看到晚餐的第二页：</span><span class="sxs-lookup"><span data-stu-id="7355e-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="7355e-152">添加页导航用户界面</span><span class="sxs-lookup"><span data-stu-id="7355e-152">Adding page navigation UI</span></span>

<span data-ttu-id="7355e-153">完成我们分页的方案的最后一步是实现"下一步"和"早期/之前"中的导航 UI 我们查看模板，以使用户能够轻松地跳过 Dinner 数据。</span><span class="sxs-lookup"><span data-stu-id="7355e-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="7355e-154">若要正确实现此操作，我们将需要知道的晚餐总数在数据库中，以及如何数据的多个页面这将转换为。</span><span class="sxs-lookup"><span data-stu-id="7355e-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="7355e-155">然后，我们将需要以计算当前请求的"页"值的开头或末尾数据，并显示或隐藏"上一页"和"下一页"UI 相应地。</span><span class="sxs-lookup"><span data-stu-id="7355e-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="7355e-156">在我们 index （） 操作方法中，我们无法实现此逻辑。</span><span class="sxs-lookup"><span data-stu-id="7355e-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="7355e-157">或者我们可以向我们的更多重复使用的方式封装此逻辑的项目添加一个帮助器类。</span><span class="sxs-lookup"><span data-stu-id="7355e-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="7355e-158">下面是一个简单的"PaginatedList"帮助程序类，派生自列表&lt;T&gt;集合类内置于.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="7355e-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="7355e-159">它可实现可用于分页 IQueryable 数据的任何序列的可重用集合类。</span><span class="sxs-lookup"><span data-stu-id="7355e-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="7355e-160">在我们 NerdDinner 应用程序中我们将用它处理通过 IQueryable&lt;Dinner&gt;结果，但它无法轻松地对使用 IQueryable&lt;产品&gt;或 IQueryable&lt;客户&gt;导致其他应用程序方案：</span><span class="sxs-lookup"><span data-stu-id="7355e-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="7355e-161">此公式计算上面注意到，然后公开属性如"PageIndex"、"PageSize"、"TotalCount"和"TotalPages"。</span><span class="sxs-lookup"><span data-stu-id="7355e-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="7355e-162">它还公开两个帮助器属性"HasPreviousPage"和"HasNextPage"，指示集合中的数据的页的开头或原始序列的末尾。</span><span class="sxs-lookup"><span data-stu-id="7355e-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="7355e-163">上面的代码将导致两个 SQL 查询要运行的第一个要检索的 Dinner 对象总数的计数 （这不会返回的对象 – 它而是执行返回一个整数的"选择计数"语句），第二个检索只需的行我们需要从我们的数据的当前页的数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="7355e-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="7355e-164">然后，我们可以更新我们 DinnersController.Index() helper 方法，以创建 PaginatedList&lt;Dinner&gt;从我们 DinnerRepository.FindUpcomingDinners() 结果，并将它传递给我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="7355e-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="7355e-165">然后，我们可以更新 \Views\Dinners\Index.aspx 视图模板以继承 ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt;而不是 ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;，然后将以下代码添加到我们查看模板以显示或隐藏下一步和以前导航用户界面底部：</span><span class="sxs-lookup"><span data-stu-id="7355e-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="7355e-166">请注意上面如何我们将使用 Html.RouteLink() 帮助器方法来生成我们超链接。</span><span class="sxs-lookup"><span data-stu-id="7355e-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="7355e-167">此方法是类似于我们以前曾使用过的 Html.ActionLink() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="7355e-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="7355e-168">不同之处在于，我们要生成使用"UpcomingDinners"路由规则我们我们 Global.asax 文件中设置的 URL。</span><span class="sxs-lookup"><span data-stu-id="7355e-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="7355e-169">这将确保我们将为我们的 index （） 操作方法中具有格式生成 Url: */Dinners/页 / {page}* – 其中 {页} 值是我们提供上面基于当前 PageIndex 的变量。</span><span class="sxs-lookup"><span data-stu-id="7355e-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="7355e-170">现在我们运行我们的应用程序时试我们将看到一次 10 晚餐在我们的浏览器中：</span><span class="sxs-lookup"><span data-stu-id="7355e-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="7355e-171">我们还必须&lt; &lt; &lt;和&gt; &gt; &gt;导航，我们便可以跳过向前和向后通过我们的数据使用搜索引擎可访问的 Url 的页面底部的用户界面：</span><span class="sxs-lookup"><span data-stu-id="7355e-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="7355e-172">**端主题内容： 了解 IQueryable 的含义&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="7355e-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="7355e-173">IQueryable&lt;T&gt;是非常强大的功能，使各种有趣的延迟的执行方案 （如分页和组合基于查询）。</span><span class="sxs-lookup"><span data-stu-id="7355e-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="7355e-174">作为与所有强大的功能，你想要谨慎使用它，并确保不被滥用。</span><span class="sxs-lookup"><span data-stu-id="7355e-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="7355e-175">务必要识别该返回 IQueryable&lt;T&gt;从存储库的结果使调用代码可以追加到其中，连锁的运算符方法，并使参与 ultimate 查询执行。</span><span class="sxs-lookup"><span data-stu-id="7355e-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="7355e-176">如果你不希望提供此功能的调用代码，则应返回备份 IList&lt;T&gt;或 IEnumerable&lt;T&gt;结果-包含已执行查询的结果。</span><span class="sxs-lookup"><span data-stu-id="7355e-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="7355e-177">分页方案中，这将要求你将实际数据分页逻辑推入所调用的存储库方法。</span><span class="sxs-lookup"><span data-stu-id="7355e-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="7355e-178">在此方案中，我们可能会更新我们 FindUpcomingDinners() finder 方法，请返回 PaginatedList 的签名： PaginatedList&lt; Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或回到是 IList&lt;Dinner&gt;，然后使用"totalCount"out param 返回晚餐的总计数： IList&lt;Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize，出 int totalCount） {}</span><span class="sxs-lookup"><span data-stu-id="7355e-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="7355e-179">下一步</span><span class="sxs-lookup"><span data-stu-id="7355e-179">Next Step</span></span>

<span data-ttu-id="7355e-180">让我们现在看一下我们可以如何添加身份验证和授权支持到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7355e-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7355e-181">[上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="7355e-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
