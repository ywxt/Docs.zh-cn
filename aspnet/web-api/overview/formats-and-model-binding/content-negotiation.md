---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: 内容协商 ASP.NET Web API 中的 |Microsoft Docs
author: MikeWasson
description: 介绍如何 ASP.NET Web API 实现 HTTP 内容协商。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/20/2012
ms.topic: article
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: c4e7a0c2601ca60f081876e83757997a2e920298
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368924"
---
<a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API 中的内容协商
====================
通过[Mike Wasson](https://github.com/MikeWasson)

本指南介绍了 ASP.NET Web API 如何实现内容协商。

HTTP 规范 (RFC 2616) 定义为"有可用的多种表示形式时选择的最佳表示对于给定的响应的处理。"的内容协商 在 HTTP 内容协商的主要机制是这些请求标头：

- **接受：** 哪些媒体类型是可接受的响应，如"application/json;"的"application/xml"或自定义媒体类型，如&quot;application/vnd.example+xml&quot;
- **接受字符集：** 哪些字符集是可以接受的如 utf-8 或 ISO 8859-1。
- **接受的编码：** 哪种内容编码是可以接受的例如 gzip。
- **接受语言：** 首选的自然语言，例如"en-我们"。

服务器还可以查看在 HTTP 请求的其他部分。 例如，如果请求包含 X-请求-具有标头，指示 AJAX 请求，服务器可能默认为 JSON 没有 Accept 标头是否。

在本文中，我们将介绍 Web API 如何使用 Accept 和 Accept-charset 标头。 （在此期间，用于接受编码或接受语言没有内置支持。)

## <a name="serialization"></a>序列化

如果 Web API 控制器返回作为 CLR 类型的资源，管道将序列化为返回值，并将其写入到 HTTP 响应正文。

例如，考虑以下控制器操作：

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

客户端可能会发送此 HTTP 请求：

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

在响应中，可能会发送服务器：

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

在此示例中，客户端请求的 JSON、 Javascript 或"任何"(\*/\*)。 服务器响应的 JSON 表示形式的`Product`对象。 请注意，在响应中的内容类型标头设置为&quot;应用程序 /json&quot;。

此外可以返回一个控制器**HttpResponseMessage**对象。 若要指定响应正文的 CLR 对象，调用**CreateResponse**扩展方法：

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

此选项可提供更好地控制响应的详细信息。 可以设置的状态代码，添加 HTTP 标头，等等。

序列化该资源的对象称为*媒体格式化程序*。 媒体格式化程序派生自**MediaTypeFormatter**类。 Web API 提供媒体格式化程序的 XML 和 JSON，并且可以创建自定义格式化程序，以支持其他媒体类型。 有关编写自定义格式化程序的信息，请参阅[媒体格式化程序](media-formatters.md)。

## <a name="how-content-negotiation-works"></a>如何在内容协商的工作原理

首先，获取管道**IContentNegotiator**服务从**HttpConfiguration**对象。 它还可以获取从媒体格式化程序的列表**HttpConfiguration.Formatters**集合。

接下来，调用管道**IContentNegotiatior.Negotiate**、 传入：

- 要序列化的对象类型
- 媒体格式化程序的集合
- HTTP 请求

**Negotiate**方法将返回两条信息：

- 若要使用的格式化程序
- 响应的媒体类型

如果不找到任何格式化程序，则**Negotiate**方法将返回**null**，和客户端收到 HTTP 错误 406 （不可接受）。

下面的代码演示如何在控制器可直接调用内容协商：

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

此代码等同于管道自动执行。

## <a name="default-content-negotiator"></a>默认内容协商者

**为 DefaultContentNegotiator**类提供的默认实现**IContentNegotiator**。 它使用多个条件来选择格式化程序。

首先，格式化程序必须能够序列化该类型。 这通过调用验证**MediaTypeFormatter.CanWriteType**。

接下来，内容协商者会查看每个格式化程序，并计算结果的 HTTP 请求与匹配的程度。 若要评估匹配，内容协商者查看两件事上个格式化程序：

- **SupportedMediaTypes**集合，其中包含受支持的媒体类型的列表。 内容协商者尝试匹配此列表中对请求的 Accept 标头。 请注意，Accept 标头可以包含范围。 例如，"text/plain"是文本的匹配项 /\*或\* / \*。
- **MediaTypeMappings**集合，其中包含一系列**MediaTypeMapping**对象。 **MediaTypeMapping**类提供的 HTTP 请求匹配的媒体类型的泛型方法。 例如，它可以将自定义 HTTP 标头映射到某个特定媒体类型。

如果有多个匹配，与最高的质量因子 wins 的匹配项。 例如：

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

在此示例中，应用程序 /json 具有值为 1.0，隐式的质量因子，因此它对应用程序/xml 是首选。

如果不找到任何匹配项，内容协商者尝试匹配上的媒体类型的请求正文中，如果有的话。 例如，如果请求包含 JSON 数据，为 JSON 格式化程序将查找的内容协商者。

如果仍有没有匹配项，内容协商者只需选择可以序列化该类型的第一个格式化程序。

## <a name="selecting-a-character-encoding"></a>选择一种字符编码

内容协商选择格式化程序后，选择通过查看的最佳字符编码**SupportedEncodings**属性格式化程序，并将其与请求中的 Accept-charset 标头匹配 （如果有）。
