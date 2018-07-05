---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: 在 FormView (VB) 中使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中，它我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1bb3ad274ba6c8617643fa4d7894a73de4b5cdff
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396180"
---
<a name="using-textboxwatermark-in-a-formview-vb"></a>在 FormView (VB) 中使用 TextBoxWatermark
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中时，它将被清空。 如果用户离开而无需输入文本的框中，将重新出现已预先的文本。 这也是可能在 FormView 控件内。


## <a name="overview"></a>概述

`TextBoxWatermark` AJAX 控件工具包中的控件扩展的文本框中，以便在框中显示文本。 当用户单击到框中时，它将被清空。 如果用户离开而无需输入文本的框中，将重新出现已预先的文本。 也可以在此设置`FormView`控件。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。

对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

然后，将数据源添加到支持页`DELETE`，`INSERT`和`UPDATE`SQL 语句。 如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。 以下标记显示了正确的语法：

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

请记住的名称 (`ID`) 的数据源，因为它会在`DataSourceID`属性的`FormView`控件。 `<InsertItemTemplate>`一部分`FormView`包含一个文本框，后者则通过扩展`TextBoxWatermarkExtender`控件。 请确保该扩展器驻留在模板中并没有超出其。

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

现在用户更改到的插入模式`FormView`控制，请在文本字段的新供应商预先填充感谢到`TextBoxWatermarkExtender`控件。 在文本框内的单击一下填充符文本消失。


[![该字段中的水印来自扩展程序](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

该字段中的水印来自扩展程序 ([单击此项可查看原尺寸图像](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-textboxwatermark-with-validation-controls-cs.md)
> [下一页](using-textboxwatermark-with-validation-controls-vb.md)
