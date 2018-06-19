---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: 支持 ASP.NET Web API 2 中的 OData 查询选项 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/04/2013
ms.topic: article
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 004c029db6f01627f7cadff26aaf5554ce2b93a5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508016"
---
<a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="24c0a-102">ASP.NET Web API 2 中支持的 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-102">Supporting OData Query Options in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="24c0a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="24c0a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="24c0a-104">OData 定义可以用于修改 OData 查询参数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-104">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="24c0a-105">客户端的请求 URI 查询字符串中发送这些参数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-105">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="24c0a-106">例如，若要对结果进行排序，客户端使用 $orderby 参数：</span><span class="sxs-lookup"><span data-stu-id="24c0a-106">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="24c0a-107">这些参数调用 OData 规范*查询选项*。</span><span class="sxs-lookup"><span data-stu-id="24c0a-107">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="24c0a-108">你可以在你的项目 （&） #8212; 启用任何 Web API 控制器的 OData 查询选项控制器不必是一个 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="24c0a-108">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="24c0a-109">这样，可以方便地添加如筛选和排序的任何 Web API 应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="24c0a-109">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="24c0a-110">启用查询选项，请阅读主题之前[OData 安全指南](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="24c0a-110">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="24c0a-111">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-111">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="24c0a-112">示例查询</span><span class="sxs-lookup"><span data-stu-id="24c0a-112">Example Queries</span></span>](#examples)
- [<span data-ttu-id="24c0a-113">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="24c0a-113">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="24c0a-114">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-114">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="24c0a-115">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-115">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="24c0a-116">查询验证</span><span class="sxs-lookup"><span data-stu-id="24c0a-116">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="24c0a-117">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-117">Enabling OData Query Options</span></span>

<span data-ttu-id="24c0a-118">Web API 支持以下 OData 查询选项：</span><span class="sxs-lookup"><span data-stu-id="24c0a-118">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="24c0a-119">选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-119">Option</span></span> | <span data-ttu-id="24c0a-120">描述</span><span class="sxs-lookup"><span data-stu-id="24c0a-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24c0a-121">$expand</span><span class="sxs-lookup"><span data-stu-id="24c0a-121">$expand</span></span> | <span data-ttu-id="24c0a-122">展开相关的实体内联。</span><span class="sxs-lookup"><span data-stu-id="24c0a-122">Expands related entities inline.</span></span> |
| <span data-ttu-id="24c0a-123">$filter</span><span class="sxs-lookup"><span data-stu-id="24c0a-123">$filter</span></span> | <span data-ttu-id="24c0a-124">筛选结果，并基于布尔条件。</span><span class="sxs-lookup"><span data-stu-id="24c0a-124">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="24c0a-125">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="24c0a-125">$inlinecount</span></span> | <span data-ttu-id="24c0a-126">指示服务器在响应中包含的匹配的实体的总数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-126">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="24c0a-127">（适用于服务器端分页。）</span><span class="sxs-lookup"><span data-stu-id="24c0a-127">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="24c0a-128">$orderby</span><span class="sxs-lookup"><span data-stu-id="24c0a-128">$orderby</span></span> | <span data-ttu-id="24c0a-129">对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="24c0a-129">Sorts the results.</span></span> |
| <span data-ttu-id="24c0a-130">$select</span><span class="sxs-lookup"><span data-stu-id="24c0a-130">$select</span></span> | <span data-ttu-id="24c0a-131">选择要在响应中包含哪些属性。</span><span class="sxs-lookup"><span data-stu-id="24c0a-131">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="24c0a-132">$skip</span><span class="sxs-lookup"><span data-stu-id="24c0a-132">$skip</span></span> | <span data-ttu-id="24c0a-133">跳过前 n 个结果。</span><span class="sxs-lookup"><span data-stu-id="24c0a-133">Skips the first n results.</span></span> |
| <span data-ttu-id="24c0a-134">$top</span><span class="sxs-lookup"><span data-stu-id="24c0a-134">$top</span></span> | <span data-ttu-id="24c0a-135">返回仅的第一个 n 的结果。</span><span class="sxs-lookup"><span data-stu-id="24c0a-135">Returns only the first n the results.</span></span> |

<span data-ttu-id="24c0a-136">若要使用 OData 查询选项，必须显式启用它们。</span><span class="sxs-lookup"><span data-stu-id="24c0a-136">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="24c0a-137">可以全局启用整个应用程序，或为特定控制器或特定操作启用它们。</span><span class="sxs-lookup"><span data-stu-id="24c0a-137">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="24c0a-138">若要全局启用 OData 查询选项，请调用**EnableQuerySupport**上**HttpConfiguration**在启动时的类：</span><span class="sxs-lookup"><span data-stu-id="24c0a-138">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="24c0a-139">**EnableQuerySupport**方法启用返回任何控制器操作为全局查询选项**IQueryable**类型。</span><span class="sxs-lookup"><span data-stu-id="24c0a-139">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="24c0a-140">如果你不希望对整个应用程序启用的查询选项，你可以启用它们特定控制器操作的添加 **[Queryable]** 属性设为的操作方法。</span><span class="sxs-lookup"><span data-stu-id="24c0a-140">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="24c0a-141">示例查询</span><span class="sxs-lookup"><span data-stu-id="24c0a-141">Example Queries</span></span>

<span data-ttu-id="24c0a-142">此部分显示的可能使用的 OData 查询选项的查询的类型。</span><span class="sxs-lookup"><span data-stu-id="24c0a-142">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="24c0a-143">有关查询选项的特定详细信息，请参阅位于 OData 文档[www.odata.org](http://www.odata.org/)。</span><span class="sxs-lookup"><span data-stu-id="24c0a-143">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="24c0a-144">有关 $展开和 $select，请参阅[使用 $select，$expand、 和 ASP.NET Web API OData 中的 $value](using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="24c0a-144">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="24c0a-145">**客户端驱动的分页**</span><span class="sxs-lookup"><span data-stu-id="24c0a-145">**Client-Driven Paging**</span></span>

<span data-ttu-id="24c0a-146">大型实体集的情况下，客户端可能会想要限制结果数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-146">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="24c0a-147">例如，客户端可能在一次，以获取下一结果页的"下一步"链接显示 10 个条目。</span><span class="sxs-lookup"><span data-stu-id="24c0a-147">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="24c0a-148">若要执行此操作，客户端，请使用 $top 和 $skip 选项。</span><span class="sxs-lookup"><span data-stu-id="24c0a-148">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="24c0a-149">$Top 选项提供要返回的最大项数并 $skip 选项提供要跳过的项数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-149">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="24c0a-150">前面的示例提取条目 21 到 30。</span><span class="sxs-lookup"><span data-stu-id="24c0a-150">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="24c0a-151">**筛选**</span><span class="sxs-lookup"><span data-stu-id="24c0a-151">**Filtering**</span></span>

<span data-ttu-id="24c0a-152">$Filter 选项允许客户端通过将应用的布尔表达式筛选结果。</span><span class="sxs-lookup"><span data-stu-id="24c0a-152">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="24c0a-153">筛选器表达式是功能非常强大;它们包括逻辑和算术运算符、 字符串函数和日期函数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-153">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="24c0a-154">返回与类别的所有产品等于"Toys"。</span><span class="sxs-lookup"><span data-stu-id="24c0a-154">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="24c0a-155">`http://localhost/Products?$filter=Category`eq 'Toys</span><span class="sxs-lookup"><span data-stu-id="24c0a-155">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="24c0a-156">返回价格小于 10 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="24c0a-156">Return all products with price less than 10.</span></span> | <span data-ttu-id="24c0a-157">`http://localhost/Products?$filter=Price`lt 10</span><span class="sxs-lookup"><span data-stu-id="24c0a-157">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="24c0a-158">逻辑运算符： 返回的所有产品其中价格 > = 5 和价格 < = 15。</span><span class="sxs-lookup"><span data-stu-id="24c0a-158">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="24c0a-159">`http://localhost/Products?$filter=Price`ge 5 和价格 le 15</span><span class="sxs-lookup"><span data-stu-id="24c0a-159">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="24c0a-160">字符串函数： 返回名称中使用"zz"的所有产品。</span><span class="sxs-lookup"><span data-stu-id="24c0a-160">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="24c0a-161">日期函数： 返回 2005年之后的与 ReleaseDate 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="24c0a-161">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="24c0a-162">`http://localhost/Products?$filter=year(ReleaseDate)`gt 2005</span><span class="sxs-lookup"><span data-stu-id="24c0a-162">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="24c0a-163">**排序**</span><span class="sxs-lookup"><span data-stu-id="24c0a-163">**Sorting**</span></span>

<span data-ttu-id="24c0a-164">若要对结果进行排序，请使用 $orderby 筛选器。</span><span class="sxs-lookup"><span data-stu-id="24c0a-164">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="24c0a-165">价格按排序。</span><span class="sxs-lookup"><span data-stu-id="24c0a-165">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="24c0a-166">按降序排序 （最高到低） 的价格排序。</span><span class="sxs-lookup"><span data-stu-id="24c0a-166">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="24c0a-167">按类别，进行排序，然后按降序排序类别中的价格进行排序。</span><span class="sxs-lookup"><span data-stu-id="24c0a-167">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="24c0a-168">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="24c0a-168">Server-Driven Paging</span></span>

<span data-ttu-id="24c0a-169">如果你的数据库包含数百万条记录，你不想将其发送全部位于一个负载。</span><span class="sxs-lookup"><span data-stu-id="24c0a-169">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="24c0a-170">为了防止此情况，服务器可能会限制单个响应中发送的条目数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-170">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="24c0a-171">若要启用服务器分页，设置**PageSize**中的属性**Queryable**属性。</span><span class="sxs-lookup"><span data-stu-id="24c0a-171">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="24c0a-172">值为要返回的最大项数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-172">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="24c0a-173">如果你的控制器返回 OData 格式，则响应正文将包含指向下一页数据的链接：</span><span class="sxs-lookup"><span data-stu-id="24c0a-173">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="24c0a-174">客户端可以使用此链接以提取下一步的页。</span><span class="sxs-lookup"><span data-stu-id="24c0a-174">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="24c0a-175">若要了解在结果集中的总项数，客户端可以设置 $inlinecount 查询选项的值"allpages"。</span><span class="sxs-lookup"><span data-stu-id="24c0a-175">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="24c0a-176">值"allpages"指示服务器在响应中包含的总计数：</span><span class="sxs-lookup"><span data-stu-id="24c0a-176">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="24c0a-177">下一步页链接和内联计数都需要 OData 格式。</span><span class="sxs-lookup"><span data-stu-id="24c0a-177">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="24c0a-178">原因是 OData 响应正文以保留的链接和计数中定义特殊的字段。</span><span class="sxs-lookup"><span data-stu-id="24c0a-178">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="24c0a-179">对于非 OData 格式，它是支持通过包装中的查询结果的下一页链接和内联计数，仍可能**PageResult&lt;T&gt;** 对象。</span><span class="sxs-lookup"><span data-stu-id="24c0a-179">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="24c0a-180">但是，它需要更多代码。</span><span class="sxs-lookup"><span data-stu-id="24c0a-180">However, it requires a bit more code.</span></span> <span data-ttu-id="24c0a-181">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="24c0a-181">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="24c0a-182">此处是一个示例 JSON 响应：</span><span class="sxs-lookup"><span data-stu-id="24c0a-182">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="24c0a-183">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-183">Limiting the Query Options</span></span>

<span data-ttu-id="24c0a-184">查询选项为客户提供了大量的控制在服务器运行的查询。</span><span class="sxs-lookup"><span data-stu-id="24c0a-184">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="24c0a-185">在某些情况下，你可能想要限制可用于安全或性能原因的选项。</span><span class="sxs-lookup"><span data-stu-id="24c0a-185">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="24c0a-186">**[Queryable]** 属性具有一些属性中为此生成的。</span><span class="sxs-lookup"><span data-stu-id="24c0a-186">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="24c0a-187">以下是一些示例。</span><span class="sxs-lookup"><span data-stu-id="24c0a-187">Here are some examples.</span></span>

<span data-ttu-id="24c0a-188">允许使用仅 $skip 和 $top，以支持分页和其他任何内容：</span><span class="sxs-lookup"><span data-stu-id="24c0a-188">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="24c0a-189">允许排序只能由某些属性，以防止排序不在数据库中编制索引的属性：</span><span class="sxs-lookup"><span data-stu-id="24c0a-189">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="24c0a-190">允许使用"eq"逻辑函数，但没有其他逻辑函数：</span><span class="sxs-lookup"><span data-stu-id="24c0a-190">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="24c0a-191">不允许任何算术运算符：</span><span class="sxs-lookup"><span data-stu-id="24c0a-191">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="24c0a-192">你可以通过构造全局限制选项**QueryableAttribute**实例和将其传递给**EnableQuerySupport**函数：</span><span class="sxs-lookup"><span data-stu-id="24c0a-192">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="24c0a-193">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="24c0a-193">Invoking Query Options Directly</span></span>

<span data-ttu-id="24c0a-194">而不是使用 **[Queryable]** 属性中，你可以直接在你的控制器中调用的查询选项。</span><span class="sxs-lookup"><span data-stu-id="24c0a-194">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="24c0a-195">为此，请添加**ODataQueryOptions**控制器方法的参数。</span><span class="sxs-lookup"><span data-stu-id="24c0a-195">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="24c0a-196">在这种情况下，不需要 **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="24c0a-196">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="24c0a-197">Web API 填充**ODataQueryOptions**从 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="24c0a-197">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="24c0a-198">若要应用该查询，将传递**IQueryable**到**ApplyTo**方法。</span><span class="sxs-lookup"><span data-stu-id="24c0a-198">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="24c0a-199">该方法返回另一个**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="24c0a-199">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="24c0a-200">对于高级方案，如果你没有**IQueryable**查询提供程序，你可以检查**ODataQueryOptions** ，将转换到另一种形式的查询选项。</span><span class="sxs-lookup"><span data-stu-id="24c0a-200">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="24c0a-201">(有关示例，请参阅 RaghuRam Nadiminti 博客文章[HQL 转换 OData 查询](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中也包含[示例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。)</span><span class="sxs-lookup"><span data-stu-id="24c0a-201">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="24c0a-202">查询验证</span><span class="sxs-lookup"><span data-stu-id="24c0a-202">Query Validation</span></span>

<span data-ttu-id="24c0a-203">**[Queryable]** 属性在执行前验证查询。</span><span class="sxs-lookup"><span data-stu-id="24c0a-203">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="24c0a-204">在中执行的验证步骤**QueryableAttribute.ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="24c0a-204">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="24c0a-205">你还可以自定义验证过程。</span><span class="sxs-lookup"><span data-stu-id="24c0a-205">You can also customize the validation process.</span></span>

<span data-ttu-id="24c0a-206">另请参阅[OData 安全指南](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="24c0a-206">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="24c0a-207">首先，在中定义一个验证程序，它是类的替代**Web.Http.OData.Query.Validators**命名空间。</span><span class="sxs-lookup"><span data-stu-id="24c0a-207">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="24c0a-208">例如，下面的验证程序类禁用 $orderby 选项的 desc 选项。</span><span class="sxs-lookup"><span data-stu-id="24c0a-208">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="24c0a-209">子类 **[Queryable]** 属性重写**ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="24c0a-209">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="24c0a-210">然后设置你的自定义特性包括全局或每个控制器：</span><span class="sxs-lookup"><span data-stu-id="24c0a-210">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="24c0a-211">如果你使用**ODataQueryOptions**直接的选项中设置验证程序：</span><span class="sxs-lookup"><span data-stu-id="24c0a-211">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
