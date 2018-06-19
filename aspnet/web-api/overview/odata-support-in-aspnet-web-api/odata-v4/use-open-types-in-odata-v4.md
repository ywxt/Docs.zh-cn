---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在 ASP.NET web API OData v4 中打开类型 |Microsoft 文档
author: microsoft
description: 在 OData v4 开放类型是一个 stuctured 类型，包含动态属性，除了在类型定义中声明的任何属性。 打开...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/15/2014
ms.topic: article
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fe67b9a11a82b55d5f3e0e5f1b0cee10a58833d2
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
ms.locfileid: "29153267"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="b7d92-104">在 ASP.NET web API OData v4 中打开类型</span><span class="sxs-lookup"><span data-stu-id="b7d92-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="b7d92-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b7d92-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b7d92-106">在 OData v4*打开键入*是 stuctured 类型包含动态属性，除了在类型定义中声明的任何属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="b7d92-107">开放类型允许你添加到数据模型的灵活性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="b7d92-108">本教程演示如何在 ASP.NET Web API OData 中使用开放类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="b7d92-109">本教程假定你已经知道如何在 ASP.NET Web API 中创建 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="b7d92-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="b7d92-110">如果不是，应首先阅读[创建 OData v4 终结点](create-an-odata-v4-endpoint.md)第一个。</span><span class="sxs-lookup"><span data-stu-id="b7d92-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b7d92-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="b7d92-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b7d92-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="b7d92-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="b7d92-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="b7d92-113">OData v4</span></span>


<span data-ttu-id="b7d92-114">首先，一些 OData 术语：</span><span class="sxs-lookup"><span data-stu-id="b7d92-114">First, some OData terminology:</span></span>

- <span data-ttu-id="b7d92-115">实体类型： 与键是结构化的类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="b7d92-116">复杂类型： 没有密钥的结构化的类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="b7d92-117">打开类型： 具有动态属性的类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="b7d92-118">实体类型和复杂类型可以是开放式的。</span><span class="sxs-lookup"><span data-stu-id="b7d92-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="b7d92-119">动态属性的值可以是基元类型、 复杂类型或枚举类型;或任何这些类型的集合。</span><span class="sxs-lookup"><span data-stu-id="b7d92-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="b7d92-120">有关打开的类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="b7d92-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="b7d92-121">安装 Web OData 库</span><span class="sxs-lookup"><span data-stu-id="b7d92-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="b7d92-122">使用 NuGet 包管理器安装最新的 Web API OData 库。</span><span class="sxs-lookup"><span data-stu-id="b7d92-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="b7d92-123">从包管理器控制台窗口中：</span><span class="sxs-lookup"><span data-stu-id="b7d92-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="b7d92-124">定义的 CLR 类型</span><span class="sxs-lookup"><span data-stu-id="b7d92-124">Define the CLR Types</span></span>

<span data-ttu-id="b7d92-125">首先定义为 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="b7d92-126">在创建实体数据模型 (EDM)，</span><span class="sxs-lookup"><span data-stu-id="b7d92-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="b7d92-127">`Category`是枚举类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="b7d92-128">`Address`为复杂类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-128">`Address` is a complex type.</span></span> <span data-ttu-id="b7d92-129">（它有一个键，因此它不是一个实体类型。）</span><span class="sxs-lookup"><span data-stu-id="b7d92-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="b7d92-130">`Customer`是实体类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-130">`Customer` is an entity type.</span></span> <span data-ttu-id="b7d92-131">（它具有一个键）。</span><span class="sxs-lookup"><span data-stu-id="b7d92-131">(It has a key.)</span></span>
- <span data-ttu-id="b7d92-132">`Press`为开放式复杂类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="b7d92-133">`Book`是打开的实体类型。</span><span class="sxs-lookup"><span data-stu-id="b7d92-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="b7d92-134">若要创建开放类型，CLR 类型必须具有类型的属性`IDictionary<string, object>`，其中包含的动态属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="b7d92-135">生成 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="b7d92-135">Build the EDM Model</span></span>

<span data-ttu-id="b7d92-136">如果你使用**ODataConventionModelBuilder**创建 EDM，`Press`和`Book`自动添加为开放类型，基于是否存在`IDictionary<string, object>`属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="b7d92-137">你也可以生成 EDM 显式使用**ODataModelBuilder**。</span><span class="sxs-lookup"><span data-stu-id="b7d92-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="b7d92-138">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="b7d92-138">Add an OData Controller</span></span>

<span data-ttu-id="b7d92-139">接下来，添加一个 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="b7d92-139">Next, add an OData controller.</span></span> <span data-ttu-id="b7d92-140">对于本教程中，我们将使用只是支持获取，和 POST 请求，并使用内存中列表来存储实体的简化的控制器。</span><span class="sxs-lookup"><span data-stu-id="b7d92-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="b7d92-141">请注意，第一个`Book`实例都有任何动态属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="b7d92-142">第二个`Book`实例具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="b7d92-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="b7d92-143">"发布": 基元类型</span><span class="sxs-lookup"><span data-stu-id="b7d92-143">"Published": Primitive type</span></span>
- <span data-ttu-id="b7d92-144">"作者": 基元类型的集合</span><span class="sxs-lookup"><span data-stu-id="b7d92-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="b7d92-145">"OtherCategories": 枚举类型的集合。</span><span class="sxs-lookup"><span data-stu-id="b7d92-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="b7d92-146">此外，`Press`属性，`Book`实例具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="b7d92-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="b7d92-147">"博客": 基元类型</span><span class="sxs-lookup"><span data-stu-id="b7d92-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="b7d92-148">"Address": 复杂类型</span><span class="sxs-lookup"><span data-stu-id="b7d92-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="b7d92-149">查询的元数据</span><span class="sxs-lookup"><span data-stu-id="b7d92-149">Query the Metadata</span></span>

<span data-ttu-id="b7d92-150">若要获取的 OData 元数据文档，发送 GET 请求到`~/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="b7d92-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="b7d92-151">响应正文应类似于此：</span><span class="sxs-lookup"><span data-stu-id="b7d92-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="b7d92-152">从元数据文档中，你可以看到:</span><span class="sxs-lookup"><span data-stu-id="b7d92-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="b7d92-153">有关`Book`和`Press`类型的值`OpenType`属性为 true。</span><span class="sxs-lookup"><span data-stu-id="b7d92-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="b7d92-154">`Customer`和`Address`类型不具有此属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="b7d92-155">`Book`实体类型具有三个声明的属性： ISBN、 标题和按。</span><span class="sxs-lookup"><span data-stu-id="b7d92-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="b7d92-156">OData 元数据不包括`Book.Properties`从 CLR 类的属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="b7d92-157">同样，`Press`复杂类型具有只有两个声明的属性： 名称和类别。</span><span class="sxs-lookup"><span data-stu-id="b7d92-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="b7d92-158">元数据不包括`Press.DynamicProperties`从 CLR 类的属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="b7d92-159">查询的实体</span><span class="sxs-lookup"><span data-stu-id="b7d92-159">Query an Entity</span></span>

<span data-ttu-id="b7d92-160">若要获取的书 ISBN 等于"978-0-7356-7942-9"，发送 GET 请求到`~/Books('978-0-7356-7942-9')`。</span><span class="sxs-lookup"><span data-stu-id="b7d92-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="b7d92-161">响应正文应类似于以下。</span><span class="sxs-lookup"><span data-stu-id="b7d92-161">The response body should look similar to the following.</span></span> <span data-ttu-id="b7d92-162">（缩进以使其更具可读性。）</span><span class="sxs-lookup"><span data-stu-id="b7d92-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="b7d92-163">请注意，动态属性以内联形式包含声明的属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="b7d92-164">POST 实体</span><span class="sxs-lookup"><span data-stu-id="b7d92-164">POST an Entity</span></span>

<span data-ttu-id="b7d92-165">若要添加的书籍实体，发送 POST 请求到`~/Books`。</span><span class="sxs-lookup"><span data-stu-id="b7d92-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="b7d92-166">客户端可以在请求负载中设置动态属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="b7d92-167">下面是请求的示例。</span><span class="sxs-lookup"><span data-stu-id="b7d92-167">Here is an example request.</span></span> <span data-ttu-id="b7d92-168">请注意"Price"和"已发布"属性。</span><span class="sxs-lookup"><span data-stu-id="b7d92-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="b7d92-169">如果控制器方法中设置断点，你可以看到 Web API 添加到这些属性`Properties`字典。</span><span class="sxs-lookup"><span data-stu-id="b7d92-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="b7d92-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="b7d92-170">Additional Resources</span></span>

[<span data-ttu-id="b7d92-171">OData 打开类型示例</span><span class="sxs-lookup"><span data-stu-id="b7d92-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
