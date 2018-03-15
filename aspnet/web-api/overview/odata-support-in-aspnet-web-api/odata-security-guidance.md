---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: "安全指南用于 ASP.NET Web API 2 OData |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/06/2013
ms.topic: article
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 799e2a0c742b545acf3b5cd27531d734aa7def80
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="39f22-102">安全指南用于 ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="39f22-102">Security Guidance for ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="39f22-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="39f22-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="39f22-104">本主题介绍一些公开通过 OData 的数据集时应考虑的安全问题。</span><span class="sxs-lookup"><span data-stu-id="39f22-104">This topic describes some of the security issues that you should consider when exposing a dataset through OData.</span></span>

## <a name="edm-security"></a><span data-ttu-id="39f22-105">EDM 安全</span><span class="sxs-lookup"><span data-stu-id="39f22-105">EDM Security</span></span>

<span data-ttu-id="39f22-106">查询语义基于实体数据模型 (EDM) 中，不是基础的模型类型。</span><span class="sxs-lookup"><span data-stu-id="39f22-106">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="39f22-107">您可以从 EDM 排除属性和它将看不到查询。</span><span class="sxs-lookup"><span data-stu-id="39f22-107">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="39f22-108">例如，假设您的模型包含具有薪金属性的员工类型。</span><span class="sxs-lookup"><span data-stu-id="39f22-108">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="39f22-109">你可能想要从 EDM 以隐藏它从客户端排除此属性。</span><span class="sxs-lookup"><span data-stu-id="39f22-109">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="39f22-110">有两种方法对排除来自 EDM 的属性。</span><span class="sxs-lookup"><span data-stu-id="39f22-110">There are two ways to exlude a property from the EDM.</span></span> <span data-ttu-id="39f22-111">你可以设置**[IgnoreDataMember]**模型类中的属性上的属性：</span><span class="sxs-lookup"><span data-stu-id="39f22-111">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="39f22-112">您还可以删除该属性从 EDM 以编程方式：</span><span class="sxs-lookup"><span data-stu-id="39f22-112">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="39f22-113">查询安全</span><span class="sxs-lookup"><span data-stu-id="39f22-113">Query Security</span></span>

<span data-ttu-id="39f22-114">恶意或 naïve 客户端可以来构造查询中需要很长时间才能执行。</span><span class="sxs-lookup"><span data-stu-id="39f22-114">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="39f22-115">在最坏情况下这可能会中断服务的访问权限。</span><span class="sxs-lookup"><span data-stu-id="39f22-115">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="39f22-116">**[Queryable]**属性是一个操作筛选器，用于分析、 验证，并适用查询。</span><span class="sxs-lookup"><span data-stu-id="39f22-116">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="39f22-117">筛选器将转换为 LINQ 表达式的查询选项。</span><span class="sxs-lookup"><span data-stu-id="39f22-117">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="39f22-118">当 OData 控制器返回**IQueryable**类型， **IQueryable** LINQ 提供程序将查询转换为 LINQ 表达式。</span><span class="sxs-lookup"><span data-stu-id="39f22-118">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="39f22-119">因此，性能取决于使用时，LINQ 提供程序和数据集或数据库架构的特定特征。</span><span class="sxs-lookup"><span data-stu-id="39f22-119">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="39f22-120">有关在 ASP.NET Web API 中使用 OData 查询选项的详细信息，请参阅[支持 OData 查询选项](supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="39f22-120">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="39f22-121">如果你知道所有客户端信任 （例如，在企业环境中），或如果你的数据集很小，查询性能可能不是问题。</span><span class="sxs-lookup"><span data-stu-id="39f22-121">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="39f22-122">否则，应考虑以下建议。</span><span class="sxs-lookup"><span data-stu-id="39f22-122">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="39f22-123">测试你的服务与各种查询和分析数据库。</span><span class="sxs-lookup"><span data-stu-id="39f22-123">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="39f22-124">启用服务器驱动的分页，若要避免在一个查询中返回大型数据集。</span><span class="sxs-lookup"><span data-stu-id="39f22-124">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="39f22-125">有关详细信息，请参阅[Server-Driven 分页](supporting-odata-query-options.md#server-paging)。</span><span class="sxs-lookup"><span data-stu-id="39f22-125">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="39f22-126">你需要 $filter 和 $orderby 吗？</span><span class="sxs-lookup"><span data-stu-id="39f22-126">Do you need $filter and $orderby?</span></span> <span data-ttu-id="39f22-127">某些应用程序可能允许客户端分页，使用 $top 和 $skip，但禁用其他查询选项。</span><span class="sxs-lookup"><span data-stu-id="39f22-127">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="39f22-128">请考虑将 $orderby 限制为聚集索引中的属性。</span><span class="sxs-lookup"><span data-stu-id="39f22-128">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="39f22-129">对没有聚集索引的大型数据进行排序很慢。</span><span class="sxs-lookup"><span data-stu-id="39f22-129">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="39f22-130">最大节点计数： **MaxNodeCount**属性**[Queryable]**设置 $filter 语法树中允许的最大数字节点。</span><span class="sxs-lookup"><span data-stu-id="39f22-130">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="39f22-131">默认值为 100，但你可能想要设置较低的值，因为大量的节点可能会很慢进行编译。</span><span class="sxs-lookup"><span data-stu-id="39f22-131">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="39f22-132">这是如果你使用 LINQ to Objects （即，在内存中，而不使用中间的 LINQ 提供程序的集合的 LINQ 查询） 尤其如此。</span><span class="sxs-lookup"><span data-stu-id="39f22-132">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="39f22-133">考虑禁用了 any （） 和 all() 函数中，因为这些可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="39f22-133">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="39f22-134">如果任何字符串属性包含大的字符串 （#8212for 示例、 产品说明或博客文章） #8212consider 禁用字符串函数。</span><span class="sxs-lookup"><span data-stu-id="39f22-134">If any string properties contain large strings&#8212for example, a product description or a blog entry&#8212consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="39f22-135">请考虑不允许对导航属性筛选。</span><span class="sxs-lookup"><span data-stu-id="39f22-135">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="39f22-136">对导航属性筛选，可能会导致出现联接，它可能会比较慢，具体取决于你的数据库架构。</span><span class="sxs-lookup"><span data-stu-id="39f22-136">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="39f22-137">下面的代码演示可防止对导航属性筛选的查询验证程序。</span><span class="sxs-lookup"><span data-stu-id="39f22-137">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="39f22-138">有关查询验证程序的详细信息，请参阅[查询验证](supporting-odata-query-options.md#query-validation)。</span><span class="sxs-lookup"><span data-stu-id="39f22-138">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="39f22-139">请考虑通过编写自定义你的数据库的一个验证程序限制 $filter 查询。</span><span class="sxs-lookup"><span data-stu-id="39f22-139">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="39f22-140">例如，考虑这两个查询：</span><span class="sxs-lookup"><span data-stu-id="39f22-140">For example, consider these two queries:</span></span> 

    - <span data-ttu-id="39f22-141">具有 actors 最后一个名称以 A 开头的所有影片。</span><span class="sxs-lookup"><span data-stu-id="39f22-141">All movies with actors whose last name starts with ‘A'.</span></span>
    - <span data-ttu-id="39f22-142">1994 年发布的所有影片。</span><span class="sxs-lookup"><span data-stu-id="39f22-142">All movies released in 1994.</span></span>

    <span data-ttu-id="39f22-143">除非电影参与者编制索引，第一个查询可能需要数据库引擎，扫描整个的影片列表。</span><span class="sxs-lookup"><span data-stu-id="39f22-143">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="39f22-144">而第二个查询可能是可接受的那么电影会按发行年份编制索引。</span><span class="sxs-lookup"><span data-stu-id="39f22-144">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="39f22-145">下面的代码演示的验证程序，允许筛选上的"ReleaseYear"和"Title"属性但没有其他属性。</span><span class="sxs-lookup"><span data-stu-id="39f22-145">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="39f22-146">一般情况下，请考虑你需要哪些 $filter 函数。</span><span class="sxs-lookup"><span data-stu-id="39f22-146">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="39f22-147">如果你的客户端不需要 $filter 完整表现力，你可以限制允许的函数。</span><span class="sxs-lookup"><span data-stu-id="39f22-147">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
