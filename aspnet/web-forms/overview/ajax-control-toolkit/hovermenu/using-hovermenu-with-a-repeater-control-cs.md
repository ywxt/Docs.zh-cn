---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: 通过 Repeater 控件 (C#) 使用 HoverMenu |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 HoverMenu 控件提供了一个简单的弹出窗口效果： 当鼠标指针悬停在元素上时，可以在显示弹出窗口...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: f3135eb52bab1550b1c89dd6ce62044640e80198
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831992"
---
<a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="6f434-103">通过 Repeater 控件 (C#) 使用 HoverMenu</span><span class="sxs-lookup"><span data-stu-id="6f434-103">Using HoverMenu with a Repeater Control (C#)</span></span>
====================
<span data-ttu-id="6f434-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6f434-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6f434-105">[下载代码](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6f434-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="6f434-106">AJAX 控件工具包中的 HoverMenu 控件提供了一个简单的弹出窗口效果： 当鼠标指针悬停在元素上时，在指定位置处显示弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6f434-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="6f434-107">还有可能要使用 repeater 中的此控件。</span><span class="sxs-lookup"><span data-stu-id="6f434-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="6f434-108">概述</span><span class="sxs-lookup"><span data-stu-id="6f434-108">Overview</span></span>

<span data-ttu-id="6f434-109">`HoverMenu` AJAX 控件工具包中的控件提供了一个简单的弹出窗口效果： 当鼠标指针悬停在元素上时，在指定位置处显示弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6f434-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="6f434-110">还有可能要使用 repeater 中的此控件。</span><span class="sxs-lookup"><span data-stu-id="6f434-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="6f434-111">步骤</span><span class="sxs-lookup"><span data-stu-id="6f434-111">Steps</span></span>

<span data-ttu-id="6f434-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="6f434-112">First of all, a data source is required.</span></span> <span data-ttu-id="6f434-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="6f434-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6f434-114">数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="6f434-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6f434-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="6f434-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6f434-116">若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="6f434-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6f434-117">对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="6f434-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6f434-118">如果你的设置不同，您必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="6f434-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6f434-119">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="6f434-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="6f434-120">然后，将数据源添加到页面。</span><span class="sxs-lookup"><span data-stu-id="6f434-120">Then, add a data source to the page.</span></span> <span data-ttu-id="6f434-121">若要使用有限的数量的数据，我们仅在 AdventureWorks 数据库的 Vendor 表中选择前五个项。</span><span class="sxs-lookup"><span data-stu-id="6f434-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="6f434-122">如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="6f434-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="6f434-123">以下标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="6f434-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="6f434-124">接下来，添加一个面板作为模式弹出框：</span><span class="sxs-lookup"><span data-stu-id="6f434-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="6f434-125">现在，`HoverMenuExtender`发挥作用的。</span><span class="sxs-lookup"><span data-stu-id="6f434-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="6f434-126">扩展器，以便在数据源中的每个元素获取其自己的弹出窗口，必须放在 repeater 的`<ItemTemplate>`部分。</span><span class="sxs-lookup"><span data-stu-id="6f434-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="6f434-127">此处为标记：</span><span class="sxs-lookup"><span data-stu-id="6f434-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="6f434-128">现在，数据源中的每个项显示一个弹出窗口，向右 (`PopupPosition`属性) 的 50 毫秒的延迟后 (`PopDelay`属性)。</span><span class="sxs-lookup"><span data-stu-id="6f434-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="6f434-129">[![在 repeater 中每个项的旁边显示的悬停菜单](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f434-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f434-130">在 repeater 中每个项的旁边显示的悬停菜单 ([单击此项可查看原尺寸图像](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6f434-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6f434-131">下一篇</span><span class="sxs-lookup"><span data-stu-id="6f434-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
