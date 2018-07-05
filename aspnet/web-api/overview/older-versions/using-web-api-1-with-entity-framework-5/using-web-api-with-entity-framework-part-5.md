---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第 5 部分： 使用 Knockout.js 创建动态 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: 7d8bd4732ecf73c14251ceebfd667310f6e197b4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37801688"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>第 5 部分： 使用 Knockout.js 创建动态 UI
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>使用 Knockout.js 创建动态 UI

在本部分中，我们将使用 Knockout.js 将功能添加到管理员视图。

[Knockout.js](http://knockoutjs.com/)是一个 Javascript 库，它可以更轻松地将 HTML 控件绑定到数据。 Knockout.js 使用模型-视图-视图模型 (MVVM) 模式。

- *模型*（在我们的用例、 产品和订单） 的业务域中的数据的服务器端表示形式。
- *视图*是表示层 (HTML)。
- *视图模型*是 Javascript 对象，用于保存模型数据。 视图模型是在 ui 的代码抽象。 它并不知道 HTML 表示形式。 相反，它表示抽象视图，例如"的项列表"的功能。

该视图是数据绑定到视图模型。 向视图模型的更新会自动反映在视图中。 视图模型还获取从视图中，如按钮单击事件，并对该模型，例如，创建订单执行操作。

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

首先，我们将定义视图模型。 之后，我们将向视图模型绑定的 HTML 标记。

将以下 Razor 部分添加到 Admin.cshtml:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

可以在文件中的任意位置添加此部分。 呈现视图时，在 HTML 页的底部会出现的部分是否在关闭前右键&lt;/b o d&gt;标记。

所有的此页的脚本将放入注释所指示的脚本标记：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

首先，定义一个视图模型类：

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**ko.observableArray**是一种特殊的 Knockout，调用中的对象*可观察量*。 从[Knockout.js 文档](http://knockoutjs.com/documentation/observables.html)： 可观察量是"JavaScript 对象，它可以通知有关更改的订阅服务器。" 当一个可观测对象的内容更改时，视图将自动更新以匹配。

若要填充`products`数组中向 web API 发出 AJAX 请求。 还记得我们存储的基 URI 的视图包中的 API (请参阅[第 4 部分](using-web-api-with-entity-framework-part-4.md)本教程的)。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

接下来，将函数添加到视图模型来创建、 更新和删除产品。 这些函数将提交到 web API 的 AJAX 调用，并使用结果更新视图模型。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

现在最重要的部分： DOM 时是 fulled 加载，调用**ko.applyBindings**函数并传递中的新实例`ProductsViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**Ko.applyBindings**方法激活 Knockout，并将视图模型连接到视图。

现在，我们有一个视图模型，我们可以创建绑定。 Knockout.js，在您执行此操作通过添加`data-bind`属性到 HTML 元素。 例如，若要将 HTML 列表绑定到一个数组，使用`foreach`绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach`绑定循环访问数组和数组中创建子元素的每个对象。 数组对象的属性可以引用上的子元素的绑定。

将以下绑定添加到"产品更新"列表：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>`元素的作用域中出现**foreach**绑定。 表示 Knockout 将呈现一次的每个产品中的元素`products`数组。 所有内绑定`<li>`元素引用该产品实例。 例如，`$data.Name`是指`Name`产品上的属性。

若要设置的文本输入的值，使用`value`绑定。 按钮绑定到函数上的模型-视图，使用`click`绑定。 Product 实例作为参数传递给每个函数。 有关详细信息[Knockout.js 文档](http://knockoutjs.com/documentation/observables.html)具有很好的各种绑定的说明。

接下来，添加的绑定**提交**添加产品窗体上的事件：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

此绑定调用`create`视图模型来创建一个新的产品上的函数。

下面是管理员视图的完整代码：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

运行应用程序、 管理员帐户，登录并单击"管理员"链接。 应看到的产品列表，并能够创建、 更新或删除产品。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-4.md)
> [下一页](using-web-api-with-entity-framework-part-6.md)
