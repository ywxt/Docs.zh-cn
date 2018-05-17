---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: 模型 ASP.NET Web API 中的验证 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/20/2012
ms.topic: article
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 409a91eceb8baa48a7dded1b850d59a27cec2c60
ms.sourcegitcommit: 5ae0c125ee3bbd324edef3818d1d160f4dd84602
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
<a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="5d8cf-102">ASP.NET Web API 中的模型验证</span><span class="sxs-lookup"><span data-stu-id="5d8cf-102">Model Validation in ASP.NET Web API</span></span>
====================
<span data-ttu-id="5d8cf-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5d8cf-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5d8cf-104">当客户端将数据发送到你的 web API 时，通常你想要在进行任何处理之前验证数据。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-104">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> <span data-ttu-id="5d8cf-105">这篇文章演示如何添加批注您的模型、 批注用于数据验证和处理你的 web API 中的验证错误。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span>

## <a name="data-annotations"></a><span data-ttu-id="5d8cf-106">数据注释</span><span class="sxs-lookup"><span data-stu-id="5d8cf-106">Data Annotations</span></span>

<span data-ttu-id="5d8cf-107">在 ASP.NET Web API，你可以使用中的属性[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间在您的模型上设置属性的验证规则。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-107">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="5d8cf-108">请考虑以下模型：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-108">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="5d8cf-109">如果在 ASP.NET MVC 中使用了模型验证，这应该熟悉。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-109">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="5d8cf-110">**所需**属性告知`Name`属性不得为空。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-110">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="5d8cf-111">**范围**属性告知`Weight`必须是介于 0 和 999 之间。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-111">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="5d8cf-112">假设客户端发送 POST 请求的以下 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-112">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="5d8cf-113">你可以看到客户端未包括`Name`属性，它被标记为必需。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-113">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="5d8cf-114">当 Web API 将转换为 JSON`Product`实例，它会验证`Product`针对验证属性。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-114">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="5d8cf-115">在你的控制器操作，你可以检查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-115">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="5d8cf-116">模型验证不保证客户端数据的安全。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-116">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="5d8cf-117">应用程序的其他层中，可能需要其他验证。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-117">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="5d8cf-118">（例如，数据层可能会强制执行外键约束。）本教程[使用实体框架使用 Web API](../data/using-web-api-with-entity-framework/part-1.md)探讨一些这些问题。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-118">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="5d8cf-119">**"未得到充分发布"**： 客户端省略了某些属性时发生未得到充分发布。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-119">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="5d8cf-120">例如，假设客户端发送以下：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-120">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="5d8cf-121">在这里，客户端未指定值`Price`或`Weight`。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-121">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="5d8cf-122">JSON 格式化程序将分配默认值为 0 到缺少的属性。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-122">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="5d8cf-123">模型状态无效，因为这些属性的有效值是零。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-123">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="5d8cf-124">这是否是一个问题取决于你的方案。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-124">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="5d8cf-125">例如，在更新操作中，你可能想要区分"零"和"未设置。"</span><span class="sxs-lookup"><span data-stu-id="5d8cf-125">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="5d8cf-126">若要强制客户端可以设置一个值，将该属性可以为 null，并且已设置**所需**属性：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-126">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="5d8cf-127">**"过多发布"**： 客户端还可以发送*详细*比你预期的数据。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-127">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="5d8cf-128">例如：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-128">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="5d8cf-129">在这里，JSON 包括中不存在的属性 ("Color")`Product`模型。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-129">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="5d8cf-130">在这种情况下，JSON 格式化程序只需将忽略此值。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-130">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="5d8cf-131">（XML 格式化程序执行相同的操作。）如果你的模型具有你想要为只读的属性，过度发布会导致问题。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-131">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="5d8cf-132">例如：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-132">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="5d8cf-133">你不希望用户更新`IsAdmin`属性并将自身提升至管理员 ！</span><span class="sxs-lookup"><span data-stu-id="5d8cf-133">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="5d8cf-134">安全策略是使用完全匹配什么则允许客户端发送一个模型类：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-134">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="5d8cf-135">Brad wilson 制作的博客文章"[输入验证 vs。模型中的 ASP.NET MVC 的验证](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"具有未得到充分发布和过度发布的良好讨论。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-135">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="5d8cf-136">尽管有关 ASP.NET MVC 2 是 post，但问题仍然是相关到 Web API。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-136">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="5d8cf-137">处理验证错误</span><span class="sxs-lookup"><span data-stu-id="5d8cf-137">Handling Validation Errors</span></span>

<span data-ttu-id="5d8cf-138">Web API 不会自动返回错误客户端验证失败时。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-138">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="5d8cf-139">负责检查模型状态和做出相应响应的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-139">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="5d8cf-140">你还可以创建一个可调用的控制器操作之前检查模型状态的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-140">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="5d8cf-141">下面的代码演示一个示例：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-141">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="5d8cf-142">如果模型验证失败，则此筛选器将返回包含验证错误的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-142">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="5d8cf-143">在这种情况下，不调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="5d8cf-143">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="5d8cf-144">若要将此筛选器应用于所有的 Web API 控制器，将添加到筛选器的实例**HttpConfiguration.Filters**在配置期间的集合：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-144">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="5d8cf-145">另一个选项是在各个控制器或控制器操作上设置作为特性的筛选器：</span><span class="sxs-lookup"><span data-stu-id="5d8cf-145">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
