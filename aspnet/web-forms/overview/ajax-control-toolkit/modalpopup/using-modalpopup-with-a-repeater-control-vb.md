---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: 通过 Repeater 控件 (VB) 使用 ModalPopup |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 还有可能要使用此 contr....
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 2854cc8fcc9845cb4a4f97cfaf2f3c79ba031a93
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384065"
---
<a name="using-modalpopup-with-a-repeater-control-vb"></a>通过 Repeater 控件 (VB) 使用 ModalPopup
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)

> 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 还有可能要使用 repeater 中的此控件。


## <a name="overview"></a>概述

在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 还有可能要使用 repeater 中的此控件。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。 对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。 若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

然后，将数据源添加到页面。 若要使用有限的数量的数据，我们仅在 AdventureWorks 数据库的 Vendor 表中选择前五个项。 如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。 以下标记显示了正确的语法：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

接下来，添加一个面板作为模式弹出框。 它包含`Button`控件可再次关闭弹出窗口：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

为了使弹出项在 repeater 中工作`ModalPopupExtender`控件必须放在`<ItemTemplate>`中继器的部分。 这样的面板是外部 repeater，但是扩展器内。 下面是针对 repeater 标记：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

然后，数据源中的每个项将显示触发模式弹出框旁边的按钮。


[![可以为每个数据源输入触发模式弹出框](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)

可以为每个数据源输入触发模式弹出框 ([单击此项可查看原尺寸图像](using-modalpopup-with-a-repeater-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](launching-a-modal-popup-window-from-server-code-vb.md)
> [下一页](handling-postbacks-from-a-modalpopup-vb.md)
