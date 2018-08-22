---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 使用 ASP.NET Web API OData v4 中的复杂类型继承 |Microsoft Docs
author: microsoft
description: 根据 OData v4 规范中，可以从另一种复杂类型继承的复杂类型。 （一种复杂类型是结构化的类型没有键。）Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 8dbf7dc4cfc70e1ea1ed6f72ffc0751a56809c09
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830662"
---
<a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="00a45-104">使用 ASP.NET Web API OData v4 中的复杂类型继承</span><span class="sxs-lookup"><span data-stu-id="00a45-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="00a45-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="00a45-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="00a45-106">根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，可以从另一种复杂类型继承的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="00a45-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="00a45-107">(A*复杂*类型是结构化的类型没有键。)Web API OData 5.3 支持复杂类型继承。</span><span class="sxs-lookup"><span data-stu-id="00a45-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="00a45-108">本主题演示如何生成实体数据模型 (EDM) 的复杂的继承类型。</span><span class="sxs-lookup"><span data-stu-id="00a45-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="00a45-109">有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="00a45-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="00a45-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="00a45-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="00a45-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="00a45-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="00a45-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="00a45-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="00a45-113">模型层次结构</span><span class="sxs-lookup"><span data-stu-id="00a45-113">Model Hierarchy</span></span>

<span data-ttu-id="00a45-114">为了说明复杂类型继承，我们将使用以下类层次结构。</span><span class="sxs-lookup"><span data-stu-id="00a45-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="00a45-115">`Shape` 是抽象的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="00a45-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="00a45-116">`Rectangle``Triangle`，并`Circle`复杂类型派生自`Shape`，和`RoundRectangle`派生`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="00a45-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="00a45-117">`Window` 是一个实体类型，包含`Shape`实例。</span><span class="sxs-lookup"><span data-stu-id="00a45-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="00a45-118">以下是定义这些类型的 CLR 类。</span><span class="sxs-lookup"><span data-stu-id="00a45-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="00a45-119">生成的 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="00a45-119">Build the EDM Model</span></span>

<span data-ttu-id="00a45-120">若要创建 EDM，可以使用**ODataConventionModelBuilder**，，推断从 CLR 类型的继承关系。</span><span class="sxs-lookup"><span data-stu-id="00a45-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="00a45-121">您还可以构建 EDM 显式使用**ODataModelBuilder**。</span><span class="sxs-lookup"><span data-stu-id="00a45-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="00a45-122">这需要更多代码，但提供对 EDM 的更多控制。</span><span class="sxs-lookup"><span data-stu-id="00a45-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="00a45-123">这两个示例创建相同的 EDM 架构。</span><span class="sxs-lookup"><span data-stu-id="00a45-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="00a45-124">元数据文档</span><span class="sxs-lookup"><span data-stu-id="00a45-124">Metadata Document</span></span>

<span data-ttu-id="00a45-125">下面是显示复杂类型继承的 OData 元数据文档。</span><span class="sxs-lookup"><span data-stu-id="00a45-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="00a45-126">从元数据文档中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="00a45-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="00a45-127">`Shape`复杂类型是抽象的。</span><span class="sxs-lookup"><span data-stu-id="00a45-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="00a45-128">`Rectangle`， `Triangle`，并`Circle`复杂类型具有基类型`Shape`。</span><span class="sxs-lookup"><span data-stu-id="00a45-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="00a45-129">`RoundRectangle`类型具有基类型`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="00a45-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="00a45-130">强制转换的复杂类型</span><span class="sxs-lookup"><span data-stu-id="00a45-130">Casting Complex Types</span></span>

<span data-ttu-id="00a45-131">现在支持对复杂类型强制转换。</span><span class="sxs-lookup"><span data-stu-id="00a45-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="00a45-132">例如，下面的查询强制转换`Shape`到`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="00a45-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="00a45-133">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="00a45-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
