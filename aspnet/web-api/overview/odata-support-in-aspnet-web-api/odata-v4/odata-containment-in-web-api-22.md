---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: 包含 OData v4 中的使用 Web API 2.2 |Microsoft Docs
author: rick-anderson
description: 传统上，如果它已封装在实体集内可以只访问实体。 但是，OData v4 提供两个其他选项，单独预测查询和 Con...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 33ff49f69d70dd3a8179445d2895c418d2185e49
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365602"
---
<a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="2a8aa-104">使用 Web API 2.2 OData v4 中的包含关系</span><span class="sxs-lookup"><span data-stu-id="2a8aa-104">Containment in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="2a8aa-105">通过 Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="2a8aa-105">by Jinfu Tan</span></span>

> <span data-ttu-id="2a8aa-106">传统上，如果它已封装在实体集内可以只访问实体。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="2a8aa-107">但 OData v4 提供了两个附加选项，单独预测查询和包含关系，这两种支持 WebAPI 2.2。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="2a8aa-108">本主题演示如何定义包含 WebApi 2.2 中的 OData 终结点中。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="2a8aa-109">包含有关详细信息，请参阅[包含即将与 OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="2a8aa-110">若要创建 Web API OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="2a8aa-111">首先，我们将在 OData 服务中，使用此数据模型创建包含域模型：</span><span class="sxs-lookup"><span data-stu-id="2a8aa-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![数据模型](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="2a8aa-113">一个帐户包含许多 PaymentInstruments (PI)，但我们未定义的实体集为 PI。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="2a8aa-114">相反，仅可以通过帐户访问 Pi。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="2a8aa-115">您可以下载从本主题中使用的解决方案[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="2a8aa-116">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="2a8aa-116">Defining the data model</span></span>

1. <span data-ttu-id="2a8aa-117">定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="2a8aa-118">`Contained`属性用于包含导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="2a8aa-119">生成基于 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="2a8aa-120">`ODataConventionModelBuilder`将处理生成的 EDM 模型，如果`Contained`属性添加到相应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="2a8aa-121">如果属性为集合类型，`GetCount(string NameContains)`还将创建函数。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="2a8aa-122">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="2a8aa-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="2a8aa-123">`ContainsTarget`属性指示的导航属性为包含。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="2a8aa-124">定义包含实体集控制器</span><span class="sxs-lookup"><span data-stu-id="2a8aa-124">Define the containing entity set controller</span></span>

<span data-ttu-id="2a8aa-125">包含的实体不具有其自己的控制器;包含实体集控制器中定义该操作。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="2a8aa-126">在此示例中，没有 AccountsController，但没有 PaymentInstrumentsController。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="2a8aa-127">如果 OData 路径是 4 个或多个段，仅特性路由的工作原理，如`[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]`上述控制器中。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="2a8aa-128">否则，属性和传统路由工作原理： 例如，`GetPayInPIs(int key)`匹配`GET ~/Accounts(1)/PayinPIs`。</span><span class="sxs-lookup"><span data-stu-id="2a8aa-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="2a8aa-129">*感谢您对 Leo Hu 这篇文章的原始内容。*</span><span class="sxs-lookup"><span data-stu-id="2a8aa-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
