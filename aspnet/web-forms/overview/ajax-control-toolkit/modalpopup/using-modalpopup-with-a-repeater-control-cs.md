---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: 转发器控件 (C#) 使用 ModalPopup |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。 它还可使用此 contr....
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7124ca3fc346d78c3b235d1756695b008afb47aa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872937"
---
<a name="using-modalpopup-with-a-repeater-control-c"></a><span data-ttu-id="38324-104">转发器控件 (C#) 使用 ModalPopup</span><span class="sxs-lookup"><span data-stu-id="38324-104">Using ModalPopup with a Repeater Control (C#)</span></span>
====================
<span data-ttu-id="38324-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="38324-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="38324-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="38324-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span></span>

> <span data-ttu-id="38324-107">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="38324-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="38324-108">还有可能要使用此控件在中继器内。</span><span class="sxs-lookup"><span data-stu-id="38324-108">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="38324-109">概述</span><span class="sxs-lookup"><span data-stu-id="38324-109">Overview</span></span>

<span data-ttu-id="38324-110">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="38324-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="38324-111">还有可能要使用此控件在中继器内。</span><span class="sxs-lookup"><span data-stu-id="38324-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="38324-112">步骤</span><span class="sxs-lookup"><span data-stu-id="38324-112">Steps</span></span>

<span data-ttu-id="38324-113">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="38324-113">First of all, a data source is required.</span></span> <span data-ttu-id="38324-114">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="38324-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="38324-115">数据库是 （包括速成版） 的 Visual Studio 安装的可选部分，还可用作下单独下载[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="38324-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="38324-116">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="38324-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="38324-117">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 和附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="38324-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="38324-118">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="38324-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="38324-119">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="38324-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="38324-120">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="38324-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="38324-121">然后，将数据源添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="38324-121">Then, add a data source to the page.</span></span> <span data-ttu-id="38324-122">若要使用的数据量有限，我们仅在 AdventureWorks 数据库的供应商表中选择前五个项。</span><span class="sxs-lookup"><span data-stu-id="38324-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="38324-123">如果使用 Visual Studio 助手来创建数据源，请记住的当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="38324-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="38324-124">以下标记显示正确的语法：</span><span class="sxs-lookup"><span data-stu-id="38324-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="38324-125">接下来，添加一个面板，它可作为模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="38324-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="38324-126">它包含`Button`控件再次关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="38324-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="38324-127">为了使在转发器中, 工作的弹出窗口`ModalPopupExtender`控件必须放置在`<ItemTemplate>`的转发器的部分。</span><span class="sxs-lookup"><span data-stu-id="38324-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="38324-128">因此面板位于外部转发器，但扩展程序位于。</span><span class="sxs-lookup"><span data-stu-id="38324-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="38324-129">下面是转发器的标记：</span><span class="sxs-lookup"><span data-stu-id="38324-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="38324-130">然后，将包含用于触发模式弹出它旁边的按钮显示数据源中的每个项。</span><span class="sxs-lookup"><span data-stu-id="38324-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>


<span data-ttu-id="38324-131">[![可以为每个数据源条目触发模式弹出窗口](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="38324-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="38324-132">可以为每个数据源条目触发模式弹出窗口 ([单击以查看实际尺寸的图像](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="38324-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38324-133">[上一页](launching-a-modal-popup-window-from-server-code-cs.md)
> [下一页](handling-postbacks-from-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="38324-133">[Previous](launching-a-modal-popup-window-from-server-code-cs.md)
[Next](handling-postbacks-from-a-modalpopup-cs.md)</span></span>
