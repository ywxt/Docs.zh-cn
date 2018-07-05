---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 中的路由约定 Odata |Microsoft Docs
author: MikeWasson
description: 本文介绍 Web API 使用的 OData 终结点的路由约定。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/31/2013
ms.topic: article
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63a0e4f4f61580ea9da3bd491e7a45f20cd7aaae
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370534"
---
<a name="routing-conventions-in-aspnet-web-api-2-odata"></a><span data-ttu-id="2bed0-103">ASP.NET Web API 2 中的路由约定 Odata</span><span class="sxs-lookup"><span data-stu-id="2bed0-103">Routing Conventions in ASP.NET Web API 2 Odata</span></span>
====================
<span data-ttu-id="2bed0-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2bed0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="2bed0-105">本文介绍 Web API 使用的 OData 终结点的路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-105">This article describes the routing conventions that Web API uses for OData endpoints.</span></span>


<span data-ttu-id="2bed0-106">当 Web API 获取 OData 请求时，但它会将请求映射到控制器名称和操作名称。</span><span class="sxs-lookup"><span data-stu-id="2bed0-106">When Web API gets an OData request, it maps the request to a controller name and an action name.</span></span> <span data-ttu-id="2bed0-107">映射为基础的 HTTP 方法和 URI。</span><span class="sxs-lookup"><span data-stu-id="2bed0-107">The mapping is based on the HTTP method and the URI.</span></span> <span data-ttu-id="2bed0-108">例如，`GET /odata/Products(1)`映射到`ProductsController.GetProduct`。</span><span class="sxs-lookup"><span data-stu-id="2bed0-108">For example, `GET /odata/Products(1)` maps to `ProductsController.GetProduct`.</span></span>

<span data-ttu-id="2bed0-109">在这篇文章的第 1 部分中，我将介绍内置的 OData 路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-109">In part 1 of this article, I describe the built-in OData routing conventions.</span></span> <span data-ttu-id="2bed0-110">这些约定专为 OData 终结点，并且它们替换默认 Web API 路由系统。</span><span class="sxs-lookup"><span data-stu-id="2bed0-110">These conventions are designed specifically for OData endpoints, and they replace the default Web API routing system.</span></span> <span data-ttu-id="2bed0-111">(在调用时，会发生情况替换**MapODataRoute**。)</span><span class="sxs-lookup"><span data-stu-id="2bed0-111">(The replacement happens when you call **MapODataRoute**.)</span></span>

<span data-ttu-id="2bed0-112">在第 2 部分，我将介绍如何添加自定义的路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-112">In part 2, I show how to add custom routing conventions.</span></span> <span data-ttu-id="2bed0-113">当前的内置约定不涵盖整个范围的 OData Uri，但你可以扩展它们来处理其他情况。</span><span class="sxs-lookup"><span data-stu-id="2bed0-113">Currently the built-in conventions do not cover the entire range of OData URIs, but you can extend them to handle additional cases.</span></span>

- [<span data-ttu-id="2bed0-114">内置路由约定</span><span class="sxs-lookup"><span data-stu-id="2bed0-114">Built-in Routing Conventions</span></span>](#conventions)
- [<span data-ttu-id="2bed0-115">自定义的路由约定</span><span class="sxs-lookup"><span data-stu-id="2bed0-115">Custom Routing Conventions</span></span>](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a><span data-ttu-id="2bed0-116">内置路由约定</span><span class="sxs-lookup"><span data-stu-id="2bed0-116">Built-in Routing Conventions</span></span>

<span data-ttu-id="2bed0-117">我将介绍 Web API 中的 OData 路由约定之前，它是有助于您了解 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="2bed0-117">Before I describe the OData routing conventions in Web API, it's helpful to understand OData URIs.</span></span> <span data-ttu-id="2bed0-118">[OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)组成：</span><span class="sxs-lookup"><span data-stu-id="2bed0-118">An [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) consists of:</span></span>

- <span data-ttu-id="2bed0-119">服务根</span><span class="sxs-lookup"><span data-stu-id="2bed0-119">The service root</span></span>
- <span data-ttu-id="2bed0-120">资源路径</span><span class="sxs-lookup"><span data-stu-id="2bed0-120">The resource path</span></span>
- <span data-ttu-id="2bed0-121">查询选项</span><span class="sxs-lookup"><span data-stu-id="2bed0-121">Query options</span></span>

![](odata-routing-conventions/_static/image1.png)

<span data-ttu-id="2bed0-122">对于路由，重要的部分是资源路径。</span><span class="sxs-lookup"><span data-stu-id="2bed0-122">For routing, the important part is the resource path.</span></span> <span data-ttu-id="2bed0-123">资源路径分为段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-123">The resource path is divided into segments.</span></span> <span data-ttu-id="2bed0-124">例如，`/Products(1)/Supplier`有三个段：</span><span class="sxs-lookup"><span data-stu-id="2bed0-124">For example, `/Products(1)/Supplier` has three segments:</span></span>

- <span data-ttu-id="2bed0-125">`Products` 引用名为"产品"实体集。</span><span class="sxs-lookup"><span data-stu-id="2bed0-125">`Products` refers to an entity set named "Products".</span></span>
- <span data-ttu-id="2bed0-126">`1` 是否为实体键，从组中选择单个实体。</span><span class="sxs-lookup"><span data-stu-id="2bed0-126">`1` is an entity key, selecting a single entity from the set.</span></span>
- <span data-ttu-id="2bed0-127">`Supplier` 是一个导航属性，选择相关的实体。</span><span class="sxs-lookup"><span data-stu-id="2bed0-127">`Supplier` is a navigation property that selects a related entity.</span></span>

<span data-ttu-id="2bed0-128">因此此路径提取产品 1 的供应商。</span><span class="sxs-lookup"><span data-stu-id="2bed0-128">So this path picks out the supplier of product 1.</span></span>

> [!NOTE]
> <span data-ttu-id="2bed0-129">OData 路径段不始终对应于 URI 段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-129">OData path segments do not always correspond to URI segments.</span></span> <span data-ttu-id="2bed0-130">例如，"1"被视为一个路径段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-130">For example, "1" is considered a path segment.</span></span>


<span data-ttu-id="2bed0-131">**控制器名称。**</span><span class="sxs-lookup"><span data-stu-id="2bed0-131">**Controller Names.**</span></span> <span data-ttu-id="2bed0-132">控制器名称始终被派生自的实体集的资源路径根目录。</span><span class="sxs-lookup"><span data-stu-id="2bed0-132">The controller name is always derived from the entity set at the root of the resource path.</span></span> <span data-ttu-id="2bed0-133">例如，如果资源路径是`/Products(1)/Supplier`，Web API 将查找名为的控制器`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="2bed0-133">For example, if the resource path is `/Products(1)/Supplier`, Web API looks for a controller named `ProductsController`.</span></span>

<span data-ttu-id="2bed0-134">**操作名称。**</span><span class="sxs-lookup"><span data-stu-id="2bed0-134">**Action Names.**</span></span> <span data-ttu-id="2bed0-135">操作名称派生自的路径段以及实体数据模型 (EDM) 中，为以下表格中列出。</span><span class="sxs-lookup"><span data-stu-id="2bed0-135">Action names are derived from the path segments plus the entity data model (EDM), as listed in the following tables.</span></span> <span data-ttu-id="2bed0-136">在某些情况下，有两个选择的操作名称。</span><span class="sxs-lookup"><span data-stu-id="2bed0-136">In some cases, you have two choices for the action name.</span></span> <span data-ttu-id="2bed0-137">例如，"Get"或&quot;GetProducts&quot;。</span><span class="sxs-lookup"><span data-stu-id="2bed0-137">For example, "Get" or &quot;GetProducts&quot;.</span></span>

<span data-ttu-id="2bed0-138">**查询实体**</span><span class="sxs-lookup"><span data-stu-id="2bed0-138">**Querying Entities**</span></span>

| <span data-ttu-id="2bed0-139">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-139">Request</span></span> | <span data-ttu-id="2bed0-140">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-140">Example URI</span></span> | <span data-ttu-id="2bed0-141">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-141">Action Name</span></span> | <span data-ttu-id="2bed0-142">示例操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-142">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2bed0-143">获取 /entityset</span><span class="sxs-lookup"><span data-stu-id="2bed0-143">GET /entityset</span></span> | <span data-ttu-id="2bed0-144">/ 产品</span><span class="sxs-lookup"><span data-stu-id="2bed0-144">/Products</span></span> | <span data-ttu-id="2bed0-145">GetEntitySet 或 Get</span><span class="sxs-lookup"><span data-stu-id="2bed0-145">GetEntitySet or Get</span></span> | <span data-ttu-id="2bed0-146">GetProducts</span><span class="sxs-lookup"><span data-stu-id="2bed0-146">GetProducts</span></span> |
| <span data-ttu-id="2bed0-147">获取 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="2bed0-147">GET /entityset(key)</span></span> | <span data-ttu-id="2bed0-148">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="2bed0-148">/Products(1)</span></span> | <span data-ttu-id="2bed0-149">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="2bed0-149">GetEntityType or Get</span></span> | <span data-ttu-id="2bed0-150">为 getproduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-150">GetProduct</span></span> |
| <span data-ttu-id="2bed0-151">获取 /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="2bed0-151">GET /entityset(key)/cast</span></span> | <span data-ttu-id="2bed0-152">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="2bed0-152">/Products(1)/Models.Book</span></span> | <span data-ttu-id="2bed0-153">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="2bed0-153">GetEntityType or Get</span></span> | <span data-ttu-id="2bed0-154">GetBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-154">GetBook</span></span> |

<span data-ttu-id="2bed0-155">有关详细信息，请参阅[创建只读 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="2bed0-155">For more information, see [Create a Read-Only OData Endpoint](odata-v3/creating-an-odata-endpoint.md).</span></span>

<span data-ttu-id="2bed0-156">**创建、 更新和删除实体**</span><span class="sxs-lookup"><span data-stu-id="2bed0-156">**Creating, Updating, and Deleting Entities**</span></span>

| <span data-ttu-id="2bed0-157">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-157">Request</span></span> | <span data-ttu-id="2bed0-158">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-158">Example URI</span></span> | <span data-ttu-id="2bed0-159">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-159">Action Name</span></span> | <span data-ttu-id="2bed0-160">示例操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-160">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2bed0-161">发布 /entityset</span><span class="sxs-lookup"><span data-stu-id="2bed0-161">POST /entityset</span></span> | <span data-ttu-id="2bed0-162">/ 产品</span><span class="sxs-lookup"><span data-stu-id="2bed0-162">/Products</span></span> | <span data-ttu-id="2bed0-163">PostEntityType 或 Post</span><span class="sxs-lookup"><span data-stu-id="2bed0-163">PostEntityType or Post</span></span> | <span data-ttu-id="2bed0-164">PostProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-164">PostProduct</span></span> |
| <span data-ttu-id="2bed0-165">放置 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="2bed0-165">PUT /entityset(key)</span></span> | <span data-ttu-id="2bed0-166">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="2bed0-166">/Products(1)</span></span> | <span data-ttu-id="2bed0-167">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="2bed0-167">PutEntityType or Put</span></span> | <span data-ttu-id="2bed0-168">PutProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-168">PutProduct</span></span> |
| <span data-ttu-id="2bed0-169">PUT /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="2bed0-169">PUT /entityset(key)/cast</span></span> | <span data-ttu-id="2bed0-170">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="2bed0-170">/Products(1)/Models.Book</span></span> | <span data-ttu-id="2bed0-171">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="2bed0-171">PutEntityType or Put</span></span> | <span data-ttu-id="2bed0-172">PutBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-172">PutBook</span></span> |
| <span data-ttu-id="2bed0-173">修补程序 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="2bed0-173">PATCH /entityset(key)</span></span> | <span data-ttu-id="2bed0-174">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="2bed0-174">/Products(1)</span></span> | <span data-ttu-id="2bed0-175">PatchEntityType 或修补程序</span><span class="sxs-lookup"><span data-stu-id="2bed0-175">PatchEntityType or Patch</span></span> | <span data-ttu-id="2bed0-176">PatchProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-176">PatchProduct</span></span> |
| <span data-ttu-id="2bed0-177">修补程序 /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="2bed0-177">PATCH /entityset(key)/cast</span></span> | <span data-ttu-id="2bed0-178">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="2bed0-178">/Products(1)/Models.Book</span></span> | <span data-ttu-id="2bed0-179">PatchEntityType 或修补程序</span><span class="sxs-lookup"><span data-stu-id="2bed0-179">PatchEntityType or Patch</span></span> | <span data-ttu-id="2bed0-180">PatchBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-180">PatchBook</span></span> |
| <span data-ttu-id="2bed0-181">删除 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="2bed0-181">DELETE /entityset(key)</span></span> | <span data-ttu-id="2bed0-182">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="2bed0-182">/Products(1)</span></span> | <span data-ttu-id="2bed0-183">DeleteEntityType 或 Delete</span><span class="sxs-lookup"><span data-stu-id="2bed0-183">DeleteEntityType or Delete</span></span> | <span data-ttu-id="2bed0-184">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-184">DeleteProduct</span></span> |
| <span data-ttu-id="2bed0-185">删除 /entityset （密钥）/强制转换</span><span class="sxs-lookup"><span data-stu-id="2bed0-185">DELETE /entityset(key)/cast</span></span> | <span data-ttu-id="2bed0-186">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="2bed0-186">/Products(1)/Models.Book</span></span> | <span data-ttu-id="2bed0-187">DeleteEntityType 或 Delete</span><span class="sxs-lookup"><span data-stu-id="2bed0-187">DeleteEntityType or Delete</span></span> | <span data-ttu-id="2bed0-188">DeleteBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-188">DeleteBook</span></span> |

<span data-ttu-id="2bed0-189">**查询的导航属性**</span><span class="sxs-lookup"><span data-stu-id="2bed0-189">**Querying a Navigation Property**</span></span>

| <span data-ttu-id="2bed0-190">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-190">Request</span></span> | <span data-ttu-id="2bed0-191">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-191">Example URI</span></span> | <span data-ttu-id="2bed0-192">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-192">Action Name</span></span> | <span data-ttu-id="2bed0-193">示例操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-193">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2bed0-194">GET /entityset （密钥） / 导航</span><span class="sxs-lookup"><span data-stu-id="2bed0-194">GET /entityset(key)/navigation</span></span> | <span data-ttu-id="2bed0-195">/ 产品 （1）/供应商</span><span class="sxs-lookup"><span data-stu-id="2bed0-195">/Products(1)/Supplier</span></span> | <span data-ttu-id="2bed0-196">GetNavigationFromEntityType 或 GetNavigation</span><span class="sxs-lookup"><span data-stu-id="2bed0-196">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="2bed0-197">GetSupplierFromProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-197">GetSupplierFromProduct</span></span> |
| <span data-ttu-id="2bed0-198">获取 /entityset （密钥）/转换/导航</span><span class="sxs-lookup"><span data-stu-id="2bed0-198">GET /entityset(key)/cast/navigation</span></span> | <span data-ttu-id="2bed0-199">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="2bed0-199">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="2bed0-200">GetNavigationFromEntityType 或 GetNavigation</span><span class="sxs-lookup"><span data-stu-id="2bed0-200">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="2bed0-201">GetAuthorFromBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-201">GetAuthorFromBook</span></span> |

<span data-ttu-id="2bed0-202">有关详细信息，请参阅[使用的实体关系](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="2bed0-202">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

<span data-ttu-id="2bed0-203">**创建和删除链接**</span><span class="sxs-lookup"><span data-stu-id="2bed0-203">**Creating and Deleting Links**</span></span>

| <span data-ttu-id="2bed0-204">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-204">Request</span></span> | <span data-ttu-id="2bed0-205">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-205">Example URI</span></span> | <span data-ttu-id="2bed0-206">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-206">Action Name</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2bed0-207">开机自检 /entityset （密钥） / $links/导航</span><span class="sxs-lookup"><span data-stu-id="2bed0-207">POST /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="2bed0-208">/ 产品 （1） / $ 链接/供应商</span><span class="sxs-lookup"><span data-stu-id="2bed0-208">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="2bed0-209">CreateLink</span><span class="sxs-lookup"><span data-stu-id="2bed0-209">CreateLink</span></span> |
| <span data-ttu-id="2bed0-210">PUT 的 /entityset （密钥） / $links/导航</span><span class="sxs-lookup"><span data-stu-id="2bed0-210">PUT /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="2bed0-211">/ 产品 （1） / $ 链接/供应商</span><span class="sxs-lookup"><span data-stu-id="2bed0-211">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="2bed0-212">CreateLink</span><span class="sxs-lookup"><span data-stu-id="2bed0-212">CreateLink</span></span> |
| <span data-ttu-id="2bed0-213">删除 /entityset （密钥） / $links/导航</span><span class="sxs-lookup"><span data-stu-id="2bed0-213">DELETE /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="2bed0-214">/ 产品 （1） / $ 链接/供应商</span><span class="sxs-lookup"><span data-stu-id="2bed0-214">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="2bed0-215">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="2bed0-215">DeleteLink</span></span> |
| <span data-ttu-id="2bed0-216">删除 /entityset(key)/$links/navigation(relatedKey)</span><span class="sxs-lookup"><span data-stu-id="2bed0-216">DELETE /entityset(key)/$links/navigation(relatedKey)</span></span> | <span data-ttu-id="2bed0-217">/Products/(1)/$links/Suppliers(1)</span><span class="sxs-lookup"><span data-stu-id="2bed0-217">/Products/(1)/$links/Suppliers(1)</span></span> | <span data-ttu-id="2bed0-218">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="2bed0-218">DeleteLink</span></span> |

<span data-ttu-id="2bed0-219">有关详细信息，请参阅[使用的实体关系](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="2bed0-219">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

<span data-ttu-id="2bed0-220">**属性**</span><span class="sxs-lookup"><span data-stu-id="2bed0-220">**Properties**</span></span>

<span data-ttu-id="2bed0-221">*需要 Web API 2*</span><span class="sxs-lookup"><span data-stu-id="2bed0-221">*Requires Web API 2*</span></span>

| <span data-ttu-id="2bed0-222">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-222">Request</span></span> | <span data-ttu-id="2bed0-223">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-223">Example URI</span></span> | <span data-ttu-id="2bed0-224">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-224">Action Name</span></span> | <span data-ttu-id="2bed0-225">示例操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-225">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2bed0-226">GET /entityset （密钥） / 属性</span><span class="sxs-lookup"><span data-stu-id="2bed0-226">GET /entityset(key)/property</span></span> | <span data-ttu-id="2bed0-227">/Products(1)/Name</span><span class="sxs-lookup"><span data-stu-id="2bed0-227">/Products(1)/Name</span></span> | <span data-ttu-id="2bed0-228">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="2bed0-228">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="2bed0-229">GetNameFromProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-229">GetNameFromProduct</span></span> |
| <span data-ttu-id="2bed0-230">获取 /entityset （密钥）/转换/属性</span><span class="sxs-lookup"><span data-stu-id="2bed0-230">GET /entityset(key)/cast/property</span></span> | <span data-ttu-id="2bed0-231">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="2bed0-231">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="2bed0-232">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="2bed0-232">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="2bed0-233">GetTitleFromBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-233">GetTitleFromBook</span></span> |

<span data-ttu-id="2bed0-234">**操作**</span><span class="sxs-lookup"><span data-stu-id="2bed0-234">**Actions**</span></span>

| <span data-ttu-id="2bed0-235">请求</span><span class="sxs-lookup"><span data-stu-id="2bed0-235">Request</span></span> | <span data-ttu-id="2bed0-236">示例 URI</span><span class="sxs-lookup"><span data-stu-id="2bed0-236">Example URI</span></span> | <span data-ttu-id="2bed0-237">操作名称</span><span class="sxs-lookup"><span data-stu-id="2bed0-237">Action Name</span></span> | <span data-ttu-id="2bed0-238">示例操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-238">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2bed0-239">开机自检 /entityset （密钥） / 操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-239">POST /entityset(key)/action</span></span> | <span data-ttu-id="2bed0-240">/ 产品 （1）/速率</span><span class="sxs-lookup"><span data-stu-id="2bed0-240">/Products(1)/Rate</span></span> | <span data-ttu-id="2bed0-241">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="2bed0-241">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="2bed0-242">RateOnProduct</span><span class="sxs-lookup"><span data-stu-id="2bed0-242">RateOnProduct</span></span> |
| <span data-ttu-id="2bed0-243">后 /entityset （密钥）/转换/操作</span><span class="sxs-lookup"><span data-stu-id="2bed0-243">POST /entityset(key)/cast/action</span></span> | <span data-ttu-id="2bed0-244">/Products(1)/Models.Book/CheckOut</span><span class="sxs-lookup"><span data-stu-id="2bed0-244">/Products(1)/Models.Book/CheckOut</span></span> | <span data-ttu-id="2bed0-245">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="2bed0-245">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="2bed0-246">CheckOutOnBook</span><span class="sxs-lookup"><span data-stu-id="2bed0-246">CheckOutOnBook</span></span> |

<span data-ttu-id="2bed0-247">有关详细信息，请参阅[OData 操作](odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="2bed0-247">For more information, see [OData Actions](odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="2bed0-248">**方法签名**</span><span class="sxs-lookup"><span data-stu-id="2bed0-248">**Method Signatures**</span></span>

<span data-ttu-id="2bed0-249">下面是一些规则的方法签名：</span><span class="sxs-lookup"><span data-stu-id="2bed0-249">Here are some rules for the method signatures:</span></span>

- <span data-ttu-id="2bed0-250">如果路径包含一个键，操作应具有一个名为参数*密钥*。</span><span class="sxs-lookup"><span data-stu-id="2bed0-250">If the path contains a key, the action should have a parameter named *key*.</span></span>
- <span data-ttu-id="2bed0-251">如果路径包含一个键到导航属性，该操作应具有名为的参数*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="2bed0-251">If the path contains a key into a navigation property, the action should have a parameter named *relatedKey*.</span></span>
- <span data-ttu-id="2bed0-252">修饰*键*并*relatedKey*使用的参数 **[FromODataUri]** 参数。</span><span class="sxs-lookup"><span data-stu-id="2bed0-252">Decorate *key* and *relatedKey* parameters with the **[FromODataUri]** parameter.</span></span>
- <span data-ttu-id="2bed0-253">POST 和 PUT 请求需要实体类型的参数。</span><span class="sxs-lookup"><span data-stu-id="2bed0-253">POST and PUT requests take a parameter of the entity type.</span></span>
- <span data-ttu-id="2bed0-254">PATCH 请求采用的类型参数**增量&lt;T&gt;**，其中*T*是实体类型。</span><span class="sxs-lookup"><span data-stu-id="2bed0-254">PATCH requests take a parameter of type **Delta&lt;T&gt;**, where *T* is the entity type.</span></span>

<span data-ttu-id="2bed0-255">有关参考，下面是一个示例，说明每个内置的 OData 路由约定的方法签名。</span><span class="sxs-lookup"><span data-stu-id="2bed0-255">For reference, here is an example that shows method signatures for every built-in OData routing convention.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a><span data-ttu-id="2bed0-256">自定义的路由约定</span><span class="sxs-lookup"><span data-stu-id="2bed0-256">Custom Routing Conventions</span></span>

<span data-ttu-id="2bed0-257">当前的内置约定不涵盖所有可能的 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="2bed0-257">Currently the built-in conventions do not cover all possible OData URIs.</span></span> <span data-ttu-id="2bed0-258">可以通过实现来添加新的惯例**IODataRoutingConvention**接口。</span><span class="sxs-lookup"><span data-stu-id="2bed0-258">You can add new conventions by implementing the **IODataRoutingConvention** interface.</span></span> <span data-ttu-id="2bed0-259">此接口有两个方法：</span><span class="sxs-lookup"><span data-stu-id="2bed0-259">This interface has two methods:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- <span data-ttu-id="2bed0-260">**SelectController**返回控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="2bed0-260">**SelectController** returns the name of the controller.</span></span>
- <span data-ttu-id="2bed0-261">**SelectAction**返回操作的名称。</span><span class="sxs-lookup"><span data-stu-id="2bed0-261">**SelectAction** returns the name of the action.</span></span>

<span data-ttu-id="2bed0-262">对于这两种方法，如果约定不适用于该请求，该方法应返回 null。</span><span class="sxs-lookup"><span data-stu-id="2bed0-262">For both methods, if the convention does not apply to that request, the method should return null.</span></span>

<span data-ttu-id="2bed0-263">**ODataPath**参数表示已分析的 OData 资源路径。</span><span class="sxs-lookup"><span data-stu-id="2bed0-263">The **ODataPath** parameter represents the parsed OData resource path.</span></span> <span data-ttu-id="2bed0-264">它包含一系列**[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 实例，一个用于资源路径的每个段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-264">It contains a list of **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** instances, one for each segment of the resource path.</span></span> <span data-ttu-id="2bed0-265">**ODataPathSegment**是一个抽象类; 每个段类型由派生的类**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="2bed0-265">**ODataPathSegment** is an abstract class; each segment type is represented by a class that derives from **ODataPathSegment**.</span></span>

<span data-ttu-id="2bed0-266">**ODataPath.TemplatePath**属性是一个字符串，表示串联所有路径段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-266">The **ODataPath.TemplatePath** property is a string that represents the concatenation all of the path segments.</span></span> <span data-ttu-id="2bed0-267">例如，如果 URI 是`/Products(1)/Supplier`，路径模板&quot;~/entityset/key/navigation&quot;。</span><span class="sxs-lookup"><span data-stu-id="2bed0-267">For example, if the URI is `/Products(1)/Supplier`, the path template is &quot;~/entityset/key/navigation&quot;.</span></span> <span data-ttu-id="2bed0-268">请注意，段不直接对应于 URI 段。</span><span class="sxs-lookup"><span data-stu-id="2bed0-268">Notice that the segments don't correspond directly to URI segments.</span></span> <span data-ttu-id="2bed0-269">例如，实体键 (1) 表示为其自身**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="2bed0-269">For example, the entity key (1) is represented as its own **ODataPathSegment**.</span></span>

<span data-ttu-id="2bed0-270">通常情况下，实现**IODataRoutingConvention**执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2bed0-270">Typically, an implementation of **IODataRoutingConvention** does the following:</span></span>

1. <span data-ttu-id="2bed0-271">进行比较以查看此约定应用于当前请求的路径模板。</span><span class="sxs-lookup"><span data-stu-id="2bed0-271">Compare the path template to see if this convention applies to the current request.</span></span> <span data-ttu-id="2bed0-272">如果不适用，则返回 null。</span><span class="sxs-lookup"><span data-stu-id="2bed0-272">If it does not apply, return null.</span></span>
2. <span data-ttu-id="2bed0-273">如果约定适用，则使用的属性**ODataPathSegment**控制器和操作名称派生的实例。</span><span class="sxs-lookup"><span data-stu-id="2bed0-273">If the convention applies, use properties of the **ODataPathSegment** instances to derive controller and action names.</span></span>
3. <span data-ttu-id="2bed0-274">对于操作，将添加到路由字典应绑定到操作参数 （通常是实体键） 的任何值。</span><span class="sxs-lookup"><span data-stu-id="2bed0-274">For actions, add any values to the route dictionary that should bind to the action parameters (typically entity keys).</span></span>

<span data-ttu-id="2bed0-275">让我们看一下具体的示例。</span><span class="sxs-lookup"><span data-stu-id="2bed0-275">Let's look at a specific example.</span></span> <span data-ttu-id="2bed0-276">导航集合中建立索引不支持的内置路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-276">The built-in routing conventions do not support indexing into a navigation collection.</span></span> <span data-ttu-id="2bed0-277">换而言之，没有任何 Uri 约定如下所示：</span><span class="sxs-lookup"><span data-stu-id="2bed0-277">In other words, there is no convention for URIs like the following:</span></span>

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

<span data-ttu-id="2bed0-278">下面是查询的自定义的路由约定来处理此类型。</span><span class="sxs-lookup"><span data-stu-id="2bed0-278">Here is a custom routing convention to handle this type of query.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

<span data-ttu-id="2bed0-279">注意：</span><span class="sxs-lookup"><span data-stu-id="2bed0-279">Notes:</span></span>

1. <span data-ttu-id="2bed0-280">我从派生出**EntitySetRoutingConvention**，因为**SelectController**在该类中的方法适合于此新的路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-280">I derive from **EntitySetRoutingConvention**, because the **SelectController** method in that class is appropriate for this new routing convention.</span></span> <span data-ttu-id="2bed0-281">这意味着我无需重新实现**SelectController**。</span><span class="sxs-lookup"><span data-stu-id="2bed0-281">That means I don't need to re-implement **SelectController**.</span></span>
2. <span data-ttu-id="2bed0-282">约定仅适用于 GET 请求和路径模板时才&quot;~/entityset/key/navigation/key&quot;。</span><span class="sxs-lookup"><span data-stu-id="2bed0-282">The convention applies only to GET requests, and only when the path template is &quot;~/entityset/key/navigation/key&quot;.</span></span>
3. <span data-ttu-id="2bed0-283">操作名称是&quot;获取 {EntityType}&quot;，其中 *{EntityType}* 是导航集合的类型。</span><span class="sxs-lookup"><span data-stu-id="2bed0-283">The action name is &quot;Get{EntityType}&quot;, where *{EntityType}* is the type of the navigation collection.</span></span> <span data-ttu-id="2bed0-284">例如， &quot;GetSupplier&quot;。</span><span class="sxs-lookup"><span data-stu-id="2bed0-284">For example, &quot;GetSupplier&quot;.</span></span> <span data-ttu-id="2bed0-285">可以使用你喜欢的任何命名约定&#8212;只需确保控制器操作匹配。</span><span class="sxs-lookup"><span data-stu-id="2bed0-285">You can use any naming convention that you like &#8212; just make sure your controller actions match.</span></span>
4. <span data-ttu-id="2bed0-286">将名为两个参数的操作*键*并*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="2bed0-286">The action takes two parameters named *key* and *relatedKey*.</span></span> <span data-ttu-id="2bed0-287">(有关某些预定义的参数名称的列表，请参阅[ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="2bed0-287">(For a list of some predefined parameter names, see [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)</span></span>

<span data-ttu-id="2bed0-288">下一步将新的约定添加到路由约定的列表。</span><span class="sxs-lookup"><span data-stu-id="2bed0-288">The next step is adding the new convention to the list of routing conventions.</span></span> <span data-ttu-id="2bed0-289">发生这种情况在配置期间，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="2bed0-289">This happens during configuration, as shown in the following code:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

<span data-ttu-id="2bed0-290">下面是一些其他示例路由约定的有用来研究：</span><span class="sxs-lookup"><span data-stu-id="2bed0-290">Here are some other sample routing conventions that be useful to study:</span></span>

- [<span data-ttu-id="2bed0-291">CompositeKeyRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="2bed0-291">CompositeKeyRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [<span data-ttu-id="2bed0-292">CustomNavigationRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="2bed0-292">CustomNavigationRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [<span data-ttu-id="2bed0-293">NonBindableActionRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="2bed0-293">NonBindableActionRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [<span data-ttu-id="2bed0-294">ODataVersionRouteConstraint</span><span class="sxs-lookup"><span data-stu-id="2bed0-294">ODataVersionRouteConstraint</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

<span data-ttu-id="2bed0-295">Web API 本身当然是开放源代码，以便您可以看到[源代码](http://aspnetwebstack.codeplex.com/)的内置路由约定。</span><span class="sxs-lookup"><span data-stu-id="2bed0-295">And of course Web API itself is open-source, so you can see the [source code](http://aspnetwebstack.codeplex.com/) for the built-in routing conventions.</span></span> <span data-ttu-id="2bed0-296">这些定义在**System.Web.Http.OData.Routing.Conventions**命名空间。</span><span class="sxs-lookup"><span data-stu-id="2bed0-296">These are defined in the **System.Web.Http.OData.Routing.Conventions** namespace.</span></span>
