---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: 使用 Web API 2.2 中 OData v4 的包含关系 |Microsoft 文档
author: rick-anderson
description: 传统上，如果它已封装在实体集可以仅访问实体。 但 OData v4 提供两个其他选项，单一实例和 Con...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 7d3c81bf3d2a43faa3e71155637e031f81143782
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26507996"
---
<a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="952ab-104">使用 Web API 2.2 中 OData v4 的包含关系</span><span class="sxs-lookup"><span data-stu-id="952ab-104">Containment in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="952ab-105">通过 Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="952ab-105">by Jinfu Tan</span></span>

> <span data-ttu-id="952ab-106">传统上，如果它已封装在实体集可以仅访问实体。</span><span class="sxs-lookup"><span data-stu-id="952ab-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="952ab-107">但在 OData v4 提供单一实例和包含，这两种 WebAPI 2.2 支持的两个附加选项。</span><span class="sxs-lookup"><span data-stu-id="952ab-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="952ab-108">本主题演示如何在 WebApi 2.2 中的 OData 终结点中定义包含。</span><span class="sxs-lookup"><span data-stu-id="952ab-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="952ab-109">包含有关的详细信息，请参阅[包含即将与 OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="952ab-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="952ab-110">若要在 Web API 中创建 OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="952ab-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="952ab-111">首先，我们将在 OData 服务中，使用此数据模型创建的包含域模型：</span><span class="sxs-lookup"><span data-stu-id="952ab-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![数据模型](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="952ab-113">帐户包含许多 PaymentInstruments (PI)，但我们未定义实体集 PI。</span><span class="sxs-lookup"><span data-stu-id="952ab-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="952ab-114">相反，pi 均仅可以通过帐户访问。</span><span class="sxs-lookup"><span data-stu-id="952ab-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="952ab-115">你可以下载从本主题中使用的解决方案[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)。</span><span class="sxs-lookup"><span data-stu-id="952ab-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="952ab-116">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="952ab-116">Defining the data model</span></span>

1. <span data-ttu-id="952ab-117">定义的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="952ab-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="952ab-118">`Contained`属性用于包含导航属性。</span><span class="sxs-lookup"><span data-stu-id="952ab-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="952ab-119">生成基于 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="952ab-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="952ab-120">`ODataConventionModelBuilder`将处理生成 EDM 模型，如果`Contained`属性会被添加到对应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="952ab-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="952ab-121">如果属性是集合类型，`GetCount(string NameContains)`还将创建函数。</span><span class="sxs-lookup"><span data-stu-id="952ab-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="952ab-122">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="952ab-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="952ab-123">`ContainsTarget`属性指示的导航属性为包含。</span><span class="sxs-lookup"><span data-stu-id="952ab-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="952ab-124">定义包含的实体集控制器</span><span class="sxs-lookup"><span data-stu-id="952ab-124">Define the containing entity set controller</span></span>

<span data-ttu-id="952ab-125">包含的实体没有其自己的控制器;包含的实体集控制器中定义该操作。</span><span class="sxs-lookup"><span data-stu-id="952ab-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="952ab-126">在此示例中，没有 AccountsController，但没有 PaymentInstrumentsController。</span><span class="sxs-lookup"><span data-stu-id="952ab-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="952ab-127">如果该 OData 路径是 4 个或多个段，仅属性路由工作原理，如`[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]`上述控制器中。</span><span class="sxs-lookup"><span data-stu-id="952ab-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="952ab-128">否则，属性和传统路由工作原理： 例如，`GetPayInPIs(int key)`匹配`GET ~/Accounts(1)/PayinPIs`。</span><span class="sxs-lookup"><span data-stu-id="952ab-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="952ab-129">*到 Leo Hu 感谢这篇文章的原始内容。*</span><span class="sxs-lookup"><span data-stu-id="952ab-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
