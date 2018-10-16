---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: 属性路由在 ASP.NET Web API 2 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 22eb2fd748d52ec95e813ada8b1bf3b4826ad573
ms.sourcegitcommit: 6e6002de467cd135a69e5518d4ba9422d693132a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348476"
---
<a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的属性路由
====================
通过[Mike Wasson](https://github.com/MikeWasson)

*路由*是 Web API 如何匹配到某个操作的 URI。 Web API 2 支持一种新类型的路由，称为*的属性路由*。 顾名思义，属性路由使用属性定义的路由。 属性路由可以更好地控制 Uri 在你的 web API。 例如，您可以轻松创建描述层次结构的资源的 Uri。

早期样式的路由，名为基于约定的路由，但仍完全支持。 事实上，您可以组合在同一项目中的这两种技术。

本主题演示如何启用属性路由并描述了各种选项的属性路由。 有关使用属性路由的端到端教程，请参阅[使用 Web API 2 中的属性路由创建 REST API](create-a-rest-api-with-attribute-routing.md)。

## <a name="prerequisites"></a>系统必备

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、 Professional 或 Enterprise edition

或者，使用 NuGet 包管理器安装所需的包。 从**工具**在 Visual Studio 中，选择菜单**NuGet 包管理器**，然后选择**程序包管理器控制台**。 在包管理器控制台窗口中输入以下命令：

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>为什么属性路由？

使用 Web API 的第一版*基于约定的*路由。 在该类型的路由，则定义一个或多个路由模板，它们基本上是参数化字符串。 当框架收到请求时，它可匹配与路由模板的 URI。 (有关基于约定的路由的详细信息，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

基于约定的路由的一个优点是在单个位置，定义模板，并路由规则一致地应用于所有控制器。 遗憾的是，基于约定的路由会难以支持某些 URI 模式常用于 RESTful Api。 例如，资源通常包含子资源： 客户拥有订单、 电影具有参与者、 丛书有作者，等等。 很自然地创建反映这些关系的 Uri:

`/customers/1/orders`

此类型的 URI 很难创建使用基于约定的路由。 尽管可以完成，结果不能扩展，如果有多个控制器或资源类型。

属性路由中，它就很简单，此 uri 定义路由。 您只需将属性添加到控制器操作：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

以下是一些其他路由使简单的模式。

**API 版本控制**

在此示例中，"/ api/v1/产品"将路由到控制器不同"/ api/v2/产品"。

`/api/v1/products`
`/api/v2/products`

**重载的 URI 段**

在此示例中，"1"是订单号，但是"挂起"映射到集合。

`/orders/1`
`/orders/pending`

**多个参数类型**

在此示例中，"1"是订单号，但指定一个日期，"2013年/06/16"。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>启用属性路由

若要启用的属性路由，请调用**MapHttpAttributeRoutes**在配置过程。 此扩展方法中定义**System.Web.Http.HttpConfigurationExtensions**类。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

属性路由可以与组合[基于约定的](routing-in-aspnet-web-api.md)路由。 若要定义基于约定的路由，请调用**MapHttpRoute**方法。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

有关配置 Web API 的详细信息，请参阅[配置 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意： 从 Web API 1 迁移

在 Web API 2 之前的 Web API 项目模板生成的代码如下：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

如果启用属性路由，则此代码将引发异常。 如果升级现有的 Web API 项目，以使用属性路由，请务必更新此配置代码所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 有关详细信息，请参阅[配置与 ASP.NET 托管的 Web API](../advanced/configuring-aspnet-web-api.md#webhost)。


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>添加路由属性

下面是路由的使用属性定义的示例：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

将字符串&quot;客户 / {customerId} orders&quot;是用于路由的 URI 模板。 Web API 会尝试匹配请求 URI 的模板。 在此示例中，"客户"和"orders"文本段，并且在"{customerId}"是一个变量参数。 下面的 Uri 与此模板相匹配：

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

你可以限制通过匹配[约束](#constraints)，本主题后面所述。

请注意， &quot;{customerId}&quot;路由模板中的参数的名称匹配*customerId*方法中的参数。 当 Web API 调用的控制器操作时，它会将路由参数绑定。 例如，如果 URI 是`http://example.com/customers/1/orders`，Web API 将尝试绑定的值"1"向*customerId*操作中的参数。

URI 模板可以具有多个参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

路由属性不具有任何控制器方法使用基于约定的路由。 这样一来，您可以组合这两种类型的同一个项目中的路由。

## <a name="http-methods"></a>HTTP 方法

Web API 还将选择操作请求 （GET、 POST 等） 的 HTTP 方法。 默认情况下，Web API 将查找与控制器方法名称的开头的不区分大小写匹配。 例如，名为的控制器方法`PutCustomers`匹配 HTTP PUT 请求。

以下属性来修饰的方法与任何替代此约定：

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

下面的示例将 CreateBook 方法映射到 HTTP POST 请求。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

对于所有其他 HTTP 方法，包括非标准的方法，使用**AcceptVerbs**属性，它使用的 HTTP 方法列表。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>路由前缀

通常情况下，所有以相同前缀开头的控制器中路由。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

可以通过使用针对整个控制器设置公共前缀 **[RoutePrefix]** 属性：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

使用 method 属性上颚化符 （~） 重写的路由前缀：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

路由前缀可以包含参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>路由约束

路由约束让你限制如何匹配路由模板中的参数。 常规语法&quot;{参数： 约束}&quot;。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

在这里，第一个路由将仅选择如果&quot;id&quot; URI 段是一个整数。 否则，将选择第二个路由。

下表列出了支持的约束。

| 约束 | 描述 | 示例 |
| --- | --- | --- |
| alpha | 匹配大写或小写字符 (-z、 A-Z) | {x: alpha} |
| bool | 匹配一个布尔值。 | {x: bool} |
| datetime | 匹配项**DateTime**值。 | {x: datetime} |
| decimal | 匹配十进制值。 | {x： 小数} |
| double | 与 64 位浮点值匹配。 | {x： 双} |
| float | 与 32 位浮点值匹配。 | {x: float} |
| guid | 匹配的 GUID 值。 | {x: guid} |
| int | 与 32 位整数值匹配。 | {x: int} |
| length | 与具有指定长度或长度的指定范围内的字符串匹配。 | {x: length(6)}{x: length(1,20)} |
| long | 与 64 位整数值匹配。 | {x： 长时间} |
| max | 匹配一个整数，其最大值。 | {x:max(10)} |
| maxlength | 与最大长度的字符串匹配。 | {x: maxlength(10)} |
| min | 匹配一个整数，其最小值。 | {x: min(10)} |
| minlength | 与最小长度的字符串相匹配。 | {x: minlength(10)} |
| range | 一个整数值的范围内的匹配项。 | {x: range(10,50)} |
| 正则表达式 | 与正则表达式匹配。 | {x: regex(^\d{3}-\d{3}-\d{4}$)} |

请注意，某些约束，如&quot;min&quot;，在括号中采用自变量。 可以将多个约束应用于参数，用冒号分隔。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>自定义路由约束

您可以通过实现来创建自定义路由约束**IHttpRouteConstraint**接口。 例如，以下限制将限制为非零的整数值的参数。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

下面的代码演示如何注册该约束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

现在可以将约束应用在路由中：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

也可以替换整个**DefaultInlineConstraintResolver**类的实现**IInlineConstraintResolver**接口。 执行此操作将替换的所有内置的约束，除非你的实现**IInlineConstraintResolver**专门将它们添加。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>可选 URI 参数和默认值

可以通过将问号添加到路由参数，使 URI 参数可选。 如果某个路由参数是可选的则必须定义方法参数的默认值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

在此示例中，`/api/books/locale/1033`和`/api/books/locale`返回相同的资源。

或者，可以指定在路由模板中，默认值，如下所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

这是上一示例中，几乎相同，但没有行为的细微的差别在于时应用的默认值。

- 在第一个示例 ("{lcid？}") 中，1033年的默认值是直接分配给方法参数，因此该参数会将此确切值。
- 在第二个示例 ("{lcid = 1033年}")，"1033"的默认值都通过模型绑定过程。 默认模型联编程序会将数字值 1033年为"1033"。 但是，您可以插入自定义模型联编程序，这可能会执行一些不同。

（在大多数情况下，除非你有自定义模型绑定器在管道中的两种形式将等效。）

<a id="route-names"></a>
## <a name="route-names"></a>路由名称

在 Web API 中，每个路由都有一个名称。 路由名称可用于生成链接，以便可以在 HTTP 响应中包含一个链接。

若要指定路由名称，设置**名称**特性的属性。 下面的示例演示如何设置路由名称，以及如何生成一个链接时使用的路由名称。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>路由顺序

当框架尝试匹配与路由的 URI 时，它会评估按特定顺序的路由。 若要指定的顺序，将设置**顺序**路由属性上的属性。 首先计算较低的值。 默认顺序值为零。

下面是如何确定总排序：

1. 比较**顺序**路由属性的属性。
2. 查看路由模板中的每个 URI 段。 为每个段进行排序，如下所示：

    1. 文本段。
    2. 将路由参数的约束。
    3. 不受限制的路由参数。
    4. 通配符参数具有约束的段。
    5. 通配符参数不受限制的段。
3. 对于一个路由排序不区分大小写的序号字符串比较 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) 的路由模板。

这是一个示例。 假设定义以下控制器：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

这些路由排序，如下所示。

1. 订单/详细信息
2. 订单 / {id}
3. orders/{customerName}
4. orders/{\*date}
5. 订单 / 挂起

请注意"详细信息"是一个文本段和出现之前"{id}"，但"挂起"会显示上一次由于**顺序**属性为 1。 (本示例假定那里没有客户名为"详细信息"或"挂起"。 一般情况下，尝试避免不明确的路由。 在此示例中，更好的路由模板`GetByCustomer`是"客户 / {customerName}")
