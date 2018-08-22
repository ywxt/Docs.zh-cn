---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型验证 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/20/2012
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 611a6466e160387592df678b3b8556625ff8e234
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830455"
---
<a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="b6e88-102">ASP.NET Web API 中的模型验证</span><span class="sxs-lookup"><span data-stu-id="b6e88-102">Model Validation in ASP.NET Web API</span></span>
====================
<span data-ttu-id="b6e88-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b6e88-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b6e88-104">当客户端将数据发送到 web API 时，通常要执行任何处理之前验证数据。</span><span class="sxs-lookup"><span data-stu-id="b6e88-104">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> <span data-ttu-id="b6e88-105">本文介绍如何对模型进行批注、 使用批注以进行数据验证和处理你的 web API 中的验证错误。</span><span class="sxs-lookup"><span data-stu-id="b6e88-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span>

## <a name="data-annotations"></a><span data-ttu-id="b6e88-106">数据注释</span><span class="sxs-lookup"><span data-stu-id="b6e88-106">Data Annotations</span></span>

<span data-ttu-id="b6e88-107">在 ASP.NET Web API 中，可以使用中的属性[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间来对模型设置属性的验证规则。</span><span class="sxs-lookup"><span data-stu-id="b6e88-107">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="b6e88-108">请考虑以下模型：</span><span class="sxs-lookup"><span data-stu-id="b6e88-108">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="b6e88-109">如果已在 ASP.NET MVC 中使用模型验证，这应该很熟悉。</span><span class="sxs-lookup"><span data-stu-id="b6e88-109">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="b6e88-110">**所需**属性指出`Name`属性不能为 null。</span><span class="sxs-lookup"><span data-stu-id="b6e88-110">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="b6e88-111">**范围**属性指出`Weight`必须是介于 0 和 999 之间。</span><span class="sxs-lookup"><span data-stu-id="b6e88-111">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="b6e88-112">假设客户端发送 POST 请求，其中以下 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="b6e88-112">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="b6e88-113">您可以看到客户端未包括`Name`属性，它被标记为必需。</span><span class="sxs-lookup"><span data-stu-id="b6e88-113">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="b6e88-114">当 Web API 将转换为 JSON`Product`实例，它会验证`Product`针对验证特性。</span><span class="sxs-lookup"><span data-stu-id="b6e88-114">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="b6e88-115">在你的控制器操作，可以检查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="b6e88-115">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="b6e88-116">模型验证不保证客户端数据的安全。</span><span class="sxs-lookup"><span data-stu-id="b6e88-116">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="b6e88-117">其他验证可能需要在应用程序的其他层中。</span><span class="sxs-lookup"><span data-stu-id="b6e88-117">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="b6e88-118">（例如，数据层可能会强制实施外键约束。）本教程[使用实体框架使用 Web API](../data/using-web-api-with-entity-framework/part-1.md)探讨了其中一些问题。</span><span class="sxs-lookup"><span data-stu-id="b6e88-118">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="b6e88-119">**"未得到充分发布"**： 客户端将省略某些属性会发生未得到充分的发布。</span><span class="sxs-lookup"><span data-stu-id="b6e88-119">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="b6e88-120">例如，假设客户端发送以下：</span><span class="sxs-lookup"><span data-stu-id="b6e88-120">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="b6e88-121">在这里，客户端未指定值`Price`或`Weight`。</span><span class="sxs-lookup"><span data-stu-id="b6e88-121">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="b6e88-122">JSON 格式化程序将分配默认值为 0 到缺少的属性。</span><span class="sxs-lookup"><span data-stu-id="b6e88-122">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="b6e88-123">模型状态无效，因为零是这些属性的有效值。</span><span class="sxs-lookup"><span data-stu-id="b6e88-123">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="b6e88-124">这是否是一个问题取决于你的方案。</span><span class="sxs-lookup"><span data-stu-id="b6e88-124">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="b6e88-125">例如，在更新操作中，可能想要区分"零"和"未设置。"</span><span class="sxs-lookup"><span data-stu-id="b6e88-125">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="b6e88-126">若要强制客户端可以设置一个值，使该属性可以为 null，并且已设置**所需**属性：</span><span class="sxs-lookup"><span data-stu-id="b6e88-126">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="b6e88-127">**"过度发布"**： 客户端还可以将发送*详细*比预期的数据。</span><span class="sxs-lookup"><span data-stu-id="b6e88-127">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="b6e88-128">例如：</span><span class="sxs-lookup"><span data-stu-id="b6e88-128">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="b6e88-129">在这里，JSON 包括中不存在的属性 ("Color")`Product`模型。</span><span class="sxs-lookup"><span data-stu-id="b6e88-129">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="b6e88-130">在这种情况下，JSON 格式化程序只需将忽略此值。</span><span class="sxs-lookup"><span data-stu-id="b6e88-130">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="b6e88-131">（XML 格式化程序执行相同操作。）如果您的模型具有你想要为只读属性，过度提交会导致问题。</span><span class="sxs-lookup"><span data-stu-id="b6e88-131">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="b6e88-132">例如：</span><span class="sxs-lookup"><span data-stu-id="b6e88-132">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="b6e88-133">你不希望用户更新`IsAdmin`属性并将自己提升为管理员 ！</span><span class="sxs-lookup"><span data-stu-id="b6e88-133">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="b6e88-134">最安全的策略是使用与客户端可以发送完全匹配的模型类：</span><span class="sxs-lookup"><span data-stu-id="b6e88-134">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="b6e88-135">Brad Wilson 的博客文章"[输入验证 vs。ASP.NET MVC 中的模型验证](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"具有未得到充分的发布和过度提交了适当探讨。</span><span class="sxs-lookup"><span data-stu-id="b6e88-135">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="b6e88-136">虽然文章是有关 ASP.NET MVC 2，但是是仍然与 Web API 相关的问题。</span><span class="sxs-lookup"><span data-stu-id="b6e88-136">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="b6e88-137">处理验证错误</span><span class="sxs-lookup"><span data-stu-id="b6e88-137">Handling Validation Errors</span></span>

<span data-ttu-id="b6e88-138">Web API 不会自动返回错误到客户端验证失败时。</span><span class="sxs-lookup"><span data-stu-id="b6e88-138">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="b6e88-139">负责检查模型状态并做出相应的响应的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b6e88-139">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="b6e88-140">此外可以创建一个操作筛选器来调用控制器操作之前检查模型状态。</span><span class="sxs-lookup"><span data-stu-id="b6e88-140">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="b6e88-141">下面的代码演示一个示例：</span><span class="sxs-lookup"><span data-stu-id="b6e88-141">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="b6e88-142">如果模型验证失败，此筛选器将返回 HTTP 响应，其中包含验证错误。</span><span class="sxs-lookup"><span data-stu-id="b6e88-142">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="b6e88-143">在这种情况下，不会调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b6e88-143">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="b6e88-144">若要将此筛选器应用于所有的 Web API 控制器，将添加到筛选器的实例**HttpConfiguration.Filters**在配置期间的集合：</span><span class="sxs-lookup"><span data-stu-id="b6e88-144">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="b6e88-145">另一个选项是设置筛选器作为特性上各个控制器或控制器操作：</span><span class="sxs-lookup"><span data-stu-id="b6e88-145">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
