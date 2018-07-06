---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 创建视图 (UI) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: eeaa36ede45b82afd112a270acf68105d1ae6dbc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820981"
---
<a name="create-the-view-ui"></a>创建视图 (UI)
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，您将开始定义的 HTML 应用程序中，并添加 HTML 和视图模型之间的数据绑定。

打开文件 Views/Home/Index.cshtml。 该文件的全部内容替换为以下。

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

大部分`div`元素是否有用于[Bootstrap](http://getbootstrap.com/)设置样式。 重要元素是与`data-bind`属性。 此属性链接到视图模型的 HTML。

例如：

[!code-html[Main](part-7/samples/sample2.html)]

在此示例中， &quot; `text` &quot;绑定会导致`<p>`元素以显示的值`error`从视图模型的属性。 请记住，`error`被声明为`ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

每当一个新值分配给`error`，Knockout 更新中的文本`<p>`元素。

`foreach`绑定告知 Knockout 可循环访问的内容`books`数组。 对于数组中每个项，Knockout 都创建一个新&lt;li&gt;元素。 绑定的上下文中的`foreach`引用对数组项的属性。 例如：

[!code-html[Main](part-7/samples/sample4.html)]

此处`text`绑定将读取每本书的作者属性。

如果您运行应用程序现在，它应如下所示：

![](part-7/_static/image1.png)

在页面加载后，以异步方式加载的书籍列表。 现在，&quot;详细信息&quot;链接不起作用。 我们将在下一节中添加此功能。

> [!div class="step-by-step"]
> [上一页](part-6.md)
> [下一页](part-8.md)
