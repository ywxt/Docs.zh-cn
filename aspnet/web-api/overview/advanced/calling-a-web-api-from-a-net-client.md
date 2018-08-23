---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: 调用 Web API 从.NET 客户端 (C#) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 11/24/2017
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: be237bee43bc5e32939cb0b3e0948fd8b35bd1eb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833718"
---
<a name="call-a-web-api-from-a-net-client-c"></a>从.NET 客户端 (C#) 中调用 Web API
====================
通过[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)

[下载已完成的项目](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。 [下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。 

本教程演示如何从.NET 应用程序调用 web API 使用[System.Net.Http.HttpClient。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

在本教程中，使用以下 web API 编写的客户端应用程序：

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 获取按 ID 的产品 | GET | /api/产品/*id* |
| 创建一个新的产品 | 发布 | / api/产品 |
| 将产品更新 | PUT | /api/产品/*id* |
| 删除产品 | DELETE | /api/产品/*id* |

若要了解如何实现此 API 与 ASP.NET Web API 配合使用，请参阅[创建支持 CRUD 操作的 Web API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。

为简单起见，本教程中的客户端应用程序是一个 Windows 控制台应用程序。 **HttpClient**也支持 Windows Phone 和 Windows 应用商店应用。 有关详细信息，请参阅[编写 Web API 客户端代码的多个平台使用可移植库](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>创建控制台应用程序

在 Visual Studio 中，创建一个新的 Windows 控制台应用，名为**HttpClientSample**并粘贴以下代码：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

前面的代码是完整的客户端应用程序。

`RunAsync` 运行并阻止，直到它完成。 大多数**HttpClient**方法是异步，因为它们执行网络 I/O。 所有异步任务完成内`RunAsync`。 应用程序通常不会阻止主线程，但此应用不允许任何交互。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>安装 Web API 客户端库

使用 NuGet 包管理器安装 Web API 客户端库包。

从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。 在包管理器控制台 (PMC) 中，键入以下命令：

`Install-Package Microsoft.AspNet.WebApi.Client`

上述命令将以下 NuGet 包添加到项目：

* Microsoft.AspNet.WebApi.Client
* Newtonsoft.Json

Json.NET 是用于.NET 的热门高性能 JSON 框架。

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>添加模型类

检查`Product`类：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

此类匹配由 web API 使用的数据模型。 应用程序可以使用**HttpClient**读取`Product`的 HTTP 响应中的实例。 应用程序无需编写任何反序列化代码。

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>创建和初始化 HttpClient

检查静态**HttpClient**属性：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient**是用于实例化一次，并在应用程序的生命周期中重复使用。 以下条件可能会导致**SocketException**错误：

* 创建一个新**HttpClient**每个请求的实例。
* 负载较重的服务器。

创建一个新**HttpClient**每个请求的实例可以耗尽可用的套接字。

下面的代码初始化**HttpClient**实例：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

前面的代码：

* 设置 HTTP 请求的基 URI。 将端口号更改为服务器应用程序中使用的端口。 使用端口，服务器应用的应用程序才能工作。
* 设置为"application/json"Accept 标头。 设置此标头指示服务器以 JSON 格式发送数据。

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>发送 GET 请求以检索资源

以下代码将发送一个产品的 GET 请求：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**GetAsync**方法将发送 HTTP GET 请求。 当方法完成时，它将返回**HttpResponseMessage**包含 HTTP 响应。 如果在响应中的状态代码是一个成功代码，响应正文将包含产品的 JSON 表示形式。 调用**ReadAsAsync**要反序列化到 JSON 有效负载`Product`实例。 **ReadAsAsync**方法是异步的因为响应正文可以是任意大。

**HttpClient** HTTP 响应包含错误代码时不引发异常。 相反， **IsSuccessStatusCode**属性是**false**如果状态为错误代码。 如果想要将视为异常的 HTTP 错误代码，调用[HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)响应对象上。 `EnsureSuccessStatusCode` 如果超出了范围 200 状态代码将引发异常&ndash;299。 请注意， **HttpClient**可能会由于其他原因引发异常&mdash;例如，如果请求超时。

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>媒体类型格式化程序用于反序列化

当**ReadAsAsync**调用不带任何参数，它使用一组默认的*媒体格式化程序*读取响应正文。 默认格式化程序支持 JSON、 XML 和窗体 url 编码数据。

而不是使用默认格式化程序，可以提供到格式化程序的列表**ReadAsAsync**方法。  使用格式化程序的列表是如果您有自定义媒体类型格式化程序：

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

有关详细信息，请参阅[ASP.NET Web API 2 中的媒体格式化程序](../formats-and-model-binding/media-formatters.md)

## <a name="sending-a-post-request-to-create-a-resource"></a>发送 POST 请求创建资源

下面的代码发送 POST 请求包含`Product`以 JSON 格式的实例：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**PostAsJsonAsync**方法：

* 序列化到 JSON 对象。
* 在 POST 请求中发送的 JSON 有效负载。

如果请求成功：

* 它应返回 201 （已创建） 响应。
* 响应位置标头中应该包含创建的资源的 URL。

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>发送 PUT 的请求以更新资源

以下代码将发送 PUT 请求将产品更新：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**PutAsJsonAsync**方法的工作方式类似于**PostAsJsonAsync**，只不过它将发送 PUT 请求，而不是 POST。

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>发送 DELETE 请求以删除资源

以下代码将发送 DELETE 请求删除某个产品：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

如 GET、 DELETE 请求没有请求正文。 不需要删除与指定 JSON 或 XML 格式。

## <a name="test-the-sample"></a>测试示例

若要测试客户端应用：

1. [下载](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)并运行服务器应用程序。 [下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。 验证服务器应用程序正常工作。 有关 exaxmple，`http://localhost:64195/api/products`应返回的产品的列表。
2. 设置 HTTP 请求的基 URI。 将端口号更改为服务器应用程序中使用的端口。
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. 运行客户端应用程序。 将生成以下输出：

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
