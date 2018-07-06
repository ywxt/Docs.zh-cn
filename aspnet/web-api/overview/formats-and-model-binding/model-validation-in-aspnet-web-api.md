---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型验证 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/20/2012
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: be681a97a65a95a6bb83196d29c60ae750a523a1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820008"
---
<a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API 中的模型验证
====================
通过[Mike Wasson](https://github.com/MikeWasson)

当客户端将数据发送到 web API 时，通常要执行任何处理之前验证数据。 本文介绍如何对模型进行批注、 使用批注以进行数据验证和处理你的 web API 中的验证错误。

## <a name="data-annotations"></a>数据注释

在 ASP.NET Web API 中，可以使用中的属性[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间来对模型设置属性的验证规则。 请考虑以下模型：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

如果已在 ASP.NET MVC 中使用模型验证，这应该很熟悉。 **所需**属性指出`Name`属性不能为 null。 **范围**属性指出`Weight`必须是介于 0 和 999 之间。

假设客户端发送 POST 请求，其中以下 JSON 表示形式：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

您可以看到客户端未包括`Name`属性，它被标记为必需。 当 Web API 将转换为 JSON`Product`实例，它会验证`Product`针对验证特性。 在你的控制器操作，可以检查模型是否有效：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

模型验证不保证客户端数据的安全。 其他验证可能需要在应用程序的其他层中。 （例如，数据层可能会强制实施外键约束。）本教程[使用实体框架使用 Web API](../data/using-web-api-with-entity-framework/part-1.md)探讨了其中一些问题。

**"未得到充分发布"**： 客户端将省略某些属性会发生未得到充分的发布。 例如，假设客户端发送以下：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

在这里，客户端未指定值`Price`或`Weight`。 JSON 格式化程序将分配默认值为 0 到缺少的属性。

![](model-validation-in-aspnet-web-api/_static/image1.png)

模型状态无效，因为零是这些属性的有效值。 这是否是一个问题取决于你的方案。 例如，在更新操作中，可能想要区分"零"和"未设置。" 若要强制客户端可以设置一个值，使该属性可以为 null，并且已设置**所需**属性：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"过度发布"**： 客户端还可以将发送*详细*比预期的数据。 例如：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

在这里，JSON 包括中不存在的属性 ("Color")`Product`模型。 在这种情况下，JSON 格式化程序只需将忽略此值。 （XML 格式化程序执行相同操作。）如果您的模型具有你想要为只读属性，过度提交会导致问题。 例如：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

你不希望用户更新`IsAdmin`属性并将自己提升为管理员 ！ 最安全的策略是使用与客户端可以发送完全匹配的模型类：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson 的博客文章"[输入验证 vs。ASP.NET MVC 中的模型验证](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"具有未得到充分的发布和过度提交了适当探讨。 虽然文章是有关 ASP.NET MVC 2，但是是仍然与 Web API 相关的问题。


## <a name="handling-validation-errors"></a>处理验证错误

Web API 不会自动返回错误到客户端验证失败时。 负责检查模型状态并做出相应的响应的控制器操作。

此外可以创建一个操作筛选器来调用控制器操作之前检查模型状态。 下面的代码演示一个示例：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

如果模型验证失败，此筛选器将返回 HTTP 响应，其中包含验证错误。 在这种情况下，不会调用控制器操作。

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

若要将此筛选器应用于所有的 Web API 控制器，将添加到筛选器的实例**HttpConfiguration.Filters**在配置期间的集合：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

另一个选项是设置筛选器作为特性上各个控制器或控制器操作：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
