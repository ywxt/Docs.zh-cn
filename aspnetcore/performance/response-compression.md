---
title: "有关 ASP.NET 核心响应压缩中间件"
author: guardrex
description: "了解如何响应压缩以及如何在 ASP.NET Core 应用中使用响应压缩中间件。"
manager: wpickett
ms.author: riande
ms.date: 08/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/response-compression
ms.openlocfilehash: eae51e74c7f2b2f038638c765d4e833a1d9b1232
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="response-compression-middleware-for-aspnet-core"></a><span data-ttu-id="fbc32-103">有关 ASP.NET 核心响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="fbc32-103">Response Compression Middleware for ASP.NET Core</span></span>

<span data-ttu-id="fbc32-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="fbc32-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="fbc32-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="fbc32-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="fbc32-106">网络带宽是有限的资源。</span><span class="sxs-lookup"><span data-stu-id="fbc32-106">Network bandwidth is a limited resource.</span></span> <span data-ttu-id="fbc32-107">通常减小响应的大小将通常显著增加应用的响应能力。</span><span class="sxs-lookup"><span data-stu-id="fbc32-107">Reducing the size of the response usually increases the responsiveness of an app, often dramatically.</span></span> <span data-ttu-id="fbc32-108">减小负载大小的一种方法是压缩应用的响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-108">One way to reduce payload sizes is to compress an app's responses.</span></span>

## <a name="when-to-use-response-compression-middleware"></a><span data-ttu-id="fbc32-109">何时使用响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="fbc32-109">When to use Response Compression Middleware</span></span>
<span data-ttu-id="fbc32-110">使用在 IIS、 Apache 或 Nginx 基于服务器的响应压缩技术。</span><span class="sxs-lookup"><span data-stu-id="fbc32-110">Use server-based response compression technologies in IIS, Apache, or Nginx.</span></span> <span data-ttu-id="fbc32-111">中间件的性能可能不会与匹配服务器模块。</span><span class="sxs-lookup"><span data-stu-id="fbc32-111">The performance of the middleware probably won't match that of the server modules.</span></span> <span data-ttu-id="fbc32-112">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)和[Kestrel](xref:fundamentals/servers/kestrel)当前不提供内置的压缩支持。</span><span class="sxs-lookup"><span data-stu-id="fbc32-112">[HTTP.sys server](xref:fundamentals/servers/httpsys) and [Kestrel](xref:fundamentals/servers/kestrel) don't currently offer built-in compression support.</span></span>

<span data-ttu-id="fbc32-113">当你时，请使用响应压缩中间件：</span><span class="sxs-lookup"><span data-stu-id="fbc32-113">Use Response Compression Middleware when you're:</span></span>

* <span data-ttu-id="fbc32-114">无法使用以下基于服务器的压缩技术：</span><span class="sxs-lookup"><span data-stu-id="fbc32-114">Unable to use the following server-based compression technologies:</span></span>
  * [<span data-ttu-id="fbc32-115">IIS 动态压缩模块</span><span class="sxs-lookup"><span data-stu-id="fbc32-115">IIS Dynamic Compression module</span></span>](https://www.iis.net/overview/reliability/dynamiccachingandcompression)
  * [<span data-ttu-id="fbc32-116">Apache mod_deflate 模块</span><span class="sxs-lookup"><span data-stu-id="fbc32-116">Apache mod_deflate module</span></span>](http://httpd.apache.org/docs/current/mod/mod_deflate.html)
  * [<span data-ttu-id="fbc32-117">Nginx 压缩和解压缩</span><span class="sxs-lookup"><span data-stu-id="fbc32-117">Nginx Compression and Decompression</span></span>](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)
* <span data-ttu-id="fbc32-118">直接在上托管：</span><span class="sxs-lookup"><span data-stu-id="fbc32-118">Hosting directly on:</span></span>
  * <span data-ttu-id="fbc32-119">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)(以前称为[WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="fbc32-119">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>
  * [<span data-ttu-id="fbc32-120">Kestrel</span><span class="sxs-lookup"><span data-stu-id="fbc32-120">Kestrel</span></span>](xref:fundamentals/servers/kestrel)

## <a name="response-compression"></a><span data-ttu-id="fbc32-121">响应压缩</span><span class="sxs-lookup"><span data-stu-id="fbc32-121">Response compression</span></span>
<span data-ttu-id="fbc32-122">通常情况下，本身不压缩任何响应可从响应压缩中受益。</span><span class="sxs-lookup"><span data-stu-id="fbc32-122">Usually, any response not natively compressed can benefit from response compression.</span></span> <span data-ttu-id="fbc32-123">通常本身不压缩的响应包括： CSS、 JavaScript、 HTML、 XML 和 JSON。</span><span class="sxs-lookup"><span data-stu-id="fbc32-123">Responses not natively compressed typically include: CSS, JavaScript, HTML, XML, and JSON.</span></span> <span data-ttu-id="fbc32-124">本机压缩的资产，如 PNG 文件，你不应将其压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-124">You shouldn't compress natively compressed assets, such as PNG files.</span></span> <span data-ttu-id="fbc32-125">如果你尝试进一步压缩本机压缩的响应，任何小的其他缩短的大小和传输的时间将可能屏蔽按处理压缩所花费的时间。</span><span class="sxs-lookup"><span data-stu-id="fbc32-125">If you attempt to further compress a natively compressed response, any small additional reduction in size and transmission time will likely be overshadowed by the time it took to process the compression.</span></span> <span data-ttu-id="fbc32-126">不压缩小于大约 150-1000年字节 （具体取决于该文件的内容和压缩的效率） 的文件。</span><span class="sxs-lookup"><span data-stu-id="fbc32-126">Don't compress files smaller than about 150-1000 bytes (depending on the file's content and the efficiency of compression).</span></span> <span data-ttu-id="fbc32-127">压缩的小文件的开销可能会产生大于未压缩的文件的压缩的文件。</span><span class="sxs-lookup"><span data-stu-id="fbc32-127">The overhead of compressing small files may produce a compressed file larger than the uncompressed file.</span></span>

<span data-ttu-id="fbc32-128">客户端时客户端可以处理压缩的内容，必须通过发送通知其功能的服务器`Accept-Encoding`与请求的标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-128">When a client can process compressed content, the client must inform the server of its capabilities by sending the `Accept-Encoding` header with the request.</span></span> <span data-ttu-id="fbc32-129">当服务器发送压缩的内容时，它必须包括中的信息`Content-Encoding`如何编码压缩的响应标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-129">When a server sends compressed content, it must include information in the `Content-Encoding` header on how the compressed response is encoded.</span></span> <span data-ttu-id="fbc32-130">支持的中间件的内容编码指定下表所示。</span><span class="sxs-lookup"><span data-stu-id="fbc32-130">Content encoding designations supported by the middleware are shown in the following table.</span></span>

| <span data-ttu-id="fbc32-131">`Accept-Encoding`标头值</span><span class="sxs-lookup"><span data-stu-id="fbc32-131">`Accept-Encoding` header values</span></span> | <span data-ttu-id="fbc32-132">支持的中间件</span><span class="sxs-lookup"><span data-stu-id="fbc32-132">Middleware Supported</span></span> | <span data-ttu-id="fbc32-133">描述</span><span class="sxs-lookup"><span data-stu-id="fbc32-133">Description</span></span>                                                 |
| :-----------------------------: | :------------------: | ----------------------------------------------------------- |
| `br`                            | <span data-ttu-id="fbc32-134">否</span><span class="sxs-lookup"><span data-stu-id="fbc32-134">No</span></span>                   | <span data-ttu-id="fbc32-135">Brotli 压缩的数据格式</span><span class="sxs-lookup"><span data-stu-id="fbc32-135">Brotli Compressed Data Format</span></span>                               |
| `compress`                      | <span data-ttu-id="fbc32-136">否</span><span class="sxs-lookup"><span data-stu-id="fbc32-136">No</span></span>                   | <span data-ttu-id="fbc32-137">UNIX"压缩"的数据格式</span><span class="sxs-lookup"><span data-stu-id="fbc32-137">UNIX "compress" data format</span></span>                                 |
| `deflate`                       | <span data-ttu-id="fbc32-138">否</span><span class="sxs-lookup"><span data-stu-id="fbc32-138">No</span></span>                   | <span data-ttu-id="fbc32-139">"deflate"内的"zlib"数据格式的压缩的数据</span><span class="sxs-lookup"><span data-stu-id="fbc32-139">"deflate" compressed data inside the "zlib" data format</span></span>     |
| `exi`                           | <span data-ttu-id="fbc32-140">否</span><span class="sxs-lookup"><span data-stu-id="fbc32-140">No</span></span>                   | <span data-ttu-id="fbc32-141">W3C 高效 XML 交换</span><span class="sxs-lookup"><span data-stu-id="fbc32-141">W3C Efficient XML Interchange</span></span>                               |
| `gzip`                          | <span data-ttu-id="fbc32-142">是 （默认值）</span><span class="sxs-lookup"><span data-stu-id="fbc32-142">Yes (default)</span></span>        | <span data-ttu-id="fbc32-143">gzip 文件格式</span><span class="sxs-lookup"><span data-stu-id="fbc32-143">gzip file format</span></span>                                            |
| `identity`                      | <span data-ttu-id="fbc32-144">是</span><span class="sxs-lookup"><span data-stu-id="fbc32-144">Yes</span></span>                  | <span data-ttu-id="fbc32-145">"没有编码"标识符： 响应必须进行编码。</span><span class="sxs-lookup"><span data-stu-id="fbc32-145">"No encoding" identifier: The response must not be encoded.</span></span> |
| `pack200-gzip`                  | <span data-ttu-id="fbc32-146">否</span><span class="sxs-lookup"><span data-stu-id="fbc32-146">No</span></span>                   | <span data-ttu-id="fbc32-147">Java 存档的网络传输格式</span><span class="sxs-lookup"><span data-stu-id="fbc32-147">Network Transfer Format for Java Archives</span></span>                   |
| `*`                             | <span data-ttu-id="fbc32-148">是</span><span class="sxs-lookup"><span data-stu-id="fbc32-148">Yes</span></span>                  | <span data-ttu-id="fbc32-149">编码不显式请求的任何可用内容</span><span class="sxs-lookup"><span data-stu-id="fbc32-149">Any available content encoding not explicitly requested</span></span>     |

<span data-ttu-id="fbc32-150">有关详细信息，请参阅[IANA 官方内容编码列表](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-150">For more information, see the [IANA Official Content Coding List](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry).</span></span>

<span data-ttu-id="fbc32-151">该中间件，可添加额外的压缩提供程序自定义`Accept-Encoding`标头值。</span><span class="sxs-lookup"><span data-stu-id="fbc32-151">The middleware allows you to add additional compression providers for custom `Accept-Encoding` header values.</span></span> <span data-ttu-id="fbc32-152">有关详细信息，请参阅[自定义提供程序](#custom-providers)下面。</span><span class="sxs-lookup"><span data-stu-id="fbc32-152">For more information, see [Custom Providers](#custom-providers) below.</span></span>

<span data-ttu-id="fbc32-153">该中间件是能够对的质量值作出反应 (qvalue， `q`) 权重时客户端发送为优先处理压缩方案。</span><span class="sxs-lookup"><span data-stu-id="fbc32-153">The middleware is capable of reacting to quality value (qvalue, `q`) weighting when sent by the client to prioritize compression schemes.</span></span> <span data-ttu-id="fbc32-154">有关详细信息，请参阅[RFC 7231: Accept-encoding](https://tools.ietf.org/html/rfc7231#section-5.3.4)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-154">For more information, see [RFC 7231: Accept-Encoding](https://tools.ietf.org/html/rfc7231#section-5.3.4).</span></span>

<span data-ttu-id="fbc32-155">压缩算法受到压缩速度和压缩的效率之间的权衡。</span><span class="sxs-lookup"><span data-stu-id="fbc32-155">Compression algorithms are subject to a tradeoff between compression speed and the effectiveness of the compression.</span></span> <span data-ttu-id="fbc32-156">*有效性*在此上下文中引用的输出的大小压缩后。</span><span class="sxs-lookup"><span data-stu-id="fbc32-156">*Effectiveness* in this context refers to the size of the output after compression.</span></span> <span data-ttu-id="fbc32-157">最小大小通过最*最佳*压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-157">The smallest size is achieved by the most *optimal* compression.</span></span>

<span data-ttu-id="fbc32-158">参与请求的标头，发送、 缓存和接收压缩的内容是下表中所述。</span><span class="sxs-lookup"><span data-stu-id="fbc32-158">The headers involved in requesting, sending, caching, and receiving compressed content are described in the table below.</span></span>

| <span data-ttu-id="fbc32-159">Header</span><span class="sxs-lookup"><span data-stu-id="fbc32-159">Header</span></span>             | <span data-ttu-id="fbc32-160">角色</span><span class="sxs-lookup"><span data-stu-id="fbc32-160">Role</span></span> |
| ------------------ | ---- |
| `Accept-Encoding`  | <span data-ttu-id="fbc32-161">从客户端发送到服务器以指示编码方案可接受的客户端的内容。</span><span class="sxs-lookup"><span data-stu-id="fbc32-161">Sent from the client to the server to indicate the content encoding schemes acceptable to the client.</span></span> |
| `Content-Encoding` | <span data-ttu-id="fbc32-162">从服务器发送到客户端以指示负载中的内容的编码。</span><span class="sxs-lookup"><span data-stu-id="fbc32-162">Sent from the server to the client to indicate the encoding of the content in the payload.</span></span> |
| `Content-Length`   | <span data-ttu-id="fbc32-163">在进行压缩时会，`Content-Length`标头被删除，因为正文内容更改时压缩响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-163">When compression occurs, the `Content-Length` header is removed, since the body content changes when the response is compressed.</span></span> |
| `Content-MD5`      | <span data-ttu-id="fbc32-164">在进行压缩时会，`Content-MD5`移除标头，因为已更改的正文内容，且哈希将不再有效。</span><span class="sxs-lookup"><span data-stu-id="fbc32-164">When compression occurs, the `Content-MD5` header is removed, since the body content has changed and the hash is no longer valid.</span></span> |
| `Content-Type`     | <span data-ttu-id="fbc32-165">指定内容的 MIME 的类型。</span><span class="sxs-lookup"><span data-stu-id="fbc32-165">Specifies the MIME type of the content.</span></span> <span data-ttu-id="fbc32-166">每个响应应指定其`Content-Type`。</span><span class="sxs-lookup"><span data-stu-id="fbc32-166">Every response should specify its `Content-Type`.</span></span> <span data-ttu-id="fbc32-167">该中间件检查此值以确定是否应压缩响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-167">The middleware checks this value to determine if the response should be compressed.</span></span> <span data-ttu-id="fbc32-168">该中间件指定的一组[默认 MIME 类型](#mime-types)其可以进行编码，但您可以替换或添加 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="fbc32-168">The middleware specifies a set of [default MIME types](#mime-types) that it can encode, but you can replace or add MIME types.</span></span> |
| `Vary`             | <span data-ttu-id="fbc32-169">由值为服务器发送时`Accept-Encoding`到客户端和代理，`Vary`标头指示的客户端或代理，它应缓存 （有所不同） 响应基于值`Accept-Encoding`的请求标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-169">When sent by the server with a value of `Accept-Encoding` to clients and proxies, the `Vary` header indicates to the client or proxy that it should cache (vary) responses based on the value of the `Accept-Encoding` header of the request.</span></span> <span data-ttu-id="fbc32-170">返回具有内容的结果`Vary: Accept-Encoding`标头是同时压缩和未压缩的响应将单独进行缓存。</span><span class="sxs-lookup"><span data-stu-id="fbc32-170">The result of returning content with the `Vary: Accept-Encoding` header is that both compressed and uncompressed responses are cached separately.</span></span> |

<span data-ttu-id="fbc32-171">你可以浏览的功能与的响应压缩中间件[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-171">You can explore the features of the Response Compression Middleware with the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples).</span></span> <span data-ttu-id="fbc32-172">此示例阐释了：</span><span class="sxs-lookup"><span data-stu-id="fbc32-172">The sample illustrates:</span></span>
* <span data-ttu-id="fbc32-173">使用 gzip 和自定义压缩提供程序的应用程序响应的压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-173">The compression of app responses using gzip and custom compression providers.</span></span>
* <span data-ttu-id="fbc32-174">如何将 MIME 类型添加到压缩的 MIME 类型的默认列表。</span><span class="sxs-lookup"><span data-stu-id="fbc32-174">How to add a MIME type to the default list of MIME types for compression.</span></span>

## <a name="package"></a><span data-ttu-id="fbc32-175">Package</span><span class="sxs-lookup"><span data-stu-id="fbc32-175">Package</span></span>
<span data-ttu-id="fbc32-176">若要在你的项目中包含该中间件，添加到引用[ `Microsoft.AspNetCore.ResponseCompression` ](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/)包或使用[ `Microsoft.AspNetCore.All` ](https://www.nuget.org/packages/Microsoft.AspNetCore.All/)包。</span><span class="sxs-lookup"><span data-stu-id="fbc32-176">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.ResponseCompression`](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/) package or use the [`Microsoft.AspNetCore.All`](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) package.</span></span> <span data-ttu-id="fbc32-177">此功能是可用于应用程序面向 ASP.NET 核心 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="fbc32-177">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="configuration"></a><span data-ttu-id="fbc32-178">配置</span><span class="sxs-lookup"><span data-stu-id="fbc32-178">Configuration</span></span>
<span data-ttu-id="fbc32-179">下面的代码演示如何启用与响应压缩中间件与默认 gzip 压缩和默认 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="fbc32-179">The following code shows how to enable the Response Compression Middleware with the with the default gzip compression and for default MIME types.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fbc32-180">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-180">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/StartupBasic.cs?name=snippet1&highlight=4,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fbc32-181">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-181">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/StartupBasic.cs?name=snippet1&highlight=3,8)]

---

> [!NOTE]
> <span data-ttu-id="fbc32-182">使用之类的工具[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)设置`Accept-Encoding`请求标头并研究响应标头、 大小和正文。</span><span class="sxs-lookup"><span data-stu-id="fbc32-182">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span>

<span data-ttu-id="fbc32-183">提交到示例应用程序而无需请求`Accept-Encoding`标头并观察响应是否未压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-183">Submit a request to the sample app without the `Accept-Encoding` header and observe that the response is uncompressed.</span></span> <span data-ttu-id="fbc32-184">`Content-Encoding`和`Vary`标头不在响应上存在。</span><span class="sxs-lookup"><span data-stu-id="fbc32-184">The `Content-Encoding` and `Vary` headers aren't present on the response.</span></span>

![Fiddler 窗口中显示的无 Accept-encoding 标头的请求的结果。](response-compression/_static/request-uncompressed.png)

<span data-ttu-id="fbc32-187">向示例应用程序与提交一个申请`Accept-Encoding: gzip`标头并观察压缩的响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-187">Submit a request to the sample app with the `Accept-Encoding: gzip` header and observe that the response is compressed.</span></span> <span data-ttu-id="fbc32-188">`Content-Encoding`和`Vary`标头会显示在响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-188">The `Content-Encoding` and `Vary` headers are present on the response.</span></span>

![Fiddler 窗口中显示的 Accept-encoding 标头的请求的结果和 gzip 的值。](response-compression/_static/request-compressed.png)

## <a name="providers"></a><span data-ttu-id="fbc32-192">提供程序</span><span class="sxs-lookup"><span data-stu-id="fbc32-192">Providers</span></span>
### <a name="gzipcompressionprovider"></a><span data-ttu-id="fbc32-193">GzipCompressionProvider</span><span class="sxs-lookup"><span data-stu-id="fbc32-193">GzipCompressionProvider</span></span>
<span data-ttu-id="fbc32-194">使用`GzipCompressionProvider`以压缩使用 gzip 响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-194">Use the `GzipCompressionProvider` to compress responses with gzip.</span></span> <span data-ttu-id="fbc32-195">如果未指定，这是默认压缩提供程序。</span><span class="sxs-lookup"><span data-stu-id="fbc32-195">This is the default compression provider if none are specified.</span></span> <span data-ttu-id="fbc32-196">你可以设置压缩级别与`GzipCompressionProviderOptions`。</span><span class="sxs-lookup"><span data-stu-id="fbc32-196">You can set the compression level with the `GzipCompressionProviderOptions`.</span></span> 

<span data-ttu-id="fbc32-197">Gzip 压缩提供程序默认为最快的压缩级别 (`CompressionLevel.Fastest`)，这可能不会产生最有效的压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-197">The gzip compression provider defaults to the fastest compression level (`CompressionLevel.Fastest`), which might not produce the most efficient compression.</span></span> <span data-ttu-id="fbc32-198">如果需要最有效的压缩，则你可以配置的中间件理想的压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-198">If the most efficient compression is desired, you can configure the middleware for optimal compression.</span></span>

| <span data-ttu-id="fbc32-199">压缩级别</span><span class="sxs-lookup"><span data-stu-id="fbc32-199">Compression Level</span></span>                | <span data-ttu-id="fbc32-200">描述</span><span class="sxs-lookup"><span data-stu-id="fbc32-200">Description</span></span>                                                                                                   |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `CompressionLevel.Fastest`       | <span data-ttu-id="fbc32-201">即使未以最佳方式压缩生成的输出，应尽可能快地完成压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-201">Compression should complete as quickly as possible, even if the resulting output isn't optimally compressed.</span></span> |
| `CompressionLevel.NoCompression` | <span data-ttu-id="fbc32-202">应执行不进行压缩。</span><span class="sxs-lookup"><span data-stu-id="fbc32-202">No compression should be performed.</span></span>                                                                           |
| `CompressionLevel.Optimal`       | <span data-ttu-id="fbc32-203">响应应以最佳方式压缩，即使压缩操作将使用更多时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="fbc32-203">Responses should be optimally compressed, even if the compression takes more time to complete.</span></span>                |


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fbc32-204">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-204">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=3,8-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fbc32-205">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-205">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=5,10-13)]

---

## <a name="mime-types"></a><span data-ttu-id="fbc32-206">MIME 类型</span><span class="sxs-lookup"><span data-stu-id="fbc32-206">MIME types</span></span>
<span data-ttu-id="fbc32-207">该中间件指定一组默认的 MIME 类型为压缩：</span><span class="sxs-lookup"><span data-stu-id="fbc32-207">The middleware specifies a default set of MIME types for compression:</span></span>
* `text/plain`
* `text/css`
* `application/javascript`
* `text/html`
* `application/xml`
* `text/xml`
* `application/json`
* `text/json`

<span data-ttu-id="fbc32-208">您可以替换或追加的响应压缩中间件选项的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="fbc32-208">You can replace or append MIME types with the Response Compression Middleware options.</span></span> <span data-ttu-id="fbc32-209">请注意该通配符 MIME 类型，如`text/*`不受支持。</span><span class="sxs-lookup"><span data-stu-id="fbc32-209">Note that wildcard MIME types, such as `text/*` aren't supported.</span></span> <span data-ttu-id="fbc32-210">示例应用程序添加的 MIME 类型`image/svg+xml`和压缩，并提供横幅图像的 ASP.NET Core (*banner.svg*)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-210">The sample app adds a MIME type for `image/svg+xml` and compresses and serves the ASP.NET Core banner image (*banner.svg*).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fbc32-211">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-211">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fbc32-212">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-212">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=7)]

---

### <a name="custom-providers"></a><span data-ttu-id="fbc32-213">自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="fbc32-213">Custom providers</span></span>
<span data-ttu-id="fbc32-214">你可以创建自定义压缩实现与`ICompressionProvider`。</span><span class="sxs-lookup"><span data-stu-id="fbc32-214">You can create custom compression implementations with `ICompressionProvider`.</span></span> <span data-ttu-id="fbc32-215">`EncodingName`表示的内容编码此`ICompressionProvider`生成。</span><span class="sxs-lookup"><span data-stu-id="fbc32-215">The `EncodingName` represents the content encoding that this `ICompressionProvider` produces.</span></span> <span data-ttu-id="fbc32-216">该中间件使用此信息来选择基于列表中指定的提供程序`Accept-Encoding`的请求标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-216">The middleware uses this information to choose the provider based on the list specified in the `Accept-Encoding` header of the request.</span></span>

<span data-ttu-id="fbc32-217">使用示例应用程序，客户端提交的请求`Accept-Encoding: mycustomcompression`标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-217">Using the sample app, the client submits a request with the `Accept-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="fbc32-218">该中间件使用自定义压缩的实现，并返回响应，其中`Content-Encoding: mycustomcompression`标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-218">The middleware uses the custom compression implementation and returns the response with a `Content-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="fbc32-219">客户端必须能够解压缩顺序用于工作的自定义压缩实现的自定义编码。</span><span class="sxs-lookup"><span data-stu-id="fbc32-219">The client must be able to decompress the custom encoding in order for a custom compression implementation to work.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fbc32-220">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-220">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=4)]

[!code-csharp[Main](response-compression/samples/2.x/CustomCompressionProvider.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fbc32-221">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fbc32-221">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=6)]

[!code-csharp[Main](response-compression/samples/1.x/CustomCompressionProvider.cs?name=snippet1)]

---

<span data-ttu-id="fbc32-222">向示例应用程序与提交一个申请`Accept-Encoding: mycustomcompression`标头并观察响应标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-222">Submit a request to the sample app with the `Accept-Encoding: mycustomcompression` header and observe the response headers.</span></span> <span data-ttu-id="fbc32-223">`Vary`和`Content-Encoding`标头会显示在响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-223">The `Vary` and `Content-Encoding` headers are present on the response.</span></span> <span data-ttu-id="fbc32-224">此示例未压缩响应正文 （未显示）。</span><span class="sxs-lookup"><span data-stu-id="fbc32-224">The response body (not shown) isn't compressed by the sample.</span></span> <span data-ttu-id="fbc32-225">没有在压缩的实现`CustomCompressionProvider`类中的示例。</span><span class="sxs-lookup"><span data-stu-id="fbc32-225">There isn't a compression implementation in the `CustomCompressionProvider` class of the sample.</span></span> <span data-ttu-id="fbc32-226">但是，此示例演示您可以用来实现此类的压缩算法。</span><span class="sxs-lookup"><span data-stu-id="fbc32-226">However, the sample shows where you would implement such a compression algorithm.</span></span>

![Fiddler 窗口中显示的 Accept-encoding 标头的请求的结果和 mycustomcompression 的值。](response-compression/_static/request-custom-compression.png)

## <a name="compression-with-secure-protocol"></a><span data-ttu-id="fbc32-229">使用安全的协议压缩</span><span class="sxs-lookup"><span data-stu-id="fbc32-229">Compression with secure protocol</span></span>
<span data-ttu-id="fbc32-230">可以通过安全连接压缩的响应来控制`EnableForHttps`选项，它默认处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="fbc32-230">Compressed responses over secure connections can be controlled with the `EnableForHttps` option, which is disabled by default.</span></span> <span data-ttu-id="fbc32-231">使用动态生成的页压缩可以导致安全问题如[犯罪](https://wikipedia.org/wiki/CRIME_(security_exploit))和[违反](https://wikipedia.org/wiki/BREACH_(security_exploit))攻击。</span><span class="sxs-lookup"><span data-stu-id="fbc32-231">Using compression with dynamically generated pages can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span>

## <a name="adding-the-vary-header"></a><span data-ttu-id="fbc32-232">添加 Vary 标头</span><span class="sxs-lookup"><span data-stu-id="fbc32-232">Adding the Vary header</span></span>
<span data-ttu-id="fbc32-233">当压缩响应基于`Accept-Encoding`标头，有可能的多个压缩的版本响应和未压缩的版本。</span><span class="sxs-lookup"><span data-stu-id="fbc32-233">When compressing responses based on the `Accept-Encoding` header, there are potentially multiple compressed versions of the response and an uncompressed version.</span></span> <span data-ttu-id="fbc32-234">若要指示客户端和代理服务器缓存，多个版本存在，并且应存储`Vary`标头添加与`Accept-Encoding`值。</span><span class="sxs-lookup"><span data-stu-id="fbc32-234">In order to instruct client and proxy caches that multiple versions exist and should be stored, the `Vary` header is added with an `Accept-Encoding` value.</span></span> <span data-ttu-id="fbc32-235">在 ASP.NET Core 1.x 添加`Vary`手动完成到响应的标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-235">In ASP.NET Core 1.x, adding the `Vary` header to the response is accomplished manually.</span></span> <span data-ttu-id="fbc32-236">在 ASP.NET Core 2.x，中间件将添加`Vary`压缩响应时自动标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-236">In ASP.NET Core 2.x, the middleware adds the `Vary` header automatically when the response is compressed.</span></span>

<span data-ttu-id="fbc32-237">**ASP.NET 核心 1.x 仅**</span><span class="sxs-lookup"><span data-stu-id="fbc32-237">**ASP.NET Core 1.x only**</span></span>

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet1)]

## <a name="middleware-issue-when-behind-an-nginx-reverse-proxy"></a><span data-ttu-id="fbc32-238">后面 Nginx 反向代理时的中间件问题</span><span class="sxs-lookup"><span data-stu-id="fbc32-238">Middleware issue when behind an Nginx reverse proxy</span></span>
<span data-ttu-id="fbc32-239">当请求代理 nginx，`Accept-Encoding`删除标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-239">When a request is proxied by Nginx, the `Accept-Encoding` header is removed.</span></span> <span data-ttu-id="fbc32-240">这可以防止该中间件压缩响应。</span><span class="sxs-lookup"><span data-stu-id="fbc32-240">This prevents the middleware from compressing the response.</span></span> <span data-ttu-id="fbc32-241">有关详细信息，请参阅[NGINX： 压缩和解压缩](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-241">For more information, see [NGINX: Compression and Decompression](https://www.nginx.com/resources/admin-guide/compression-and-decompression/).</span></span> <span data-ttu-id="fbc32-242">此问题将跟踪[找出传递压缩 Nginx (BasicMiddleware #123)](https://github.com/aspnet/BasicMiddleware/issues/123)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-242">This issue is tracked by [Figure out pass-through compression for Nginx (BasicMiddleware #123)](https://github.com/aspnet/BasicMiddleware/issues/123).</span></span>

## <a name="working-with-iis-dynamic-compression"></a><span data-ttu-id="fbc32-243">使用 IIS 动态压缩</span><span class="sxs-lookup"><span data-stu-id="fbc32-243">Working with IIS dynamic compression</span></span>
<span data-ttu-id="fbc32-244">如果你有一个 active IIS 动态压缩模块你想要禁用的应用程序的服务器级别配置，可以进行此操作而添加到你*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="fbc32-244">If you have an active IIS Dynamic Compression Module configured at the server level that you would like to disable for an app, you can do so with an addition to your *web.config* file.</span></span> <span data-ttu-id="fbc32-245">有关详细信息，请参阅[禁用 IIS 模块](xref:host-and-deploy/iis/modules#disabling-iis-modules)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-245">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fbc32-246">疑难解答</span><span class="sxs-lookup"><span data-stu-id="fbc32-246">Troubleshooting</span></span>
<span data-ttu-id="fbc32-247">使用之类的工具[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)，这允许你设置`Accept-Encoding`请求标头并研究响应标头、 大小和正文。</span><span class="sxs-lookup"><span data-stu-id="fbc32-247">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/), which allow you to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span> <span data-ttu-id="fbc32-248">响应压缩中间件压缩满足以下条件的响应：</span><span class="sxs-lookup"><span data-stu-id="fbc32-248">The Response Compression Middleware compresses responses that meet the following conditions:</span></span>
* <span data-ttu-id="fbc32-249">`Accept-Encoding`标头的值位于`gzip`， `*`，或与匹配的自定义压缩提供程序已建立的自定义编码。</span><span class="sxs-lookup"><span data-stu-id="fbc32-249">The `Accept-Encoding` header is present with a value of `gzip`, `*`, or custom encoding that matches a custom compression provider that you've established.</span></span> <span data-ttu-id="fbc32-250">值不能`identity`或具有质量值 (qvalue， `q`) 设置为 0 （零）。</span><span class="sxs-lookup"><span data-stu-id="fbc32-250">The value must not be `identity` or have a quality value (qvalue, `q`) setting of 0 (zero).</span></span>
* <span data-ttu-id="fbc32-251">MIME 类型 (`Content-Type`) 必须设置，并且必须匹配上配置的 MIME 类型`ResponseCompressionOptions`。</span><span class="sxs-lookup"><span data-stu-id="fbc32-251">The MIME type (`Content-Type`) must be set and must match a MIME type configured on the `ResponseCompressionOptions`.</span></span>
* <span data-ttu-id="fbc32-252">请求不得包括`Content-Range`标头。</span><span class="sxs-lookup"><span data-stu-id="fbc32-252">The request must not include the `Content-Range` header.</span></span>
* <span data-ttu-id="fbc32-253">请求必须使用不安全的协议 (http)，除非在响应压缩中间件选项中配置安全协议 (https)。</span><span class="sxs-lookup"><span data-stu-id="fbc32-253">The request must use insecure protocol (http), unless secure protocol (https) is configured in the Response Compression Middleware options.</span></span> <span data-ttu-id="fbc32-254">*请注意危险[上述](#compression-with-secure-protocol)启用安全的内容压缩时。*</span><span class="sxs-lookup"><span data-stu-id="fbc32-254">*Note the danger [described above](#compression-with-secure-protocol) when enabling secure content compression.*</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbc32-255">其他资源</span><span class="sxs-lookup"><span data-stu-id="fbc32-255">Additional resources</span></span>
* [<span data-ttu-id="fbc32-256">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="fbc32-256">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="fbc32-257">中间件</span><span class="sxs-lookup"><span data-stu-id="fbc32-257">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="fbc32-258">Mozilla 开发人员网络： 接受的编码</span><span class="sxs-lookup"><span data-stu-id="fbc32-258">Mozilla Developer Network: Accept-Encoding</span></span>](https://developer.mozilla.org/docs/Web/HTTP/Headers/Accept-Encoding)
* [<span data-ttu-id="fbc32-259">RFC 7231 部分 3.1.2.1： 内容 Codings</span><span class="sxs-lookup"><span data-stu-id="fbc32-259">RFC 7231 Section 3.1.2.1: Content Codings</span></span>](https://tools.ietf.org/html/rfc7231#section-3.1.2.1)
* [<span data-ttu-id="fbc32-260">RFC 7230 部分 4.2.3: Gzip 编码</span><span class="sxs-lookup"><span data-stu-id="fbc32-260">RFC 7230 Section 4.2.3: Gzip Coding</span></span>](https://tools.ietf.org/html/rfc7230#section-4.2.3)
* [<span data-ttu-id="fbc32-261">GZIP 文件格式规范版本 4.3</span><span class="sxs-lookup"><span data-stu-id="fbc32-261">GZIP file format specification version 4.3</span></span>](http://www.ietf.org/rfc/rfc1952.txt)
