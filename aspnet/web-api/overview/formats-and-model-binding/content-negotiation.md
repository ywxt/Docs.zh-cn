---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: 内容协商 ASP.NET Web API 中的 |Microsoft Docs
author: MikeWasson
description: 介绍如何 ASP.NET Web API 实现 HTTP 内容协商。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/20/2012
ms.topic: article
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: c4e7a0c2601ca60f081876e83757997a2e920298
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368924"
---
<a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="2c97b-103">ASP.NET Web API 中的内容协商</span><span class="sxs-lookup"><span data-stu-id="2c97b-103">Content Negotiation in ASP.NET Web API</span></span>
====================
<span data-ttu-id="2c97b-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2c97b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2c97b-105">本指南介绍了 ASP.NET Web API 如何实现内容协商。</span><span class="sxs-lookup"><span data-stu-id="2c97b-105">This article describes how ASP.NET Web API implements content negotiation.</span></span>

<span data-ttu-id="2c97b-106">HTTP 规范 (RFC 2616) 定义为"有可用的多种表示形式时选择的最佳表示对于给定的响应的处理。"的内容协商</span><span class="sxs-lookup"><span data-stu-id="2c97b-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="2c97b-107">在 HTTP 内容协商的主要机制是这些请求标头：</span><span class="sxs-lookup"><span data-stu-id="2c97b-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="2c97b-108">**接受：** 哪些媒体类型是可接受的响应，如"application/json;"的"application/xml"或自定义媒体类型，如&quot;application/vnd.example+xml&quot;</span><span class="sxs-lookup"><span data-stu-id="2c97b-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="2c97b-109">**接受字符集：** 哪些字符集是可以接受的如 utf-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="2c97b-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="2c97b-110">**接受的编码：** 哪种内容编码是可以接受的例如 gzip。</span><span class="sxs-lookup"><span data-stu-id="2c97b-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="2c97b-111">**接受语言：** 首选的自然语言，例如"en-我们"。</span><span class="sxs-lookup"><span data-stu-id="2c97b-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="2c97b-112">服务器还可以查看在 HTTP 请求的其他部分。</span><span class="sxs-lookup"><span data-stu-id="2c97b-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="2c97b-113">例如，如果请求包含 X-请求-具有标头，指示 AJAX 请求，服务器可能默认为 JSON 没有 Accept 标头是否。</span><span class="sxs-lookup"><span data-stu-id="2c97b-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="2c97b-114">在本文中，我们将介绍 Web API 如何使用 Accept 和 Accept-charset 标头。</span><span class="sxs-lookup"><span data-stu-id="2c97b-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="2c97b-115">（在此期间，用于接受编码或接受语言没有内置支持。)</span><span class="sxs-lookup"><span data-stu-id="2c97b-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="2c97b-116">序列化</span><span class="sxs-lookup"><span data-stu-id="2c97b-116">Serialization</span></span>

<span data-ttu-id="2c97b-117">如果 Web API 控制器返回作为 CLR 类型的资源，管道将序列化为返回值，并将其写入到 HTTP 响应正文。</span><span class="sxs-lookup"><span data-stu-id="2c97b-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="2c97b-118">例如，考虑以下控制器操作：</span><span class="sxs-lookup"><span data-stu-id="2c97b-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="2c97b-119">客户端可能会发送此 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="2c97b-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="2c97b-120">在响应中，可能会发送服务器：</span><span class="sxs-lookup"><span data-stu-id="2c97b-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="2c97b-121">在此示例中，客户端请求的 JSON、 Javascript 或"任何"(\*/\*)。</span><span class="sxs-lookup"><span data-stu-id="2c97b-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="2c97b-122">服务器响应的 JSON 表示形式的`Product`对象。</span><span class="sxs-lookup"><span data-stu-id="2c97b-122">The server responsed with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="2c97b-123">请注意，在响应中的内容类型标头设置为&quot;应用程序 /json&quot;。</span><span class="sxs-lookup"><span data-stu-id="2c97b-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="2c97b-124">此外可以返回一个控制器**HttpResponseMessage**对象。</span><span class="sxs-lookup"><span data-stu-id="2c97b-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="2c97b-125">若要指定响应正文的 CLR 对象，调用**CreateResponse**扩展方法：</span><span class="sxs-lookup"><span data-stu-id="2c97b-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="2c97b-126">此选项可提供更好地控制响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2c97b-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="2c97b-127">可以设置的状态代码，添加 HTTP 标头，等等。</span><span class="sxs-lookup"><span data-stu-id="2c97b-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="2c97b-128">序列化该资源的对象称为*媒体格式化程序*。</span><span class="sxs-lookup"><span data-stu-id="2c97b-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="2c97b-129">媒体格式化程序派生自**MediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="2c97b-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="2c97b-130">Web API 提供媒体格式化程序的 XML 和 JSON，并且可以创建自定义格式化程序，以支持其他媒体类型。</span><span class="sxs-lookup"><span data-stu-id="2c97b-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="2c97b-131">有关编写自定义格式化程序的信息，请参阅[媒体格式化程序](media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="2c97b-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="2c97b-132">如何在内容协商的工作原理</span><span class="sxs-lookup"><span data-stu-id="2c97b-132">How Content Negotiation Works</span></span>

<span data-ttu-id="2c97b-133">首先，获取管道**IContentNegotiator**服务从**HttpConfiguration**对象。</span><span class="sxs-lookup"><span data-stu-id="2c97b-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="2c97b-134">它还可以获取从媒体格式化程序的列表**HttpConfiguration.Formatters**集合。</span><span class="sxs-lookup"><span data-stu-id="2c97b-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="2c97b-135">接下来，调用管道**IContentNegotiatior.Negotiate**、 传入：</span><span class="sxs-lookup"><span data-stu-id="2c97b-135">Next, the pipeline calls **IContentNegotiatior.Negotiate**, passing in:</span></span>

- <span data-ttu-id="2c97b-136">要序列化的对象类型</span><span class="sxs-lookup"><span data-stu-id="2c97b-136">The type of object to serialize</span></span>
- <span data-ttu-id="2c97b-137">媒体格式化程序的集合</span><span class="sxs-lookup"><span data-stu-id="2c97b-137">The collection of media formatters</span></span>
- <span data-ttu-id="2c97b-138">HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="2c97b-138">The HTTP request</span></span>

<span data-ttu-id="2c97b-139">**Negotiate**方法将返回两条信息：</span><span class="sxs-lookup"><span data-stu-id="2c97b-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="2c97b-140">若要使用的格式化程序</span><span class="sxs-lookup"><span data-stu-id="2c97b-140">Which formatter to use</span></span>
- <span data-ttu-id="2c97b-141">响应的媒体类型</span><span class="sxs-lookup"><span data-stu-id="2c97b-141">The media type for the response</span></span>

<span data-ttu-id="2c97b-142">如果不找到任何格式化程序，则**Negotiate**方法将返回**null**，和客户端收到 HTTP 错误 406 （不可接受）。</span><span class="sxs-lookup"><span data-stu-id="2c97b-142">If no formatter is found, the **Negotiate** method returns **null**, and the client recevies HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="2c97b-143">下面的代码演示如何在控制器可直接调用内容协商：</span><span class="sxs-lookup"><span data-stu-id="2c97b-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="2c97b-144">此代码等同于管道自动执行。</span><span class="sxs-lookup"><span data-stu-id="2c97b-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="2c97b-145">默认内容协商者</span><span class="sxs-lookup"><span data-stu-id="2c97b-145">Default Content Negotiator</span></span>

<span data-ttu-id="2c97b-146">**为 DefaultContentNegotiator**类提供的默认实现**IContentNegotiator**。</span><span class="sxs-lookup"><span data-stu-id="2c97b-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="2c97b-147">它使用多个条件来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2c97b-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="2c97b-148">首先，格式化程序必须能够序列化该类型。</span><span class="sxs-lookup"><span data-stu-id="2c97b-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="2c97b-149">这通过调用验证**MediaTypeFormatter.CanWriteType**。</span><span class="sxs-lookup"><span data-stu-id="2c97b-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="2c97b-150">接下来，内容协商者会查看每个格式化程序，并计算结果的 HTTP 请求与匹配的程度。</span><span class="sxs-lookup"><span data-stu-id="2c97b-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="2c97b-151">若要评估匹配，内容协商者查看两件事上个格式化程序：</span><span class="sxs-lookup"><span data-stu-id="2c97b-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="2c97b-152">**SupportedMediaTypes**集合，其中包含受支持的媒体类型的列表。</span><span class="sxs-lookup"><span data-stu-id="2c97b-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="2c97b-153">内容协商者尝试匹配此列表中对请求的 Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="2c97b-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="2c97b-154">请注意，Accept 标头可以包含范围。</span><span class="sxs-lookup"><span data-stu-id="2c97b-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="2c97b-155">例如，"text/plain"是文本的匹配项 /\*或\* / \*。</span><span class="sxs-lookup"><span data-stu-id="2c97b-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="2c97b-156">**MediaTypeMappings**集合，其中包含一系列**MediaTypeMapping**对象。</span><span class="sxs-lookup"><span data-stu-id="2c97b-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="2c97b-157">**MediaTypeMapping**类提供的 HTTP 请求匹配的媒体类型的泛型方法。</span><span class="sxs-lookup"><span data-stu-id="2c97b-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="2c97b-158">例如，它可以将自定义 HTTP 标头映射到某个特定媒体类型。</span><span class="sxs-lookup"><span data-stu-id="2c97b-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="2c97b-159">如果有多个匹配，与最高的质量因子 wins 的匹配项。</span><span class="sxs-lookup"><span data-stu-id="2c97b-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="2c97b-160">例如：</span><span class="sxs-lookup"><span data-stu-id="2c97b-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="2c97b-161">在此示例中，应用程序 /json 具有值为 1.0，隐式的质量因子，因此它对应用程序/xml 是首选。</span><span class="sxs-lookup"><span data-stu-id="2c97b-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="2c97b-162">如果不找到任何匹配项，内容协商者尝试匹配上的媒体类型的请求正文中，如果有的话。</span><span class="sxs-lookup"><span data-stu-id="2c97b-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="2c97b-163">例如，如果请求包含 JSON 数据，为 JSON 格式化程序将查找的内容协商者。</span><span class="sxs-lookup"><span data-stu-id="2c97b-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="2c97b-164">如果仍有没有匹配项，内容协商者只需选择可以序列化该类型的第一个格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2c97b-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="2c97b-165">选择一种字符编码</span><span class="sxs-lookup"><span data-stu-id="2c97b-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="2c97b-166">内容协商选择格式化程序后，选择通过查看的最佳字符编码**SupportedEncodings**属性格式化程序，并将其与请求中的 Accept-charset 标头匹配 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="2c97b-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
