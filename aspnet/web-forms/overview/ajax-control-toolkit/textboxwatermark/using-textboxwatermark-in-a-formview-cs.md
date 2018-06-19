---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: 在 FormView (C#) 中使用 TextBoxWatermark |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中，它我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 90e532d33756a995a85994254c48889517c5bb8d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870773"
---
<a name="using-textboxwatermark-in-a-formview-c"></a><span data-ttu-id="871e7-104">在 FormView (C#) 中使用 TextBoxWatermark</span><span class="sxs-lookup"><span data-stu-id="871e7-104">Using TextBoxWatermark in a FormView (C#)</span></span>
====================
<span data-ttu-id="871e7-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="871e7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="871e7-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="871e7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span></span>

> <span data-ttu-id="871e7-107">AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="871e7-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="871e7-108">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="871e7-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="871e7-109">如果用户离开而无需输入文本框中，再次显示已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="871e7-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="871e7-110">这也是可能 FormView 控件内。</span><span class="sxs-lookup"><span data-stu-id="871e7-110">This is also possible within a FormView control.</span></span>


## <a name="overview"></a><span data-ttu-id="871e7-111">概述</span><span class="sxs-lookup"><span data-stu-id="871e7-111">Overview</span></span>

<span data-ttu-id="871e7-112">`TextBoxWatermark` AJAX 控件工具包中的控件扩展文本框中，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="871e7-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="871e7-113">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="871e7-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="871e7-114">如果用户离开而无需输入文本框中，再次显示已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="871e7-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="871e7-115">也可以在此设置`FormView`控件。</span><span class="sxs-lookup"><span data-stu-id="871e7-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="871e7-116">步骤</span><span class="sxs-lookup"><span data-stu-id="871e7-116">Steps</span></span>

<span data-ttu-id="871e7-117">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="871e7-117">First of all, a data source is required.</span></span> <span data-ttu-id="871e7-118">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="871e7-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="871e7-119">数据库是 （包括速成版） 的 Visual Studio 安装的可选部分，还可用作下单独下载[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="871e7-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="871e7-120">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="871e7-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="871e7-121">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 和附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="871e7-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="871e7-122">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="871e7-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="871e7-123">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="871e7-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="871e7-124">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="871e7-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

<span data-ttu-id="871e7-125">然后，将数据源添加到支持的页面`DELETE`，`INSERT`和`UPDATE`SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="871e7-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="871e7-126">如果使用 Visual Studio 助手来创建数据源，请记住的当前版本中的 bug 不前缀表名 (`Vendor`) 与`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="871e7-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="871e7-127">以下标记显示正确的语法：</span><span class="sxs-lookup"><span data-stu-id="871e7-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

<span data-ttu-id="871e7-128">记住的名称 (`ID`) 的数据源，因为它将使用在`DataSourceID`属性`FormView`控件。</span><span class="sxs-lookup"><span data-stu-id="871e7-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="871e7-129">`<InsertItemTemplate>`部分`FormView`包含文本框中，后者通过扩展`TextBoxWatermarkExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="871e7-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="871e7-130">请确保扩展程序驻留在模板中并不外部。</span><span class="sxs-lookup"><span data-stu-id="871e7-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

<span data-ttu-id="871e7-131">现在用户更改到在插入模式的`FormView`控制，请在文本字段为新的供应商预先填入感谢到`TextBoxWatermarkExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="871e7-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="871e7-132">在文本框中单击允许填充符文本消失。</span><span class="sxs-lookup"><span data-stu-id="871e7-132">A click inside the textbox lets the filler text disappear.</span></span>


<span data-ttu-id="871e7-133">[![字段中的水印来自扩展器](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="871e7-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span></span>

<span data-ttu-id="871e7-134">字段中的水印来自扩展器 ([单击以查看实际尺寸的图像](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="871e7-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="871e7-135">下一篇</span><span class="sxs-lookup"><span data-stu-id="871e7-135">Next</span></span>](using-textboxwatermark-with-validation-controls-cs.md)
