---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 创建单一实例 OData v4 中的使用 Web API 2.2 |Microsoft 文档
author: rick-anderson
description: 本主题演示如何定义中的 Web API 2.2 OData 终结点中的单一实例。
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 92c5056548b1e39defb28ac36f83b001dd108f5f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508206"
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="ed27d-103">创建单一实例 OData v4 中的使用 Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="ed27d-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="ed27d-104">通过 Zoe Luo</span><span class="sxs-lookup"><span data-stu-id="ed27d-104">by Zoe Luo</span></span>

> <span data-ttu-id="ed27d-105">传统上，如果它已封装在实体集可以仅访问实体。</span><span class="sxs-lookup"><span data-stu-id="ed27d-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="ed27d-106">但在 OData v4 提供单一实例和包含，这两种 WebAPI 2.2 支持的两个附加选项。</span><span class="sxs-lookup"><span data-stu-id="ed27d-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="ed27d-107">这篇文章演示如何在中的 Web API 2.2 OData 终结点中定义单一实例。</span><span class="sxs-lookup"><span data-stu-id="ed27d-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="ed27d-108">有关哪些单一实例，你将可以从使用它中受益的信息，请参阅[使用单一实例定义特殊实体](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ed27d-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="ed27d-109">若要在 Web API 中创建 OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="ed27d-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="ed27d-110">Web API 项目使用以下数据模型中，我们将创建单一实例：</span><span class="sxs-lookup"><span data-stu-id="ed27d-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![数据模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="ed27d-112">名为的单独`Umbrella`将基于类型定义`Company`，和的实体集命名`Employees`将基于类型定义`Employee`。</span><span class="sxs-lookup"><span data-stu-id="ed27d-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="ed27d-113">本教程中使用该解决方案可以从下载[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)。</span><span class="sxs-lookup"><span data-stu-id="ed27d-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="ed27d-114">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="ed27d-114">Define the data model</span></span>

1. <span data-ttu-id="ed27d-115">定义的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="ed27d-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="ed27d-116">生成基于 CLR 类型的 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="ed27d-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="ed27d-117">在这里，`builder.Singleton<Company>("Umbrella")`告知模型生成器来创建名为的单独`Umbrella`EDM 模型中。</span><span class="sxs-lookup"><span data-stu-id="ed27d-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="ed27d-118">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed27d-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="ed27d-119">从元数据中我们可以看到，导航属性`Company`中`Employees`实体集绑定到单一实例`Umbrella`。</span><span class="sxs-lookup"><span data-stu-id="ed27d-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="ed27d-120">会自动完成绑定`ODataConventionModelBuilder`，因为仅`Umbrella`具有`Company`类型。</span><span class="sxs-lookup"><span data-stu-id="ed27d-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="ed27d-121">如果模型中没有任何多义性，则可以使用`HasSingletonBinding`显式将导航属性绑定到单一实例;`HasSingletonBinding`具有相同的效果与使用`Singleton`CLR 类型定义中的属性：</span><span class="sxs-lookup"><span data-stu-id="ed27d-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="ed27d-122">定义的 singleton 控制器</span><span class="sxs-lookup"><span data-stu-id="ed27d-122">Define the singleton controller</span></span>

<span data-ttu-id="ed27d-123">EntitySet 控制器中，如继承自 singleton 控制器`ODataController`，和 singleton 控制器名称应为`[singletonName]Controller`。</span><span class="sxs-lookup"><span data-stu-id="ed27d-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="ed27d-124">若要处理不同类型的请求，操作都需要在控制器中预定义。</span><span class="sxs-lookup"><span data-stu-id="ed27d-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="ed27d-125">**属性路由**WebApi 2.2 中默认启用。</span><span class="sxs-lookup"><span data-stu-id="ed27d-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="ed27d-126">例如，若要定义要处理查询的操作`Revenue`从`Company`使用的属性路由，使用以下：</span><span class="sxs-lookup"><span data-stu-id="ed27d-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="ed27d-127">如果你不愿意来定义每个操作的属性，只需定义按照你操作[OData 路由约定](../odata-routing-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="ed27d-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="ed27d-128">由于不需要查询单一实例的密钥，则单独控制器中定义的操作中略有不同从 entityset 控制器中定义的操作。</span><span class="sxs-lookup"><span data-stu-id="ed27d-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="ed27d-129">作为参考，下面列出了在单独控制器中的每个操作定义的方法签名。</span><span class="sxs-lookup"><span data-stu-id="ed27d-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="ed27d-130">基本上，这是你需要在服务端上执行操作。</span><span class="sxs-lookup"><span data-stu-id="ed27d-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="ed27d-131">[示例项目](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含所有为解决方案和演示如何使用单独的 OData 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="ed27d-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="ed27d-132">客户端生成的中的步骤[创建 OData v4 客户端应用](create-an-odata-v4-client-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ed27d-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="ed27d-133">.</span><span class="sxs-lookup"><span data-stu-id="ed27d-133">.</span></span> 

<span data-ttu-id="ed27d-134">*到 Leo Hu 感谢这篇文章的原始内容。*</span><span class="sxs-lookup"><span data-stu-id="ed27d-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
