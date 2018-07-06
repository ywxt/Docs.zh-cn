---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 使用 Web 服务后端 (VB) 创建数字加/减控件 |Microsoft Docs
author: wenz
description: 而不是让用户复选框中键入一个值，数字增大/减小控件 （它同时存在于 Windows 和其他操作系统） 可能会证明随着更多 c...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: bebf70093dacb81331c009c6642c2f2d649b8567
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805368"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>使用 Web 服务后端 (VB) 创建数字增大/减小控件
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 而不是让用户复选框中键入一个值，数值加/减控件 （即存在于 Windows 和其他操作系统） 可以证明随着更多熟练。 默认情况下，NumericUpDown 控件始终每增加或减少值 1，但 web 服务可证明更大的灵活性。


## <a name="overview"></a>概述

而不是让用户复选框中键入一个值，数值加/减控件 （即存在于 Windows 和其他操作系统） 可以证明随着更多熟练。 默认情况下，`NumericUpDown`控件始终每增加或减少值 1，但 web 服务可证明更大的灵活性。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含`NumericUpDown`扩展程序，其会自动添加到文本框中的两个按钮： 一个用于增加其值，一个用于减小其。 但是该控件还支持 web 服务调用 （或页面方法调用）。 每当向上或向下按钮单击时的 JavaScript 代码连接到 web 服务器和执行方法存在。 方法签名是如下：

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current`自变量是文本框; 中的当前值`tag`属性是可以设置为的一个属性的其他上下文数据`NumericUpDown`扩展器 （但不是必需的）。

对于此示例中，数值加/减控件应仅允许为 2 的幂的值： 1、 2、 4、 8、 16、 32、 64，依此类推。 因此，当用户想要增加的值时执行的方法必须两倍的旧值;另一种方法必须值除以两个。 这是完整的 web 服务：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

最后，创建一个新的 ASP.NET 页面。 像往常一样，需要`ScriptManager`控件，`TextBox`控件和一个`NumericUpDownExtender`控件。 对于后者，你必须提供 web 服务信息：

- `ServiceDownMethod` web 方法或页面方法的列表名称
- `ServiceDownPath` 向下的服务方法; 与 web 服务的路径如果使用的页面方法，忽略
- `ServiceUpMethod` 名称最多的 web 方法或页面方法
- `ServiceUpPath` 与最服务方法; web 服务的路径如果使用的页面方法，忽略

下面是页面的完整标记：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

如果运行该页面，请注意如何在文本框中的值始终加倍时单击上部的按钮，并单击低按钮时，减少了一半。


[![出现是 2 的幂的数字](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

出现是 2 的幂的数字 ([单击此项可查看原尺寸图像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
