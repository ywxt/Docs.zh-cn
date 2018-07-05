---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: 调用 Web API 从.NET 客户端 (C#) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/24/2017
ms.topic: article
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 434515692a53c0939652b643b080cea9f2102564
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370913"
---
<a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="83193-102">从.NET 客户端 (C#) 中调用 Web API</span><span class="sxs-lookup"><span data-stu-id="83193-102">Call a Web API From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="83193-103">通过[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="83193-103">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="83193-104">[下载已完成的项目](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。</span><span class="sxs-lookup"><span data-stu-id="83193-104">[Download Completed Project](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="83193-105">[下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="83193-105">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="83193-106">本教程演示如何从.NET 应用程序调用 web API 使用[System.Net.Http.HttpClient。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="83193-106">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="83193-107">在本教程中，使用以下 web API 编写的客户端应用程序：</span><span class="sxs-lookup"><span data-stu-id="83193-107">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="83193-108">操作</span><span class="sxs-lookup"><span data-stu-id="83193-108">Action</span></span> | <span data-ttu-id="83193-109">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="83193-109">HTTP method</span></span> | <span data-ttu-id="83193-110">相对 URI</span><span class="sxs-lookup"><span data-stu-id="83193-110">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83193-111">获取按 ID 的产品</span><span class="sxs-lookup"><span data-stu-id="83193-111">Get a product by ID</span></span> | <span data-ttu-id="83193-112">GET</span><span class="sxs-lookup"><span data-stu-id="83193-112">GET</span></span> | <span data-ttu-id="83193-113">/api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="83193-113">/api/products/*id*</span></span> |
| <span data-ttu-id="83193-114">创建一个新的产品</span><span class="sxs-lookup"><span data-stu-id="83193-114">Create a new product</span></span> | <span data-ttu-id="83193-115">发布</span><span class="sxs-lookup"><span data-stu-id="83193-115">POST</span></span> | <span data-ttu-id="83193-116">/ api/产品</span><span class="sxs-lookup"><span data-stu-id="83193-116">/api/products</span></span> |
| <span data-ttu-id="83193-117">将产品更新</span><span class="sxs-lookup"><span data-stu-id="83193-117">Update a product</span></span> | <span data-ttu-id="83193-118">PUT</span><span class="sxs-lookup"><span data-stu-id="83193-118">PUT</span></span> | <span data-ttu-id="83193-119">/api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="83193-119">/api/products/*id*</span></span> |
| <span data-ttu-id="83193-120">删除产品</span><span class="sxs-lookup"><span data-stu-id="83193-120">Delete a product</span></span> | <span data-ttu-id="83193-121">DELETE</span><span class="sxs-lookup"><span data-stu-id="83193-121">DELETE</span></span> | <span data-ttu-id="83193-122">/api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="83193-122">/api/products/*id*</span></span> |

<span data-ttu-id="83193-123">若要了解如何实现此 API 与 ASP.NET Web API 配合使用，请参阅[创建支持 CRUD 操作的 Web API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="83193-123">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="83193-124">为简单起见，本教程中的客户端应用程序是一个 Windows 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="83193-124">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="83193-125">**HttpClient**也支持 Windows Phone 和 Windows 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="83193-125">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="83193-126">有关详细信息，请参阅[编写 Web API 客户端代码的多个平台使用可移植库](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="83193-126">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="83193-127">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="83193-127">Create the Console Application</span></span>

<span data-ttu-id="83193-128">在 Visual Studio 中，创建一个新的 Windows 控制台应用，名为**HttpClientSample**并粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="83193-128">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="83193-129">前面的代码是完整的客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="83193-129">The preceding code is the complete client app.</span></span>

<span data-ttu-id="83193-130">`RunAsync` 运行并阻止，直到它完成。</span><span class="sxs-lookup"><span data-stu-id="83193-130">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="83193-131">大多数**HttpClient**方法是异步，因为它们执行网络 I/O。</span><span class="sxs-lookup"><span data-stu-id="83193-131">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="83193-132">所有异步任务完成内`RunAsync`。</span><span class="sxs-lookup"><span data-stu-id="83193-132">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="83193-133">应用程序通常不会阻止主线程，但此应用不允许任何交互。</span><span class="sxs-lookup"><span data-stu-id="83193-133">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="83193-134">安装 Web API 客户端库</span><span class="sxs-lookup"><span data-stu-id="83193-134">Install the Web API Client Libraries</span></span>

<span data-ttu-id="83193-135">使用 NuGet 包管理器安装 Web API 客户端库包。</span><span class="sxs-lookup"><span data-stu-id="83193-135">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="83193-136">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="83193-136">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="83193-137">在包管理器控制台 (PMC) 中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="83193-137">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="83193-138">上述命令将以下 NuGet 包添加到项目：</span><span class="sxs-lookup"><span data-stu-id="83193-138">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="83193-139">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="83193-139">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="83193-140">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="83193-140">Newtonsoft.Json</span></span>

<span data-ttu-id="83193-141">Json.NET 是用于.NET 的热门高性能 JSON 框架。</span><span class="sxs-lookup"><span data-stu-id="83193-141">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="83193-142">添加模型类</span><span class="sxs-lookup"><span data-stu-id="83193-142">Add a Model Class</span></span>

<span data-ttu-id="83193-143">检查`Product`类：</span><span class="sxs-lookup"><span data-stu-id="83193-143">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="83193-144">此类匹配由 web API 使用的数据模型。</span><span class="sxs-lookup"><span data-stu-id="83193-144">This class matches the data model used by the web API.</span></span> <span data-ttu-id="83193-145">应用程序可以使用**HttpClient**读取`Product`的 HTTP 响应中的实例。</span><span class="sxs-lookup"><span data-stu-id="83193-145">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="83193-146">应用程序无需编写任何反序列化代码。</span><span class="sxs-lookup"><span data-stu-id="83193-146">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="83193-147">创建和初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="83193-147">Create and Initialize HttpClient</span></span>

<span data-ttu-id="83193-148">检查静态**HttpClient**属性：</span><span class="sxs-lookup"><span data-stu-id="83193-148">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="83193-149">**HttpClient**是用于实例化一次，并在应用程序的生命周期中重复使用。</span><span class="sxs-lookup"><span data-stu-id="83193-149">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="83193-150">以下条件可能会导致**SocketException**错误：</span><span class="sxs-lookup"><span data-stu-id="83193-150">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="83193-151">创建一个新**HttpClient**每个请求的实例。</span><span class="sxs-lookup"><span data-stu-id="83193-151">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="83193-152">负载较重的服务器。</span><span class="sxs-lookup"><span data-stu-id="83193-152">Server under heavy load.</span></span>

<span data-ttu-id="83193-153">创建一个新**HttpClient**每个请求的实例可以耗尽可用的套接字。</span><span class="sxs-lookup"><span data-stu-id="83193-153">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="83193-154">下面的代码初始化**HttpClient**实例：</span><span class="sxs-lookup"><span data-stu-id="83193-154">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="83193-155">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="83193-155">The preceding code:</span></span>

* <span data-ttu-id="83193-156">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="83193-156">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="83193-157">将端口号更改为服务器应用程序中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="83193-157">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="83193-158">使用端口，服务器应用的应用程序才能工作。</span><span class="sxs-lookup"><span data-stu-id="83193-158">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="83193-159">设置为"application/json"Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="83193-159">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="83193-160">设置此标头指示服务器以 JSON 格式发送数据。</span><span class="sxs-lookup"><span data-stu-id="83193-160">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="83193-161">发送 GET 请求以检索资源</span><span class="sxs-lookup"><span data-stu-id="83193-161">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="83193-162">以下代码将发送一个产品的 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="83193-162">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="83193-163">**GetAsync**方法将发送 HTTP GET 请求。</span><span class="sxs-lookup"><span data-stu-id="83193-163">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="83193-164">当方法完成时，它将返回**HttpResponseMessage**包含 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="83193-164">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="83193-165">如果在响应中的状态代码是一个成功代码，响应正文将包含产品的 JSON 表示形式。</span><span class="sxs-lookup"><span data-stu-id="83193-165">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="83193-166">调用**ReadAsAsync**要反序列化到 JSON 有效负载`Product`实例。</span><span class="sxs-lookup"><span data-stu-id="83193-166">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="83193-167">**ReadAsAsync**方法是异步的因为响应正文可以是任意大。</span><span class="sxs-lookup"><span data-stu-id="83193-167">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="83193-168">**HttpClient** HTTP 响应包含错误代码时不引发异常。</span><span class="sxs-lookup"><span data-stu-id="83193-168">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="83193-169">相反， **IsSuccessStatusCode**属性是**false**如果状态为错误代码。</span><span class="sxs-lookup"><span data-stu-id="83193-169">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="83193-170">如果想要将视为异常的 HTTP 错误代码，调用[HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)响应对象上。</span><span class="sxs-lookup"><span data-stu-id="83193-170">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="83193-171">`EnsureSuccessStatusCode` 如果超出了范围 200 状态代码将引发异常&ndash;299。</span><span class="sxs-lookup"><span data-stu-id="83193-171">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="83193-172">请注意， **HttpClient**可能会由于其他原因引发异常&mdash;例如，如果请求超时。</span><span class="sxs-lookup"><span data-stu-id="83193-172">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="83193-173">媒体类型格式化程序用于反序列化</span><span class="sxs-lookup"><span data-stu-id="83193-173">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="83193-174">当**ReadAsAsync**调用不带任何参数，它使用一组默认的*媒体格式化程序*读取响应正文。</span><span class="sxs-lookup"><span data-stu-id="83193-174">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="83193-175">默认格式化程序支持 JSON、 XML 和窗体 url 编码数据。</span><span class="sxs-lookup"><span data-stu-id="83193-175">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="83193-176">而不是使用默认格式化程序，可以提供到格式化程序的列表**ReadAsAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="83193-176">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="83193-177">使用格式化程序的列表是如果您有自定义媒体类型格式化程序：</span><span class="sxs-lookup"><span data-stu-id="83193-177">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="83193-178">有关详细信息，请参阅[ASP.NET Web API 2 中的媒体格式化程序](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="83193-178">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="83193-179">发送 POST 请求创建资源</span><span class="sxs-lookup"><span data-stu-id="83193-179">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="83193-180">下面的代码发送 POST 请求包含`Product`以 JSON 格式的实例：</span><span class="sxs-lookup"><span data-stu-id="83193-180">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="83193-181">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="83193-181">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="83193-182">序列化到 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="83193-182">Serializes an object to JSON.</span></span>
* <span data-ttu-id="83193-183">在 POST 请求中发送的 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="83193-183">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="83193-184">如果请求成功：</span><span class="sxs-lookup"><span data-stu-id="83193-184">If the request succeeds:</span></span>

* <span data-ttu-id="83193-185">它应返回 201 （已创建） 响应。</span><span class="sxs-lookup"><span data-stu-id="83193-185">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="83193-186">响应位置标头中应该包含创建的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="83193-186">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="83193-187">发送 PUT 的请求以更新资源</span><span class="sxs-lookup"><span data-stu-id="83193-187">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="83193-188">以下代码将发送 PUT 请求将产品更新：</span><span class="sxs-lookup"><span data-stu-id="83193-188">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="83193-189">**PutAsJsonAsync**方法的工作方式类似于**PostAsJsonAsync**，只不过它将发送 PUT 请求，而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="83193-189">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="83193-190">发送 DELETE 请求以删除资源</span><span class="sxs-lookup"><span data-stu-id="83193-190">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="83193-191">以下代码将发送 DELETE 请求删除某个产品：</span><span class="sxs-lookup"><span data-stu-id="83193-191">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="83193-192">如 GET、 DELETE 请求没有请求正文。</span><span class="sxs-lookup"><span data-stu-id="83193-192">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="83193-193">不需要删除与指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="83193-193">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="83193-194">测试示例</span><span class="sxs-lookup"><span data-stu-id="83193-194">Test the sample</span></span>

<span data-ttu-id="83193-195">若要测试客户端应用：</span><span class="sxs-lookup"><span data-stu-id="83193-195">To test the client app:</span></span>

1. <span data-ttu-id="83193-196">[下载](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)并运行服务器应用程序。</span><span class="sxs-lookup"><span data-stu-id="83193-196">[Download](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="83193-197">[下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="83193-197">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="83193-198">验证服务器应用程序正常工作。</span><span class="sxs-lookup"><span data-stu-id="83193-198">Verify the server app is working.</span></span> <span data-ttu-id="83193-199">有关 exaxmple，`http://localhost:64195/api/products`应返回的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="83193-199">For exaxmple, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="83193-200">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="83193-200">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="83193-201">将端口号更改为服务器应用程序中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="83193-201">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="83193-202">运行客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="83193-202">Run the client app.</span></span> <span data-ttu-id="83193-203">将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="83193-203">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
