---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: "ASP.NET Web API 2 中的路由约定 Odata |Microsoft 文档"
author: MikeWasson
description: "本指南介绍了 Web API 使用 OData 终结点的路由约定。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/31/2013
ms.topic: article
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 0ab99dd443040b90ffefd2f5b9261a63b91e9463
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="routing-conventions-in-aspnet-web-api-2-odata"></a><span data-ttu-id="0fa3f-103">ASP.NET Web API 2 中的路由约定 Odata</span><span class="sxs-lookup"><span data-stu-id="0fa3f-103">Routing Conventions in ASP.NET Web API 2 Odata</span></span>
====================
<span data-ttu-id="0fa3f-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="0fa3f-105">本指南介绍了 Web API 使用 OData 终结点的路由约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-105">This article describes the routing conventions that Web API uses for OData endpoints.</span></span>


<span data-ttu-id="0fa3f-106">当 Web API 获取 OData 请求时，它将请求映射到的控制器名称和操作名称。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-106">When Web API gets an OData request, it maps the request to a controller name and an action name.</span></span> <span data-ttu-id="0fa3f-107">映射基于 HTTP 方法和 URI。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-107">The mapping is based on the HTTP method and the URI.</span></span> <span data-ttu-id="0fa3f-108">例如，`GET /odata/Products(1)`映射到`ProductsController.GetProduct`。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-108">For example, `GET /odata/Products(1)` maps to `ProductsController.GetProduct`.</span></span>

<span data-ttu-id="0fa3f-109">在本文的第 1 部分中，我介绍了内置的 OData 路由约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-109">In part 1 of this article, I describe the built-in OData routing conventions.</span></span> <span data-ttu-id="0fa3f-110">这些约定专为 OData 终结点，并且它们将默认的 Web API 路由系统。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-110">These conventions are designed specifically for OData endpoints, and they replace the default Web API routing system.</span></span> <span data-ttu-id="0fa3f-111">(在调用时，会发生情况替换**MapODataRoute**。)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-111">(The replacement happens when you call **MapODataRoute**.)</span></span>

<span data-ttu-id="0fa3f-112">在第 2 部分，我将介绍如何添加自定义路由的约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-112">In part 2, I show how to add custom routing conventions.</span></span> <span data-ttu-id="0fa3f-113">当前的内置约定未涵盖整个范围的 OData Uri，但你可以扩展它们以处理其他情况。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-113">Currently the built-in conventions do not cover the entire range of OData URIs, but you can extend them to handle additional cases.</span></span>

- [<span data-ttu-id="0fa3f-114">内置路由约定</span><span class="sxs-lookup"><span data-stu-id="0fa3f-114">Built-in Routing Conventions</span></span>](#conventions)
- [<span data-ttu-id="0fa3f-115">自定义路由约定</span><span class="sxs-lookup"><span data-stu-id="0fa3f-115">Custom Routing Conventions</span></span>](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a><span data-ttu-id="0fa3f-116">内置路由约定</span><span class="sxs-lookup"><span data-stu-id="0fa3f-116">Built-in Routing Conventions</span></span>

<span data-ttu-id="0fa3f-117">我介绍了 Web API 中的 OData 路由约定之前，最好先了解 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-117">Before I describe the OData routing conventions in Web API, it's helpful to understand OData URIs.</span></span> <span data-ttu-id="0fa3f-118">[OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)组成：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-118">An [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) consists of:</span></span>

- <span data-ttu-id="0fa3f-119">服务根</span><span class="sxs-lookup"><span data-stu-id="0fa3f-119">The service root</span></span>
- <span data-ttu-id="0fa3f-120">资源路径</span><span class="sxs-lookup"><span data-stu-id="0fa3f-120">The resource path</span></span>
- <span data-ttu-id="0fa3f-121">查询选项</span><span class="sxs-lookup"><span data-stu-id="0fa3f-121">Query options</span></span>

![](odata-routing-conventions/_static/image1.png)

<span data-ttu-id="0fa3f-122">用于路由，重要的部分是资源路径。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-122">For routing, the important part is the resource path.</span></span> <span data-ttu-id="0fa3f-123">资源路径分为段。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-123">The resource path is divided into segments.</span></span> <span data-ttu-id="0fa3f-124">例如，`/Products(1)/Supplier`具有三个段：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-124">For example, `/Products(1)/Supplier` has three segments:</span></span>

- <span data-ttu-id="0fa3f-125">`Products`引用名为"产品"实体集。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-125">`Products` refers to an entity set named "Products".</span></span>
- <span data-ttu-id="0fa3f-126">`1`是否为实体键，从组中选择单个实体。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-126">`1` is an entity key, selecting a single entity from the set.</span></span>
- <span data-ttu-id="0fa3f-127">`Supplier`是一个导航属性，选择相关的实体。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-127">`Supplier` is a navigation property that selects a related entity.</span></span>

<span data-ttu-id="0fa3f-128">因此出供应商产品 1 会选取此路径。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-128">So this path picks out the supplier of product 1.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa3f-129">OData 路径段始终不对应 URI 段。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-129">OData path segments do not always correspond to URI segments.</span></span> <span data-ttu-id="0fa3f-130">例如，"1"被视为路径段。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-130">For example, "1" is considered a path segment.</span></span>


<span data-ttu-id="0fa3f-131">**控制器名称。**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-131">**Controller Names.**</span></span> <span data-ttu-id="0fa3f-132">控制器名称始终被派生自的实体集的资源路径的根目录。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-132">The controller name is always derived from the entity set at the root of the resource path.</span></span> <span data-ttu-id="0fa3f-133">例如，如果资源路径是`/Products(1)/Supplier`，Web API 查找名为的控制器`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-133">For example, if the resource path is `/Products(1)/Supplier`, Web API looks for a controller named `ProductsController`.</span></span>

<span data-ttu-id="0fa3f-134">**操作名称。**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-134">**Action Names.**</span></span> <span data-ttu-id="0fa3f-135">操作名称派生自的路径段以及实体数据模型 (EDM) 中，为以下表格中列出。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-135">Action names are derived from the path segments plus the entity data model (EDM), as listed in the following tables.</span></span> <span data-ttu-id="0fa3f-136">在某些情况下，你具有的操作名称的两种方法。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-136">In some cases, you have two choices for the action name.</span></span> <span data-ttu-id="0fa3f-137">例如，"Get"或&quot;GetProducts&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-137">For example, "Get" or &quot;GetProducts&quot;.</span></span>

<span data-ttu-id="0fa3f-138">**查询实体**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-138">**Querying Entities**</span></span>

| <span data-ttu-id="0fa3f-139">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-139">Request</span></span> | <span data-ttu-id="0fa3f-140">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-140">Example URI</span></span> | <span data-ttu-id="0fa3f-141">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-141">Action Name</span></span> | <span data-ttu-id="0fa3f-142">示例操作</span><span class="sxs-lookup"><span data-stu-id="0fa3f-142">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fa3f-143">获取 /entityset</span><span class="sxs-lookup"><span data-stu-id="0fa3f-143">GET /entityset</span></span> | <span data-ttu-id="0fa3f-144">/ 产品</span><span class="sxs-lookup"><span data-stu-id="0fa3f-144">/Products</span></span> | <span data-ttu-id="0fa3f-145">GetEntitySet 或 Get</span><span class="sxs-lookup"><span data-stu-id="0fa3f-145">GetEntitySet or Get</span></span> | <span data-ttu-id="0fa3f-146">GetProducts</span><span class="sxs-lookup"><span data-stu-id="0fa3f-146">GetProducts</span></span> |
| <span data-ttu-id="0fa3f-147">获取 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-147">GET /entityset(key)</span></span> | <span data-ttu-id="0fa3f-148">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-148">/Products(1)</span></span> | <span data-ttu-id="0fa3f-149">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="0fa3f-149">GetEntityType or Get</span></span> | <span data-ttu-id="0fa3f-150">GetProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-150">GetProduct</span></span> |
| <span data-ttu-id="0fa3f-151">获取 /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="0fa3f-151">GET /entityset(key)/cast</span></span> | <span data-ttu-id="0fa3f-152">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="0fa3f-152">/Products(1)/Models.Book</span></span> | <span data-ttu-id="0fa3f-153">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="0fa3f-153">GetEntityType or Get</span></span> | <span data-ttu-id="0fa3f-154">GetBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-154">GetBook</span></span> |

<span data-ttu-id="0fa3f-155">有关详细信息，请参阅[创建只读 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-155">For more information, see [Create a Read-Only OData Endpoint](odata-v3/creating-an-odata-endpoint.md).</span></span>

<span data-ttu-id="0fa3f-156">**创建、 更新和删除实体**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-156">**Creating, Updating, and Deleting Entities**</span></span>

| <span data-ttu-id="0fa3f-157">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-157">Request</span></span> | <span data-ttu-id="0fa3f-158">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-158">Example URI</span></span> | <span data-ttu-id="0fa3f-159">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-159">Action Name</span></span> | <span data-ttu-id="0fa3f-160">示例操作</span><span class="sxs-lookup"><span data-stu-id="0fa3f-160">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fa3f-161">文章 /entityset</span><span class="sxs-lookup"><span data-stu-id="0fa3f-161">POST /entityset</span></span> | <span data-ttu-id="0fa3f-162">/ 产品</span><span class="sxs-lookup"><span data-stu-id="0fa3f-162">/Products</span></span> | <span data-ttu-id="0fa3f-163">PostEntityType 或 Post</span><span class="sxs-lookup"><span data-stu-id="0fa3f-163">PostEntityType or Post</span></span> | <span data-ttu-id="0fa3f-164">PostProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-164">PostProduct</span></span> |
| <span data-ttu-id="0fa3f-165">PUT /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-165">PUT /entityset(key)</span></span> | <span data-ttu-id="0fa3f-166">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-166">/Products(1)</span></span> | <span data-ttu-id="0fa3f-167">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="0fa3f-167">PutEntityType or Put</span></span> | <span data-ttu-id="0fa3f-168">PutProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-168">PutProduct</span></span> |
| <span data-ttu-id="0fa3f-169">PUT /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="0fa3f-169">PUT /entityset(key)/cast</span></span> | <span data-ttu-id="0fa3f-170">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="0fa3f-170">/Products(1)/Models.Book</span></span> | <span data-ttu-id="0fa3f-171">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="0fa3f-171">PutEntityType or Put</span></span> | <span data-ttu-id="0fa3f-172">PutBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-172">PutBook</span></span> |
| <span data-ttu-id="0fa3f-173">修补程序 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-173">PATCH /entityset(key)</span></span> | <span data-ttu-id="0fa3f-174">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-174">/Products(1)</span></span> | <span data-ttu-id="0fa3f-175">PatchEntityType 或修补程序</span><span class="sxs-lookup"><span data-stu-id="0fa3f-175">PatchEntityType or Patch</span></span> | <span data-ttu-id="0fa3f-176">PatchProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-176">PatchProduct</span></span> |
| <span data-ttu-id="0fa3f-177">修补程序 /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="0fa3f-177">PATCH /entityset(key)/cast</span></span> | <span data-ttu-id="0fa3f-178">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="0fa3f-178">/Products(1)/Models.Book</span></span> | <span data-ttu-id="0fa3f-179">PatchEntityType 或修补程序</span><span class="sxs-lookup"><span data-stu-id="0fa3f-179">PatchEntityType or Patch</span></span> | <span data-ttu-id="0fa3f-180">PatchBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-180">PatchBook</span></span> |
| <span data-ttu-id="0fa3f-181">DELETE /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-181">DELETE /entityset(key)</span></span> | <span data-ttu-id="0fa3f-182">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-182">/Products(1)</span></span> | <span data-ttu-id="0fa3f-183">DeleteEntityType 或删除</span><span class="sxs-lookup"><span data-stu-id="0fa3f-183">DeleteEntityType or Delete</span></span> | <span data-ttu-id="0fa3f-184">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-184">DeleteProduct</span></span> |
| <span data-ttu-id="0fa3f-185">DELETE /entityset(key)/cast</span><span class="sxs-lookup"><span data-stu-id="0fa3f-185">DELETE /entityset(key)/cast</span></span> | <span data-ttu-id="0fa3f-186">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="0fa3f-186">/Products(1)/Models.Book</span></span> | <span data-ttu-id="0fa3f-187">DeleteEntityType 或删除</span><span class="sxs-lookup"><span data-stu-id="0fa3f-187">DeleteEntityType or Delete</span></span> | <span data-ttu-id="0fa3f-188">DeleteBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-188">DeleteBook</span></span> |

<span data-ttu-id="0fa3f-189">**查询的导航属性**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-189">**Querying a Navigation Property**</span></span>

| <span data-ttu-id="0fa3f-190">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-190">Request</span></span> | <span data-ttu-id="0fa3f-191">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-191">Example URI</span></span> | <span data-ttu-id="0fa3f-192">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-192">Action Name</span></span> | <span data-ttu-id="0fa3f-193">示例操作</span><span class="sxs-lookup"><span data-stu-id="0fa3f-193">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fa3f-194">GET /entityset （密钥） / 导航</span><span class="sxs-lookup"><span data-stu-id="0fa3f-194">GET /entityset(key)/navigation</span></span> | <span data-ttu-id="0fa3f-195">/Products(1)/Supplier</span><span class="sxs-lookup"><span data-stu-id="0fa3f-195">/Products(1)/Supplier</span></span> | <span data-ttu-id="0fa3f-196">GetNavigationFromEntityType or GetNavigation</span><span class="sxs-lookup"><span data-stu-id="0fa3f-196">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="0fa3f-197">GetSupplierFromProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-197">GetSupplierFromProduct</span></span> |
| <span data-ttu-id="0fa3f-198">获取 /entityset （密钥）/转换/导航</span><span class="sxs-lookup"><span data-stu-id="0fa3f-198">GET /entityset(key)/cast/navigation</span></span> | <span data-ttu-id="0fa3f-199">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="0fa3f-199">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="0fa3f-200">GetNavigationFromEntityType or GetNavigation</span><span class="sxs-lookup"><span data-stu-id="0fa3f-200">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="0fa3f-201">GetAuthorFromBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-201">GetAuthorFromBook</span></span> |

<span data-ttu-id="0fa3f-202">有关详细信息，请参阅[使用实体关系](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-202">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

<span data-ttu-id="0fa3f-203">**创建和删除链接**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-203">**Creating and Deleting Links**</span></span>

| <span data-ttu-id="0fa3f-204">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-204">Request</span></span> | <span data-ttu-id="0fa3f-205">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-205">Example URI</span></span> | <span data-ttu-id="0fa3f-206">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-206">Action Name</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0fa3f-207">POST /entityset(key)/$links/navigation</span><span class="sxs-lookup"><span data-stu-id="0fa3f-207">POST /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="0fa3f-208">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="0fa3f-208">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="0fa3f-209">CreateLink</span><span class="sxs-lookup"><span data-stu-id="0fa3f-209">CreateLink</span></span> |
| <span data-ttu-id="0fa3f-210">PUT 的 /entityset （密钥） / $links/导航</span><span class="sxs-lookup"><span data-stu-id="0fa3f-210">PUT /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="0fa3f-211">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="0fa3f-211">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="0fa3f-212">CreateLink</span><span class="sxs-lookup"><span data-stu-id="0fa3f-212">CreateLink</span></span> |
| <span data-ttu-id="0fa3f-213">DELETE /entityset(key)/$links/navigation</span><span class="sxs-lookup"><span data-stu-id="0fa3f-213">DELETE /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="0fa3f-214">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="0fa3f-214">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="0fa3f-215">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="0fa3f-215">DeleteLink</span></span> |
| <span data-ttu-id="0fa3f-216">DELETE /entityset(key)/$links/navigation(relatedKey)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-216">DELETE /entityset(key)/$links/navigation(relatedKey)</span></span> | <span data-ttu-id="0fa3f-217">/Products/(1)/$links/Suppliers(1)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-217">/Products/(1)/$links/Suppliers(1)</span></span> | <span data-ttu-id="0fa3f-218">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="0fa3f-218">DeleteLink</span></span> |

<span data-ttu-id="0fa3f-219">有关详细信息，请参阅[使用实体关系](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-219">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

<span data-ttu-id="0fa3f-220">**属性**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-220">**Properties**</span></span>

<span data-ttu-id="0fa3f-221">*需要 Web API 2*</span><span class="sxs-lookup"><span data-stu-id="0fa3f-221">*Requires Web API 2*</span></span>

| <span data-ttu-id="0fa3f-222">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-222">Request</span></span> | <span data-ttu-id="0fa3f-223">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-223">Example URI</span></span> | <span data-ttu-id="0fa3f-224">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-224">Action Name</span></span> | <span data-ttu-id="0fa3f-225">示例操作</span><span class="sxs-lookup"><span data-stu-id="0fa3f-225">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fa3f-226">GET /entityset （密钥） / 属性</span><span class="sxs-lookup"><span data-stu-id="0fa3f-226">GET /entityset(key)/property</span></span> | <span data-ttu-id="0fa3f-227">/Products(1)/Name</span><span class="sxs-lookup"><span data-stu-id="0fa3f-227">/Products(1)/Name</span></span> | <span data-ttu-id="0fa3f-228">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="0fa3f-228">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="0fa3f-229">GetNameFromProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-229">GetNameFromProduct</span></span> |
| <span data-ttu-id="0fa3f-230">获取 /entityset （密钥）/转换/属性</span><span class="sxs-lookup"><span data-stu-id="0fa3f-230">GET /entityset(key)/cast/property</span></span> | <span data-ttu-id="0fa3f-231">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="0fa3f-231">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="0fa3f-232">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="0fa3f-232">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="0fa3f-233">GetTitleFromBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-233">GetTitleFromBook</span></span> |

<span data-ttu-id="0fa3f-234">**操作**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-234">**Actions**</span></span>

| <span data-ttu-id="0fa3f-235">请求</span><span class="sxs-lookup"><span data-stu-id="0fa3f-235">Request</span></span> | <span data-ttu-id="0fa3f-236">示例 URI</span><span class="sxs-lookup"><span data-stu-id="0fa3f-236">Example URI</span></span> | <span data-ttu-id="0fa3f-237">操作名称</span><span class="sxs-lookup"><span data-stu-id="0fa3f-237">Action Name</span></span> | <span data-ttu-id="0fa3f-238">示例操作</span><span class="sxs-lookup"><span data-stu-id="0fa3f-238">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fa3f-239">POST /entityset(key)/action</span><span class="sxs-lookup"><span data-stu-id="0fa3f-239">POST /entityset(key)/action</span></span> | <span data-ttu-id="0fa3f-240">/Products(1)/Rate</span><span class="sxs-lookup"><span data-stu-id="0fa3f-240">/Products(1)/Rate</span></span> | <span data-ttu-id="0fa3f-241">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="0fa3f-241">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="0fa3f-242">RateOnProduct</span><span class="sxs-lookup"><span data-stu-id="0fa3f-242">RateOnProduct</span></span> |
| <span data-ttu-id="0fa3f-243">POST /entityset(key)/cast/action</span><span class="sxs-lookup"><span data-stu-id="0fa3f-243">POST /entityset(key)/cast/action</span></span> | <span data-ttu-id="0fa3f-244">/Products(1)/Models.Book/CheckOut</span><span class="sxs-lookup"><span data-stu-id="0fa3f-244">/Products(1)/Models.Book/CheckOut</span></span> | <span data-ttu-id="0fa3f-245">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="0fa3f-245">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="0fa3f-246">CheckOutOnBook</span><span class="sxs-lookup"><span data-stu-id="0fa3f-246">CheckOutOnBook</span></span> |

<span data-ttu-id="0fa3f-247">有关详细信息，请参阅[OData 操作](odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-247">For more information, see [OData Actions](odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="0fa3f-248">**方法签名**</span><span class="sxs-lookup"><span data-stu-id="0fa3f-248">**Method Signatures**</span></span>

<span data-ttu-id="0fa3f-249">下面是方法签名的一些规则：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-249">Here are some rules for the method signatures:</span></span>

- <span data-ttu-id="0fa3f-250">如果路径包含一个密钥，该操作应具有一个名为参数*密钥*。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-250">If the path contains a key, the action should have a parameter named *key*.</span></span>
- <span data-ttu-id="0fa3f-251">如果路径包含转换的导航属性的密钥，该操作应具有一个名为参数*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-251">If the path contains a key into a navigation property, the action should have a parameter named *relatedKey*.</span></span>
- <span data-ttu-id="0fa3f-252">修饰*密钥*和*relatedKey*参数**[FromODataUri]**参数。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-252">Decorate *key* and *relatedKey* parameters with the **[FromODataUri]** parameter.</span></span>
- <span data-ttu-id="0fa3f-253">POST 和 PUT 请求需要实体类型的参数。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-253">POST and PUT requests take a parameter of the entity type.</span></span>
- <span data-ttu-id="0fa3f-254">PATCH 请求需要类型的参数**增量&lt;T&gt;**，其中*T*是实体类型。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-254">PATCH requests take a parameter of type **Delta&lt;T&gt;**, where *T* is the entity type.</span></span>

<span data-ttu-id="0fa3f-255">作为参考，此处是显示每个内置的 OData 路由约定的方法签名的示例。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-255">For reference, here is an example that shows method signatures for every built-in OData routing convention.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a><span data-ttu-id="0fa3f-256">自定义路由约定</span><span class="sxs-lookup"><span data-stu-id="0fa3f-256">Custom Routing Conventions</span></span>

<span data-ttu-id="0fa3f-257">当前的内置约定并未涵盖所有可能的 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-257">Currently the built-in conventions do not cover all possible OData URIs.</span></span> <span data-ttu-id="0fa3f-258">你可以通过实现来添加新约定**IODataRoutingConvention**接口。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-258">You can add new conventions by implementing the **IODataRoutingConvention** interface.</span></span> <span data-ttu-id="0fa3f-259">此接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-259">This interface has two methods:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- <span data-ttu-id="0fa3f-260">**SelectController**返回控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-260">**SelectController** returns the name of the controller.</span></span>
- <span data-ttu-id="0fa3f-261">**SelectAction**返回操作的名称。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-261">**SelectAction** returns the name of the action.</span></span>

<span data-ttu-id="0fa3f-262">对于这两种方法，如果约定不适用于该请求，该方法应返回 null。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-262">For both methods, if the convention does not apply to that request, the method should return null.</span></span>

<span data-ttu-id="0fa3f-263">**ODataPath**参数表示的已分析的 OData 资源路径。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-263">The **ODataPath** parameter represents the parsed OData resource path.</span></span> <span data-ttu-id="0fa3f-264">它包含的列表 **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 实例，每个段的资源路径的一个。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-264">It contains a list of **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** instances, one for each segment of the resource path.</span></span> <span data-ttu-id="0fa3f-265">**ODataPathSegment**是一个抽象类; 每个段类型由派生自的类**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-265">**ODataPathSegment** is an abstract class; each segment type is represented by a class that derives from **ODataPathSegment**.</span></span>

<span data-ttu-id="0fa3f-266">**ODataPath.TemplatePath**属性是一个字符串，表示串联所有的路径段。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-266">The **ODataPath.TemplatePath** property is a string that represents the concatenation all of the path segments.</span></span> <span data-ttu-id="0fa3f-267">例如，如果的 URI 是`/Products(1)/Supplier`，路径模板是&quot;~/entityset/key/navigation&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-267">For example, if the URI is `/Products(1)/Supplier`, the path template is &quot;~/entityset/key/navigation&quot;.</span></span> <span data-ttu-id="0fa3f-268">请注意，段不直接对应 URI 段。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-268">Notice that the segments don't correspond directly to URI segments.</span></span> <span data-ttu-id="0fa3f-269">例如，实体键 (1) 表示为其自身**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-269">For example, the entity key (1) is represented as its own **ODataPathSegment**.</span></span>

<span data-ttu-id="0fa3f-270">通常，实现**IODataRoutingConvention**执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-270">Typically, an implementation of **IODataRoutingConvention** does the following:</span></span>

1. <span data-ttu-id="0fa3f-271">比较路径模板以查看是否此约定适用于当前的请求。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-271">Compare the path template to see if this convention applies to the current request.</span></span> <span data-ttu-id="0fa3f-272">如果不适用，返回 null。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-272">If it does not apply, return null.</span></span>
2. <span data-ttu-id="0fa3f-273">如果要将约定应用，使用属性**ODataPathSegment**控制器和操作名称派生的实例。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-273">If the convention applies, use properties of the **ODataPathSegment** instances to derive controller and action names.</span></span>
3. <span data-ttu-id="0fa3f-274">对于操作，将添加到路由字典，其中应绑定到操作参数 （通常实体键） 的任何值。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-274">For actions, add any values to the route dictionary that should bind to the action parameters (typically entity keys).</span></span>

<span data-ttu-id="0fa3f-275">我们来看具体示例的信息。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-275">Let's look at a specific example.</span></span> <span data-ttu-id="0fa3f-276">内置路由约定不支持导航集合索引。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-276">The built-in routing conventions do not support indexing into a navigation collection.</span></span> <span data-ttu-id="0fa3f-277">换而言之，没有 uri 约定如下所示：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-277">In other words, there is no convention for URIs like the following:</span></span>

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

<span data-ttu-id="0fa3f-278">下面是查询的自定义的路由约定来处理这种类型。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-278">Here is a custom routing convention to handle this type of query.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

<span data-ttu-id="0fa3f-279">注意：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-279">Notes:</span></span>

1. <span data-ttu-id="0fa3f-280">我派生自**EntitySetRoutingConvention**，这是因为**SelectController**在该类的方法适合于此新的路由约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-280">I derive from **EntitySetRoutingConvention**, because the **SelectController** method in that class is appropriate for this new routing convention.</span></span> <span data-ttu-id="0fa3f-281">这意味着我不需要重新实现**SelectController**。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-281">That means I don't need to re-implement **SelectController**.</span></span>
2. <span data-ttu-id="0fa3f-282">约定适用仅对 GET 请求中，并且仅当路径模板时&quot;~/entityset/key/navigation/key&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-282">The convention applies only to GET requests, and only when the path template is &quot;~/entityset/key/navigation/key&quot;.</span></span>
3. <span data-ttu-id="0fa3f-283">操作名称是&quot;获取 {EntityType}&quot;，其中*{EntityType}*是导航集合的类型。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-283">The action name is &quot;Get{EntityType}&quot;, where *{EntityType}* is the type of the navigation collection.</span></span> <span data-ttu-id="0fa3f-284">例如， &quot;GetSupplier&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-284">For example, &quot;GetSupplier&quot;.</span></span> <span data-ttu-id="0fa3f-285">您可以使用任何您喜欢的命名约定和 #8212;只需确保你与匹配的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-285">You can use any naming convention that you like &#8212; just make sure your controller actions match.</span></span>
4. <span data-ttu-id="0fa3f-286">将名为的两个参数的操作*密钥*和*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-286">The action takes two parameters named *key* and *relatedKey*.</span></span> <span data-ttu-id="0fa3f-287">(有关某些预定义的参数名称的列表，请参阅[ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="0fa3f-287">(For a list of some predefined parameter names, see [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)</span></span>

<span data-ttu-id="0fa3f-288">下一步向路由约定的列表添加新的约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-288">The next step is adding the new convention to the list of routing conventions.</span></span> <span data-ttu-id="0fa3f-289">发生这种情况在配置期间，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-289">This happens during configuration, as shown in the following code:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

<span data-ttu-id="0fa3f-290">下面是一些其他示例路由约定的有用来研究：</span><span class="sxs-lookup"><span data-stu-id="0fa3f-290">Here are some other sample routing conventions that be useful to study:</span></span>

- [<span data-ttu-id="0fa3f-291">CompositeKeyRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="0fa3f-291">CompositeKeyRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [<span data-ttu-id="0fa3f-292">CustomNavigationRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="0fa3f-292">CustomNavigationRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [<span data-ttu-id="0fa3f-293">NonBindableActionRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="0fa3f-293">NonBindableActionRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [<span data-ttu-id="0fa3f-294">ODataVersionRouteConstraint</span><span class="sxs-lookup"><span data-stu-id="0fa3f-294">ODataVersionRouteConstraint</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

<span data-ttu-id="0fa3f-295">当然 Web API 本身是开放源代码，以便你可以查看[源代码](http://aspnetwebstack.codeplex.com/)的内置路由约定。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-295">And of course Web API itself is open-source, so you can see the [source code](http://aspnetwebstack.codeplex.com/) for the built-in routing conventions.</span></span> <span data-ttu-id="0fa3f-296">这些定义在**System.Web.Http.OData.Routing.Conventions**命名空间。</span><span class="sxs-lookup"><span data-stu-id="0fa3f-296">These are defined in the **System.Web.Http.OData.Routing.Conventions** namespace.</span></span>
