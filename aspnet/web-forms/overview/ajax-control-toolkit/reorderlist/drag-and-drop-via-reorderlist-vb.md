---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: 拖放通过 ReorderList (VB) |Microsoft 文档
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 99f47b969dc75efeec8485254d311c93dc0b5d35
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="79118-103">拖放通过 ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="79118-103">Drag and Drop via ReorderList (VB)</span></span>
====================
<span data-ttu-id="79118-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="79118-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="79118-105">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="79118-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="79118-106">AJAX 控件工具包中的 ReorderList 控件提供可由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="79118-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="79118-107">应在服务器保留对当前的列表顺序。</span><span class="sxs-lookup"><span data-stu-id="79118-107">The current order of the list shall be persisted on the server.</span></span>


## <a name="overview"></a><span data-ttu-id="79118-108">概述</span><span class="sxs-lookup"><span data-stu-id="79118-108">Overview</span></span>

<span data-ttu-id="79118-109">`ReorderList` AJAX 控件工具包中的控件提供可由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="79118-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="79118-110">应在服务器保留对当前的列表顺序。</span><span class="sxs-lookup"><span data-stu-id="79118-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="79118-111">步骤</span><span class="sxs-lookup"><span data-stu-id="79118-111">Steps</span></span>

<span data-ttu-id="79118-112">`ReorderList`控件支持将数据从数据库绑定到列表。</span><span class="sxs-lookup"><span data-stu-id="79118-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="79118-113">最重要的是，它还支持将更改写入回数据存储区的列表元素的顺序。</span><span class="sxs-lookup"><span data-stu-id="79118-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="79118-114">此示例使用作为数据存储区的 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="79118-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="79118-115">数据库是包括速成版的 Visual Studio 安装的可选 （和可用） 组成部分。</span><span class="sxs-lookup"><span data-stu-id="79118-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="79118-116">此外，还可以作为单独的下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="79118-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="79118-117">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="79118-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="79118-118">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="79118-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="79118-119">将数据库设置的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) )。</span><span class="sxs-lookup"><span data-stu-id="79118-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="79118-120">连接到服务器，请双击`Databases`并创建一个新的数据库 (右键单击并选择`New Database`) 调用`Tutorials`。</span><span class="sxs-lookup"><span data-stu-id="79118-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="79118-121">在此数据库中，创建名为的新表`AJAX`与以下四列：</span><span class="sxs-lookup"><span data-stu-id="79118-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="79118-122">`id` (主键，整数，标识，不为 NULL)</span><span class="sxs-lookup"><span data-stu-id="79118-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="79118-123">`char` （char （1)，NULL）</span><span class="sxs-lookup"><span data-stu-id="79118-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="79118-124">`description` (varchar(50)，NULL)</span><span class="sxs-lookup"><span data-stu-id="79118-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="79118-125">`position` (int、 NULL)</span><span class="sxs-lookup"><span data-stu-id="79118-125">`position` (int, NULL)</span></span>


<span data-ttu-id="79118-126">[![AJAX 表的布局](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="79118-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="79118-127">AJAX 表的布局 ([单击以查看实际尺寸的图像](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="79118-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>


<span data-ttu-id="79118-128">接下来，使用几个值填充表。</span><span class="sxs-lookup"><span data-stu-id="79118-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="79118-129">请注意，`position`的列包含的元素的排序顺序。</span><span class="sxs-lookup"><span data-stu-id="79118-129">Note that the `position` column holds the sort order of the elements.</span></span>


<span data-ttu-id="79118-130">[![AJAX 表中的初始数据](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="79118-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="79118-131">AJAX 表中的初始数据 ([单击以查看实际尺寸的图像](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="79118-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>


<span data-ttu-id="79118-132">下一步需要生成`SqlDataSource`控件与新的数据库和它的表进行通信。</span><span class="sxs-lookup"><span data-stu-id="79118-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="79118-133">数据源必须支持`SELECT`和`UPDATE`SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="79118-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="79118-134">当列表元素的顺序更高版本发生更改时，`ReorderList`控件会自动将提交到数据源的两个值`Update`命令： 新的位置和元素的 ID。</span><span class="sxs-lookup"><span data-stu-id="79118-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="79118-135">因此，数据源需要`<UpdateParameters>`这两个值的部分：</span><span class="sxs-lookup"><span data-stu-id="79118-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="79118-136">`ReorderList`控件需要设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="79118-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="79118-137">`AllowReorder`： 是否可以重新排列列表项</span><span class="sxs-lookup"><span data-stu-id="79118-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="79118-138">`DataSourceID`： 数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="79118-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="79118-139">`DataKeyField`： 的名称的数据源中主键列</span><span class="sxs-lookup"><span data-stu-id="79118-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="79118-140">`SortOrderField`： 提供的列表项的排序顺序数据源列</span><span class="sxs-lookup"><span data-stu-id="79118-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="79118-141">在`<DragHandleTemplate>`和`<ItemTemplate>`部分中，列表的布局可以细微调整。</span><span class="sxs-lookup"><span data-stu-id="79118-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="79118-142">此外，数据绑定是可能使用`Eval()`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="79118-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="79118-143">以下 CSS 样式信息 (中引用`<DragHandleTemplate>`部分`ReorderList`控件) 可确保，鼠标指针将相应更改当悬停拖动句柄：</span><span class="sxs-lookup"><span data-stu-id="79118-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="79118-144">最后，`ScriptManager`控件初始化 ASP.NET AJAX 页：</span><span class="sxs-lookup"><span data-stu-id="79118-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="79118-145">在浏览器中运行此示例和有点重新排列列表项。</span><span class="sxs-lookup"><span data-stu-id="79118-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="79118-146">然后，重新加载该页面和/或具有在数据库的外观。</span><span class="sxs-lookup"><span data-stu-id="79118-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="79118-147">更改的位置所保留的天数和中的值也会反映`position`列数据库中的所有无需任何代码，只使用标记。</span><span class="sxs-lookup"><span data-stu-id="79118-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>


<span data-ttu-id="79118-148">[![中的新列表项顺序根据数据库更改的数据](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="79118-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="79118-149">根据新列表的数据库更改数据项顺序 ([单击以查看实际尺寸的图像](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="79118-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="79118-150">上一篇</span><span class="sxs-lookup"><span data-stu-id="79118-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
