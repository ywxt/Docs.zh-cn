---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: 使用 $select，$expand、 和中 ASP.NET Web API 2 OData $value |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/11/2013
ms.topic: article
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: f229cdbd8850a787dd3585e0640e8e66f6109331
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="73cdd-102">使用 $select，$expand、 和中 ASP.NET Web API 2 OData $value</span><span class="sxs-lookup"><span data-stu-id="73cdd-102">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="73cdd-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="73cdd-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="73cdd-104">为 $expand、 $select，$value 中和选项 OData web API 2 添加了支持。</span><span class="sxs-lookup"><span data-stu-id="73cdd-104">Web API 2 adds support for the $expand, $select, and $value options in OData.</span></span> <span data-ttu-id="73cdd-105">这些选项允许客户端控制从服务器重新获取的表示形式。</span><span class="sxs-lookup"><span data-stu-id="73cdd-105">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="73cdd-106">**$expand**导致相关的实体以内联形式包含在响应中的。</span><span class="sxs-lookup"><span data-stu-id="73cdd-106">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="73cdd-107">**$select**选择要在响应中包含的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="73cdd-107">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="73cdd-108">**$value**获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="73cdd-108">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="73cdd-109">示例架构</span><span class="sxs-lookup"><span data-stu-id="73cdd-109">Example Schema</span></span>

<span data-ttu-id="73cdd-110">对于本文中，我将使用定义三个实体的 OData 服务： 产品、 供应商和类别。</span><span class="sxs-lookup"><span data-stu-id="73cdd-110">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="73cdd-111">每个产品均具有一个类别和一个供应商。</span><span class="sxs-lookup"><span data-stu-id="73cdd-111">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="73cdd-112">下面是定义实体模型的 C# 类：</span><span class="sxs-lookup"><span data-stu-id="73cdd-112">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="73cdd-113">请注意，`Product`类定义导航属性`Supplier`和`Category`。</span><span class="sxs-lookup"><span data-stu-id="73cdd-113">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="73cdd-114">`Category`类定义每个类别中的产品的导航属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-114">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="73cdd-115">若要创建此架构的 OData 终结点，使用 Visual Studio 2013 的基架中, 所述[在 ASP.NET Web API 中创建 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="73cdd-115">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="73cdd-116">为产品、 类别和供应商添加单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="73cdd-116">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="73cdd-117">启用 $展开和 $select</span><span class="sxs-lookup"><span data-stu-id="73cdd-117">Enabling $expand and $select</span></span>

<span data-ttu-id="73cdd-118">在 Visual Studio 2013 中，Web API OData 基架创建一个控制器，该自动支持 $expand 和 $select。</span><span class="sxs-lookup"><span data-stu-id="73cdd-118">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="73cdd-119">对于引用，这里有支持 $ 的要求可展开和 $select 控制器中的。</span><span class="sxs-lookup"><span data-stu-id="73cdd-119">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="73cdd-120">对于集合，控制器`Get`方法必须返回**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="73cdd-120">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="73cdd-121">对于单个实体，返回**SingleResult&lt;T&gt;**，其中 T 为**IQueryable** ，其中包含零个或一个实体。</span><span class="sxs-lookup"><span data-stu-id="73cdd-121">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="73cdd-122">此外，修饰你`Get`方法 **[Queryable]** 特性，如前面的代码段中所示。</span><span class="sxs-lookup"><span data-stu-id="73cdd-122">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="73cdd-123">或者，调用**EnableQuerySupport**上**HttpConfiguration**在启动时的对象。</span><span class="sxs-lookup"><span data-stu-id="73cdd-123">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="73cdd-124">(有关详细信息，请参阅[启用 OData 查询选项](supporting-odata-query-options.md#enable)。)</span><span class="sxs-lookup"><span data-stu-id="73cdd-124">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="73cdd-125">使用 $展开</span><span class="sxs-lookup"><span data-stu-id="73cdd-125">Using $expand</span></span>

<span data-ttu-id="73cdd-126">当查询 OData 实体或集合时，默认响应不包括相关的实体。</span><span class="sxs-lookup"><span data-stu-id="73cdd-126">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="73cdd-127">例如，以下是类别实体集的默认响应：</span><span class="sxs-lookup"><span data-stu-id="73cdd-127">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="73cdd-128">如你所见，响应将不包括任何产品，即使 Category 实体具有产品导航链接。</span><span class="sxs-lookup"><span data-stu-id="73cdd-128">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="73cdd-129">但是，客户端可以使用 $扩展以获取每个类别的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="73cdd-129">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="73cdd-130">$Expand 选项将会填入请求的查询字符串：</span><span class="sxs-lookup"><span data-stu-id="73cdd-130">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="73cdd-131">现在服务器将包含每个类别，各类别的内联的产品。</span><span class="sxs-lookup"><span data-stu-id="73cdd-131">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="73cdd-132">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="73cdd-132">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="73cdd-133">请注意，"value"数组中的每个条目包含产品列表。</span><span class="sxs-lookup"><span data-stu-id="73cdd-133">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="73cdd-134">$ Expand 选项的导航属性以展开的采用逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="73cdd-134">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="73cdd-135">以下请求将展开类别和产品供应商。</span><span class="sxs-lookup"><span data-stu-id="73cdd-135">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="73cdd-136">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="73cdd-136">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="73cdd-137">你可以展开导航属性的多个的级别。</span><span class="sxs-lookup"><span data-stu-id="73cdd-137">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="73cdd-138">下面的示例包含的类别的所有产品以及每个产品供应商。</span><span class="sxs-lookup"><span data-stu-id="73cdd-138">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="73cdd-139">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="73cdd-139">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="73cdd-140">默认情况下，Web API 限制为 2 的最大扩展深度。</span><span class="sxs-lookup"><span data-stu-id="73cdd-140">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="73cdd-141">可阻止客户端发送类似的复杂请求`$expand=Orders/OrderDetails/Product/Supplier/Region`，这可能很低效查询并创建大型的响应。</span><span class="sxs-lookup"><span data-stu-id="73cdd-141">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="73cdd-142">若要覆盖默认值，设置**MaxExpansionDepth**属性 **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-142">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="73cdd-143">有关详细信息，有关 $expand 选项，请参阅[展开 ($expand) 系统查询选项](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand)正式的 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="73cdd-143">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="73cdd-144">使用 $select</span><span class="sxs-lookup"><span data-stu-id="73cdd-144">Using $select</span></span>

<span data-ttu-id="73cdd-145">$Select 选项指定要包含在响应正文中的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="73cdd-145">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="73cdd-146">例如，若要获取的名称和每个产品的价格，请使用以下查询：</span><span class="sxs-lookup"><span data-stu-id="73cdd-146">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="73cdd-147">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="73cdd-147">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="73cdd-148">你可以组合 $select 和 $expand 在同一查询中。</span><span class="sxs-lookup"><span data-stu-id="73cdd-148">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="73cdd-149">请确保要包含在 $select 选项中的扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-149">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="73cdd-150">例如，以下请求将获取的产品名称和供应商。</span><span class="sxs-lookup"><span data-stu-id="73cdd-150">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="73cdd-151">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="73cdd-151">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="73cdd-152">你还可以选择中的扩展属性的属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-152">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="73cdd-153">以下请求将展开产品，且选择类别名称和产品名称。</span><span class="sxs-lookup"><span data-stu-id="73cdd-153">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="73cdd-154">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="73cdd-154">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="73cdd-155">有关 $select 选项的详细信息，请参阅[选择系统查询选项 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select)正式的 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="73cdd-155">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="73cdd-156">获取单个实体 ($value) 属性</span><span class="sxs-lookup"><span data-stu-id="73cdd-156">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="73cdd-157">有两种方式的 OData 客户端可以从实体中获取的单个属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-157">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="73cdd-158">客户端可以获取 OData 格式中的值或获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="73cdd-158">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="73cdd-159">以下请求 OData 格式中获取的属性。</span><span class="sxs-lookup"><span data-stu-id="73cdd-159">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="73cdd-160">下面是 JSON 格式的示例响应：</span><span class="sxs-lookup"><span data-stu-id="73cdd-160">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="73cdd-161">若要获取属性的原始值，请将 $value 追加到 URI:</span><span class="sxs-lookup"><span data-stu-id="73cdd-161">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="73cdd-162">下面是响应。</span><span class="sxs-lookup"><span data-stu-id="73cdd-162">Here is the response.</span></span> <span data-ttu-id="73cdd-163">请注意，内容类型不"文本/plain"JSON。</span><span class="sxs-lookup"><span data-stu-id="73cdd-163">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="73cdd-164">若要在 OData 控制器中支持这些查询，将添加一个名为方法`GetProperty`，其中`Property`是属性的名称。</span><span class="sxs-lookup"><span data-stu-id="73cdd-164">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="73cdd-165">例如，要获取的 Name 属性的方法将被命名为`GetName`。</span><span class="sxs-lookup"><span data-stu-id="73cdd-165">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="73cdd-166">该方法应返回该属性的值：</span><span class="sxs-lookup"><span data-stu-id="73cdd-166">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
