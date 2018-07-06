---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: 通过 Repeater 控件 (VB) 使用 ModalPopup |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 还有可能要使用此 contr....
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c51ddd4b2bcc17c7d8c5dee0926903bea6ac749f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826609"
---
<a name="using-modalpopup-with-a-repeater-control-vb"></a><span data-ttu-id="e05b9-104">通过 Repeater 控件 (VB) 使用 ModalPopup</span><span class="sxs-lookup"><span data-stu-id="e05b9-104">Using ModalPopup with a Repeater Control (VB)</span></span>
====================
<span data-ttu-id="e05b9-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e05b9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e05b9-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e05b9-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span></span>

> <span data-ttu-id="e05b9-107">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="e05b9-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e05b9-108">还有可能要使用 repeater 中的此控件。</span><span class="sxs-lookup"><span data-stu-id="e05b9-108">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="e05b9-109">概述</span><span class="sxs-lookup"><span data-stu-id="e05b9-109">Overview</span></span>

<span data-ttu-id="e05b9-110">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="e05b9-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e05b9-111">还有可能要使用 repeater 中的此控件。</span><span class="sxs-lookup"><span data-stu-id="e05b9-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="e05b9-112">步骤</span><span class="sxs-lookup"><span data-stu-id="e05b9-112">Steps</span></span>

<span data-ttu-id="e05b9-113">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="e05b9-113">First of all, a data source is required.</span></span> <span data-ttu-id="e05b9-114">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="e05b9-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="e05b9-115">数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="e05b9-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="e05b9-116">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="e05b9-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="e05b9-117">若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="e05b9-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="e05b9-118">对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="e05b9-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="e05b9-119">如果你的设置不同，您必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="e05b9-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="e05b9-120">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="e05b9-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="e05b9-121">然后，将数据源添加到页面。</span><span class="sxs-lookup"><span data-stu-id="e05b9-121">Then, add a data source to the page.</span></span> <span data-ttu-id="e05b9-122">若要使用有限的数量的数据，我们仅在 AdventureWorks 数据库的 Vendor 表中选择前五个项。</span><span class="sxs-lookup"><span data-stu-id="e05b9-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="e05b9-123">如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="e05b9-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="e05b9-124">以下标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="e05b9-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="e05b9-125">接下来，添加一个面板作为模式弹出框。</span><span class="sxs-lookup"><span data-stu-id="e05b9-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="e05b9-126">它包含`Button`控件可再次关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="e05b9-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="e05b9-127">为了使弹出项在 repeater 中工作`ModalPopupExtender`控件必须放在`<ItemTemplate>`中继器的部分。</span><span class="sxs-lookup"><span data-stu-id="e05b9-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="e05b9-128">这样的面板是外部 repeater，但是扩展器内。</span><span class="sxs-lookup"><span data-stu-id="e05b9-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="e05b9-129">下面是针对 repeater 标记：</span><span class="sxs-lookup"><span data-stu-id="e05b9-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="e05b9-130">然后，数据源中的每个项将显示触发模式弹出框旁边的按钮。</span><span class="sxs-lookup"><span data-stu-id="e05b9-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>


<span data-ttu-id="e05b9-131">[![可以为每个数据源输入触发模式弹出框](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e05b9-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="e05b9-132">可以为每个数据源输入触发模式弹出框 ([单击此项可查看原尺寸图像](using-modalpopup-with-a-repeater-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e05b9-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e05b9-133">[上一页](launching-a-modal-popup-window-from-server-code-vb.md)
> [下一页](handling-postbacks-from-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e05b9-133">[Previous](launching-a-modal-popup-window-from-server-code-vb.md)
[Next](handling-postbacks-from-a-modalpopup-vb.md)</span></span>
