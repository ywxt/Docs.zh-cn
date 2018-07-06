---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第 7 部分： 创建主页面 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: c5b6cb0f2e48cdea3d6cc5cde72d08a99126f05f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825630"
---
<a name="part-7-creating-the-main-page"></a>第 7 部分： 创建主页面
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>创建主页面

在本部分中，将创建主应用程序页。 此页会比在管理页中，更复杂，因此我们将在几个步骤中处理它。 此过程中，你将看到一些更高级的 Knockout.js 技术。 下面是基本页的布局：

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "产品"包含产品的数组。
- "购物车"包含产品数量与的数组。 单击"添加添加到购物车"更新购物车。
- "Orders"保留订单 Id 的数组。
- "详细信息"包含订单详细信息，这是一个数组项 （产品数量）

我们将开始通过不带任何数据绑定或脚本在 HTML 中，定义一些基本布局。 打开文件 Views/Home/Index.cshtml 并使用以下内容替换中的所有内容：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

接下来，添加脚本部分，并创建一个空的视图模型：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

根据前面质地的设计，我们的视图模型需要的产品、 购物车、 订单和详细信息可观察量。 添加以下变量添加到`AppViewModel`对象：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

用户可以将项从产品列表添加到购物车中，并从购物车中删除项目。 若要将这些功能封装，我们将创建表示产品的另一个视图模型类。 将下列代码添加到 `AppViewModel`：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel`类包含用于向 / 从购物车移动产品的两个函数：`addItemToCart`将该产品的一个单元添加到购物车中，和`removeAllFromCart`中移除所有的产品数量。

用户可以选择现有订单，并获取订单详细信息。 我们将封装此功能加入到另一个视图模型：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel`初始化采用的顺序，它通过向服务器发送 AJAX 请求提取订单详细信息。

另请注意`total`属性上的`OrderDetailsViewModel`。 此属性是一种特殊的可观察对象调用[计算可观察量](http://knockoutjs.com/documentation/computedObservables.html)。 如名称所示，计算可观察量可数据绑定到计算值&#8212;在这种情况下，总费用的顺序。

接下来，添加到这些函数`AppViewModel`:

- `resetCart` 从购物车中移除所有项。
- `getDetails` 获取订单的详细信息 (通过一个新的 p 通过`OrderDetailsViewModel`拖动到`details`列表)。
- `createOrder` 创建新订单并清空该购物车。


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

最后，通过发出 AJAX 请求的产品和订单初始化视图模型：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

好了，这是很多代码，但我们构建它向上逐步进行，因此希望设计已清除。 现在我们可以将某些 Knockout.js 绑定添加到 HTML。

**产品**

下面是产品列表的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

此循环访问产品数组并显示的名称和价格。 仅当用户登录时，则显示"添加到 Order"按钮。

"添加到 Order"按钮调用`addItemToCart`上`ProductViewModel`产品的实例。 此示例演示一个不错的功能的 Knockout.js： 当视图模型中包含其他视图模型时，可以应用这些绑定到的内部模型。 在此示例中，在绑定`foreach`应用于每个`ProductViewModel`实例。 这种方法是功能的将所有放到一个视图模型更加清晰。

**购物车**

下面是在购物车的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

此循环车数组并显示名称、 价格和数量。 请注意，"删除"链接和"创建订单"按钮绑定到视图模型的函数。

**订单**

下面是有关订单列表的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

此循环访问订单和显示订单 id。 链接的 click 事件绑定到`getDetails`函数。

**订单详细信息**

下面是订单详细信息的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

此循环按顺序的项并显示产品、 价格和数量。 周围的 div 是详细信息数组包含一个或多个项时才可见。

## <a name="conclusion"></a>结束语

在本教程中，您可以创建使用 Entity Framework 数据库和 ASP.NET Web API 提供面向公众的接口在数据层的顶部进行通信的应用程序。 我们使用 ASP.NET MVC 4 来呈现 HTML 页面和 Knockout.js 以及 jQuery，以提供动态交互，而无需重新加载页面。

其他资源：

- [ASP.NET 数据访问内容映射](https://msdn.microsoft.com/library/6759sth4.aspx)
- [实体框架开发人员中心](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [上一篇](using-web-api-with-entity-framework-part-6.md)
