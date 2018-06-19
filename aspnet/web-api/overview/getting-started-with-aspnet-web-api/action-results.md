---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: 操作会导致 Web API 2 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/03/2014
ms.topic: article
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: d0db5c6d45020861d7295ab1db989caee525fff9
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28036461"
---
<a name="action-results-in-web-api-2"></a><span data-ttu-id="784dd-102">Web API 2 中的操作结果</span><span class="sxs-lookup"><span data-stu-id="784dd-102">Action Results in Web API 2</span></span>
====================
<span data-ttu-id="784dd-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="784dd-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="784dd-104">本主题介绍如何 ASP.NET Web API 将返回的值转换成一条 HTTP 响应消息的控制器操作从。</span><span class="sxs-lookup"><span data-stu-id="784dd-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="784dd-105">Web API 控制器操作可以返回以下任一项：</span><span class="sxs-lookup"><span data-stu-id="784dd-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="784dd-106">void</span><span class="sxs-lookup"><span data-stu-id="784dd-106">void</span></span>
2. <span data-ttu-id="784dd-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="784dd-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="784dd-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="784dd-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="784dd-109">某些其他类型</span><span class="sxs-lookup"><span data-stu-id="784dd-109">Some other type</span></span>

<span data-ttu-id="784dd-110">具体取决于以下哪种返回时，Web API 使用另一种机制来创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="784dd-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="784dd-111">返回类型</span><span class="sxs-lookup"><span data-stu-id="784dd-111">Return type</span></span> | <span data-ttu-id="784dd-112">Web API 如何创建响应</span><span class="sxs-lookup"><span data-stu-id="784dd-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="784dd-113">void</span><span class="sxs-lookup"><span data-stu-id="784dd-113">void</span></span> | <span data-ttu-id="784dd-114">返回空 204 （无内容）</span><span class="sxs-lookup"><span data-stu-id="784dd-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="784dd-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="784dd-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="784dd-116">将转换直接为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="784dd-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="784dd-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="784dd-117">**IHttpActionResult**</span></span> | <span data-ttu-id="784dd-118">调用**ExecuteAsync**创建**HttpResponseMessage**，然后将转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="784dd-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="784dd-119">其他类型</span><span class="sxs-lookup"><span data-stu-id="784dd-119">Other type</span></span> | <span data-ttu-id="784dd-120">将序列化的返回值写入到响应正文中;返回 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="784dd-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="784dd-121">本主题的其余部分介绍更多详细信息中的每个选项。</span><span class="sxs-lookup"><span data-stu-id="784dd-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="784dd-122">void</span><span class="sxs-lookup"><span data-stu-id="784dd-122">void</span></span>

<span data-ttu-id="784dd-123">如果返回类型为`void`，Web API 只返回状态代码 204 （无内容） 的空 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="784dd-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="784dd-124">示例控制器：</span><span class="sxs-lookup"><span data-stu-id="784dd-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="784dd-125">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="784dd-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="784dd-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="784dd-126">HttpResponseMessage</span></span>

<span data-ttu-id="784dd-127">如果操作返回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 将返回的值转换为 HTTP 响应消息中，直接使用的属性**HttpResponseMessage**要填充对象响应。</span><span class="sxs-lookup"><span data-stu-id="784dd-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="784dd-128">此选项提供了大量的响应消息上的控件。</span><span class="sxs-lookup"><span data-stu-id="784dd-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="784dd-129">例如，以下的控制器操作设置的缓存控制标头。</span><span class="sxs-lookup"><span data-stu-id="784dd-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="784dd-130">响应：</span><span class="sxs-lookup"><span data-stu-id="784dd-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="784dd-131">如果传递到的域模型**CreateResponse**方法时，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)要序列化的模型写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="784dd-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="784dd-132">Web API 使用 Accept 标头在请求中选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="784dd-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="784dd-133">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="784dd-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="784dd-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="784dd-134">IHttpActionResult</span></span>

<span data-ttu-id="784dd-135">**IHttpActionResult** Web API 2 中引入了接口。</span><span class="sxs-lookup"><span data-stu-id="784dd-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="784dd-136">从根本上来说，它定义**HttpResponseMessage**工厂。</span><span class="sxs-lookup"><span data-stu-id="784dd-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="784dd-137">以下是使用的某些优点**IHttpActionResult**接口：</span><span class="sxs-lookup"><span data-stu-id="784dd-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="784dd-138">简化了[单元测试](../testing-and-debugging/unit-testing-controllers-in-web-api.md)你的控制器。</span><span class="sxs-lookup"><span data-stu-id="784dd-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="784dd-139">将移动到单独的类创建 HTTP 响应的常见逻辑。</span><span class="sxs-lookup"><span data-stu-id="784dd-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="784dd-140">通过隐藏构造响应的低级别的详细信息会更清晰、 控制器操作的意图。</span><span class="sxs-lookup"><span data-stu-id="784dd-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="784dd-141">**IHttpActionResult**包含单个方法**ExecuteAsync**，这将以异步方式创建**HttpResponseMessage**实例。</span><span class="sxs-lookup"><span data-stu-id="784dd-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="784dd-142">如果控制器操作返回**IHttpActionResult**，Web API 调用**ExecuteAsync**方法来创建**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="784dd-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="784dd-143">然后它将转换**HttpResponseMessage**到 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="784dd-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="784dd-144">下面是的简单实现**IHttpActionResult**创建纯文本响应：</span><span class="sxs-lookup"><span data-stu-id="784dd-144">Here is a simple implementaton of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="784dd-145">示例控制器操作：</span><span class="sxs-lookup"><span data-stu-id="784dd-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="784dd-146">响应：</span><span class="sxs-lookup"><span data-stu-id="784dd-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="784dd-147">更多时候，你将使用**IHttpActionResult**中定义的实现 **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 命名空间。</span><span class="sxs-lookup"><span data-stu-id="784dd-147">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="784dd-148">**ApiController**类定义返回这些内置操作结果的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="784dd-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="784dd-149">在下面的示例中，如果请求不匹配现有产品 ID，控制器调用[ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)创建 404 （未找到） 响应。</span><span class="sxs-lookup"><span data-stu-id="784dd-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="784dd-150">否则，控制器会调用[ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx)，这将创建一个 200 (OK) 响应，包含产品。</span><span class="sxs-lookup"><span data-stu-id="784dd-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="784dd-151">其他返回类型</span><span class="sxs-lookup"><span data-stu-id="784dd-151">Other Return Types</span></span>

<span data-ttu-id="784dd-152">对于所有其他返回类型，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)序列化的返回值。</span><span class="sxs-lookup"><span data-stu-id="784dd-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="784dd-153">Web API 将序列化的值写入到响应正文。</span><span class="sxs-lookup"><span data-stu-id="784dd-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="784dd-154">响应状态代码为 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="784dd-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="784dd-155">此方法的缺点是，不能直接返回错误代码，如 404。</span><span class="sxs-lookup"><span data-stu-id="784dd-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="784dd-156">但是，你可以引发**HttpResponseException**有关错误代码。</span><span class="sxs-lookup"><span data-stu-id="784dd-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="784dd-157">有关详细信息，请参阅[ASP.NET Web API 中的异常处理](../error-handling/exception-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="784dd-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="784dd-158">Web API 使用 Accept 标头在请求中选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="784dd-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="784dd-159">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="784dd-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="784dd-160">示例请求</span><span class="sxs-lookup"><span data-stu-id="784dd-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="784dd-161">示例响应：</span><span class="sxs-lookup"><span data-stu-id="784dd-161">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
