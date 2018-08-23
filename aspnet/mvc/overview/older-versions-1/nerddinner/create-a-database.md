---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 创建数据库 |Microsoft Docs
author: microsoft
description: 步骤 2 显示了创建可容纳所有 dinner 数据库并立即回复即可我们 NerdDinner 应用程序的数据的步骤。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b6ab0740f251889f0fa0561809cac2bbe79bcb3a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834964"
---
<a name="create-a-database"></a>创建数据库
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的第 2 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 2 显示了创建可容纳所有 dinner 数据库并立即回复即可我们 NerdDinner 应用程序的数据的步骤。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner 步骤 2： 创建数据库

我们将使用数据库来存储所有的 Dinner 和 RSVP 数据 NerdDinner 应用程序。

以下步骤演示了创建使用免费的 SQL Server Express edition 数据库 (可以轻松地安装使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx))。 我们将编写的代码的所有适用于 SQL Server Express 和完整的 SQL Server。

### <a name="creating-a-new-sql-server-express-database"></a>创建新的 SQL Server Express 数据库

我们将开始通过我们的 web 项目，右键单击并选择**Add-&gt;新项**菜单命令：

![](create-a-database/_static/image1.png)

这将打开 Visual Studio 的"添加新项"对话框。 我们将按"数据"类别筛选，并选择"SQL Server 数据库"项模板：

![](create-a-database/_static/image2.png)

我们将命名为我们想要创建"NerdDinner.mdf"并点击确定的 SQL Server Express 的数据库。 Visual Studio 然后会要求到我们我们想要将此文件添加到我们 \App\_数据目录 （即目录已设置具有两个读取和写入安全 Acl）：

![](create-a-database/_static/image3.png)

我们将单击"是"，并将创建新数据库，并将其添加到我们的解决方案资源管理器：

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>创建我们的数据库中的表

我们现在有新的空数据库。 让我们向其添加一些表。

为此我们将导航到 Visual Studio 中，这使我们能够管理数据库和服务器内的"服务器资源管理器"选项卡窗口。 SQL Server Express 数据库存储在 \App\_我们的应用程序数据文件夹会自动显示在服务器资源管理器。 我们可以选择使用"连接到数据库"图标"服务器资源管理器"窗口顶部到列表以及添加其他 SQL Server 数据库 （本地和远程）：

![](create-a-database/_static/image5.png)

我们将添加到我们的 NerdDinner 数据库 – 一个来存储我们 Dinners，以及其他可以跟踪对它们的 RSVP 接受两个表。 我们可以通过右键单击在我们的数据库中的"表"文件夹，然后选择"添加新表"菜单命令创建新表：

![](create-a-database/_static/image6.png)

这将打开表设计器，可用于配置我们的表的架构。 对于我们"Dinners"表中，我们将添加 10 个列的数据：

![](create-a-database/_static/image7.png)

我们想要唯一主键的表的"DinnerID"列。 我们可以配置此"DinnerID"列上右键单击并选择"设置主键"菜单项：

![](create-a-database/_static/image8.png)

除了使 DinnerID 为主键，我们还想要将其配置为其值自动递增，如新的数据行添加到表的"标识"列 （这意味着第一个插入的 Dinner 行将具有 1 DinnerID，第二个插入行将具有 DinnerID 为 2，等等)。

我们可以通过选择"DinnerID"列来执行此操作，然后使用"列属性"编辑器"（是标识）"属性设置为"是"在列上。 我们将使用标准身份默认值 （从 1 开始并递增 1 上的每个新的 Dinner 行）：

![](create-a-database/_static/image9.png)

我们将通过键入 Ctrl-S 或通过使用保存我们的表格**文件-&gt;保存**菜单命令。 这将提示我们可以将表命名。 我们将它命名为"Dinners":

![](create-a-database/_static/image10.png)

我们的新 Dinners 表将显示我们在服务器资源管理器中的数据库中。

然后，我们将重复上述步骤，并创建"RSVP"表。 具有此表具有 3 个列。 我们将设置 RsvpID 列作为主键，并还将为标识列：

![](create-a-database/_static/image11.png)

我们会将其保存，并为其指定名称"回复"。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>设置表之间的外键关系

现在，我们会在我们的数据库中有两个表。 我们最后一个架构设计步骤将设置这两个表 – 之间的"多"关系，以便我们可以将 Dinner 的每一行与零个或多个将应用于它的 RSVP 行相关联。 我们将执行此操作通过配置 RSVP 表的"DinnerID"列"Dinners"表中有"DinnerID"列的外键关系。

为此我们将在服务器资源管理器中双击该中打开表设计器中的 RSVP 表。 然后，我们将选择"DinnerID"列中，右键单击，然后选择"Relationshps..."上下文菜单命令：

![](create-a-database/_static/image12.png)

此时会弹出一个对话框，我们可以使用安装程序表之间的关系：

![](create-a-database/_static/image13.png)

我们将单击"添加"按钮以向对话框添加新的关系。 添加关系后，我们将右侧的对话框中，展开属性网格中的"表和列规范"树视图节点，然后单击右侧的"..."按钮：

![](create-a-database/_static/image14.png)

单击"..."按钮将显示另一个对话框，可用于指定哪些表和列关系中涉及到，以及使我们能够命名关系。

我们将更改为"Dinners"主键表并选择 Dinners 表中的"DinnerID"列作为主键。 我们的 RSVP 表将外键表中，并且 RSVP。DinnerID 列将作为外键相关联：

![](create-a-database/_static/image15.png)

现在的 RSVP 表中每一行将与 Dinner 表中的一行关联。 SQL Server 将为我们带来维护引用完整性并防止我们添加一个新的 RSVP 行，如果它不指向有效的 Dinner 行。 它还将阻止我们删除 Dinner 行，如果有仍立即回复即可引用它的行。

### <a name="adding-data-to-our-tables"></a>将数据添加到我们的表

让我们通过将一些示例数据添加到我们 Dinners 表来完成。 我们可以将数据添加到表，它在服务器资源管理器中右键单击并选择"显示表数据"命令：

![](create-a-database/_static/image16.png)

我们将添加几行我们可以在以后当我们开始实现应用程序使用的 Dinner 数据：

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>下一步

我们已经完成了创建我们的数据库。 让我们现在创建我们可用于查询和更新它的模型类。

> [!div class="step-by-step"]
> [上一页](create-a-new-aspnet-mvc-project.md)
> [下一页](build-a-model-with-business-rule-validations.md)
