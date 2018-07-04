---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: 数据绑定到 Accordion (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明 w...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bc11aa96577919c2ca5dfca4ffc6301da67645ea
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377423"
---
<a name="databinding-to-an-accordion-vb"></a>数据绑定到 Accordion (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明内页面本身，但绑定到数据源提供了更大的灵活性。


## <a name="overview"></a>概述

AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明内页面本身，但绑定到数据源提供了更大的灵活性。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。

对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

然后，将数据源添加到页面。 若要使用有限的数量的数据，我们仅在 AdventureWorks 数据库的 Vendor 表中选择前五个项。 如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。 以下标记显示了正确的语法：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

请记住数据源的名称 (ID)。 此非常标识必须随后可在使用`DataSourceID`Accordion 控件的属性：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

在可折叠面板控件中，可以为各个部分的控件，包括标头提供模板 (`<HeaderTemplate>`) 和内容 (`<ContentTemplate>`)。 这些元素中直接输出数据从数据源，使用`DataBinder.Eval()`方法：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

加载页面时，数据源必须绑定到此服务器端代码可折叠面板：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

若要结束此示例，需要在可折叠面板控件中定义两个引用的 CSS 类 (在其属性中`HeaderCssClass`和`ContentCssClass`)。 将以下标记放入`<head>`页部分：

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]


[![可折叠面板中的数据直接来自数据源](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

可折叠面板中的数据直接来自数据源 ([单击此项可查看原尺寸图像](databinding-to-an-accordion-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](dynamically-adding-an-accordion-pane-cs.md)
> [下一页](dynamically-adding-an-accordion-pane-vb.md)
