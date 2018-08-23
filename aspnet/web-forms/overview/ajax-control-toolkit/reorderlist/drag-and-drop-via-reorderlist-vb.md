---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: 通过 reorderlist 进行 (VB) 拖放 |Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 12c5aa60aa6bb71c99e267a1a71b40ed718df8cf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832531"
---
<a name="drag-and-drop-via-reorderlist-vb"></a>拖放到通过 reorderlist 进行 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)

> AJAX 控件工具包中的 ReorderList 控件提供了可以由用户通过拖放重新排序的列表。 当前列表的顺序应保留在服务器上。


## <a name="overview"></a>概述

`ReorderList` AJAX 控件工具包中的控件提供了可以由用户通过拖放重新排序的列表。 当前列表的顺序应保留在服务器上。

## <a name="steps"></a>步骤

`ReorderList`控件支持将数据从数据库绑定到列表。 最重要的是，它还支持编写更改回数据存储区的列表元素的顺序。

此示例使用 Microsoft SQL Server 2005 Express Edition 作为数据存储。 数据库是包括速成版的 Visual Studio 安装一个可选的 （且免费的） 部分。 此外，还可以作为单独的下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。

若要将数据库设置的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) )。 连接到服务器，双击`Databases`并创建新数据库 (右键单击并选择`New Database`) 调用`Tutorials`。

在此数据库中，创建名为的新表`AJAX`与以下四列：

- `id` (主要密钥，整数，标识，不为 NULL)
- `char` （char （1)，NULL）
- `description` (varchar(50)，NULL)
- `position` (int，NULL)


[![AJAX 表的布局](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)

AJAX 表的布局 ([单击此项可查看原尺寸图像](drag-and-drop-via-reorderlist-vb/_static/image3.png))


接下来，几个值填充该表。 请注意，`position`列包含的元素的排序顺序。


[![AJAX 表中的初始数据](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)

AJAX 表中的初始数据 ([单击此项可查看原尺寸图像](drag-and-drop-via-reorderlist-vb/_static/image6.png))


下一步需要生成`SqlDataSource`控制与新的数据库和它的表进行通信。 数据源必须支持`SELECT`和`UPDATE`SQL 命令。 列表元素的顺序更高版本更改时，`ReorderList`控件自动提交到数据源的两个值`Update`命令： 的新位置和元素的 ID。 因此，数据源需要`<UpdateParameters>`部分，了解这两个值：

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

`ReorderList`控件需要设置以下属性：

- `AllowReorder`： 是否可以重新排列列表项
- `DataSourceID`： 数据源的 ID
- `DataKeyField`： 数据源中的主键列的名称
- `SortOrderField`： 提供的列表项的排序顺序数据源列

在中`<DragHandleTemplate>`和`<ItemTemplate>`的部分中，列表的布局可以细微调整。 此外，数据绑定是可能使用`Eval()`方法，如下所示：

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

以下 CSS 样式信息 (在被引用`<DragHandleTemplate>`一部分`ReorderList`控件) 可确保，鼠标指针能够相应地更改时悬停拖动句柄：

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

最后，`ScriptManager`控件初始化 ASP.NET AJAX 页面：

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

运行此示例中，浏览器和有点重新排列的列表项。 然后，重新加载页面和/或我们来看一下数据库。 更改后的位置维护和中的值也会反映`position`中的数据库列不需任何代码，只需通过使用标记。


[![中的新列表项顺序根据数据库更改的数据](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)

根据新列表的数据库更改数据项顺序 ([单击此项可查看原尺寸图像](drag-and-drop-via-reorderlist-vb/_static/image9.png))

> [!div class="step-by-step"]
> [上一篇](using-postbacks-with-reorderlist-vb.md)
