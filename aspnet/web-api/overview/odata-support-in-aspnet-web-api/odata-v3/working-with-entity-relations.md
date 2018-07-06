---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 支持使用 Web API 2 OData v3 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。 使用 OData，可以通过导航的客户端...
ms.author: aspnetcontent
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: b24e3ca4e3d39b424bec6bb408bb0f85825c6761
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810739"
---
<a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="6016e-104">支持使用 Web API 2 OData v3 中的实体关系</span><span class="sxs-lookup"><span data-stu-id="6016e-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>
====================
<span data-ttu-id="6016e-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6016e-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6016e-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="6016e-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="6016e-107">大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。</span><span class="sxs-lookup"><span data-stu-id="6016e-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="6016e-108">使用 OData，可以通过实体关系导航的客户端。</span><span class="sxs-lookup"><span data-stu-id="6016e-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="6016e-109">给定产品，您可以找到供应商。</span><span class="sxs-lookup"><span data-stu-id="6016e-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="6016e-110">此外可以创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="6016e-110">You can also create or remove relationships.</span></span> <span data-ttu-id="6016e-111">例如，可以设置一种产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="6016e-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="6016e-112">本教程演示如何在 ASP.NET Web API 中支持这些操作。</span><span class="sxs-lookup"><span data-stu-id="6016e-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="6016e-113">本教程以教程为基础[创建具有 Web API 2 OData v3 终结点](creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="6016e-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6016e-114">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6016e-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6016e-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="6016e-115">Web API 2</span></span>
> - <span data-ttu-id="6016e-116">OData 版本 3</span><span class="sxs-lookup"><span data-stu-id="6016e-116">OData Version 3</span></span>
> - <span data-ttu-id="6016e-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="6016e-117">Entity Framework 6</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="6016e-118">添加 Supplier 实体</span><span class="sxs-lookup"><span data-stu-id="6016e-118">Add a Supplier Entity</span></span>

<span data-ttu-id="6016e-119">首先，我们需要将新的实体类型添加到我们的 OData 源。</span><span class="sxs-lookup"><span data-stu-id="6016e-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="6016e-120">我们将添加`Supplier`类。</span><span class="sxs-lookup"><span data-stu-id="6016e-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="6016e-121">此类使用的实体键的字符串。</span><span class="sxs-lookup"><span data-stu-id="6016e-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="6016e-122">在实践中，这可能比使用整数键不太常见。</span><span class="sxs-lookup"><span data-stu-id="6016e-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="6016e-123">但值得查看 OData 如何处理整数除其他密钥类型。</span><span class="sxs-lookup"><span data-stu-id="6016e-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="6016e-124">接下来，我们将通过添加创建关系`Supplier`属性设置为`Product`类：</span><span class="sxs-lookup"><span data-stu-id="6016e-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="6016e-125">添加一个新**DbSet**到`ProductServiceContext`类，以便实体框架将包括`Supplier`数据库表中的。</span><span class="sxs-lookup"><span data-stu-id="6016e-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="6016e-126">在 WebApiConfig.cs 中，将添加到 EDM 模型的"供应商"实体：</span><span class="sxs-lookup"><span data-stu-id="6016e-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="6016e-127">导航属性</span><span class="sxs-lookup"><span data-stu-id="6016e-127">Navigation Properties</span></span>

<span data-ttu-id="6016e-128">若要获取产品的供应商，客户端发送 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="6016e-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="6016e-129">以下"供应商"是导航属性上`Product`类型。</span><span class="sxs-lookup"><span data-stu-id="6016e-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="6016e-130">在这种情况下，`Supplier`引用到单个项，但一个导航属性还可以返回的集合 （一个对多或多对多关系）。</span><span class="sxs-lookup"><span data-stu-id="6016e-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="6016e-131">若要支持此请求，添加以下方法`ProductsController`类：</span><span class="sxs-lookup"><span data-stu-id="6016e-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="6016e-132">*密钥*参数是该产品的关键。</span><span class="sxs-lookup"><span data-stu-id="6016e-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="6016e-133">该方法在这种情况下，返回相关的实体 & #8212`Supplier`实例。</span><span class="sxs-lookup"><span data-stu-id="6016e-133">The method returns the related entity&#8212in this case, a `Supplier` instance.</span></span> <span data-ttu-id="6016e-134">方法名称和参数名称都很重要。</span><span class="sxs-lookup"><span data-stu-id="6016e-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="6016e-135">一般情况下，如果导航属性名为"X"，您需要添加一个名为"GetX"方法。</span><span class="sxs-lookup"><span data-stu-id="6016e-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="6016e-136">方法必须采用名为的参数"*密钥*"父项的键的数据类型匹配的。</span><span class="sxs-lookup"><span data-stu-id="6016e-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="6016e-137">还有一点需要包括 **[FromOdataUri]** 属性中*密钥*参数。</span><span class="sxs-lookup"><span data-stu-id="6016e-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="6016e-138">此属性告知 Web API 使用 OData 语法规则分析请求 URI 中的键时。</span><span class="sxs-lookup"><span data-stu-id="6016e-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="6016e-139">创建和删除链接</span><span class="sxs-lookup"><span data-stu-id="6016e-139">Creating and Deleting Links</span></span>

<span data-ttu-id="6016e-140">OData 支持两个实体之间创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="6016e-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="6016e-141">在 OData 术语中，关系是"link"。</span><span class="sxs-lookup"><span data-stu-id="6016e-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="6016e-142">每个链接都有一个 URI 处理该窗体*实体*/$links /*实体*。</span><span class="sxs-lookup"><span data-stu-id="6016e-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="6016e-143">例如，从产品到供应商的链接如下所示：</span><span class="sxs-lookup"><span data-stu-id="6016e-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="6016e-144">若要创建新的链接，客户端将 POST 请求发送到链接 URI。</span><span class="sxs-lookup"><span data-stu-id="6016e-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="6016e-145">请求正文是目标实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="6016e-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="6016e-146">例如，假定有与键"CTSO"供应商。</span><span class="sxs-lookup"><span data-stu-id="6016e-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="6016e-147">若要创建从"Product(1)"到"Supplier('CTSO')"的链接，客户端发送的请求如下所示：</span><span class="sxs-lookup"><span data-stu-id="6016e-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="6016e-148">若要删除的链接，客户端向链接 URI 发送 DELETE 请求。</span><span class="sxs-lookup"><span data-stu-id="6016e-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="6016e-149">**创建链接**</span><span class="sxs-lookup"><span data-stu-id="6016e-149">**Creating Links**</span></span>

<span data-ttu-id="6016e-150">若要启用客户端创建供应商的产品链接，以下代码添加到`ProductsController`类：</span><span class="sxs-lookup"><span data-stu-id="6016e-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="6016e-151">此方法采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="6016e-151">This method takes three parameters:</span></span>

- <span data-ttu-id="6016e-152">*密钥*： 到父实体 （产品） 的密钥</span><span class="sxs-lookup"><span data-stu-id="6016e-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="6016e-153">*navigationProperty*： 导航属性的名称。</span><span class="sxs-lookup"><span data-stu-id="6016e-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="6016e-154">在此示例中，唯一有效的导航属性是"供应商"。</span><span class="sxs-lookup"><span data-stu-id="6016e-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="6016e-155">*链接*： 相关实体的 OData URI。</span><span class="sxs-lookup"><span data-stu-id="6016e-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="6016e-156">此值是从请求正文中提取的。</span><span class="sxs-lookup"><span data-stu-id="6016e-156">This value is taken from the request body.</span></span> <span data-ttu-id="6016e-157">例如，链接 URI 可能是"`http://localhost/odata/Suppliers('CTSO')`，这意味着供应商 id = CTSO。</span><span class="sxs-lookup"><span data-stu-id="6016e-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="6016e-158">该方法使用该链接来查找供应商。</span><span class="sxs-lookup"><span data-stu-id="6016e-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="6016e-159">如果找到匹配的供应商，则该方法将设置`Product.Supplier`属性，并将结果保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="6016e-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="6016e-160">最难的部分分析链接 URI。</span><span class="sxs-lookup"><span data-stu-id="6016e-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="6016e-161">基本上，您需要模拟向该 URI 发送 GET 请求的结果。</span><span class="sxs-lookup"><span data-stu-id="6016e-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="6016e-162">下面的帮助器方法演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6016e-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="6016e-163">该方法调用 Web API 路由过程，然后取回**ODataPath**实例，它表示已分析的 OData 路径。</span><span class="sxs-lookup"><span data-stu-id="6016e-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="6016e-164">对于链接 URI，其中一个段应为实体键。</span><span class="sxs-lookup"><span data-stu-id="6016e-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="6016e-165">（如果没有，客户端发送错误的 URI。）</span><span class="sxs-lookup"><span data-stu-id="6016e-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="6016e-166">**删除链接**</span><span class="sxs-lookup"><span data-stu-id="6016e-166">**Deleting Links**</span></span>

<span data-ttu-id="6016e-167">若要删除的链接，将以下代码添加到`ProductsController`类：</span><span class="sxs-lookup"><span data-stu-id="6016e-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="6016e-168">在此示例中，导航属性是一个`Supplier`实体。</span><span class="sxs-lookup"><span data-stu-id="6016e-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="6016e-169">如果导航属性是一个集合，要删除的链接的 URI 必须包括相关实体的键。</span><span class="sxs-lookup"><span data-stu-id="6016e-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="6016e-170">例如：</span><span class="sxs-lookup"><span data-stu-id="6016e-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="6016e-171">此请求从客户 1 删除订单 1。</span><span class="sxs-lookup"><span data-stu-id="6016e-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="6016e-172">在这种情况下，DeleteLink 方法将具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="6016e-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="6016e-173">*RelatedKey*参数提供了相关实体的键。</span><span class="sxs-lookup"><span data-stu-id="6016e-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="6016e-174">因此，在你`DeleteLink`方法中，查找由主实体*密钥*参数，查找由相关的实体*relatedKey*参数，并删除关联。</span><span class="sxs-lookup"><span data-stu-id="6016e-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="6016e-175">具体取决于您的数据模型，您可能需要实施的这两个版本`DeleteLink`。</span><span class="sxs-lookup"><span data-stu-id="6016e-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="6016e-176">Web API 将调用基于在请求 URI 上的正确版本。</span><span class="sxs-lookup"><span data-stu-id="6016e-176">Web API will call the correct version based on the request URI.</span></span>
