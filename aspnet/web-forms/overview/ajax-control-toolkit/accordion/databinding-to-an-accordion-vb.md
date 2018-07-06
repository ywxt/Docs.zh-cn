---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: 数据绑定到 Accordion (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明 w...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: e21eeacf776111656eb539b1fef8203db1b761c7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805883"
---
<a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="95767-104">数据绑定到 Accordion (VB)</span><span class="sxs-lookup"><span data-stu-id="95767-104">Databinding to an Accordion (VB)</span></span>
====================
<span data-ttu-id="95767-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="95767-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="95767-106">[下载代码](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="95767-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="95767-107">AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="95767-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="95767-108">面板通常声明内页面本身，但绑定到数据源提供了更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="95767-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="95767-109">概述</span><span class="sxs-lookup"><span data-stu-id="95767-109">Overview</span></span>

<span data-ttu-id="95767-110">AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="95767-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="95767-111">面板通常声明内页面本身，但绑定到数据源提供了更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="95767-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="95767-112">步骤</span><span class="sxs-lookup"><span data-stu-id="95767-112">Steps</span></span>

<span data-ttu-id="95767-113">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="95767-113">First of all, a data source is required.</span></span> <span data-ttu-id="95767-114">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="95767-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="95767-115">数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="95767-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="95767-116">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="95767-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="95767-117">若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="95767-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="95767-118">对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="95767-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="95767-119">如果你的设置不同，您必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="95767-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="95767-120">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="95767-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="95767-121">然后，将数据源添加到页面。</span><span class="sxs-lookup"><span data-stu-id="95767-121">Then, add a data source to the page.</span></span> <span data-ttu-id="95767-122">若要使用有限的数量的数据，我们仅在 AdventureWorks 数据库的 Vendor 表中选择前五个项。</span><span class="sxs-lookup"><span data-stu-id="95767-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="95767-123">如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="95767-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="95767-124">以下标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="95767-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="95767-125">请记住数据源的名称 (ID)。</span><span class="sxs-lookup"><span data-stu-id="95767-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="95767-126">此非常标识必须随后可在使用`DataSourceID`Accordion 控件的属性：</span><span class="sxs-lookup"><span data-stu-id="95767-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="95767-127">在可折叠面板控件中，可以为各个部分的控件，包括标头提供模板 (`<HeaderTemplate>`) 和内容 (`<ContentTemplate>`)。</span><span class="sxs-lookup"><span data-stu-id="95767-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="95767-128">这些元素中直接输出数据从数据源，使用`DataBinder.Eval()`方法：</span><span class="sxs-lookup"><span data-stu-id="95767-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="95767-129">加载页面时，数据源必须绑定到此服务器端代码可折叠面板：</span><span class="sxs-lookup"><span data-stu-id="95767-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="95767-130">若要结束此示例，需要在可折叠面板控件中定义两个引用的 CSS 类 (在其属性中`HeaderCssClass`和`ContentCssClass`)。</span><span class="sxs-lookup"><span data-stu-id="95767-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="95767-131">将以下标记放入`<head>`页部分：</span><span class="sxs-lookup"><span data-stu-id="95767-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]


<span data-ttu-id="95767-132">[![可折叠面板中的数据直接来自数据源](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="95767-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span></span>

<span data-ttu-id="95767-133">可折叠面板中的数据直接来自数据源 ([单击此项可查看原尺寸图像](databinding-to-an-accordion-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="95767-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95767-134">[上一页](dynamically-adding-an-accordion-pane-cs.md)
> [下一页](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="95767-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
