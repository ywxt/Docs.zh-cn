---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: 使用 ASP.NET Web API 2.2 OData v4 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。 使用 OData，可以通过导航的客户端...
ms.author: aspnetcontent
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 98f65b068d8f22e3eeef48ca7fa441434939db8b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827941"
---
<a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="dcc3a-104">使用 ASP.NET Web API 2.2 OData v4 中的实体关系</span><span class="sxs-lookup"><span data-stu-id="dcc3a-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="dcc3a-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dcc3a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="dcc3a-106">大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="dcc3a-107">使用 OData，可以通过实体关系导航的客户端。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="dcc3a-108">给定产品，您可以找到供应商。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="dcc3a-109">此外可以创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-109">You can also create or remove relationships.</span></span> <span data-ttu-id="dcc3a-110">例如，可以设置一种产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-110">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="dcc3a-111">本教程演示如何支持使用 ASP.NET Web API OData v4 中的这些操作。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="dcc3a-112">本教程以教程为基础[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dcc3a-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="dcc3a-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="dcc3a-114">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="dcc3a-114">Web API 2.1</span></span>
> - <span data-ttu-id="dcc3a-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="dcc3a-115">OData v4</span></span>
> - [<span data-ttu-id="dcc3a-116">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="dcc3a-116">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="dcc3a-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="dcc3a-117">Entity Framework 6</span></span>
> - <span data-ttu-id="dcc3a-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="dcc3a-118">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="dcc3a-119">教程版本</span><span class="sxs-lookup"><span data-stu-id="dcc3a-119">Tutorial versions</span></span>
> 
> <span data-ttu-id="dcc3a-120">OData 版本 3，请参阅[支持 OData v3 中的实体关系](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="dcc3a-121">添加 Supplier 实体</span><span class="sxs-lookup"><span data-stu-id="dcc3a-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="dcc3a-122">本教程以教程为基础[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>


<span data-ttu-id="dcc3a-123">首先，我们需要相关的实体。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-123">First, we need a related entity.</span></span> <span data-ttu-id="dcc3a-124">添加一个名为类`Supplier`模型文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="dcc3a-125">导航属性添加到`Product`类：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="dcc3a-126">添加一个新**DbSet**到`ProductsContext`类，以便实体框架将在数据库中包含的供应商表。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="dcc3a-127">在 WebApiConfig.cs 中，添加&quot;供应商&quot;实体设置为实体数据模型：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="dcc3a-128">添加供应商控制器</span><span class="sxs-lookup"><span data-stu-id="dcc3a-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="dcc3a-129">添加`SuppliersController`类到 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="dcc3a-130">我不会显示如何添加此控制器的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="dcc3a-131">步骤是产品控制器一样 (请参阅[创建 OData v4 终结点](create-an-odata-v4-endpoint.md))。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="dcc3a-132">获取相关的实体</span><span class="sxs-lookup"><span data-stu-id="dcc3a-132">Getting Related Entities</span></span>

<span data-ttu-id="dcc3a-133">若要获取产品的供应商，客户端发送 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="dcc3a-134">若要支持此请求，添加以下方法`ProductsController`类：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="dcc3a-135">此方法使用默认命名约定</span><span class="sxs-lookup"><span data-stu-id="dcc3a-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="dcc3a-136">方法名称： GetX，其中 X 是导航属性。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="dcc3a-137">参数名称：*密钥*</span><span class="sxs-lookup"><span data-stu-id="dcc3a-137">Parameter name: *key*</span></span>

<span data-ttu-id="dcc3a-138">如果遵循以下命名约定，Web API 会自动将 HTTP 请求映射到控制器方法。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="dcc3a-139">示例 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="dcc3a-140">HTTP 响应示例：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="dcc3a-141">获取相关的集合</span><span class="sxs-lookup"><span data-stu-id="dcc3a-141">Getting a related collection</span></span>

<span data-ttu-id="dcc3a-142">在上一示例中，产品有一个供应商。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="dcc3a-143">一个导航属性还可以返回一个集合。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="dcc3a-144">以下代码获取供应商的产品：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="dcc3a-145">在这种情况下，该方法返回**IQueryable**而不是**可取值为 SingleResult&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="dcc3a-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="dcc3a-146">示例 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="dcc3a-147">HTTP 响应示例：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="dcc3a-148">创建实体之间的关系</span><span class="sxs-lookup"><span data-stu-id="dcc3a-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="dcc3a-149">OData 支持创建或删除现有的两个实体之间的关系。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="dcc3a-150">在 OData v4 术语中，关系是&quot;引用&quot;。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="dcc3a-151">(在 OData v3，称为关系*链接*。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="dcc3a-152">协议差异没有影响此教程。）</span><span class="sxs-lookup"><span data-stu-id="dcc3a-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="dcc3a-153">引用具有自己的 URI，处理该窗体`/Entity/NavigationProperty/$ref`。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="dcc3a-154">例如，下面是用于解决产品和其供应商之间的引用的 URI:</span><span class="sxs-lookup"><span data-stu-id="dcc3a-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="dcc3a-155">若要添加关系时，客户端将 POST 或 PUT 请求发送到此地址。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="dcc3a-156">如果导航属性是一个单一实体，如`Product.Supplier`。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="dcc3a-157">如果导航属性是一个集合，如发布`Supplier.Products`。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="dcc3a-158">请求的正文包含关系中的其他实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="dcc3a-159">下面是示例请求：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="dcc3a-160">在此示例中，客户端发送到的 PUT 请求`/Products(6)/Supplier/$ref`，即为 $ref URI`Supplier`的产品 id = 6。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="dcc3a-161">如果请求成功，服务器会发送 204 （无内容） 响应：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="dcc3a-162">下面是要添加到关系的控制器方法`Product`:</span><span class="sxs-lookup"><span data-stu-id="dcc3a-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="dcc3a-163">*NavigationProperty*参数指定要设置的关系。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="dcc3a-164">(如果该实体的多个导航属性，可以添加更多`case`语句。)</span><span class="sxs-lookup"><span data-stu-id="dcc3a-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="dcc3a-165">*链接*参数包含供应商的 URI。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="dcc3a-166">Web API 会自动分析请求正文，以获取此参数的值。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="dcc3a-167">若要查找供应商，我们需要 ID （或密钥），这是的一部分*链接*参数。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="dcc3a-168">若要执行此操作，请使用以下帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="dcc3a-169">基本上，此方法使用 OData 库 URI 路径拆分成段，找到的段包含的密钥，然后将密钥转换为正确的类型。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="dcc3a-170">删除实体之间的关系</span><span class="sxs-lookup"><span data-stu-id="dcc3a-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="dcc3a-171">若要删除关系，客户端将 HTTP DELETE 请求发送到 $ref URI 中：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="dcc3a-172">下面是要删除某个产品和供应商之间的关系的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="dcc3a-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="dcc3a-173">在这种情况下，`Product.Supplier`是&quot;1&quot;末尾 1 对多关系，以便可以删除此关系只需通过设置`Product.Supplier`到`null`。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="dcc3a-174">在中&quot;许多&quot;末尾的关系，客户端必须指定哪些相关实体中删除。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="dcc3a-175">若要执行此操作，客户端发送请求的查询字符串中的相关实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="dcc3a-176">例如，若要删除"产品 1"从"供应商 1":</span><span class="sxs-lookup"><span data-stu-id="dcc3a-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="dcc3a-177">若要在 Web API 中支持此功能，我们需要包括中的额外参数`DeleteRef`方法。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="dcc3a-178">下面是要从产品中删除的控制器方法`Supplier.Products`关系。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="dcc3a-179">*键*参数是供应商的键和*relatedKey*参数是要从中删除从产品的关键`Products`关系。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="dcc3a-180">请注意，Web API 会自动从查询字符串获取的密钥。</span><span class="sxs-lookup"><span data-stu-id="dcc3a-180">Note that Web API automatically gets the key from the query string.</span></span>
