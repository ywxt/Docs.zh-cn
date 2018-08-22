---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: 在 FormView (C#) 中使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中，它我...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 272befe4182a459c0e1f3b6668d252d9ba4715d0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831061"
---
<a name="using-textboxwatermark-in-a-formview-c"></a><span data-ttu-id="bbf07-104">在 FormView (C#) 中使用 TextBoxWatermark</span><span class="sxs-lookup"><span data-stu-id="bbf07-104">Using TextBoxWatermark in a FormView (C#)</span></span>
====================
<span data-ttu-id="bbf07-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="bbf07-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bbf07-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="bbf07-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span></span>

> <span data-ttu-id="bbf07-107">AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="bbf07-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="bbf07-108">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="bbf07-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="bbf07-109">如果用户离开而无需输入文本的框中，将重新出现已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="bbf07-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="bbf07-110">这也是可能在 FormView 控件内。</span><span class="sxs-lookup"><span data-stu-id="bbf07-110">This is also possible within a FormView control.</span></span>


## <a name="overview"></a><span data-ttu-id="bbf07-111">概述</span><span class="sxs-lookup"><span data-stu-id="bbf07-111">Overview</span></span>

<span data-ttu-id="bbf07-112">`TextBoxWatermark` AJAX 控件工具包中的控件扩展的文本框中，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="bbf07-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="bbf07-113">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="bbf07-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="bbf07-114">如果用户离开而无需输入文本的框中，将重新出现已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="bbf07-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="bbf07-115">也可以在此设置`FormView`控件。</span><span class="sxs-lookup"><span data-stu-id="bbf07-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="bbf07-116">步骤</span><span class="sxs-lookup"><span data-stu-id="bbf07-116">Steps</span></span>

<span data-ttu-id="bbf07-117">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="bbf07-117">First of all, a data source is required.</span></span> <span data-ttu-id="bbf07-118">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="bbf07-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="bbf07-119">数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="bbf07-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="bbf07-120">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="bbf07-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="bbf07-121">若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="bbf07-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="bbf07-122">对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="bbf07-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="bbf07-123">如果你的设置不同，您必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="bbf07-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="bbf07-124">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="bbf07-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

<span data-ttu-id="bbf07-125">然后，将数据源添加到支持页`DELETE`，`INSERT`和`UPDATE`SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="bbf07-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="bbf07-126">如果使用 Visual Studio 助手创建数据源，请记住当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="bbf07-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="bbf07-127">以下标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="bbf07-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

<span data-ttu-id="bbf07-128">请记住的名称 (`ID`) 的数据源，因为它会在`DataSourceID`属性的`FormView`控件。</span><span class="sxs-lookup"><span data-stu-id="bbf07-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="bbf07-129">`<InsertItemTemplate>`一部分`FormView`包含一个文本框，后者则通过扩展`TextBoxWatermarkExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="bbf07-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="bbf07-130">请确保该扩展器驻留在模板中并没有超出其。</span><span class="sxs-lookup"><span data-stu-id="bbf07-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

<span data-ttu-id="bbf07-131">现在用户更改到的插入模式`FormView`控制，请在文本字段的新供应商预先填充感谢到`TextBoxWatermarkExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="bbf07-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="bbf07-132">在文本框内的单击一下填充符文本消失。</span><span class="sxs-lookup"><span data-stu-id="bbf07-132">A click inside the textbox lets the filler text disappear.</span></span>


<span data-ttu-id="bbf07-133">[![该字段中的水印来自扩展程序](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bbf07-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span></span>

<span data-ttu-id="bbf07-134">该字段中的水印来自扩展程序 ([单击此项可查看原尺寸图像](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bbf07-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bbf07-135">下一篇</span><span class="sxs-lookup"><span data-stu-id="bbf07-135">Next</span></span>](using-textboxwatermark-with-validation-controls-cs.md)
