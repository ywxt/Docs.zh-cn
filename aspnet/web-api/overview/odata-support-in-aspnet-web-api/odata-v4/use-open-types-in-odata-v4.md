---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在使用 ASP.NET Web API OData v4 中打开类型 |Microsoft Docs
author: microsoft
description: OData v4 中开放类型是包含动态属性，除了在类型定义中声明的任何属性的 stuctured 类型。 打开...
ms.author: aspnetcontent
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 560d47e0dc451847311eb9e2327190eed2209546
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832259"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="51396-104">在使用 ASP.NET Web API OData v4 中打开类型</span><span class="sxs-lookup"><span data-stu-id="51396-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="51396-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="51396-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="51396-106">在 OData v4*打开类型*是 stuctured 类型，其中包含动态属性，除了在类型定义中声明的任何属性。</span><span class="sxs-lookup"><span data-stu-id="51396-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="51396-107">开放类型，可以添加到数据模型的灵活性。</span><span class="sxs-lookup"><span data-stu-id="51396-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="51396-108">本教程演示如何在 ASP.NET Web API OData 中使用开放类型。</span><span class="sxs-lookup"><span data-stu-id="51396-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="51396-109">本教程假定您已经知道如何在 ASP.NET Web API 中创建 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="51396-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="51396-110">如果不是，应首先阅读[创建 OData v4 终结点](create-an-odata-v4-endpoint.md)第一个。</span><span class="sxs-lookup"><span data-stu-id="51396-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="51396-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="51396-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="51396-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="51396-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="51396-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="51396-113">OData v4</span></span>


<span data-ttu-id="51396-114">首先，OData 的一些术语：</span><span class="sxs-lookup"><span data-stu-id="51396-114">First, some OData terminology:</span></span>

- <span data-ttu-id="51396-115">实体类型： 具有一个键的结构化的类型。</span><span class="sxs-lookup"><span data-stu-id="51396-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="51396-116">复杂类型： 结构化的类型没有键。</span><span class="sxs-lookup"><span data-stu-id="51396-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="51396-117">打开类型： 具有动态属性的类型。</span><span class="sxs-lookup"><span data-stu-id="51396-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="51396-118">实体类型和复杂类型可以打开。</span><span class="sxs-lookup"><span data-stu-id="51396-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="51396-119">动态属性的值可以是基元类型、 复杂类型或枚举类型;或任何这些类型的集合。</span><span class="sxs-lookup"><span data-stu-id="51396-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="51396-120">有关开放类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="51396-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="51396-121">安装 Web OData 库</span><span class="sxs-lookup"><span data-stu-id="51396-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="51396-122">使用 NuGet 包管理器安装最新的 Web API OData 库。</span><span class="sxs-lookup"><span data-stu-id="51396-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="51396-123">从包管理器控制台窗口中：</span><span class="sxs-lookup"><span data-stu-id="51396-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="51396-124">定义 CLR 类型</span><span class="sxs-lookup"><span data-stu-id="51396-124">Define the CLR Types</span></span>

<span data-ttu-id="51396-125">首先，定义为 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="51396-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="51396-126">创建实体数据模型 (EDM) 时，</span><span class="sxs-lookup"><span data-stu-id="51396-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="51396-127">`Category` 是枚举类型。</span><span class="sxs-lookup"><span data-stu-id="51396-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="51396-128">`Address` 是一种复杂类型。</span><span class="sxs-lookup"><span data-stu-id="51396-128">`Address` is a complex type.</span></span> <span data-ttu-id="51396-129">（它没有密钥，因此它不是实体类型。）</span><span class="sxs-lookup"><span data-stu-id="51396-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="51396-130">`Customer` 是实体类型。</span><span class="sxs-lookup"><span data-stu-id="51396-130">`Customer` is an entity type.</span></span> <span data-ttu-id="51396-131">（它具有一个密钥）。</span><span class="sxs-lookup"><span data-stu-id="51396-131">(It has a key.)</span></span>
- <span data-ttu-id="51396-132">`Press` 是打开的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="51396-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="51396-133">`Book` 为开放实体类型。</span><span class="sxs-lookup"><span data-stu-id="51396-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="51396-134">若要创建开放类型，CLR 类型必须具有一个类型的属性`IDictionary<string, object>`，用于保存动态属性。</span><span class="sxs-lookup"><span data-stu-id="51396-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="51396-135">生成的 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="51396-135">Build the EDM Model</span></span>

<span data-ttu-id="51396-136">如果您使用**ODataConventionModelBuilder**若要创建 EDM`Press`和`Book`自动添加为开放类型，根据是否存在的`IDictionary<string, object>`属性。</span><span class="sxs-lookup"><span data-stu-id="51396-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="51396-137">您还可以构建 EDM 显式使用**ODataModelBuilder**。</span><span class="sxs-lookup"><span data-stu-id="51396-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="51396-138">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="51396-138">Add an OData Controller</span></span>

<span data-ttu-id="51396-139">接下来，添加一个 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="51396-139">Next, add an OData controller.</span></span> <span data-ttu-id="51396-140">对于本教程中，我们将使用简化的控制器仅支持获取，和 POST 请求，以及使用的内存中列表来存储实体。</span><span class="sxs-lookup"><span data-stu-id="51396-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="51396-141">请注意，第一个`Book`实例都有任何动态属性。</span><span class="sxs-lookup"><span data-stu-id="51396-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="51396-142">第二个`Book`实例都有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="51396-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="51396-143">"已发布": 基元类型</span><span class="sxs-lookup"><span data-stu-id="51396-143">"Published": Primitive type</span></span>
- <span data-ttu-id="51396-144">"作者": 基元类型的集合</span><span class="sxs-lookup"><span data-stu-id="51396-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="51396-145">"OtherCategories": 枚举类型的集合。</span><span class="sxs-lookup"><span data-stu-id="51396-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="51396-146">此外，`Press`属性的`Book`实例都有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="51396-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="51396-147">"博客": 基元类型</span><span class="sxs-lookup"><span data-stu-id="51396-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="51396-148">"Address": 复杂类型</span><span class="sxs-lookup"><span data-stu-id="51396-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="51396-149">查询的元数据</span><span class="sxs-lookup"><span data-stu-id="51396-149">Query the Metadata</span></span>

<span data-ttu-id="51396-150">若要获取 OData 元数据文档，请将发送 GET 请求到`~/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="51396-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="51396-151">响应正文应类似于以下所示：</span><span class="sxs-lookup"><span data-stu-id="51396-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="51396-152">从元数据文档中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="51396-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="51396-153">有关`Book`并`Press`类型的值`OpenType`属性为 true。</span><span class="sxs-lookup"><span data-stu-id="51396-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="51396-154">`Customer`和`Address`类型不具有此特性。</span><span class="sxs-lookup"><span data-stu-id="51396-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="51396-155">`Book`实体类型具有三个声明的属性： ISBN、 标题，然后按。</span><span class="sxs-lookup"><span data-stu-id="51396-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="51396-156">OData 元数据不包括`Book.Properties`从 CLR 类的属性。</span><span class="sxs-lookup"><span data-stu-id="51396-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="51396-157">同样，`Press`复杂类型具有只有两个声明的属性： 名称和类别。</span><span class="sxs-lookup"><span data-stu-id="51396-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="51396-158">元数据不包括`Press.DynamicProperties`从 CLR 类的属性。</span><span class="sxs-lookup"><span data-stu-id="51396-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="51396-159">查询的实体</span><span class="sxs-lookup"><span data-stu-id="51396-159">Query an Entity</span></span>

<span data-ttu-id="51396-160">若要获取对书籍 ISBN 等于"978-0-7356-7942-9"，将发送 GET 请求到`~/Books('978-0-7356-7942-9')`。</span><span class="sxs-lookup"><span data-stu-id="51396-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="51396-161">响应正文应类似于以下。</span><span class="sxs-lookup"><span data-stu-id="51396-161">The response body should look similar to the following.</span></span> <span data-ttu-id="51396-162">（缩进，以使其更具可读性。）</span><span class="sxs-lookup"><span data-stu-id="51396-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="51396-163">请注意，动态属性以内联形式包含声明的属性。</span><span class="sxs-lookup"><span data-stu-id="51396-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="51396-164">POST 实体</span><span class="sxs-lookup"><span data-stu-id="51396-164">POST an Entity</span></span>

<span data-ttu-id="51396-165">若要添加的书实体，发送 POST 请求到`~/Books`。</span><span class="sxs-lookup"><span data-stu-id="51396-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="51396-166">客户端可以在请求负载中设置动态属性。</span><span class="sxs-lookup"><span data-stu-id="51396-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="51396-167">下面是示例请求。</span><span class="sxs-lookup"><span data-stu-id="51396-167">Here is an example request.</span></span> <span data-ttu-id="51396-168">请注意"Price"和"已发布"属性。</span><span class="sxs-lookup"><span data-stu-id="51396-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="51396-169">如果在控制器方法中设置断点，可以看到 Web API 添加到这些属性`Properties`字典。</span><span class="sxs-lookup"><span data-stu-id="51396-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="51396-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="51396-170">Additional Resources</span></span>

[<span data-ttu-id="51396-171">OData 开放类型示例</span><span class="sxs-lookup"><span data-stu-id="51396-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
