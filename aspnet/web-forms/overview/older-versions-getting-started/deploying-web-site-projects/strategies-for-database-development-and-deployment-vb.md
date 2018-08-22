---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
title: 数据库开发和部署 (VB) 策略 |Microsoft Docs
author: rick-anderson
description: 部署第一次的数据驱动的应用程序时可以会盲目地将数据库复制到生产环境的开发环境中。 B...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 07b8905d-78ac-4252-97fb-8675b3fb0bbf
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
msc.type: authoredcontent
ms.openlocfilehash: e07da4b5263ac3c6db19c375ca00cbcf87e0b35a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830071"
---
<a name="strategies-for-database-development-and-deployment-vb"></a>数据库开发和部署 (VB) 策略
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_vb.pdf)

> 部署第一次的数据驱动的应用程序时可以会盲目地将数据库复制到生产环境的开发环境中。 但执行直接在后续部署中的副本将覆盖输入到生产数据库中的任何数据。 相反，将数据库部署涉及将应用到生产数据库上上次部署以来对开发数据库所做的更改。 本教程中检查这些挑战，并提供各种策略来帮助进行 chronicling 并将其应用自上次部署以来对数据库所做的更改。


## <a name="introduction"></a>介绍

如前面的教程中所述，部署 ASP.NET 应用程序需要将相关的内容从开发环境复制到生产环境。 部署不是一次性事件，但而不是每次发布新版本的软件时或当发生的其他 bug 或确定并解决安全问题。 在复制的 ASP.NET 页面时，图像、 JavaScript 文件和其他此类文件到生产环境不需要关注如何将这些文件已更改自上次部署以来中。 您可以会盲目地将文件复制到生产环境中，覆盖现有内容。 遗憾的是，这种简单性不扩展到部署数据库。

部署第一次的数据驱动的应用程序时可以会盲目地将数据库复制到生产环境的开发环境中。 但执行直接在后续部署中的副本将覆盖输入到生产数据库中的任何数据。 相反，部署数据库涉及应用*更改*自上次部署到生产数据库上对开发数据库。 本教程中检查这些挑战，并提供各种策略来帮助进行 chronicling 并将其应用自上次部署以来对数据库所做的更改。

## <a name="the-challenges-of-deploying-a-database"></a>部署数据库的挑战

第一次部署数据驱动的应用程序之前，只有一个数据库，即在开发环境中，这正是你可以部署第一次的数据驱动的应用程序时盲目地数据库复制中的数据库到生产环境的开发环境。 但后部署应用程序有两个数据库副本： 一个在开发一个在生产环境中。

部署之间的数据库开发和生产数据库会变得不同步。生产数据库的架构保持不变，如添加新功能可能会更改开发数据库的架构。 您可能添加或删除列、 表、 视图或存储的过程。 此外可能被添加到开发数据库的重要数据。 许多数据驱动应用程序包括使用硬编码、 特定于应用程序不是用户可编辑的数据填充查找表。 例如，拍卖网站可能有一个带有描述正在双项的条件的选项的下拉列表： 新建、 等新、 好，和公平。 而不是硬编码直接在下拉列表中的这些选项是通常最好将它们放在数据库表。 如果在开发期间，一个名为不佳的新条件添加到表然后部署该应用程序时此相同的记录将需要添加到生产数据库中的查找表。

理想情况下，将数据库部署将涉及复制数据库从开发到生产环境。 但请记住，在部署应用程序并继续开发后，生产数据库正在使用真实用户的实际数据填充。 因此，如果你打算只需将数据库复制从开发到生产环境，在下一步部署将覆盖生产数据库和丢失其现有数据。 最终结果是，将数据库部署归结为应用开发数据库自上次部署以来所做的更改。

由于将数据库部署涉及自上次部署以来应用中的架构和数据，也可能更改，更改历史记录必须维护 （或在部署时确定），以便这些更改可以应用于生产环境。 有各种技术用于管理和将更改应用于数据模型。

### <a name="defining-the-baseline"></a>定义基线

若要维护对应用程序的数据库的更改需要具有某些起始状态，向其所做的更改应用于的基线。 一种极端的起始状态可以是任何表、 视图或存储的过程的空数据库。 此类基准会导致大型更改日志，因为它必须包括所有数据库的表、 视图和存储的过程以及在初始部署之后所做的任何更改的创建。 在另一端的极端情况下可以作为最初部署到生产环境的数据库的版本设置基线。 选择此选项将产生更小的更改日志，因为它只包括对以下第一个部署的数据库所做的更改。 这是我更喜欢的方法。 当然你可以选择道路方法的多个中间定义基线初始创建数据库和数据库将首先部署之间的一些点。

后，请考虑所选基线生成可执行以重新创建基准版本的 SQL 脚本。 此类脚本可快速重新创建数据库的基准版本。 此功能便尤其有用，在大型项目中可能有多个开发人员在项目或其他环境，例如测试或过渡环境，其中每个需要其自己的数据库副本。

有各种工具，以生成基准版本的 SQL 脚本。 从 SQL Server Management Studio (SSMS) 您可以右键单击数据库，请转到任务子菜单，并选择生成脚本选项。 这将启动脚本向导中，您可以指示要生成包含创建 s 对象的数据库的 SQL 命令的文件。 另一个选项是数据库发布向导，可以生成不仅能够创建数据库架构，但数据还将数据库表中的 SQL 命令。 数据库发布向导已在详细信息中检查回到*部署数据库*教程。 无论使用何种工具，最后应具有可用于重新创建数据库，基线版本的脚本文件应需要出现。

## <a name="documenting-the-database-changes-in-prose"></a>记录中的文本信息的数据库更改

在开发阶段保持对数据模型的更改的日志的最简单方法是中的文本信息记录所做的更改。 例如，如果已部署的应用程序开发期间添加到一个新列`Employees`表中，删除某一列从`Orders`表，并添加新表 (`ProductCategories`)，你将保留文本文件或 Microsoft Word 文档使用以下历史记录：

<a id="0.8_table01"></a>


| **更改日期** | **更改的详细信息** |
| --- | --- |
| 2009-02-03: | 添加的列`DepartmentID`(`int`，不为 NULL) 到`Employees`表。 添加从外的键约束`Departments.DepartmentID`到`Employees.DepartmentID`。 |
| 2009-02-05: | 已删除的列`TotalWeight`从`Orders`表。 中已捕获的数据关联`OrderDetails`记录。 |
| 2009-02-12: | 创建`ProductCategories`表。 有以下三列： `ProductCategoryID` (`int`， `IDENTITY`， `NOT NULL`)， `CategoryName` (`nvarchar(50)`， `NOT NULL`)，并且`Active`(`bit`， `NOT NULL`)。 添加到主键约束`ProductCategoryID`，默认值为 1 到`Active`。 |


有很多这种方法的缺点。 对于初学者而言，没有任何希望实现自动化。 随时需要这些更改应用于数据库-如时部署应用程序-开发人员必须手动实现每个更改，请一次一个。 此外，如果您需要重新构造从基线使用的更改日志数据库的特定版本，这样做因此需要越来越多的时间根据日志的大小增长情况。 此方法的另一个缺点是详细的清晰，每个更改日志条目级别保留记录更改的人员。 在多个开发人员团队中一些可能会使比其他更详细、 更具可读性，或更精确的条目。 此外，错误报告中也可能包含拼写错误和其他与用户相关的数据输入错误。

记录中的文本信息的数据库更改的主要优势是简单。 您不 t 需要知道如何创建和更改数据库对象的 SQL 语法。 相反，可以在文本信息记录所做的更改，实现通过 SQL Server Management Studio s 图形用户界面。

维护你更改日志中的文本信息，不可否认，不于某些项目，例如在范围内，较大的非常复杂和获胜 t 工作具有对数据模型中，频繁更改或涉及多个开发人员。 但我曾见过这种方法很好地对数据模型仅偶尔更改且其中个人开发人员不具有坚实的背景中创建和更改数据库对象的 SQL 语法的小型的人式项目中的工作。

> [!NOTE]
> 虽然更改日志中的信息，从技术上讲，直到部署时，才需要我建议保持更改的历史记录。 但是，而不是维护一个不断增长更改日志文件，请考虑让每个数据库版本不同的更改日志文件。 通常您将希望到版本数据库每次部署它。 通过维护的更改日志的日志可以从该基线，开始重新创建任何数据库版本通过执行更改日志脚本从版本 1 开始，并继续执行直到达到版本需要重新创建。


## <a name="recording-the-sql-change-statements"></a>记录 SQL 更改语句

维护的更改日志中的文本信息的主要缺点是自动化的缺少。 理想情况下，实现对生产数据库在部署时的数据库更改会简单，只单击一个按钮用于执行脚本，而无需手动执行一系列说明。 此类自动化可通过维护包含这些 SQL 命令，用于更改数据模型的更改日志。

SQL 语法包括多个用于创建和修改各种数据库对象的语句。 例如， [ *CREATE TABLE 语句*](https://msdn.microsoft.com/library/ms174979.aspx)、 执行时，使用指定的列和约束创建一个新表。 [ *ALTER TABLE 语句*](https://msdn.microsoft.com/library/ms190273.aspx)修改现有表中，添加、 删除或修改它的列或约束。 也有语句来创建、 修改和删除索引、 视图、 用户定义的函数、 存储的过程、 触发器和其他数据库对象。

返回到前面的示例，在已部署应用程序添加到一个新列的开发过程中映像`Employees`表中，删除某一列从`Orders`表，并添加新表 (`ProductCategories`)。 此类操作会导致使用以下 SQL 命令的更改日志文件：

[!code-sql[Main](strategies-for-database-development-and-deployment-vb/samples/sample1.sql)]

将这些更改推送到生产数据库在部署时是一次单击操作： 打开 SQL Server Management Studio、 连接到您的生产数据库、 打开新查询窗口中，粘贴更改日志的内容和单击执行运行脚本。

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>使用比较工具来进行同步的数据模型

记录中的文本信息的数据库更改非常简单，但实现所做的更改需要开发人员每次更改其中一个在生产数据库上一次;记录更改 SQL 命令那样容易和快速像单击按钮，在生产数据库上实现这些更改，但需要学习和掌握的 SQL 语句和用于创建和更改数据库对象的语法。 数据库比较工具需要从这两种方法的最佳和放弃最差。

数据库比较工具比较架构或两个数据库的数据，并显示一个摘要报告，显示您数据库有何不同。 然后，只需单击一个按钮，可以生成用于同步一个或多个数据库对象的 SQL 命令。 简单地说，您可以使用数据库比较工具比较开发和生产数据库在部署时，生成文件，其中包含 SQL 命令，在执行时，会将更改应用于生产数据库的架构因此它镜像开发数据库的架构。

有多种第三方数据库提供的许多不同的供应商的比较工具。 是这样一个例子[ *SQL Compare*](http://www.red-gate.com/products/SQL_Compare/)，也可由[ *Red Gate Software*](http://www.red-gate.com/)。 让我们来演练使用 SQL 进行比较来比较和同步开发和生产数据库架构的过程。

> [!NOTE]
> 在撰写本文时 SQL Compare 的当前版本是版本 7.1 中，具有 Standard Edition 395 美元的成本计算。 通过下载免费的 14 天试用版，您可以照着操作。


SQL Compare 启动时将打开比较项目对话框中，显示已保存的 SQL Compare 项目。 创建新项目。 这将启动项目配置向导中，提示输入的数据库的相关信息进行比较 （请参阅图 1）。 输入的信息，开发和生产环境数据库。


[![开发和生产数据库进行比较](strategies-for-database-development-and-deployment-vb/_static/image2.jpg)](strategies-for-database-development-and-deployment-vb/_static/image1.jpg)

**图 1**： 比较开发和生产数据库 ([单击以查看实际尺寸的图像](strategies-for-database-development-and-deployment-vb/_static/image3.jpg))


> [!NOTE]
> 如果开发环境数据库是 SQL Express Edition 数据库文件中的`App_Data`你将需要在 SQL Server Express 数据库服务器中注册该数据库，以便从图 1 中所示的对话框中选择它的网站的文件夹。 若要实现此目的的最简单方法是打开 SQL Server Management Studio (SSMS)，连接到 SQL Server Express 数据库服务器，并附加该数据库。 如果你没有在计算机上安装的 SSMS 可以下载并安装免费[ *SQL Server 2008 Management Studio Basic 版本*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en)。


除了选择要比较的数据库，还可以指定各种比较设置从选项选项卡。你可能想要启用的一种选择是"忽略约束和索引名称。" 前面曾提到，在前面的教程，我们添加应用程序服务到开发和生产数据库的数据库对象。 如果您使用`aspnet_regsql.exe`生产数据库上创建这些对象，那么你将找到 primary key 和 unique 约束名称，在开发和生产数据库之间不同的工具。 因此，SQL Compare 将标记为不同的应用程序服务表的所有。 您可以将"忽略约束和索引名称"未选中状态和同步的约束名称，或指示 SQL Compare 要忽略这些差异。

选择到数据库后进行比较 （和查看比较选项），单击立即比较按钮以开始比较。 接下来的几秒内，通过 SQL Compare 会检查两个数据库的架构并生成报告有何不同。 我特意进行了开发数据库，以显示 SQL Compare 界面中记下此类差异是如何进行一些修改。 如图 2 所示，我添加 ve`BirthDate`列添加到`Authors`要删除的表`ISBN`从列`Books`表，并添加了一个新表， `Ratings`，这是为了让用户访问站点速率已审阅的丛书。

> [!NOTE]
> 在本教程中所做的数据模型更改是为了演示如何使用数据库比较工具。 不会在将来的教程中在数据库中查找这些更改。


[![SQL 比较列出了开发和生产数据库之间的差异](strategies-for-database-development-and-deployment-vb/_static/image5.jpg)](strategies-for-database-development-and-deployment-vb/_static/image4.jpg)

**图 2**: SQL 比较列出了开发之间的差异和生产数据库 ([单击以查看实际尺寸的图像](strategies-for-database-development-and-deployment-vb/_static/image6.jpg))


SQL Compare 分解成组的数据库对象、 快速显示哪些对象存在于这两个数据库中但不同，该对象存在于一个数据库，但不是另一个，和的对象相同。 正如您所看到的有两个数据库中存在但不同的两个对象：`Authors`表，该表具有添加的列，和`Books`表，该表包含一个删除。 只能在开发数据库，即新创建中存在的一个对象`Ratings`表。 并且有两个数据库中完全相同的 117 对象。

选择数据库对象将显示 SQL 差异窗口，其中显示了这些对象有何不同。 SQL 差异窗口中，在图 2 中，底部显示突出显示的`Authors`开发数据库表中的有`BirthDate`列，该列中找不到`Authors`生产数据库上的表。

后查看差异，并选择你想要同步的对象下, 一步是生成更新生产数据库的架构所需的 SQL 命令以匹配开发数据库。 通过同步向导完成此操作。 同步向导确认哪些对象同步，并总结了该操作计划 （参见图 3）。 您可以立即同步数据库或生成具有可以在方便的时候运行的 SQL 命令的脚本。


[![使用同步向导以同步数据库架构](strategies-for-database-development-and-deployment-vb/_static/image8.jpg)](strategies-for-database-development-and-deployment-vb/_static/image7.jpg)

**图 3**： 使用同步向导来同步数据库架构 ([单击以查看实际尺寸的图像](strategies-for-database-development-and-deployment-vb/_static/image9.jpg))


数据库比较工具，如 Red Gate Software 的 SQL Compare 请将所做的更改应用到开发数据库架构与生产数据库指向和单击一样简单。

> [!NOTE]
> SQL 比较进行比较和同步两个数据库*架构*。 遗憾的是，它不进行比较和同步两个数据库表中的数据。 Red Gate Software 提供的名为产品[ *SQL 数据比较*](http://www.red-gate.com/products/SQL_Data_Compare/)的比较和两个数据库之间同步数据，但它是从 SQL Compare 一个单独的产品，另一个 395 美元的费用。


## <a name="taking-the-application-offline-during-deployment"></a>使应用程序脱机部署过程

正如我们已看到在这些教程中，整个部署是一个过程，涉及多个步骤： 将从开发环境的 ASP.NET 页、 母版页、 CSS 文件、 JavaScript 文件、 图像和其他所需的内容复制到生产环境环境中;将复制生产环境特定的配置信息，如果需要;和自上次部署以来将所做的更改应用于数据模型。 具体取决于的文件数和更改数据库的复杂性，这些步骤可能需要从几秒钟到几分钟时间才能完成。 在此时段内的 web 应用程序在不断变化，并访问网站的用户可能会遇到错误或意外的行为。

部署网站时，最好使 web 应用程序"脱机"直至部署已完成。 使应用程序脱机 （和将其重新启动后在部署过程完成后） 非常简单，只将文件上传，然后将其删除。 从 ASP.NET 2.0 中，名为的文件的存在`app_offline.htm`在应用程序根目录使整个网站"脱机"。 对该站点上的 ASP.NET 页的任何请求自动进行响应的内容与`app_offline.htm`文件。 删除该文件后，应用程序重新联机。

采用应用程序脱机在部署期间，然后，只需上传`app_offline.htm`到生产环境的文件根目录之前开始部署过程并随后将它删除 （或将其更名为其他内容） 一次部署已完成。 有关此技术的详细信息请参阅 John Peterson 的文章，采用[ *ASP.NET 应用程序脱机*](http://www.15seconds.com/issue/061207.htm)。

## <a name="summary"></a>总结

在部署数据驱动的应用程序的主要挑战是围绕将数据库部署。 因为有两个版本的数据库的一个开发环境中，一个在生产环境中的这些两个数据库架构可能会成为同步，因为在开发过程中添加新功能。 新增更多，因为正在使用真实用户的实际数据填充为生产数据库，您不能覆盖生产数据库与已修改的开发数据库像你可以部署对构成应用程序 （ASP.NET 页的文件时图像文件等）。 相反，将数据库部署需要实现的精确的一套自上次部署以来对生产数据库上的开发数据库所做更改。

本教程介绍了用于维护并将数据库更改的日志应用三种方法。 最简单的方法是将中的文本信息记录所做的更改。 虽然这种做法使一个手动过程在生产数据库上实现这些更改，它不需要了解的 SQL 命令用于创建和更改数据库对象。 更好的方法，以及在更大的项目或项目中使用多个开发人员而言，变得更加愉快的一个是作为一系列 SQL 命令记录所做的更改。 这极大地 hastens 推出到目标数据库的这些更改。 最佳的这两种方法可以通过使用 Red Gate Software 的 SQL Compare 之类的数据库比较工具。

本教程最后，我们专注于数据驱动的应用程序部署。 下一步的系列教程探讨如何在生产环境中的错误响应。 我们将介绍如何显示友好的错误页，而不是而不是黄色死亡屏幕。 我们将了解如何记录错误 s 详细信息以及如何进行此类错误发生时发出警报。

快乐编程 ！

> [!div class="step-by-step"]
> [上一页](configuring-a-website-that-uses-application-services-vb.md)
> [下一页](displaying-a-custom-error-page-vb.md)
