---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: 从.NET 客户端 (C#) 调用 Web API |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/24/2017
ms.topic: article
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: a243eeb982ba581e237263c4e31e130d634aff0e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="ce898-102">从.NET 客户端 (C#) 调用 Web API</span><span class="sxs-lookup"><span data-stu-id="ce898-102">Call a Web API From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="ce898-103">通过[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ce898-103">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="ce898-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="ce898-104">Download Completed Project</span></span>](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)

<span data-ttu-id="ce898-105">本教程演示如何从.NET 应用程序，调用 web API 使用[System.Net.Http.HttpClient。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="ce898-105">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="ce898-106">在本教程中，客户端应用程序是编写使用以下 web API:</span><span class="sxs-lookup"><span data-stu-id="ce898-106">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="ce898-107">操作</span><span class="sxs-lookup"><span data-stu-id="ce898-107">Action</span></span> | <span data-ttu-id="ce898-108">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ce898-108">HTTP method</span></span> | <span data-ttu-id="ce898-109">相对 URI</span><span class="sxs-lookup"><span data-stu-id="ce898-109">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce898-110">获取按 ID 的产品</span><span class="sxs-lookup"><span data-stu-id="ce898-110">Get a product by ID</span></span> | <span data-ttu-id="ce898-111">GET</span><span class="sxs-lookup"><span data-stu-id="ce898-111">GET</span></span> | <span data-ttu-id="ce898-112">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="ce898-112">/api/products/*id*</span></span> |
| <span data-ttu-id="ce898-113">创建新产品</span><span class="sxs-lookup"><span data-stu-id="ce898-113">Create a new product</span></span> | <span data-ttu-id="ce898-114">发布</span><span class="sxs-lookup"><span data-stu-id="ce898-114">POST</span></span> | <span data-ttu-id="ce898-115">/ api/产品</span><span class="sxs-lookup"><span data-stu-id="ce898-115">/api/products</span></span> |
| <span data-ttu-id="ce898-116">将产品更新</span><span class="sxs-lookup"><span data-stu-id="ce898-116">Update a product</span></span> | <span data-ttu-id="ce898-117">PUT</span><span class="sxs-lookup"><span data-stu-id="ce898-117">PUT</span></span> | <span data-ttu-id="ce898-118">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="ce898-118">/api/products/*id*</span></span> |
| <span data-ttu-id="ce898-119">删除产品</span><span class="sxs-lookup"><span data-stu-id="ce898-119">Delete a product</span></span> | <span data-ttu-id="ce898-120">DELETE</span><span class="sxs-lookup"><span data-stu-id="ce898-120">DELETE</span></span> | <span data-ttu-id="ce898-121">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="ce898-121">/api/products/*id*</span></span> |

<span data-ttu-id="ce898-122">若要了解如何实现此 API 与 ASP.NET Web API，请参阅[创建该支持 CRUD 操作的 Web API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="ce898-122">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="ce898-123">为简单起见，本教程中的客户端应用程序是一个 Windows 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce898-123">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="ce898-124">**HttpClient**也支持对于 Windows Phone 和 Windows 应用商店应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce898-124">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="ce898-125">有关详细信息，请参阅[编写 Web API 的客户端代码更改为多个平台使用可移植库](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce898-125">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="ce898-126">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="ce898-126">Create the Console Application</span></span>

<span data-ttu-id="ce898-127">在 Visual Studio 中，创建名为的新 Windows 控制台应用**HttpClientSample**然后粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="ce898-127">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="ce898-128">前面的代码是完整的客户端应用。</span><span class="sxs-lookup"><span data-stu-id="ce898-128">The preceding code is the complete client app.</span></span>

<span data-ttu-id="ce898-129">`RunAsync` 运行并受到阻止，直到它完成。</span><span class="sxs-lookup"><span data-stu-id="ce898-129">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="ce898-130">大多数**HttpClient**方法是异步，因为它们执行网络 I/O。</span><span class="sxs-lookup"><span data-stu-id="ce898-130">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="ce898-131">所有异步任务完成内`RunAsync`。</span><span class="sxs-lookup"><span data-stu-id="ce898-131">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="ce898-132">应用程序通常不会阻止主线程，但此应用不允许任何交互。</span><span class="sxs-lookup"><span data-stu-id="ce898-132">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="ce898-133">安装 Web API 客户端库</span><span class="sxs-lookup"><span data-stu-id="ce898-133">Install the Web API Client Libraries</span></span>

<span data-ttu-id="ce898-134">使用 NuGet 包管理器安装 Web API 客户端库包。</span><span class="sxs-lookup"><span data-stu-id="ce898-134">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="ce898-135">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="ce898-135">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="ce898-136">在包管理器控制台 (PMC) 中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ce898-136">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="ce898-137">前一个命令向项目中添加以下 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="ce898-137">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="ce898-138">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="ce898-138">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="ce898-139">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="ce898-139">Newtonsoft.Json</span></span>

<span data-ttu-id="ce898-140">Json.NET 是用于.NET 的受欢迎的高性能 JSON 框架。</span><span class="sxs-lookup"><span data-stu-id="ce898-140">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="ce898-141">将一个模型类添加</span><span class="sxs-lookup"><span data-stu-id="ce898-141">Add a Model Class</span></span>

<span data-ttu-id="ce898-142">检查`Product`类：</span><span class="sxs-lookup"><span data-stu-id="ce898-142">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="ce898-143">此类匹配使用 web API 的数据模型。</span><span class="sxs-lookup"><span data-stu-id="ce898-143">This class matches the data model used by the web API.</span></span> <span data-ttu-id="ce898-144">应用程序可以使用**HttpClient**读取`Product`的 HTTP 响应中的实例。</span><span class="sxs-lookup"><span data-stu-id="ce898-144">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="ce898-145">应用程序无需编写任何反序列化代码。</span><span class="sxs-lookup"><span data-stu-id="ce898-145">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="ce898-146">创建和初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="ce898-146">Create and Initialize HttpClient</span></span>

<span data-ttu-id="ce898-147">检查静态**HttpClient**属性：</span><span class="sxs-lookup"><span data-stu-id="ce898-147">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="ce898-148">**HttpClient**是用于一次实例化，并且在应用程序生命周期重复使用。</span><span class="sxs-lookup"><span data-stu-id="ce898-148">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="ce898-149">以下情况可能会导致**SocketException**错误：</span><span class="sxs-lookup"><span data-stu-id="ce898-149">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="ce898-150">创建一个新**HttpClient**每个请求的实例。</span><span class="sxs-lookup"><span data-stu-id="ce898-150">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="ce898-151">服务器负载过大。</span><span class="sxs-lookup"><span data-stu-id="ce898-151">Server under heavy load.</span></span>

<span data-ttu-id="ce898-152">创建一个新**HttpClient**每个请求的实例可以耗尽可用的套接字。</span><span class="sxs-lookup"><span data-stu-id="ce898-152">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="ce898-153">下面的代码初始化**HttpClient**实例：</span><span class="sxs-lookup"><span data-stu-id="ce898-153">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="ce898-154">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="ce898-154">The preceding code:</span></span>

* <span data-ttu-id="ce898-155">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="ce898-155">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="ce898-156">将端口号更改为服务器应用程序中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="ce898-156">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="ce898-157">应用程序不起作用，除非使用为服务器应用程序的端口。</span><span class="sxs-lookup"><span data-stu-id="ce898-157">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="ce898-158">设置为"application/json"Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="ce898-158">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="ce898-159">设置此标头指示服务器以 JSON 格式发送数据。</span><span class="sxs-lookup"><span data-stu-id="ce898-159">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="ce898-160">发送 GET 请求以检索资源</span><span class="sxs-lookup"><span data-stu-id="ce898-160">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="ce898-161">下面的代码将发送 GET 请求产品：</span><span class="sxs-lookup"><span data-stu-id="ce898-161">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="ce898-162">**GetAsync**方法可发送 HTTP GET 请求。</span><span class="sxs-lookup"><span data-stu-id="ce898-162">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="ce898-163">当方法完成时，它将返回**HttpResponseMessage**包含 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="ce898-163">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="ce898-164">如果在响应中的状态代码是一个成功代码，响应正文将包含的 JSON 表示形式产品。</span><span class="sxs-lookup"><span data-stu-id="ce898-164">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="ce898-165">调用**ReadAsAsync**进行反序列化到 JSON 负载`Product`实例。</span><span class="sxs-lookup"><span data-stu-id="ce898-165">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="ce898-166">**ReadAsAsync**方法是异步的因为响应正文可以是任意大。</span><span class="sxs-lookup"><span data-stu-id="ce898-166">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="ce898-167">**HttpClient**当 HTTP 响应包含错误代码时不引发异常。</span><span class="sxs-lookup"><span data-stu-id="ce898-167">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="ce898-168">相反， **IsSuccessStatusCode**属性是**false**如果状态为错误代码。</span><span class="sxs-lookup"><span data-stu-id="ce898-168">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="ce898-169">如果想要将异常视为的 HTTP 错误代码，调用[HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)响应对象上。</span><span class="sxs-lookup"><span data-stu-id="ce898-169">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="ce898-170">`EnsureSuccessStatusCode` 如果超出了范围 200 状态代码引发异常&ndash;299。</span><span class="sxs-lookup"><span data-stu-id="ce898-170">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="ce898-171">请注意， **HttpClient**可以出于其他原因引发异常&mdash;例如，如果在请求超时时。</span><span class="sxs-lookup"><span data-stu-id="ce898-171">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="ce898-172">媒体类型格式化程序进行反序列化</span><span class="sxs-lookup"><span data-stu-id="ce898-172">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="ce898-173">当**ReadAsAsync**调用不带任何参数，它使用一组默认的*媒体格式化程序*来读取的响应正文。</span><span class="sxs-lookup"><span data-stu-id="ce898-173">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="ce898-174">默认格式化程序支持 JSON、 XML 和窗体的 url 编码的数据。</span><span class="sxs-lookup"><span data-stu-id="ce898-174">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="ce898-175">而不是使用默认格式化程序，你可以提供一份到格式化程序**ReadAsAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="ce898-175">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="ce898-176">使用格式化程序的列表是具有自定义的媒体类型格式化程序的情况下很有用：</span><span class="sxs-lookup"><span data-stu-id="ce898-176">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="ce898-177">有关详细信息，请参阅[ASP.NET Web API 2 中的媒体格式化程序](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="ce898-177">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="ce898-178">发送 POST 请求来创建资源</span><span class="sxs-lookup"><span data-stu-id="ce898-178">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="ce898-179">下面的代码发送 POST 请求包含`Product`采用 JSON 格式的实例：</span><span class="sxs-lookup"><span data-stu-id="ce898-179">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="ce898-180">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="ce898-180">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="ce898-181">序列化到 JSON 的对象。</span><span class="sxs-lookup"><span data-stu-id="ce898-181">Serializes an object to JSON.</span></span>
* <span data-ttu-id="ce898-182">在 POST 请求中发送的 JSON 负载。</span><span class="sxs-lookup"><span data-stu-id="ce898-182">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="ce898-183">如果请求成功：</span><span class="sxs-lookup"><span data-stu-id="ce898-183">If the request succeeds:</span></span>

* <span data-ttu-id="ce898-184">它应返回 201 （已创建） 响应。</span><span class="sxs-lookup"><span data-stu-id="ce898-184">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="ce898-185">响应应包含创建的资源的 URL 位置标头。</span><span class="sxs-lookup"><span data-stu-id="ce898-185">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="ce898-186">发送 PUT 的请求以更新资源</span><span class="sxs-lookup"><span data-stu-id="ce898-186">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="ce898-187">下面的代码将发送 PUT 请求将产品更新：</span><span class="sxs-lookup"><span data-stu-id="ce898-187">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="ce898-188">**PutAsJsonAsync**方法的工作原理类似**PostAsJsonAsync**，只不过它将发送 PUT 请求而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="ce898-188">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="ce898-189">发送 DELETE 请求删除资源</span><span class="sxs-lookup"><span data-stu-id="ce898-189">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="ce898-190">下面的代码将发送 DELETE 请求删除产品：</span><span class="sxs-lookup"><span data-stu-id="ce898-190">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="ce898-191">如 GET、 DELETE 请求没有请求正文。</span><span class="sxs-lookup"><span data-stu-id="ce898-191">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="ce898-192">你不需要删除的指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="ce898-192">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="ce898-193">测试此示例</span><span class="sxs-lookup"><span data-stu-id="ce898-193">Test the sample</span></span>

<span data-ttu-id="ce898-194">测试客户端应用程序：</span><span class="sxs-lookup"><span data-stu-id="ce898-194">To test the client app:</span></span>

1. <span data-ttu-id="ce898-195">[下载](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)并运行服务器应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce898-195">[Download](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="ce898-196">[下载说明](https://docs.microsoft.com/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="ce898-196">[Download instructions](https://docs.microsoft.com/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="ce898-197">验证服务器应用程序工作。</span><span class="sxs-lookup"><span data-stu-id="ce898-197">Verify the server app is working.</span></span> <span data-ttu-id="ce898-198">有关 exaxmple，`http://localhost:64195/api/products`应返回产品的列表。</span><span class="sxs-lookup"><span data-stu-id="ce898-198">For exaxmple, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="ce898-199">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="ce898-199">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="ce898-200">将端口号更改为服务器应用程序中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="ce898-200">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="ce898-201">运行客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce898-201">Run the client app.</span></span> <span data-ttu-id="ce898-202">将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="ce898-202">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
