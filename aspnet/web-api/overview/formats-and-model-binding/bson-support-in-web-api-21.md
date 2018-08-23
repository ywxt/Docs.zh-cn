---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: 在 ASP.NET Web API 2.1 对 BSON 的支持 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 709fb0266c0725176358a1bd0d08b3e07fa6e2a6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833893"
---
<a name="bson-support-in-aspnet-web-api-21"></a>在 ASP.NET Web API 2.1 对 BSON 的支持
====================
通过[Mike Wasson](https://github.com/MikeWasson)

Web API 2.1 引入了对 BSON 的支持。 本主题演示如何在 Web API 控制器 （服务器端） 和.NET 客户端应用中使用 BSON。

## <a name="what-is-bson"></a>BSON 是什么？

[BSON](http://bsonspec.org/)是一种二进制序列化格式。 "BSON"代表"二进制 JSON"，但 BSON 和 JSON 进行序列化有很大不同。 BSON 是"类似于 JSON 的"，因为对象表示为名称 / 值对，类似于 JSON。 不同于 JSON，数字数据类型存储为字节，不是字符串

BSON 旨在轻量、 易于扫描和快速地进行编码/解码。

- BSON 是可比得上大小为 JSON。 具体取决于数据，BSON 有效负载可能小于或大于 JSON 有效负载。 用于序列化二进制数据，如图像文件，BSON 小于 JSON，因为二进制数据不是 base64 编码。
- BSON 文档很容易扫描的原因是元素前缀长度的字段，因此分析器可以跳过，元素不解码它们。
- 编码和解码有效，因为是数值数据类型存储为数字，不是字符串。

本机客户端，如.NET 客户端应用可以受益于使用 BSON 代替基于文本的格式，如 JSON 或 XML 中。 对于浏览器客户端，您可能需要坚持使用 JSON，因为 JavaScript 直接转换 JSON 有效负载。

幸运的是，Web API 使用[内容协商](content-negotiation.md)，因此你的 API 可以支持这两种格式，并允许客户端选择。

## <a name="enabling-bson-on-the-server"></a>在服务器上启用 BSON

在 Web API 配置中，添加**BsonMediaTypeFormatter**到格式化程序集合。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

现在如果客户端请求"application/bson"，Web API 将使用 BSON 格式化程序。

若要将 BSON 与其他媒体类型相关联，请将它们添加到 SupportedMediaTypes 集合。 下面的代码添加到受支持的媒体类型"application/vnd.contoso":

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>示例 HTTP 会话

对于此示例中，我们将使用以下的 model 类以及一个简单的 Web API 控制器：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

客户端可能会发送以下 HTTP 请求：

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

下面是响应：

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

此处我已替换为二进制数据， &quot;。&quot;字符。 下面的屏幕截图所示 Fiddler 原始的十六进制值。

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>使用 HttpClient BSON

.NET 客户端应用程序可以使用 BSON 格式化程序与**HttpClient**。 有关详细信息**HttpClient**，请参阅[调用 Web API 从.NET 客户端](../advanced/calling-a-web-api-from-a-net-client.md)。

下面的代码将发送 GET 请求，用于接受 BSON，并随后在响应中的 BSON 有效负载反序列化。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

若要从服务器请求 BSON，设置为"application/bson"Accept 标头：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

若要反序列化响应正文，使用**BsonMediaTypeFormatter**。 此格式化程序不在默认格式化程序集合，因此你需要时读取响应正文中指定它：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

以下示例演示如何发送包含 BSON 的 POST 请求。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

此代码大部分是上一示例相同。 但在**PostAsync**方法中，指定**BsonMediaTypeFormatter**作为格式化程序：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>顶级基元类型进行序列化

BSON 的每个文档是键/值对的列表。BSON 规范并未定义用于序列化单个的原始值，例如整数或字符串的语法。

若要解决此限制， **BsonMediaTypeFormatter**基元类型视为一种特殊情况。 序列化之前, 它将值转换为键/值对使用密钥"值"。 例如，假设你的 API 控制器返回一个整数：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

序列化之前, BSON 格式化程序将此转换为以下键/值对：

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

当您反序列化时，格式化程序将数据转换回原始值。 但是，使用不同的 BSON 分析器的客户端将需要处理这种情况下，如果你的 web API 返回原始值。 一般情况下，应考虑返回结构化的数据，而不是原始值。

## <a name="additional-resources"></a>其他资源

[Web API BSON 示例](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[媒体格式化程序](media-formatters.md)
