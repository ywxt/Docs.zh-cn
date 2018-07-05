---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: 使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/11/2013
ms.topic: article
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: f7e70bd76668f2af9215d57ee1cc9e7d41948c67
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384759"
---
<a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="8bd2d-102">使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value</span><span class="sxs-lookup"><span data-stu-id="8bd2d-102">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="8bd2d-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8bd2d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8bd2d-104">Web API 2 添加了支持 $ expand，$select 和在 OData 中的 $value 选项。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-104">Web API 2 adds support for the $expand, $select, and $value options in OData.</span></span> <span data-ttu-id="8bd2d-105">这些选项允许客户端来控制该通道从服务器返回的表示形式。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-105">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="8bd2d-106">**$expand**导致相关的实体是以内联形式包含在响应中的。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-106">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="8bd2d-107">**$select**选择要在响应中包含的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-107">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="8bd2d-108">**$value**获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-108">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="8bd2d-109">示例架构</span><span class="sxs-lookup"><span data-stu-id="8bd2d-109">Example Schema</span></span>

<span data-ttu-id="8bd2d-110">对于本文中，我将使用 OData 服务，用于定义三个实体： 产品、 供应商和类别。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-110">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="8bd2d-111">每个产品都有一个类别和一个供应商。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-111">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="8bd2d-112">下面是定义实体模型的 C# 类：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-112">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="8bd2d-113">请注意，`Product`类定义的导航属性`Supplier`和`Category`。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-113">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="8bd2d-114">`Category`类定义中每个类别的产品的导航属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-114">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="8bd2d-115">若要创建此架构的 OData 终结点，请使用 Visual Studio 2013 的基架，如中所述[在 ASP.NET Web API 中创建 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-115">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="8bd2d-116">有关产品、 类别和供应商添加单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-116">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="8bd2d-117">启用 $展开和 $select</span><span class="sxs-lookup"><span data-stu-id="8bd2d-117">Enabling $expand and $select</span></span>

<span data-ttu-id="8bd2d-118">在 Visual Studio 2013 中，Web API OData 基架创建一个控制器，来自动支持 $expand 和 $select。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-118">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="8bd2d-119">有关参考，下面是支持 $ 要求展开和 $select 控制器中的。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-119">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="8bd2d-120">对于集合，该控制器`Get`方法必须返回**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-120">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="8bd2d-121">对于单个实体，返回**可取值为 SingleResult&lt;T&gt;**，其中 T 为**IQueryable** ，其中包含零个或一个实体。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-121">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="8bd2d-122">此外，修饰您`Get`方法与 **[Queryable]** 属性，如前面的代码片段中所示。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-122">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="8bd2d-123">或者，调用**EnableQuerySupport**上**HttpConfiguration**在启动时的对象。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-123">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="8bd2d-124">(有关详细信息，请参阅[启用 OData 查询选项](supporting-odata-query-options.md#enable)。)</span><span class="sxs-lookup"><span data-stu-id="8bd2d-124">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="8bd2d-125">使用 $expand</span><span class="sxs-lookup"><span data-stu-id="8bd2d-125">Using $expand</span></span>

<span data-ttu-id="8bd2d-126">在查询的 OData 实体或集合时，默认响应不包括相关的实体。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-126">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="8bd2d-127">例如，下面是类别实体集的默认响应：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-127">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="8bd2d-128">正如您所看到的即使类别实体具有一个产品的导航链接响应不包括任何产品。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-128">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="8bd2d-129">但是，客户端可以使用 $展开此项可获取每个类别的产品列表。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-129">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="8bd2d-130">$Expand 选项中请求的查询字符串：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-130">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="8bd2d-131">现在服务器将包括每个类别，各类别的内联的产品。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-131">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="8bd2d-132">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-132">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="8bd2d-133">请注意"value"数组中的每个项包含的产品列表。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-133">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="8bd2d-134">$ Expand 选项采用以逗号分隔列表与要扩展的导航属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-134">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="8bd2d-135">以下请求展开该类别和产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-135">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="8bd2d-136">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-136">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="8bd2d-137">您可以展开多个导航属性的级别。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-137">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="8bd2d-138">下面的示例包括一个类别的所有产品以及每个产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-138">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="8bd2d-139">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-139">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="8bd2d-140">默认情况下，Web API 限制为 2 的最大展开深度。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-140">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="8bd2d-141">防止发送等复杂请求客户端`$expand=Orders/OrderDetails/Product/Supplier/Region`，这可能很低效查询并创建大型的响应。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-141">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="8bd2d-142">若要重写默认值，设置**MaxExpansionDepth**上的属性 **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-142">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="8bd2d-143">详细了解 $ expand 选项，请参阅[展开 ($expand) 系统查询选项](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand)官方 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-143">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="8bd2d-144">使用 $select</span><span class="sxs-lookup"><span data-stu-id="8bd2d-144">Using $select</span></span>

<span data-ttu-id="8bd2d-145">$Select 选项指定要在响应正文中包含的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-145">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="8bd2d-146">例如，若要获取的名称和每个产品的价格，请使用以下查询：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-146">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="8bd2d-147">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-147">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="8bd2d-148">你可以组合 $select 和 $expand 中相同的查询。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-148">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="8bd2d-149">请确保在 $select 选项中包含扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-149">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="8bd2d-150">例如，以下请求获取的产品名称和供应商。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-150">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="8bd2d-151">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-151">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="8bd2d-152">此外可以选择一个扩展属性中的属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-152">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="8bd2d-153">以下请求扩展产品，并选择类别名称和产品名称。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-153">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="8bd2d-154">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-154">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="8bd2d-155">有关 $select 选项的详细信息，请参阅[Select 系统查询选项 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select)官方 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-155">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="8bd2d-156">获取单个实体 ($value) 的属性</span><span class="sxs-lookup"><span data-stu-id="8bd2d-156">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="8bd2d-157">有两种方法可从实体获取的个别属性的 OData 客户端。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-157">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="8bd2d-158">客户端可以获取 OData 格式的值或获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-158">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="8bd2d-159">以下请求获取 OData 格式的属性。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-159">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="8bd2d-160">此处是 JSON 格式的示例响应：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-160">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="8bd2d-161">若要获取的属性的原始值，向 URI 追加 $value:</span><span class="sxs-lookup"><span data-stu-id="8bd2d-161">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="8bd2d-162">下面是响应。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-162">Here is the response.</span></span> <span data-ttu-id="8bd2d-163">请注意，内容类型"text/plain"不是 JSON。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-163">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="8bd2d-164">若要在 OData 控制器中支持这些查询，将添加一个名为方法`GetProperty`，其中`Property`是属性的名称。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-164">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="8bd2d-165">例如，若要获取的 Name 属性的方法将被命名为`GetName`。</span><span class="sxs-lookup"><span data-stu-id="8bd2d-165">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="8bd2d-166">该方法应返回该属性的值：</span><span class="sxs-lookup"><span data-stu-id="8bd2d-166">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
