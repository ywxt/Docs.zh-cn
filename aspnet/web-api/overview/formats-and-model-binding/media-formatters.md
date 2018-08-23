---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2 中的媒体格式化程序 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: 7b7ba2fb3f1bba0447e700c84a017266cba305e6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833129"
---
<a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的媒体格式化程序
====================
通过[Mike Wasson](https://github.com/MikeWasson)

本教程演示如何在 ASP.NET Web API 中支持其他媒体格式。

## <a name="internet-media-types"></a>Internet 媒体类型

媒体类型，也称为 MIME 类型标识的一段数据的格式。 在 HTTP 中，媒体类型描述消息正文的格式。 媒体类型包含两个字符串、 类型和子类型。 例如：

- text/html
- image/png
- application/json

当 HTTP 消息包含实体正文时，Content-type 标头指定消息正文的格式。 这将告知接收方如何分析消息正文的内容。

例如，如果 HTTP 响应包含 PNG 图像，响应可能包含以下标头。

[!code-console[Main](media-formatters/samples/sample1.cmd)]

当客户端发送请求消息时，它可以包括 Accept 标头。 Accept 标头指示的服务器的媒体类型在客户端想要从该服务器。 例如：

[!code-console[Main](media-formatters/samples/sample2.cmd)]

此标头指示服务器在客户端希望 HTML、 XHTML 或 XML。

媒体类型确定 Web API 如何序列化和反序列化 HTTP 消息正文。 可以通过编写支持其他媒体类型和 web API 提供对 XML、 JSON、 BSON 和窗体 url 编码数据的内置支持*媒体格式化程序*。

若要创建媒体格式化程序，请从这些类之一派生：

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。 此类使用异步读取和写入方法。
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。 此类派生自**MediaTypeFormatter**但使用 sychronous 读/写方法。

派生自**BufferedMediaTypeFormatter**是更简单，因为没有异步代码，但它也意味着在 I/O 期间可以阻止调用线程。

## <a name="example-creating-a-csv-media-formatter"></a>示例： 创建 CSV 媒体格式化程序

下面的示例演示的媒体类型格式化程序可以序列化到以逗号分隔值 (CSV) 格式的产品对象。 此示例使用在本教程中定义的产品类型[创建支持 CRUD 操作的 Web API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。 下面是 Product 对象的定义：

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

若要实现 CSV 格式化程序，定义一个类，派生自**BufferedMediaTypeFormater**:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

在构造函数中，添加格式化程序支持的媒体类型。 在此示例中，格式化程序支持单一介质类型，&quot;文本/csv&quot;:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

重写**CanWriteType**方法，以指示该类型格式化程序可以序列化：

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

在此示例中，格式化程序可以序列化单个`Product`对象的集合、`Product`对象。

同样，重写**CanReadType**方法，以指示该类型格式化程序可以反序列化。 在此示例中，格式化程序不支持反序列化，因此，此方法只返回**false**。

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

最后，重写**WriteToStream**方法。 此方法通过向流写入序列化类型。 如果在格式化程序支持反序列化，还重写**ReadFromStream**方法。

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>将媒体格式化程序添加到 Web API 管道

若要添加的媒体类型格式化程序到 Web API 管道，请使用**格式化程序**上的属性**HttpConfiguration**对象。

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>字符编码

（可选） 媒体格式化程序可以支持多个字符编码，例如 utf-8 或 ISO 8859-1。

在构造函数中，添加一个或多个[System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx)类型向**SupportedEncodings**集合。 将默认的编码第一个。

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

在中**WriteToStream**并**ReadFromStream**方法，调用[MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx)选择首选的字符编码。 此方法与针对受支持的编码的列表的请求标头相匹配。 使用返回**编码**时读取或写入从流：

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
