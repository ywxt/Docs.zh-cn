---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: 折叠和展开面板从 JavaScript (VB) |Microsoft Docs
author: wenz
description: CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能以折叠其内容并将其展开...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 1f80a6979966a887db0557b4f1b98570e10b1ab7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824745"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>折叠和展开面板从 JavaScript (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能折叠其内容，并再次将其展开。 也可以从自定义 JavaScript 代码触发这两个操作。


## <a name="overview"></a>概述

CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能折叠其内容，并再次将其展开。 也可以从自定义 JavaScript 代码触发这两个操作。

## <a name="steps"></a>步骤

首先，创建一个新的 ASP.NET 页面并将包含`ScriptManager`中`<form>`元素。 这将加载 ASP.NET AJAX 库所需控件工具包：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

然后，使用一些文本创建一个面板，以便可以看到展开/折叠效果：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

正如您所看到的面板将引用的 CSS 类如下所示 （现在基本上是定义背景色和面板的宽度）：

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender`控件需要`TargetControlID`属性，以便该工具包知道哪个面板可折叠或展开根据请求：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

遗憾的是，扩展器当前不会公开特定 API 的折叠或展开面板，但未记录的一些方法即可。 首先，将三个 HTML 按钮添加到页然后会触发客户端 JavaScript 以折叠或展开面板的内容：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

在客户端的 JavaScript 代码 (入门`<script type="text/javascript">`)，则`$find()`方法需要使用访问`CollapsiblePanelExtender`。 `$find("cpe")` 将返回对它的引用。 从此处，特定的方法将解决手头的任务。

该方法用于打开 （扩展） 名控制面板`_doOpen()`; 下面的代码实现`doOpen()`单击第一个按钮时调用的函数：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

用于关闭，或折叠面板，`_doClose()`方法需要执行。 因此当用户单击第二个按钮上时，以下 JavaScript 代码调用：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

第三个按钮切换面板的状态： 从折叠到已展开，反之亦然。 `CollapsiblePanelExtender`公开`toggle()`做到这一点的方法： 反转面板的状态。 但是还有另一种方法 (由在内部使用该`toggle()`方法):`get_Collapsed()`方法的`CollapsiblePanelExtender()`告诉我们是否折叠面板。 根据此函数的返回值，面板，则可以展开 (`_doOpen()`方法) 或折叠 (`_doClose()`) 方法：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]


[![第三个按钮更改面板的状态： 从折叠到扩展和后端](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

第三个按钮更改面板的状态： 从折叠到扩展和后端 ([单击此项可查看原尺寸图像](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](collapsing-and-expanding-a-panel-from-javascript-cs.md)
