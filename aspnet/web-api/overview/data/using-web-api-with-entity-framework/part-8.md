---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 显示项的详细信息 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 268c44f842cc2beb32a0a3e4c74b83b7ca9fd787
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375170"
---
<a name="display-item-details"></a>显示项详细信息
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，将添加能够查看每个工作簿的详细信息。 在 app.js 中，将添加到视图模型的以下代码：

[!code-javascript[Main](part-8/samples/sample1.js)]

在 Views/Home/Index.cshtml，数据绑定元素添加到详细信息链接：

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

这会将绑定的单击处理程序&lt;&gt;元素`getBookDetail`视图模型上的函数。

在同一文件中，将为以下标记上：

[!code-html[Main](part-8/samples/sample3.html)]

替换为以下内容：

[!code-html[Main](part-8/samples/sample4.html)]

此标记将创建一个表，其中是数据绑定到的属性`detail`视图模型中可观察量。

"&lt;！-Ko-&gt; &quot;语法允许您包括 Knockout 绑定之外的 DOM 元素。 在这种情况下，`if`绑定会导致标记要显示的此部分时，才`details`为非 null。

[!code-html[Main](part-8/samples/sample5.html)]

现在，如果运行应用并单击其中一个&quot;详细信息&quot;的链接，该应用将显示书籍详细信息。

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [上一页](part-7.md)
> [下一页](part-9.md)
