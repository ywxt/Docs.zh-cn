---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2 中的媒体格式化程序 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: 1cb1c7e0f832a0a0160276fbd41facc017e2ae3e
ms.sourcegitcommit: 50d40c83fa641d283c097f986dde5341ebe1b44c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
ms.locfileid: "34452595"
---
<a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="0248e-102">ASP.NET Web API 2 中的媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="0248e-102">Media Formatters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="0248e-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0248e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0248e-104">本教程演示如何在 ASP.NET Web API 中支持的其他媒体格式。</span><span class="sxs-lookup"><span data-stu-id="0248e-104">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="0248e-105">Internet 媒体类型</span><span class="sxs-lookup"><span data-stu-id="0248e-105">Internet Media Types</span></span>

<span data-ttu-id="0248e-106">媒体类型，也称为 MIME 类型，标识一段数据的格式。</span><span class="sxs-lookup"><span data-stu-id="0248e-106">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="0248e-107">在 HTTP，媒体类型描述消息正文的格式。</span><span class="sxs-lookup"><span data-stu-id="0248e-107">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="0248e-108">媒体类型由两个字符串、 类型和子类型组成。</span><span class="sxs-lookup"><span data-stu-id="0248e-108">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="0248e-109">例如：</span><span class="sxs-lookup"><span data-stu-id="0248e-109">For example:</span></span>

- <span data-ttu-id="0248e-110">文本/html</span><span class="sxs-lookup"><span data-stu-id="0248e-110">text/html</span></span>
- <span data-ttu-id="0248e-111">图像/png</span><span class="sxs-lookup"><span data-stu-id="0248e-111">image/png</span></span>
- <span data-ttu-id="0248e-112">application/json</span><span class="sxs-lookup"><span data-stu-id="0248e-112">application/json</span></span>

<span data-ttu-id="0248e-113">当 HTTP 消息包含一个实体正文时，内容类型标头指定消息正文的格式。</span><span class="sxs-lookup"><span data-stu-id="0248e-113">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="0248e-114">这指示接收方如何分析消息正文的内容。</span><span class="sxs-lookup"><span data-stu-id="0248e-114">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="0248e-115">例如，如果 HTTP 响应包含 PNG 图像，响应可能包含以下标头。</span><span class="sxs-lookup"><span data-stu-id="0248e-115">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="0248e-116">当客户端发送请求消息时，它可以包括 Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="0248e-116">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="0248e-117">Accept 标头指示的服务器的媒体类型的客户端想要从服务器。</span><span class="sxs-lookup"><span data-stu-id="0248e-117">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="0248e-118">例如：</span><span class="sxs-lookup"><span data-stu-id="0248e-118">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="0248e-119">此标头指示服务器在客户端希望 HTML、 XHTML 或 XML。</span><span class="sxs-lookup"><span data-stu-id="0248e-119">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="0248e-120">媒体类型确定 Web API 如何序列化和反序列化 HTTP 消息正文。</span><span class="sxs-lookup"><span data-stu-id="0248e-120">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="0248e-121">Web API 有对 XML、 JSON、 BSON 和窗体编码形式数据的内置支持，并且你可以通过编写支持其他媒体类型*媒体格式化程序*。</span><span class="sxs-lookup"><span data-stu-id="0248e-121">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="0248e-122">若要创建媒体格式化程序，派生自这些类之一：</span><span class="sxs-lookup"><span data-stu-id="0248e-122">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="0248e-123">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0248e-123">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="0248e-124">此类使用的异步读取和写入方法。</span><span class="sxs-lookup"><span data-stu-id="0248e-124">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="0248e-125">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0248e-125">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="0248e-126">此类派生自**MediaTypeFormatter**但使用 sychronous 读/写方法。</span><span class="sxs-lookup"><span data-stu-id="0248e-126">This class derives from **MediaTypeFormatter** but uses sychronous read/write methods.</span></span>

<span data-ttu-id="0248e-127">派生自**BufferedMediaTypeFormatter**是更简单，因为没有异步代码，但它还意味着在 I/O 期间可以阻止调用线程。</span><span class="sxs-lookup"><span data-stu-id="0248e-127">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="0248e-128">示例： 创建 CSV 媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="0248e-128">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="0248e-129">下面的示例演示可以序列化到逗号分隔值 (CSV) 格式的产品对象的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="0248e-129">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="0248e-130">此示例使用在本教程中定义的产品类型[创建该支持 CRUD 操作的 Web API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="0248e-130">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="0248e-131">下面是该对象定义的产品：</span><span class="sxs-lookup"><span data-stu-id="0248e-131">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="0248e-132">若要实现一个 CSV 格式化程序，定义派生自类**BufferedMediaTypeFormater**:</span><span class="sxs-lookup"><span data-stu-id="0248e-132">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormater**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="0248e-133">在构造函数中，添加格式化程序支持的媒体类型。</span><span class="sxs-lookup"><span data-stu-id="0248e-133">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="0248e-134">在此示例中，格式化程序支持单个媒体类型，&quot;文本/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="0248e-134">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="0248e-135">重写**CanWriteType**方法，以指示该类型的格式化程序可以序列化：</span><span class="sxs-lookup"><span data-stu-id="0248e-135">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="0248e-136">在此示例中，格式化程序可以序列化为单个`Product`对象的集合以及`Product`对象。</span><span class="sxs-lookup"><span data-stu-id="0248e-136">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="0248e-137">同样，重写**CanReadType**方法，以指示该类型的格式化程序可以反序列化。</span><span class="sxs-lookup"><span data-stu-id="0248e-137">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="0248e-138">在此示例中，格式化程序不支持反序列化，因此此方法只返回**false**。</span><span class="sxs-lookup"><span data-stu-id="0248e-138">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="0248e-139">最后，重写**WriteToStream**方法。</span><span class="sxs-lookup"><span data-stu-id="0248e-139">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="0248e-140">此方法序列化类型写入流。</span><span class="sxs-lookup"><span data-stu-id="0248e-140">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="0248e-141">如果你的格式化程序支持反序列化，还重写**ReadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="0248e-141">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="0248e-142">将媒体格式化程序添加到 Web API 管道</span><span class="sxs-lookup"><span data-stu-id="0248e-142">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="0248e-143">若要添加的媒体类型到 Web API 管道的格式化程序，使用**格式化程序**属性**HttpConfiguration**对象。</span><span class="sxs-lookup"><span data-stu-id="0248e-143">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="0248e-144">字符编码</span><span class="sxs-lookup"><span data-stu-id="0248e-144">Character Encodings</span></span>

<span data-ttu-id="0248e-145">（可选） 媒体格式化程序可以支持多个的字符编码，例如 utf-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="0248e-145">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="0248e-146">在构造函数中，添加一个或多个[System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx)类型**SupportedEncodings**集合。</span><span class="sxs-lookup"><span data-stu-id="0248e-146">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="0248e-147">将编码第一个默认值。</span><span class="sxs-lookup"><span data-stu-id="0248e-147">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="0248e-148">在**WriteToStream**和**ReadFromStream**方法，调用[MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx)选择首选的字符编码。</span><span class="sxs-lookup"><span data-stu-id="0248e-148">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="0248e-149">此方法与匹配的请求标头针对支持编码的列表。</span><span class="sxs-lookup"><span data-stu-id="0248e-149">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="0248e-150">使用返回**编码**时，你可以读取或写入从流：</span><span class="sxs-lookup"><span data-stu-id="0248e-150">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
