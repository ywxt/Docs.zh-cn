---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 创建 OData v4 中的单一实例使用 Web API 2.2 |Microsoft Docs
author: rick-anderson
description: 本主题演示如何在 Web API 2.2 中的 OData 终结点中定义单一实例。
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3ae9b23fae356e387a011a190119d760dc46d022
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390922"
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="eb64c-103">创建使用 Web API 2.2 OData v4 中的单一实例</span><span class="sxs-lookup"><span data-stu-id="eb64c-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="eb64c-104">通过 Zoe 卢奥语</span><span class="sxs-lookup"><span data-stu-id="eb64c-104">by Zoe Luo</span></span>

> <span data-ttu-id="eb64c-105">传统上，如果它已封装在实体集内可以只访问实体。</span><span class="sxs-lookup"><span data-stu-id="eb64c-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="eb64c-106">但 OData v4 提供了两个附加选项，单独预测查询和包含关系，这两种支持 WebAPI 2.2。</span><span class="sxs-lookup"><span data-stu-id="eb64c-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="eb64c-107">本文介绍如何在 Web API 2.2 中的 OData 终结点中定义单一实例。</span><span class="sxs-lookup"><span data-stu-id="eb64c-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="eb64c-108">有关哪些单一实例以及如何从使用它受益的信息，请参阅[使用单一实例定义特殊实体](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eb64c-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="eb64c-109">若要创建 Web API OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="eb64c-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="eb64c-110">使用以下数据模型在 Web API 项目中，我们将创建单一实例：</span><span class="sxs-lookup"><span data-stu-id="eb64c-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![数据模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="eb64c-112">名为单一实例`Umbrella`将根据类型来定义`Company`，和实体集命名`Employees`将基于类型定义`Employee`。</span><span class="sxs-lookup"><span data-stu-id="eb64c-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="eb64c-113">可以从下载本教程中使用的解决方案[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)。</span><span class="sxs-lookup"><span data-stu-id="eb64c-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="eb64c-114">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="eb64c-114">Define the data model</span></span>

1. <span data-ttu-id="eb64c-115">定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="eb64c-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="eb64c-116">生成基于 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="eb64c-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="eb64c-117">在这里，`builder.Singleton<Company>("Umbrella")`告知模型生成器来创建名为单一实例`Umbrella`EDM 模型中。</span><span class="sxs-lookup"><span data-stu-id="eb64c-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="eb64c-118">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="eb64c-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="eb64c-119">从元数据中我们可以看到，导航属性`Company`中`Employees`实体集绑定到单一实例`Umbrella`。</span><span class="sxs-lookup"><span data-stu-id="eb64c-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="eb64c-120">会自动完成绑定`ODataConventionModelBuilder`，因为仅`Umbrella`具有`Company`类型。</span><span class="sxs-lookup"><span data-stu-id="eb64c-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="eb64c-121">如果在模型中存在任何多义性，可以使用`HasSingletonBinding`显式将一个导航属性绑定到单一实例;`HasSingletonBinding`具有相同的效果与使用`Singleton`CLR 类型定义中的属性：</span><span class="sxs-lookup"><span data-stu-id="eb64c-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="eb64c-122">定义单一实例控制器</span><span class="sxs-lookup"><span data-stu-id="eb64c-122">Define the singleton controller</span></span>

<span data-ttu-id="eb64c-123">单一实例控制器从与 EntitySet 控制器类似的继承`ODataController`，并单独控制器名称应为`[singletonName]Controller`。</span><span class="sxs-lookup"><span data-stu-id="eb64c-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="eb64c-124">若要处理不同类型的请求，操作需要进行预定义，在控制器中。</span><span class="sxs-lookup"><span data-stu-id="eb64c-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="eb64c-125">**属性路由**WebApi 2.2 中的默认情况下启用。</span><span class="sxs-lookup"><span data-stu-id="eb64c-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="eb64c-126">例如，若要定义要处理查询的操作`Revenue`从`Company`使用属性路由中，使用以下：</span><span class="sxs-lookup"><span data-stu-id="eb64c-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="eb64c-127">如果您不愿意来定义每个操作的属性，只需定义按照你的操作[OData 路由约定](../odata-routing-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="eb64c-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="eb64c-128">由于密钥不需要查询单一实例，单独控制器中定义的操作是从 entityset 控制器中定义的操作略有不同。</span><span class="sxs-lookup"><span data-stu-id="eb64c-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="eb64c-129">有关参考，下面列出了每个操作定义中的单一实例控制器中的方法签名。</span><span class="sxs-lookup"><span data-stu-id="eb64c-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="eb64c-130">基本上，这是所有需要在服务端上执行操作。</span><span class="sxs-lookup"><span data-stu-id="eb64c-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="eb64c-131">[示例项目](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含的所有解决方案和演示如何使用单一实例的 OData 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="eb64c-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="eb64c-132">中的步骤生成客户端[创建 OData v4 客户端应用](create-an-odata-v4-client-app.md)。</span><span class="sxs-lookup"><span data-stu-id="eb64c-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="eb64c-133">.</span><span class="sxs-lookup"><span data-stu-id="eb64c-133">.</span></span> 

<span data-ttu-id="eb64c-134">*感谢您对 Leo Hu 这篇文章的原始内容。*</span><span class="sxs-lookup"><span data-stu-id="eb64c-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
