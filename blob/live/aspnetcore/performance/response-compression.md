---
title: "有关 ASP.NET 核心响应压缩中间件"
author: guardrex
description: "了解如何响应压缩以及如何在 ASP.NET Core 应用中使用响应压缩中间件。"
keywords: "ASP.NET 核心，性能、 响应压缩、 gzip、 接受编码、 中间件"
ms.author: riande
manager: wpickett
ms.date: 08/20/2017
ms.topic: article
ms.assetid: de621887-c5c9-4ac8-9efd-f5cc0457a134
ms.technology: aspnet
ms.prod: asp.net-core
uid: performance/response-compression
ms.openlocfilehash: 86244179115fe6a7d0f7298495086a96ee9570d9
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="response-compression-middleware-for-aspnet-core"></a><span data-ttu-id="d6158-104">有关 ASP.NET 核心响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="d6158-104">Response Compression Middleware for ASP.NET Core</span></span>

<span data-ttu-id="d6158-105">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="d6158-105">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d6158-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="d6158-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="d6158-107">网络带宽是有限的资源。</span><span class="sxs-lookup"><span data-stu-id="d6158-107">Network bandwidth is a limited resource.</span></span> <span data-ttu-id="d6158-108">通常减小响应的大小将通常显著增加应用的响应能力。</span><span class="sxs-lookup"><span data-stu-id="d6158-108">Reducing the size of the response usually increases the responsiveness of an app, often dramatically.</span></span> <span data-ttu-id="d6158-109">减小负载大小的一种方法是压缩应用的响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-109">One way to reduce payload sizes is to compress an app's responses.</span></span>

## <a name="when-to-use-response-compression-middleware"></a><span data-ttu-id="d6158-110">何时使用响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="d6158-110">When to use Response Compression Middleware</span></span>
<span data-ttu-id="d6158-111">使用在 IIS、 Apache 或 Nginx 基于服务器的响应压缩技术。</span><span class="sxs-lookup"><span data-stu-id="d6158-111">Use server-based response compression technologies in IIS, Apache, or Nginx.</span></span> <span data-ttu-id="d6158-112">中间件的性能可能不会与匹配服务器模块。</span><span class="sxs-lookup"><span data-stu-id="d6158-112">The performance of the middleware probably won't match that of the server modules.</span></span> <span data-ttu-id="d6158-113">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)和[Kestrel](xref:fundamentals/servers/kestrel)当前不提供内置的压缩支持。</span><span class="sxs-lookup"><span data-stu-id="d6158-113">[HTTP.sys server](xref:fundamentals/servers/httpsys) and [Kestrel](xref:fundamentals/servers/kestrel) don't currently offer built-in compression support.</span></span>

<span data-ttu-id="d6158-114">当你时，请使用响应压缩中间件：</span><span class="sxs-lookup"><span data-stu-id="d6158-114">Use Response Compression Middleware when you're:</span></span>

* <span data-ttu-id="d6158-115">无法使用以下基于服务器的压缩技术：</span><span class="sxs-lookup"><span data-stu-id="d6158-115">Unable to use the following server-based compression technologies:</span></span>
  * [<span data-ttu-id="d6158-116">IIS 动态压缩模块</span><span class="sxs-lookup"><span data-stu-id="d6158-116">IIS Dynamic Compression module</span></span>](https://www.iis.net/overview/reliability/dynamiccachingandcompression)
  * [<span data-ttu-id="d6158-117">Apache mod_deflate 模块</span><span class="sxs-lookup"><span data-stu-id="d6158-117">Apache mod_deflate module</span></span>](http://httpd.apache.org/docs/current/mod/mod_deflate.html)
  * [<span data-ttu-id="d6158-118">NGINX 压缩和解压缩</span><span class="sxs-lookup"><span data-stu-id="d6158-118">NGINX Compression and Decompression</span></span>](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)
* <span data-ttu-id="d6158-119">直接在上托管：</span><span class="sxs-lookup"><span data-stu-id="d6158-119">Hosting directly on:</span></span>
  * <span data-ttu-id="d6158-120">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)(以前称为[WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="d6158-120">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>
  * [<span data-ttu-id="d6158-121">Kestrel</span><span class="sxs-lookup"><span data-stu-id="d6158-121">Kestrel</span></span>](xref:fundamentals/servers/kestrel)

## <a name="response-compression"></a><span data-ttu-id="d6158-122">响应压缩</span><span class="sxs-lookup"><span data-stu-id="d6158-122">Response compression</span></span>
<span data-ttu-id="d6158-123">通常情况下，本身不压缩任何响应可从响应压缩中受益。</span><span class="sxs-lookup"><span data-stu-id="d6158-123">Usually, any response not natively compressed can benefit from response compression.</span></span> <span data-ttu-id="d6158-124">通常本身不压缩的响应包括： CSS、 JavaScript、 HTML、 XML 和 JSON。</span><span class="sxs-lookup"><span data-stu-id="d6158-124">Responses not natively compressed typically include: CSS, JavaScript, HTML, XML, and JSON.</span></span> <span data-ttu-id="d6158-125">本机压缩的资产，如 PNG 文件，你不应将其压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-125">You shouldn't compress natively compressed assets, such as PNG files.</span></span> <span data-ttu-id="d6158-126">如果你尝试进一步压缩本机压缩的响应，任何小的其他缩短的大小和传输的时间将可能屏蔽按处理压缩所花费的时间。</span><span class="sxs-lookup"><span data-stu-id="d6158-126">If you attempt to further compress a natively compressed response, any small additional reduction in size and transmission time will likely be overshadowed by the time it took to process the compression.</span></span> <span data-ttu-id="d6158-127">不压缩小于大约 150-1000年字节 （具体取决于该文件的内容和压缩的效率） 的文件。</span><span class="sxs-lookup"><span data-stu-id="d6158-127">Don't compress files smaller than about 150-1000 bytes (depending on the file's content and the efficiency of compression).</span></span> <span data-ttu-id="d6158-128">压缩的小文件的开销可能会产生大于未压缩的文件的压缩的文件。</span><span class="sxs-lookup"><span data-stu-id="d6158-128">The overhead of compressing small files may produce a compressed file larger than the uncompressed file.</span></span>

<span data-ttu-id="d6158-129">客户端时客户端可以处理压缩的内容，必须通过发送通知其功能的服务器`Accept-Encoding`与请求的标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-129">When a client can process compressed content, the client must inform the server of its capabilities by sending the `Accept-Encoding` header with the request.</span></span> <span data-ttu-id="d6158-130">当服务器发送压缩的内容时，它必须包括中的信息`Content-Encoding`如何编码压缩的响应标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-130">When a server sends compressed content, it must include information in the `Content-Encoding` header on how the compressed response is encoded.</span></span> <span data-ttu-id="d6158-131">支持的中间件的内容编码指定下表所示。</span><span class="sxs-lookup"><span data-stu-id="d6158-131">Content encoding designations supported by the middleware are shown in the following table.</span></span>

| <span data-ttu-id="d6158-132">`Accept-Encoding`标头值</span><span class="sxs-lookup"><span data-stu-id="d6158-132">`Accept-Encoding` header values</span></span> | <span data-ttu-id="d6158-133">支持的中间件</span><span class="sxs-lookup"><span data-stu-id="d6158-133">Middleware Supported</span></span> | <span data-ttu-id="d6158-134">描述</span><span class="sxs-lookup"><span data-stu-id="d6158-134">Description</span></span>                                                 |
| :-----------------------------: | :------------------: | ----------------------------------------------------------- |
| `br`                            | <span data-ttu-id="d6158-135">否</span><span class="sxs-lookup"><span data-stu-id="d6158-135">No</span></span>                   | <span data-ttu-id="d6158-136">Brotli 压缩的数据格式</span><span class="sxs-lookup"><span data-stu-id="d6158-136">Brotli Compressed Data Format</span></span>                               |
| `compress`                      | <span data-ttu-id="d6158-137">否</span><span class="sxs-lookup"><span data-stu-id="d6158-137">No</span></span>                   | <span data-ttu-id="d6158-138">UNIX"压缩"的数据格式</span><span class="sxs-lookup"><span data-stu-id="d6158-138">UNIX "compress" data format</span></span>                                 |
| `deflate`                       | <span data-ttu-id="d6158-139">否</span><span class="sxs-lookup"><span data-stu-id="d6158-139">No</span></span>                   | <span data-ttu-id="d6158-140">"deflate"内的"zlib"数据格式的压缩的数据</span><span class="sxs-lookup"><span data-stu-id="d6158-140">"deflate" compressed data inside the "zlib" data format</span></span>     |
| `exi`                           | <span data-ttu-id="d6158-141">否</span><span class="sxs-lookup"><span data-stu-id="d6158-141">No</span></span>                   | <span data-ttu-id="d6158-142">W3C 高效 XML 交换</span><span class="sxs-lookup"><span data-stu-id="d6158-142">W3C Efficient XML Interchange</span></span>                               |
| `gzip`                          | <span data-ttu-id="d6158-143">是 （默认值）</span><span class="sxs-lookup"><span data-stu-id="d6158-143">Yes (default)</span></span>        | <span data-ttu-id="d6158-144">gzip 文件格式</span><span class="sxs-lookup"><span data-stu-id="d6158-144">gzip file format</span></span>                                            |
| `identity`                      | <span data-ttu-id="d6158-145">是</span><span class="sxs-lookup"><span data-stu-id="d6158-145">Yes</span></span>                  | <span data-ttu-id="d6158-146">"没有编码"标识符： 响应必须进行编码。</span><span class="sxs-lookup"><span data-stu-id="d6158-146">"No encoding" identifier: The response must not be encoded.</span></span> |
| `pack200-gzip`                  | <span data-ttu-id="d6158-147">否</span><span class="sxs-lookup"><span data-stu-id="d6158-147">No</span></span>                   | <span data-ttu-id="d6158-148">Java 存档的网络传输格式</span><span class="sxs-lookup"><span data-stu-id="d6158-148">Network Transfer Format for Java Archives</span></span>                   |
| `*`                             | <span data-ttu-id="d6158-149">是</span><span class="sxs-lookup"><span data-stu-id="d6158-149">Yes</span></span>                  | <span data-ttu-id="d6158-150">编码不显式请求的任何可用内容</span><span class="sxs-lookup"><span data-stu-id="d6158-150">Any available content encoding not explicitly requested</span></span>     |

<span data-ttu-id="d6158-151">有关详细信息，请参阅[IANA 官方内容编码列表](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry)。</span><span class="sxs-lookup"><span data-stu-id="d6158-151">For more information, see the [IANA Official Content Coding List](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry).</span></span>

<span data-ttu-id="d6158-152">该中间件，可添加额外的压缩提供程序自定义`Accept-Encoding`标头值。</span><span class="sxs-lookup"><span data-stu-id="d6158-152">The middleware allows you to add additional compression providers for custom `Accept-Encoding` header values.</span></span> <span data-ttu-id="d6158-153">有关详细信息，请参阅[自定义提供程序](#custom-providers)下面。</span><span class="sxs-lookup"><span data-stu-id="d6158-153">For more information, see [Custom Providers](#custom-providers) below.</span></span>

<span data-ttu-id="d6158-154">该中间件是能够对的质量值作出反应 (qvalue， `q`) 权重时客户端发送为优先处理压缩方案。</span><span class="sxs-lookup"><span data-stu-id="d6158-154">The middleware is capable of reacting to quality value (qvalue, `q`) weighting when sent by the client to prioritize compression schemes.</span></span> <span data-ttu-id="d6158-155">有关详细信息，请参阅[RFC 7231: Accept-encoding](https://tools.ietf.org/html/rfc7231#section-5.3.4)。</span><span class="sxs-lookup"><span data-stu-id="d6158-155">For more information, see [RFC 7231: Accept-Encoding](https://tools.ietf.org/html/rfc7231#section-5.3.4).</span></span>

<span data-ttu-id="d6158-156">压缩算法受到压缩速度和压缩的效率之间的权衡。</span><span class="sxs-lookup"><span data-stu-id="d6158-156">Compression algorithms are subject to a tradeoff between compression speed and the effectiveness of the compression.</span></span> <span data-ttu-id="d6158-157">*有效性*在此上下文中引用的输出的大小压缩后。</span><span class="sxs-lookup"><span data-stu-id="d6158-157">*Effectiveness* in this context refers to the size of the output after compression.</span></span> <span data-ttu-id="d6158-158">最小大小通过最*最佳*压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-158">The smallest size is achieved by the most *optimal* compression.</span></span>

<span data-ttu-id="d6158-159">参与请求的标头，发送、 缓存和接收压缩的内容是下表中所述。</span><span class="sxs-lookup"><span data-stu-id="d6158-159">The headers involved in requesting, sending, caching, and receiving compressed content are described in the table below.</span></span>

| <span data-ttu-id="d6158-160">Header</span><span class="sxs-lookup"><span data-stu-id="d6158-160">Header</span></span>             | <span data-ttu-id="d6158-161">角色</span><span class="sxs-lookup"><span data-stu-id="d6158-161">Role</span></span> |
| ------------------ | ---- |
| `Accept-Encoding`  | <span data-ttu-id="d6158-162">从客户端发送到服务器以指示编码方案可接受的客户端的内容。</span><span class="sxs-lookup"><span data-stu-id="d6158-162">Sent from the client to the server to indicate the content encoding schemes acceptable to the client.</span></span> |
| `Content-Encoding` | <span data-ttu-id="d6158-163">从服务器发送到客户端以指示负载中的内容的编码。</span><span class="sxs-lookup"><span data-stu-id="d6158-163">Sent from the server to the client to indicate the encoding of the content in the payload.</span></span> |
| `Content-Length`   | <span data-ttu-id="d6158-164">在进行压缩时会，`Content-Length`标头被删除，因为正文内容更改时压缩响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-164">When compression occurs, the `Content-Length` header is removed, since the body content changes when the response is compressed.</span></span> |
| `Content-MD5`      | <span data-ttu-id="d6158-165">在进行压缩时会，`Content-MD5`移除标头，因为已更改的正文内容，且哈希将不再有效。</span><span class="sxs-lookup"><span data-stu-id="d6158-165">When compression occurs, the `Content-MD5` header is removed, since the body content has changed and the hash is no longer valid.</span></span> |
| `Content-Type`     | <span data-ttu-id="d6158-166">指定内容的 MIME 的类型。</span><span class="sxs-lookup"><span data-stu-id="d6158-166">Specifies the MIME type of the content.</span></span> <span data-ttu-id="d6158-167">每个响应应指定其`Content-Type`。</span><span class="sxs-lookup"><span data-stu-id="d6158-167">Every response should specify its `Content-Type`.</span></span> <span data-ttu-id="d6158-168">该中间件检查此值以确定是否应压缩响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-168">The middleware checks this value to determine if the response should be compressed.</span></span> <span data-ttu-id="d6158-169">该中间件指定的一组[默认 MIME 类型](#mime-types)其可以进行编码，但您可以替换或添加 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="d6158-169">The middleware specifies a set of [default MIME types](#mime-types) that it can encode, but you can replace or add MIME types.</span></span> |
| `Vary`             | <span data-ttu-id="d6158-170">由值为服务器发送时`Accept-Encoding`到客户端和代理，`Vary`标头指示的客户端或代理，它应缓存 （有所不同） 响应基于值`Accept-Encoding`的请求标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-170">When sent by the server with a value of `Accept-Encoding` to clients and proxies, the `Vary` header indicates to the client or proxy that it should cache (vary) responses based on the value of the `Accept-Encoding` header of the request.</span></span> <span data-ttu-id="d6158-171">返回具有内容的结果`Vary: Accept-Encoding`标头是同时压缩和未压缩的响应将单独进行缓存。</span><span class="sxs-lookup"><span data-stu-id="d6158-171">The result of returning content with the `Vary: Accept-Encoding` header is that both compressed and uncompressed responses are cached separately.</span></span> |

<span data-ttu-id="d6158-172">你可以浏览的功能与的响应压缩中间件[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)。</span><span class="sxs-lookup"><span data-stu-id="d6158-172">You can explore the features of the Response Compression Middleware with the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples).</span></span> <span data-ttu-id="d6158-173">此示例阐释了：</span><span class="sxs-lookup"><span data-stu-id="d6158-173">The sample illustrates:</span></span>
* <span data-ttu-id="d6158-174">使用 gzip 和自定义压缩提供程序的应用程序响应的压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-174">The compression of app responses using gzip and custom compression providers.</span></span>
* <span data-ttu-id="d6158-175">如何将 MIME 类型添加到压缩的 MIME 类型的默认列表。</span><span class="sxs-lookup"><span data-stu-id="d6158-175">How to add a MIME type to the default list of MIME types for compression.</span></span>

## <a name="package"></a><span data-ttu-id="d6158-176">Package</span><span class="sxs-lookup"><span data-stu-id="d6158-176">Package</span></span>
<span data-ttu-id="d6158-177">若要在你的项目中包含该中间件，添加到引用[ `Microsoft.AspNetCore.ResponseCompression` ](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/)包或使用[ `Microsoft.AspNetCore.All` ](https://www.nuget.org/packages/Microsoft.AspNetCore.All/)包。</span><span class="sxs-lookup"><span data-stu-id="d6158-177">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.ResponseCompression`](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/) package or use the [`Microsoft.AspNetCore.All`](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) package.</span></span> <span data-ttu-id="d6158-178">此功能是可用于应用程序面向 ASP.NET 核心 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="d6158-178">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="configuration"></a><span data-ttu-id="d6158-179">配置</span><span class="sxs-lookup"><span data-stu-id="d6158-179">Configuration</span></span>
<span data-ttu-id="d6158-180">下面的代码演示如何启用与响应压缩中间件与默认 gzip 压缩和默认 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="d6158-180">The following code shows how to enable the Response Compression Middleware with the with the default gzip compression and for default MIME types.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="d6158-181">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="d6158-181">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/StartupBasic.cs?name=snippet1&highlight=4,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="d6158-182">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="d6158-182">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/StartupBasic.cs?name=snippet1&highlight=3,8)]

---

> [!NOTE]
> <span data-ttu-id="d6158-183">使用之类的工具[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)设置`Accept-Encoding`请求标头并研究响应标头、 大小和正文。</span><span class="sxs-lookup"><span data-stu-id="d6158-183">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span>

<span data-ttu-id="d6158-184">提交到示例应用程序而无需请求`Accept-Encoding`标头并观察响应是否未压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-184">Submit a request to the sample app without the `Accept-Encoding` header and observe that the response is uncompressed.</span></span> <span data-ttu-id="d6158-185">`Content-Encoding`和`Vary`标头不在响应上存在。</span><span class="sxs-lookup"><span data-stu-id="d6158-185">The `Content-Encoding` and `Vary` headers aren't present on the response.</span></span>

![Fiddler 窗口中显示的无 Accept-encoding 标头的请求的结果。](response-compression/_static/request-uncompressed.png)

<span data-ttu-id="d6158-188">向示例应用程序与提交一个申请`Accept-Encoding: gzip`标头并观察压缩的响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-188">Submit a request to the sample app with the `Accept-Encoding: gzip` header and observe that the response is compressed.</span></span> <span data-ttu-id="d6158-189">`Content-Encoding`和`Vary`标头会显示在响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-189">The `Content-Encoding` and `Vary` headers are present on the response.</span></span>

![Fiddler 窗口中显示的 Accept-encoding 标头的请求的结果和 gzip 的值。](response-compression/_static/request-compressed.png)

## <a name="providers"></a><span data-ttu-id="d6158-193">提供程序</span><span class="sxs-lookup"><span data-stu-id="d6158-193">Providers</span></span>
### <a name="gzipcompressionprovider"></a><span data-ttu-id="d6158-194">GzipCompressionProvider</span><span class="sxs-lookup"><span data-stu-id="d6158-194">GzipCompressionProvider</span></span>
<span data-ttu-id="d6158-195">使用`GzipCompressionProvider`以压缩使用 gzip 响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-195">Use the `GzipCompressionProvider` to compress responses with gzip.</span></span> <span data-ttu-id="d6158-196">如果未指定，这是默认压缩提供程序。</span><span class="sxs-lookup"><span data-stu-id="d6158-196">This is the default compression provider if none are specified.</span></span> <span data-ttu-id="d6158-197">你可以设置压缩级别与`GzipCompressionProviderOptions`。</span><span class="sxs-lookup"><span data-stu-id="d6158-197">You can set the compression level with the `GzipCompressionProviderOptions`.</span></span> 

<span data-ttu-id="d6158-198">Gzip 压缩提供程序默认为最快的压缩级别 (`CompressionLevel.Fastest`)，这可能不会产生最有效的压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-198">The gzip compression provider defaults to the fastest compression level (`CompressionLevel.Fastest`), which might not produce the most efficient compression.</span></span> <span data-ttu-id="d6158-199">如果需要最有效的压缩，则你可以配置的中间件理想的压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-199">If the most efficient compression is desired, you can configure the middleware for optimal compression.</span></span>

| <span data-ttu-id="d6158-200">压缩级别</span><span class="sxs-lookup"><span data-stu-id="d6158-200">Compression Level</span></span>                | <span data-ttu-id="d6158-201">描述</span><span class="sxs-lookup"><span data-stu-id="d6158-201">Description</span></span>                                                                                                   |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `CompressionLevel.Fastest`       | <span data-ttu-id="d6158-202">即使生成的输出将不会以最佳方式压缩，应尽可能快地完成压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-202">Compression should complete as quickly as possible, even if the resulting output is not optimally compressed.</span></span> |
| `CompressionLevel.NoCompression` | <span data-ttu-id="d6158-203">应执行不进行压缩。</span><span class="sxs-lookup"><span data-stu-id="d6158-203">No compression should be performed.</span></span>                                                                           |
| `CompressionLevel.Optimal`       | <span data-ttu-id="d6158-204">响应应以最佳方式压缩，即使压缩操作将使用更多时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="d6158-204">Responses should be optimally compressed, even if the compression takes more time to complete.</span></span>                |


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="d6158-205">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="d6158-205">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=3,8-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="d6158-206">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="d6158-206">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=5,10-13)]

---

## <a name="mime-types"></a><span data-ttu-id="d6158-207">MIME 类型</span><span class="sxs-lookup"><span data-stu-id="d6158-207">MIME types</span></span>
<span data-ttu-id="d6158-208">该中间件指定一组默认的 MIME 类型为压缩：</span><span class="sxs-lookup"><span data-stu-id="d6158-208">The middleware specifies a default set of MIME types for compression:</span></span>
* `text/plain`
* `text/css`
* `application/javascript`
* `text/html`
* `application/xml`
* `text/xml`
* `application/json`
* `text/json`

<span data-ttu-id="d6158-209">您可以替换或追加的响应压缩中间件选项的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="d6158-209">You can replace or append MIME types with the Response Compression Middleware options.</span></span> <span data-ttu-id="d6158-210">请注意该通配符 MIME 类型，如`text/*`不受支持。</span><span class="sxs-lookup"><span data-stu-id="d6158-210">Note that wildcard MIME types, such as `text/*` aren't supported.</span></span> <span data-ttu-id="d6158-211">示例应用程序添加的 MIME 类型`image/svg+xml`和压缩，并提供横幅图像的 ASP.NET Core (*banner.svg*)。</span><span class="sxs-lookup"><span data-stu-id="d6158-211">The sample app adds a MIME type for `image/svg+xml` and compresses and serves the ASP.NET Core banner image (*banner.svg*).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="d6158-212">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="d6158-212">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="d6158-213">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="d6158-213">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=7)]

---

### <a name="custom-providers"></a><span data-ttu-id="d6158-214">自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="d6158-214">Custom providers</span></span>
<span data-ttu-id="d6158-215">你可以创建自定义压缩实现与`ICompressionProvider`。</span><span class="sxs-lookup"><span data-stu-id="d6158-215">You can create custom compression implementations with `ICompressionProvider`.</span></span> <span data-ttu-id="d6158-216">`EncodingName`表示的内容编码此`ICompressionProvider`生成。</span><span class="sxs-lookup"><span data-stu-id="d6158-216">The `EncodingName` represents the content encoding that this `ICompressionProvider` produces.</span></span> <span data-ttu-id="d6158-217">该中间件使用此信息来选择基于列表中指定的提供程序`Accept-Encoding`的请求标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-217">The middleware uses this information to choose the provider based on the list specified in the `Accept-Encoding` header of the request.</span></span>

<span data-ttu-id="d6158-218">使用示例应用程序，客户端提交的请求`Accept-Encoding: mycustomcompression`标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-218">Using the sample app, the client submits a request with the `Accept-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="d6158-219">该中间件使用自定义压缩的实现，并返回响应，其中`Content-Encoding: mycustomcompression`标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-219">The middleware uses the custom compression implementation and returns the response with a `Content-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="d6158-220">客户端必须能够解压缩顺序用于工作的自定义压缩实现的自定义编码。</span><span class="sxs-lookup"><span data-stu-id="d6158-220">The client must be able to decompress the custom encoding in order for a custom compression implementation to work.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="d6158-221">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="d6158-221">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=4)]

[!code-csharp[Main](response-compression/samples/2.x/CustomCompressionProvider.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="d6158-222">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="d6158-222">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=6)]

[!code-csharp[Main](response-compression/samples/1.x/CustomCompressionProvider.cs?name=snippet1)]

---

<span data-ttu-id="d6158-223">向示例应用程序与提交一个申请`Accept-Encoding: mycustomcompression`标头并观察响应标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-223">Submit a request to the sample app with the `Accept-Encoding: mycustomcompression` header and observe the response headers.</span></span> <span data-ttu-id="d6158-224">`Vary`和`Content-Encoding`标头会显示在响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-224">The `Vary` and `Content-Encoding` headers are present on the response.</span></span> <span data-ttu-id="d6158-225">此示例未压缩响应正文 （未显示）。</span><span class="sxs-lookup"><span data-stu-id="d6158-225">The response body (not shown) isn't compressed by the sample.</span></span> <span data-ttu-id="d6158-226">没有在压缩的实现`CustomCompressionProvider`类中的示例。</span><span class="sxs-lookup"><span data-stu-id="d6158-226">There isn't a compression implementation in the `CustomCompressionProvider` class of the sample.</span></span> <span data-ttu-id="d6158-227">但是，此示例演示您可以用来实现此类的压缩算法。</span><span class="sxs-lookup"><span data-stu-id="d6158-227">However, the sample shows where you would implement such a compression algorithm.</span></span>

![Fiddler 窗口中显示的 Accept-encoding 标头的请求的结果和 mycustomcompression 的值。](response-compression/_static/request-custom-compression.png)

## <a name="compression-with-secure-protocol"></a><span data-ttu-id="d6158-230">使用安全的协议压缩</span><span class="sxs-lookup"><span data-stu-id="d6158-230">Compression with secure protocol</span></span>
<span data-ttu-id="d6158-231">可以通过安全连接压缩的响应来控制`EnableForHttps`选项，它默认处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="d6158-231">Compressed responses over secure connections can be controlled with the `EnableForHttps` option, which is disabled by default.</span></span> <span data-ttu-id="d6158-232">使用动态生成的页压缩可以导致安全问题如[犯罪](https://wikipedia.org/wiki/CRIME_(security_exploit))和[违反](https://wikipedia.org/wiki/BREACH_(security_exploit))攻击。</span><span class="sxs-lookup"><span data-stu-id="d6158-232">Using compression with dynamically generated pages can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span>

## <a name="adding-the-vary-header"></a><span data-ttu-id="d6158-233">添加 Vary 标头</span><span class="sxs-lookup"><span data-stu-id="d6158-233">Adding the Vary header</span></span>
<span data-ttu-id="d6158-234">当压缩响应基于`Accept-Encoding`标头，有可能的多个压缩的版本响应和未压缩的版本。</span><span class="sxs-lookup"><span data-stu-id="d6158-234">When compressing responses based on the `Accept-Encoding` header, there are potentially multiple compressed versions of the response and an uncompressed version.</span></span> <span data-ttu-id="d6158-235">若要指示客户端和代理服务器缓存，多个版本存在，并且应存储`Vary`标头添加与`Accept-Encoding`值。</span><span class="sxs-lookup"><span data-stu-id="d6158-235">In order to instruct client and proxy caches that multiple versions exist and should be stored, the `Vary` header is added with an `Accept-Encoding` value.</span></span> <span data-ttu-id="d6158-236">在 ASP.NET Core 1.x 添加`Vary`手动完成到响应的标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-236">In ASP.NET Core 1.x, adding the `Vary` header to the response is accomplished manually.</span></span> <span data-ttu-id="d6158-237">在 ASP.NET Core 2.x，中间件将添加`Vary`压缩响应时自动标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-237">In ASP.NET Core 2.x, the middleware adds the `Vary` header automatically when the response is compressed.</span></span>

<span data-ttu-id="d6158-238">**ASP.NET 核心 1.x 仅**</span><span class="sxs-lookup"><span data-stu-id="d6158-238">**ASP.NET Core 1.x only**</span></span>

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet1)]

## <a name="middleware-issue-when-behind-an-nginx-reverse-proxy"></a><span data-ttu-id="d6158-239">后面 Nginx 反向代理时的中间件问题</span><span class="sxs-lookup"><span data-stu-id="d6158-239">Middleware issue when behind an Nginx reverse proxy</span></span>
<span data-ttu-id="d6158-240">当请求代理 nginx，`Accept-Encoding`删除标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-240">When a request is proxied by Nginx, the `Accept-Encoding` header is removed.</span></span> <span data-ttu-id="d6158-241">这可以防止该中间件压缩响应。</span><span class="sxs-lookup"><span data-stu-id="d6158-241">This prevents the middleware from compressing the response.</span></span> <span data-ttu-id="d6158-242">有关详细信息，请参阅[NGINX： 压缩和解压缩](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)。</span><span class="sxs-lookup"><span data-stu-id="d6158-242">For more information, see [NGINX: Compression and Decompression](https://www.nginx.com/resources/admin-guide/compression-and-decompression/).</span></span> <span data-ttu-id="d6158-243">此问题将跟踪[找出传递压缩 nginx (BasicMiddleware #123)](https://github.com/aspnet/BasicMiddleware/issues/123)。</span><span class="sxs-lookup"><span data-stu-id="d6158-243">This issue is tracked by [Figure out pass-through compression for nginx (BasicMiddleware #123)](https://github.com/aspnet/BasicMiddleware/issues/123).</span></span>

## <a name="working-with-iis-dynamic-compression"></a><span data-ttu-id="d6158-244">使用 IIS 动态压缩</span><span class="sxs-lookup"><span data-stu-id="d6158-244">Working with IIS dynamic compression</span></span>
<span data-ttu-id="d6158-245">如果你有一个 active IIS 动态压缩模块你想要禁用的应用程序的服务器级别配置，可以进行此操作而添加到你*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d6158-245">If you have an active IIS Dynamic Compression Module configured at the server level that you would like to disable for an app, you can do so with an addition to your *web.config* file.</span></span> <span data-ttu-id="d6158-246">有关详细信息，请参阅[禁用 IIS 模块](xref:host-and-deploy/iis/modules#disabling-iis-modules)。</span><span class="sxs-lookup"><span data-stu-id="d6158-246">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d6158-247">疑难解答</span><span class="sxs-lookup"><span data-stu-id="d6158-247">Troubleshooting</span></span>
<span data-ttu-id="d6158-248">使用之类的工具[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)，这允许你设置`Accept-Encoding`请求标头并研究响应标头、 大小和正文。</span><span class="sxs-lookup"><span data-stu-id="d6158-248">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/), which allow you to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span> <span data-ttu-id="d6158-249">响应压缩中间件压缩满足以下条件的响应：</span><span class="sxs-lookup"><span data-stu-id="d6158-249">The Response Compression Middleware compresses responses that meet the following conditions:</span></span>
* <span data-ttu-id="d6158-250">`Accept-Encoding`标头的值位于`gzip`， `*`，或与匹配的自定义压缩提供程序已建立的自定义编码。</span><span class="sxs-lookup"><span data-stu-id="d6158-250">The `Accept-Encoding` header is present with a value of `gzip`, `*`, or custom encoding that matches a custom compression provider that you've established.</span></span> <span data-ttu-id="d6158-251">值不能`identity`或具有质量值 (qvalue， `q`) 设置为 0 （零）。</span><span class="sxs-lookup"><span data-stu-id="d6158-251">The value must not be `identity` or have a quality value (qvalue, `q`) setting of 0 (zero).</span></span>
* <span data-ttu-id="d6158-252">MIME 类型 (`Content-Type`) 必须设置，并且必须匹配上配置的 MIME 类型`ResponseCompressionOptions`。</span><span class="sxs-lookup"><span data-stu-id="d6158-252">The MIME type (`Content-Type`) must be set and must match a MIME type configured on the `ResponseCompressionOptions`.</span></span>
* <span data-ttu-id="d6158-253">请求不得包括`Content-Range`标头。</span><span class="sxs-lookup"><span data-stu-id="d6158-253">The request must not include the `Content-Range` header.</span></span>
* <span data-ttu-id="d6158-254">请求必须使用不安全的协议 (http)，除非在响应压缩中间件选项中配置安全协议 (https)。</span><span class="sxs-lookup"><span data-stu-id="d6158-254">The request must use insecure protocol (http), unless secure protocol (https) is configured in the Response Compression Middleware options.</span></span> <span data-ttu-id="d6158-255">*请注意危险[上述](#compression-with-secure-protocol)启用安全的内容压缩时。*</span><span class="sxs-lookup"><span data-stu-id="d6158-255">*Note the danger [described above](#compression-with-secure-protocol) when enabling secure content compression.*</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6158-256">其他资源</span><span class="sxs-lookup"><span data-stu-id="d6158-256">Additional resources</span></span>
* [<span data-ttu-id="d6158-257">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="d6158-257">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="d6158-258">中间件</span><span class="sxs-lookup"><span data-stu-id="d6158-258">Middleware</span></span>](xref:fundamentals/middleware)
* [<span data-ttu-id="d6158-259">Mozilla 开发人员网络： 接受的编码</span><span class="sxs-lookup"><span data-stu-id="d6158-259">Mozilla Developer Network: Accept-Encoding</span></span>](https://developer.mozilla.org/docs/Web/HTTP/Headers/Accept-Encoding)
* [<span data-ttu-id="d6158-260">RFC 7231 部分 3.1.2.1： 内容 Codings</span><span class="sxs-lookup"><span data-stu-id="d6158-260">RFC 7231 Section 3.1.2.1: Content Codings</span></span>](https://tools.ietf.org/html/rfc7231#section-3.1.2.1)
* [<span data-ttu-id="d6158-261">RFC 7230 部分 4.2.3: Gzip 编码</span><span class="sxs-lookup"><span data-stu-id="d6158-261">RFC 7230 Section 4.2.3: Gzip Coding</span></span>](https://tools.ietf.org/html/rfc7230#section-4.2.3)
* [<span data-ttu-id="d6158-262">GZIP 文件格式规范版本 4.3</span><span class="sxs-lookup"><span data-stu-id="d6158-262">GZIP file format specification version 4.3</span></span>](http://www.ietf.org/rfc/rfc1952.txt)