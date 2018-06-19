---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 与 ASP.NET Web API OData v4 中的复杂类型继承 |Microsoft 文档
author: microsoft
description: OData v4 规范中，根据复杂类型可以继承另一种复杂类型。 （复杂类型是结构化的类型没有键。）Web API...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: be2dbfa82b99b6c48928e4e767716852c14a463b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508416"
---
<a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="ca3d3-104">与 ASP.NET Web API OData v4 中的复杂类型继承</span><span class="sxs-lookup"><span data-stu-id="ca3d3-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="ca3d3-105">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ca3d3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ca3d3-106">根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，复杂类型可以继承另一种复杂类型。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="ca3d3-107">(A*复杂*类型是结构化的类型没有键。)Web API OData 5.3 支持复杂类型继承。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="ca3d3-108">本主题演示如何生成具有复杂的继承类型的实体数据模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="ca3d3-109">有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ca3d3-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ca3d3-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ca3d3-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="ca3d3-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="ca3d3-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="ca3d3-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="ca3d3-113">模型层次结构</span><span class="sxs-lookup"><span data-stu-id="ca3d3-113">Model Hierarchy</span></span>

<span data-ttu-id="ca3d3-114">为了说明复杂类型继承，我们将使用以下类层次结构。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="ca3d3-115">`Shape`是抽象的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="ca3d3-116">`Rectangle``Triangle`，和`Circle`复杂类型派生自`Shape`，和`RoundRectangle`派生自`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="ca3d3-117">`Window`是一个实体类型，包含`Shape`实例。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="ca3d3-118">以下是定义这些类型的 CLR 类。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="ca3d3-119">生成 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="ca3d3-119">Build the EDM Model</span></span>

<span data-ttu-id="ca3d3-120">若要创建 EDM，可以使用**ODataConventionModelBuilder**，，推断从 CLR 类型的继承关系。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="ca3d3-121">你也可以生成 EDM 显式使用**ODataModelBuilder**。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="ca3d3-122">这将更多代码，但使你更好地控制 EDM。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="ca3d3-123">这两个示例创建相同的 EDM 架构。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="ca3d3-124">元数据文档</span><span class="sxs-lookup"><span data-stu-id="ca3d3-124">Metadata Document</span></span>

<span data-ttu-id="ca3d3-125">此处是 OData 元数据文档时，显示复杂类型继承。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="ca3d3-126">从元数据文档中，你可以看到:</span><span class="sxs-lookup"><span data-stu-id="ca3d3-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="ca3d3-127">`Shape`复杂类型为抽象。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="ca3d3-128">`Rectangle`， `Triangle`，和`Circle`复杂类型具有的基类型`Shape`。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="ca3d3-129">`RoundRectangle`类型具有基类型`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="ca3d3-130">强制转换复杂类型</span><span class="sxs-lookup"><span data-stu-id="ca3d3-130">Casting Complex Types</span></span>

<span data-ttu-id="ca3d3-131">现在支持复杂类型上进行转换。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="ca3d3-132">例如，下面的查询强制转换`Shape`到`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="ca3d3-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="ca3d3-133">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="ca3d3-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
