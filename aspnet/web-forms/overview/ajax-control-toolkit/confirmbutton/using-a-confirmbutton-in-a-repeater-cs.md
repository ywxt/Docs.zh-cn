---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: 在转发器 (C#) 中使用 ConfirmButton |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 ConfirmButton 扩展程序创建是 / 没有弹出窗口，当用户单击按钮时 （包括 LinkButton 控件）。 仅当是是...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a0717083a3c1e285f0c8c4cb8503d2bbe42153b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871514"
---
<a name="using-a-confirmbutton-in-a-repeater-c"></a><span data-ttu-id="6e105-104">在转发器 (C#) 中使用 ConfirmButton</span><span class="sxs-lookup"><span data-stu-id="6e105-104">Using a ConfirmButton In a Repeater (C#)</span></span>
====================
<span data-ttu-id="6e105-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6e105-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6e105-106">[下载代码](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6e105-106">[Download Code](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span></span>

> <span data-ttu-id="6e105-107">AJAX 控件工具包中的 ConfirmButton 扩展程序创建是 / 没有弹出窗口，当用户单击按钮时 （包括 LinkButton 控件）。</span><span class="sxs-lookup"><span data-stu-id="6e105-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="6e105-108">仅当单击是，则执行是按钮的操作，否则取消。</span><span class="sxs-lookup"><span data-stu-id="6e105-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="6e105-109">也可以在中继器此设置。</span><span class="sxs-lookup"><span data-stu-id="6e105-109">This is also possible in a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="6e105-110">概述</span><span class="sxs-lookup"><span data-stu-id="6e105-110">Overview</span></span>

<span data-ttu-id="6e105-111">AJAX 控件工具包中的 ConfirmButton 扩展程序创建是 / 没有弹出窗口，当用户单击按钮时 （包括 LinkButton 控件）。</span><span class="sxs-lookup"><span data-stu-id="6e105-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="6e105-112">仅当单击是，则执行是按钮的操作，否则取消。</span><span class="sxs-lookup"><span data-stu-id="6e105-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="6e105-113">也可以在中继器此设置。</span><span class="sxs-lookup"><span data-stu-id="6e105-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="6e105-114">步骤</span><span class="sxs-lookup"><span data-stu-id="6e105-114">Steps</span></span>

<span data-ttu-id="6e105-115">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="6e105-115">First of all, a data source is required.</span></span> <span data-ttu-id="6e105-116">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="6e105-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6e105-117">数据库是 （包括速成版） 的 Visual Studio 安装的可选部分，还可用作下单独下载[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="6e105-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6e105-118">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="6e105-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6e105-119">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 和附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="6e105-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6e105-120">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="6e105-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6e105-121">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="6e105-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6e105-122">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="6e105-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

<span data-ttu-id="6e105-123">然后，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="6e105-123">Then, a data source is required.</span></span> <span data-ttu-id="6e105-124">为简单起见，会检索仅 AdventureWorks 的供应商表中的前五个条目。</span><span class="sxs-lookup"><span data-stu-id="6e105-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="6e105-125">请注意，当使用 Visual Studio 向导创建数据源，表名 (`Vendors`) 当前不使用正确的前缀与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="6e105-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="6e105-126">以下标记是正确的订阅：</span><span class="sxs-lookup"><span data-stu-id="6e105-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

<span data-ttu-id="6e105-127">然后可以内中继器使用此数据源。</span><span class="sxs-lookup"><span data-stu-id="6e105-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="6e105-128">像往常一样，`DataBinder.Eval()`方法从数据源中检索数据。</span><span class="sxs-lookup"><span data-stu-id="6e105-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="6e105-129">`ConfirmButtonExtender`控件然后必须放在`<ItemTemplate>`的转发器，使其显示为数据源中的每个条目的部分。</span><span class="sxs-lookup"><span data-stu-id="6e105-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]


<span data-ttu-id="6e105-130">[![数据源的每个条目旁边将显示确认按钮](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6e105-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span></span>

<span data-ttu-id="6e105-131">数据源的每个条目旁边将显示确认按钮 ([单击以查看实际尺寸的图像](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6e105-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6e105-132">下一篇</span><span class="sxs-lookup"><span data-stu-id="6e105-132">Next</span></span>](using-a-confirmbutton-in-a-repeater-vb.md)
