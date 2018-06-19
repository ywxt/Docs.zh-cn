---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: 转发器控件 (VB) 中使用 HoverMenu |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 HoverMenu 控件提供简单的弹出窗口效果： 当鼠标指针悬停在元素上时，指定在显示弹出窗口...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: aa107a7483683d965f3a510e6a43f174a386da0c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868394"
---
<a name="using-hovermenu-with-a-repeater-control-vb"></a><span data-ttu-id="f3983-103">转发器控件 (VB) 中使用 HoverMenu</span><span class="sxs-lookup"><span data-stu-id="f3983-103">Using HoverMenu with a Repeater Control (VB)</span></span>
====================
<span data-ttu-id="f3983-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f3983-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f3983-105">[下载代码](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f3983-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span></span>

> <span data-ttu-id="f3983-106">AJAX 控件工具包中的 HoverMenu 控件提供简单的弹出窗口效果： 当鼠标指针悬停在元素上时，在指定位置显示弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="f3983-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f3983-107">还有可能要使用此控件在中继器内。</span><span class="sxs-lookup"><span data-stu-id="f3983-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="f3983-108">概述</span><span class="sxs-lookup"><span data-stu-id="f3983-108">Overview</span></span>

<span data-ttu-id="f3983-109">`HoverMenu` AJAX 控件工具包中的控件提供一个简单的弹出窗口效果： 当鼠标指针悬停在元素上时，在指定位置显示弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="f3983-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f3983-110">还有可能要使用此控件在中继器内。</span><span class="sxs-lookup"><span data-stu-id="f3983-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="f3983-111">步骤</span><span class="sxs-lookup"><span data-stu-id="f3983-111">Steps</span></span>

<span data-ttu-id="f3983-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="f3983-112">First of all, a data source is required.</span></span> <span data-ttu-id="f3983-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="f3983-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="f3983-114">数据库是 （包括速成版） 的 Visual Studio 安装的可选部分，还可用作下单独下载[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="f3983-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f3983-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="f3983-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="f3983-116">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 和附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="f3983-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="f3983-117">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="f3983-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f3983-118">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="f3983-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f3983-119">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="f3983-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="f3983-120">然后，将数据源添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="f3983-120">Then, add a data source to the page.</span></span> <span data-ttu-id="f3983-121">若要使用的数据量有限，我们仅在 AdventureWorks 数据库的供应商表中选择前五个项。</span><span class="sxs-lookup"><span data-stu-id="f3983-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="f3983-122">如果使用 Visual Studio 助手来创建数据源，请记住的当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="f3983-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="f3983-123">以下标记显示正确的语法：</span><span class="sxs-lookup"><span data-stu-id="f3983-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="f3983-124">接下来，添加一个面板，它可作为模式弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="f3983-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="f3983-125">现在，`HoverMenuExtender`派上用场。</span><span class="sxs-lookup"><span data-stu-id="f3983-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="f3983-126">扩展器，以便数据源中的每个元素获取其自己的弹出窗口，必须放置在转发器的`<ItemTemplate>`部分。</span><span class="sxs-lookup"><span data-stu-id="f3983-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="f3983-127">此处为标记：</span><span class="sxs-lookup"><span data-stu-id="f3983-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="f3983-128">现在，数据源中的每个项向右显示一个弹出窗口 (`PopupPosition`属性) 的 50 毫秒的延迟后 (`PopDelay`属性)。</span><span class="sxs-lookup"><span data-stu-id="f3983-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="f3983-129">[![转发器在每个项旁边会出现的悬停菜单](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f3983-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="f3983-130">转发器在每个项旁边会出现的悬停菜单 ([单击以查看实际尺寸的图像](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f3983-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f3983-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="f3983-131">Previous</span></span>](using-hovermenu-with-a-repeater-control-cs.md)
