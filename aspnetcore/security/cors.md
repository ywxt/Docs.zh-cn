---
title: 启用 ASP.NET Core 中的跨域请求 (CORS)
author: rick-anderson
description: 了解如何作为一种标准允许或拒绝在 ASP.NET Core 应用中的跨域请求的 CORS。
ms.author: riande
ms.date: 08/17/2018
uid: security/cors
ms.openlocfilehash: 0dbb7933c76bb0d1d0cab519ea08c6c8f0ebedfd
ms.sourcegitcommit: 64c2ca86fff445944b155635918126165ee0f8aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2018
ms.locfileid: "41832674"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a>启用 ASP.NET Core 中的跨域请求 (CORS)

作者：[Mike Wasson](https://github.com/mikewasson)、[Shayne Boyer](https://twitter.com/spboyer) 和 [Tom Dykstra](https://github.com/tdykstra)

浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。 此限制称为“同源策略”，可防止恶意站点读取另一个站点中的敏感数据。 但是，有时你可能需要允许其他站点对你的 Web API 进行跨域请求。

[跨域资源共享](http://www.w3.org/TR/cors/)(CORS) 是一种 W3C 标准，允许服务器放宽同源策略。 使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。 CORS 比早期技术（例如 [JSONP](https://wikipedia.org/wiki/JSONP)）更安全、更灵活。 本主题演示如何在 ASP.NET Core 应用程序中启用 CORS。

## <a name="what-is-same-origin"></a>什么是"相同的原点"？

如果它们具有相同方案、 主机和端口，两个 Url 将具有相同的原点。 ([RFC 6454](http://tools.ietf.org/html/rfc6454))

以下两个 Url 具有相同的原点：

* `http://example.com/foo.html`

* `http://example.com/bar.html`

这些 Url 有两个相对上一不同的源：

* `http://example.net` -不同的域

* `http://www.example.com/foo.html` -不同的子域

* `https://example.com/foo.html` -不同的方案

* `http://example.com:9000/foo.html` -不同的端口

> [!NOTE]
> 比较来源时，Internet Explorer 不会考虑该端口。

## <a name="enable-cors"></a>启用 CORS

::: moniker range="<= aspnetcore-1.1"

若要为应用程序设置 CORS，请将 `Microsoft.AspNetCore.Cors` 包添加到项目。

::: moniker-end

调用[AddCors](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors)中`Startup.ConfigureServices`:

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors)]

## <a name="enabling-cors-with-middleware"></a>使用中间件启用 CORS

若要启用 CORS，请将 CORS 中间件添加到请求管道使用`UseCors`扩展方法。 CORS 中间件必须位于之前定义的任何终结点应用程序中你想要支持跨域请求 (例如，对任何调用之前`UseMvc`)。

添加 CORS 中间件使用时，可以指定跨域策略[CorsPolicyBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors)类。 有两种方法可以实现此目的。 第一种是调用`UseCors`lambda:

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

**注意：** 不含尾部斜杠，必须指定的 URL (`/`)。 如果 URL 以终止`/`，该比较将返回`false`，并将返回无标头。

Lambda 采用`CorsPolicyBuilder`对象。 您会发现一系列[配置选项](#cors-policy-options)本主题中更高版本。 在此示例中，该策略允许跨域请求从`http://example.com`和任何其他来源。

CorsPolicyBuilder 具有 fluent API，因此您可以将方法调用链接：

[!code-csharp[](../security/cors/sample/CorsExample3/Startup.cs?highlight=3&range=29-32)]

第二种方法是定义一个或多个命名的 CORS 策略，并在运行时按名称然后选择的策略。

[!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin)]

此示例将添加一个名为"AllowSpecificOrigin"的 CORS 策略。 若要选择的策略，将名称传递给`UseCors`。

## <a name="enabling-cors-in-mvc"></a>在 MVC 启用 CORS

您或者可以使用 MVC 应用每个操作，每个控制器，或全局范围内的所有控制器特定 CORS。 使用 MVC 启用 CORS 时都使用相同的 CORS 服务，但 CORS 中间件不是。

### <a name="per-action"></a>每个操作

若要指定特定操作的 CORS 策略添加`[EnableCors]`属性为该操作。 指定策略名称。

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction)]

### <a name="per-controller"></a>每个控制器

若要指定特定控制器的 CORS 策略添加`[EnableCors]`属性到控制器类。 指定策略名称。

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController)]

### <a name="globally"></a>全局

您可以启用 CORS 全球所有控制器通过添加`CorsAuthorizationFilterFactory`筛选器添加到全局筛选器集合：

[!code-csharp[](cors/sample/CorsMVC/Startup2.cs?name=snippet_configureservices)]

优先顺序是： 操作、 控制器、 全局。 操作级别的策略优先于控制器级别的策略，并且控制器级别的策略优先于全局策略。

### <a name="disable-cors"></a>禁用 CORS

若要禁用 CORS 的控制器或操作，请使用`[DisableCors]`属性。

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction)]

## <a name="cors-policy-options"></a>CORS 策略选项

本部分介绍您可以在 CORS 策略设置的各种选项。

* [设置允许的来源](#set-the-allowed-origins)

* [设置允许的 HTTP 方法](#set-the-allowed-http-methods)

* [设置允许的请求标头](#set-the-allowed-request-headers)

* [设置公开的响应标头](#set-the-exposed-response-headers)

* [跨域请求中的凭据](#credentials-in-cross-origin-requests)

* [将预检过期时间设置](#set-the-preflight-expiration-time)

有关一些选项，可能会有帮助读取[如何 CORS 工作](#how-cors-works)第一个。

### <a name="set-the-allowed-origins"></a>设置允许的来源

若要允许一个或多个特定源：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=19-23)]

若要允许所有来源：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs??range=27-31)]

允许任何来源的请求之前，请仔细考虑。 这意味着几乎任何网站可以进行 AJAX 调用 API。

### <a name="set-the-allowed-http-methods"></a>设置允许的 HTTP 方法

若要允许所有 HTTP 方法：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=44-49)]

这会影响预检请求和访问的控制的允许的方法标头。

### <a name="set-the-allowed-request-headers"></a>设置允许的请求标头

CORS 预检请求可能包括一个访问控制的请求标头标头，列出应用程序设置的 HTTP 标头 (所谓"author 请求标头")。

到允许列表的特定标头：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=53-58)]

若要允许所有作者的请求标头：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=62-67)]

浏览器不在它们如何设置访问控制的请求标头完全一致。 如果将标头设置到的任何内容不是"*"，您至少应包含"接受"，"内容类型"，，和"源"，以及你想要支持任何自定义标头。

### <a name="set-the-exposed-response-headers"></a>设置公开的响应标头

默认情况下，在浏览器不会公开所有向应用程序的响应标头。 (请参阅[ http://www.w3.org/TR/cors/#simple-response-header ](http://www.w3.org/TR/cors/#simple-response-header)。)默认情况下可用的响应标头是：

* Cache-Control

* 内容语言

* Content-Type

* 过期

* 上次修改

* 杂注

CORS 规范调用这些*简单响应标头*。 要使其他标头可用于应用程序：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=71-76)]

### <a name="credentials-in-cross-origin-requests"></a>跨域请求中的凭据

凭据要求特殊处理 CORS 请求中。 默认情况下，在浏览器不会发送与跨域请求的任何凭据。 凭据包含 cookie，以及 HTTP 身份验证方案。 若要发送凭据与跨域请求，客户端必须设置为 true 的 XMLHttpRequest.withCredentials。

直接使用 XMLHttpRequest:

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://www.example.com/api/test');
xhr.withCredentials = true;
```

在 jQuery 中：

```jQuery
$.ajax({
  type: 'get',
  url: 'http://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

此外，服务器必须允许凭据。 若要允许跨域凭据：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=80-85)]

现在，HTTP 响应将包括一个访问控制的允许的凭据标头，服务器允许跨域请求凭据将告诉浏览器。

如果浏览器发送的凭据，但响应不包含有效的访问控制的允许的凭据标头，在浏览器就不会暴露给应用程序，响应和 AJAX 请求失败。

允许跨域凭据时要小心。 在另一个域的网站可以向应用而无需在用户不知情的用户的名义发送登录的用户的凭据。 CORS 规范还会说明该设置到来源`"*"`（所有来源） 是无效的如果`Access-Control-Allow-Credentials`标头。

### <a name="set-the-preflight-expiration-time"></a>将预检过期时间设置

访问控制的最大有效期标头指定可以缓存预检请求的响应的时间。 若要设置此标头：

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=89-94)]

<a name="cors-how-cors-works"></a>

## <a name="how-cors-works"></a>CORS 的工作原理

本部分介绍在 CORS 请求的 HTTP 消息级别中会发生什么情况。 请务必了解，以便可以正确配置和调试时出现意外的行为的 CORS 策略 CORS 的工作原理。

CORS 规范引入了几个新的 HTTP 标头启用跨域请求。 如果浏览器支持 CORS，则将设置自动跨域请求这些标头。 自定义 JavaScript 代码不需要启用 CORS。

下面是跨域请求的示例。 `Origin`标头提供发出请求的站点的域：

```
GET http://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: http://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: http://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

如果服务器允许该请求，则将在响应中设置访问控制的允许的域标头。 此标头的值匹配源标头从请求，或为通配符值"*"，允许任何源的含义：

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

如果响应不包含访问控制的允许的域标头，AJAX 请求失败。 具体而言，在浏览器不允许该请求。 即使服务器返回成功的响应，请在浏览器不会使响应可供客户端应用程序。

### <a name="preflight-requests"></a>预检请求

对于某些 CORS 请求，浏览器发送额外的请求，名为"预检请求，"，再发送实际请求的资源。 在浏览器可以跳过预检请求，如果满足以下条件：

* 请求方法是 GET、 HEAD 或 POST，和

* 应用程序不会设置之外接受，接受语言的内容语言，任何请求标头内容类型或最后一个事件 ID 和

* 内容类型标头 (如果设置) 是以下之一：

  * application/x-www-form-urlencoded

  * 多部分/窗体数据

  * 文本/无格式

有关请求标头规则适用于通过 XMLHttpRequest 对象上调用 setRequestHeader 来设置应用程序的标头。 （CORS 规范调用这些"作者请求标头"。）此规则不适用于在浏览器可以设置，例如用户代理、 主机或内容长度标头。

下面是预检请求的示例：

```
OPTIONS http://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: http://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

预检请求使用 HTTP OPTIONS 方法。 它包括两个特殊的标头：

* 访问控制的请求的方法： 将用作实际请求 HTTP 方法。

* 访问的控件的请求的标头： 在实际请求的应用程序设置的请求标头的列表。 （同样，这不包括在浏览器设置的标头。）

下面是示例响应中，假定服务器允许请求：

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

响应包括访问的控制的允许的方法标头，其中列出了允许的方法，和 （可选） 访问的控制的允许的标头标头，其中列出了允许的标头。 如果预检请求成功，则浏览器发送实际请求，如前面所述。
