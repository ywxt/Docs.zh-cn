---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 09/17/2012
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 21ba186c11f39bbeedd1c320b98476ba13af27e2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819155"
---
<a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP Cookie
====================
通过[Mike Wasson](https://github.com/MikeWasson)

本主题介绍如何发送和接收 Web API 中的 HTTP cookie。

## <a name="background-on-http-cookies"></a>HTTP Cookie 的背景信息

本部分提供 cookie 在 HTTP 级别的实现方式的简要的概述。 有关详细信息，请查阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。

Cookie 是一种服务器发送的 HTTP 响应中的数据。 客户端 （可选） 将存储在 cookie，并返回对 subsequet 请求。 这允许客户端和服务器共享状态。 若要设置一个 cookie，服务器在响应中包含的 Set-cookie 标头。 Cookie 的格式是一个名称-值对，具有可选特性。 例如：

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

下面是包含属性的一个示例：

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

若要返回到服务器的 cookie，客户端在更高版本的请求中包括 Cookie 标头。

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 响应可以包括多个 Set-cookie 标头。

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

客户端返回使用单一的 Cookie 标头的多个 cookie。

[!code-console[Main](http-cookies/samples/sample5.cmd)]

作用域和 cookie 的持续时间受 Set-cookie 标头中的以下属性：

- **域**： 告知客户端的域应接收 cookie。 例如，如果域为"example.com"，客户端将 cookie 返回给每个子域 example.com。 如果未指定，域是源服务器。
- **路径**： 将 cookie 限制为在域中指定的路径。 如果未指定，则使用请求 URI 的路径。
- **过期**： 设置 cookie 的到期日期。 当它过期时，客户端删除的 cookie。
- **最大期限**： 设置 cookie 的最大生存期。 当它达到最大期限时，客户端删除的 cookie。

如果这两个`Expires`并`Max-Age`设置，`Max-Age`优先。 如果未设置，客户端将在当前会话结束时删除的 cookie。 （"会话"的确切含义由确定用户代理。）

但是，请注意，客户端可能会忽略 cookie。 例如，用户可能会禁用 cookie 出于隐私原因。 客户端可能会删除 cookie 之前到期，或限制 cookie 存储数。 出于隐私原因，客户端通常会拒绝"第三方"cookie，其中域与源服务器不匹配。 简单地说，服务器不应依赖于取回其设置的 cookie。

## <a name="cookies-in-web-api"></a>Web API 中的 cookie

若要添加到 HTTP 响应 cookie，创建**CookieHeaderValue**实例，它表示 cookie。 然后调用**AddCookies**扩展方法，它定义在**System.Net.Http。HttpResponseHeadersExtensions**类中，以添加该 cookie。

例如，下面的代码将添加的 cookie 中的控制器操作：

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

请注意， **AddCookies**采用的数组**CookieHeaderValue**实例。

若要从客户端请求中提取 cookie，调用**GetCookies**方法：

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

一个**CookieHeaderValue**包含一系列**CookieState**实例。 每个**CookieState**表示一个 cookie。 使用索引器方法来获取**CookieState**按名称，如所示。

## <a name="structured-cookie-data"></a>结构化的 Cookie 数据

很多浏览器限制它们将存储多少 cookie&#8212;总数，以及每个域数。 因此，它可用于结构化的数据置于单个 cookie，而不是设置多个 cookie。

> [!NOTE]
> RFC 6265 未定义 cookie 数据的结构。


使用**CookieHeaderValue**类，您可以将传递 cookie 数据的名称-值对的列表。 这些名称 / 值对编码为 URL 编码格式的 Set-cookie 标头中的数据：

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

前面的代码生成以下的 Set-cookie 标头：

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**CookieState**类提供了索引器的方法： 从请求消息中的 cookie 中读取子值：

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>示例： 设置和检索消息处理程序中的 Cookie

前面的示例显示如何使用从 Web API 控制器中的 cookie。 另一种方法是使用[消息处理程序](http-message-handlers.md)。 前面在控制器与管道中调用的消息处理程序。 消息处理程序可以请求到达控制器之前, 从请求中读取 cookie 或控制器生成响应后向响应添加 cookie。

![](http-cookies/_static/image2.png)

下面的代码演示创建的会话 Id 的消息处理程序。 会话 ID 存储在 cookie 中。 处理程序进行检查的会话 cookie 的请求。 如果请求不包含 cookie，该处理程序将生成一个新的会话 id。 在任一情况下，处理程序存储中的会话 ID **HttpRequestMessage.Properties**属性包。 它还添加到 HTTP 响应的会话 cookie。

此实现不会验证从客户端的会话 ID 实际上由服务器颁发。 不将其用作形式的身份验证 ！ 此示例的重点是显示 HTTP cookie 管理。

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

控制器可以获取会话 ID **HttpRequestMessage.Properties**属性包。

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
