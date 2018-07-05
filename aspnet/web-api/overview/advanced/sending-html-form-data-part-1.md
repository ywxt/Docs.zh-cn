---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: ASP.NET Web API 中发送 HTML 窗体数据： 窗体 url 编码的数据 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/15/2012
ms.topic: article
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 24410c92df828d4aaaa3b91dd3e9fa14575fd300
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399865"
---
<a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>ASP.NET Web API 中发送 HTML 窗体数据： 窗体 url 编码的数据
====================
通过[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>第 1 部分： 窗体 url 编码的数据

本文介绍如何发布到 Web API 控制器的窗体 url 编码数据。

- [HTML 窗体概述](#overview_of_html_forms)
- [发送复杂类型](#sending_complex_types)
- [发送通过 AJAX 的窗体数据](#sending_form_data_via_ajax)
- [发送简单类型](#sending_simple_types)

> [!NOTE]
> [下载已完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML 窗体概述

HTML 窗体使用是 GET 或 POST 将数据发送到服务器。 **方法**的属性**窗体**元素提供的 HTTP 方法：

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

默认方法是 GET。 如果该窗体使用 GET 的表单数据编码的 URI 作为查询字符串中。 如果该窗体使用 POST，窗体数据放置在请求正文中。 已过帐数据**enctype**属性指定请求正文的格式：

| enctype | 描述 |
| --- | --- |
| application/x-www-form-urlencoded | 表单数据编码为名称/值对，类似于 URI 查询字符串。 这是 POST 的默认格式。 |
| 多部分/窗体数据 | 表单数据编码为多部分 MIME 消息。 如果将文件上载到服务器，请使用此格式。 |

这篇文章的第 1 部分着重于 x-www 的窗体的 urlencoded 格式。 [第 2 部分](sending-html-form-data-part-2.md)介绍多部分 MIME。

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>发送复杂类型

通常情况下，将发送来自多个窗体控件的值所组成的复杂类型。 请考虑以下模型表示的状态更新：

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

下面是接受一个 Web API 控制器`Update`通过 POST 的对象。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> 使用此控制器[基于操作的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由模板是&quot;api / {controller} / {action} / {id}&quot;。 客户端将发布到数据&quot;/api/updates/complex&quot;。


现在让我们来编写用户提交状态更新的 HTML 窗体。

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

请注意，**操作**窗体上的属性是我们的控制器操作的 URI。 下面是在窗体中输入的某些值：

![](sending-html-form-data-part-1/_static/image1.png)

当用户单击提交时，则在浏览器发送 HTTP 请求与以下类似：

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

请注意请求正文包含格式为名称/值对的窗体数据。 Web API 会自动将名称/值对转换到的实例`Update`类。

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>发送通过 AJAX 的窗体数据

当用户提交窗体时，浏览器导航离开当前页面，并呈现响应消息的正文。 响应是 HTML 页时，这没有关系。 使用 web API，但是，响应正文是通常为空或包含结构化的数据，例如 JSON。 在这种情况下，它更有意义发送请求时使用 AJAX 的窗体数据，以便页面可以处理响应。

下面的代码演示如何使用 jQuery 表单数据发布。

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery**提交**函数将窗体操作替换的新函数。 这会替代提交按钮的默认行为。 **序列化**函数将窗体数据序列化到名称/值对。 若要将窗体数据发送到服务器，请调用`$.post()`。

请求完成时，`.success()`或`.error()`处理程序为用户显示相应的消息。

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>发送简单类型

在前面部分中，我们发送一个复杂类型，Web API 的反序列化为模型类的实例。 此外可以发送简单类型，如字符串。

> [!NOTE]
> 在发送前一种简单类型，请考虑将值改为包装在复杂类型。 这使您在服务器端的模型验证的优点，并轻松地根据需要扩展您的模型。


若要发送的简单类型的基本步骤都相同，但两个略有不同。 首先，在控制器中，必须修饰参数名称后的加**FromBody**属性。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

默认情况下，Web API 尝试从请求 URI 中获取简单类型。 **FromBody**属性告知 Web API，可从请求正文中读取值。

> [!NOTE]
> Web API 响应正文读取最多一次，因此，只有一个参数的操作可以来自请求正文。 如果需要从请求正文中获取多个值，定义复杂类型。


其次，客户端需要发送具有以下格式的值：

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

具体而言，名称/值对的名称部分必须为空的简单类型。 并非所有浏览器都支持这对于 HTML 窗体，但此格式的脚本中创建，如下所示：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

下面是示例窗体：

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

和下面是脚本来提交窗体值。 与前面的脚本的唯一区别是传递到的参数**发布**函数。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

可以使用相同的方法将发送一个简单类型数组：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>其他资源

[第 2 部分： 文件上传和多部分 MIME](sending-html-form-data-part-2.md)
