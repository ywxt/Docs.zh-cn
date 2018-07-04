---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
title: 包装事务 (VB) 内的数据库修改 |Microsoft Docs
author: rick-anderson
description: 本教程是四个查看更新、 删除和插入数据的批处理的第一个。 在本教程中我们了解如何允许数据库事务...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: 7d821db5-6cbb-4b38-af14-198f9155fc82
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
msc.type: authoredcontent
ms.openlocfilehash: cf87dd0e677a73dc81cc430157be22b01ff0f7a8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390130"
---
<a name="wrapping-database-modifications-within-a-transaction-vb"></a>包装事务 (VB) 中的数据库修改
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_VB.zip)或[下载 PDF](wrapping-database-modifications-within-a-transaction-vb/_static/datatutorial63vb1.pdf)

> 本教程是四个查看更新、 删除和插入数据的批处理的第一个。 在本教程中我们了解如何数据库事务允许批处理的修改来执行作为一个原子操作，以确保所有步骤都成功或失败的所有步骤。


## <a name="introduction"></a>介绍

正如我们看到的开头[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程中，GridView 提供内置支持用于行级编辑和删除。 只需单击几下鼠标就可以，只要你是具有编辑和删除基于每个行的内容，而无需编写一行代码，创建丰富的数据修改界面。 但是，在某些情况下，此时间不够，并且我们需要向用户提供编辑或删除一批记录的能力。

例如，最基于 web 的电子邮件客户端使用一个网格，列出每个消息其中每个行包含电子邮件的信息 （主题、 发件人，等） 以及一个复选框。 此接口允许用户通过检查它们，然后单击删除所选消息按钮删除多个消息。 编辑界面批处理非常适合在用户通常编辑许多不同的记录的情况下。 而不强制用户通过单击编辑、 其更改，然后单击更新为每个需要对其进行修改的记录，编辑界面一批呈现具有其编辑界面的每个行。 用户可以快速修改的需要进行更改的行集，并通过单击全部更新按钮保存这些更改。 在此系列教程中我们将介绍如何创建用于插入、 编辑和删除数据的批处理的接口。

执行批处理操作时它非常重要，以确定是否应该可以为一些成功的批处理中的操作，而有些失败。 请考虑一批删除接口-如果已成功，删除所选的第一个记录，但第二个失败，例如，由于外键约束冲突而应发生什么情况？ 应第一个记录的删除回滚或是可以接受的第一条记录要保留已删除？

如果所需的批处理操作被视为[原子操作](http://en.wikipedia.org/wiki/Atomic_operation)，其中一个是其中的所有步骤成功或失败的所有步骤，则需要进行扩充以支持的数据访问层[数据库事务](http://en.wikipedia.org/wiki/Database_transaction)。 数据库事务保证原子性的一套`INSERT`， `UPDATE`，和`DELETE`语句在事务的保护伞下执行，并且是所有的大多数现代数据库系统所支持的功能。

在本教程中我们将介绍如何扩展 DAL 使用数据库事务。 后续教程中将检查批处理插入、 更新和删除接口的实现 web 页。 让我们来开始 ！

> [!NOTE]
> 当修改批事务中的数据时，原子性并不总是需要。 在某些情况下，这可能是可以接受的一些成功的数据修改，在同一个批处理中的其他人失败，例如当从基于 web 的电子邮件客户端中删除一组电子邮件。 如果有 s 数据库错误会中途删除处理，它可能可接受的没有错误处理这些记录将保留已删除的 s。 在这种情况下，不需要进行修改，以支持数据库事务 DAL。 还有其他批处理操作方案，但是，原子性至关重要。 当客户将她资金从一个银行帐户移到另一个时，必须执行两项操作： 将资金必须要从第一个帐户并添加到第二个。 虽然银行可能不介意具有成功的第一步，但第二个步骤失败，其客户将可以理解的是感到不安。 我鼓励您在学习本教程并实现与 DAL 来支持数据库事务，即使您不打算将其用在批插入、 更新和删除我们将生成以下三个教程中的接口的增强功能。


## <a name="an-overview-of-transactions"></a>事务的概述

大多数数据库包括对支持*事务*，它实现了多个数据库命令，分组到单个逻辑工作单元。 构成事务的数据库命令都保证是原子的这意味着所有命令将都失败或所有将会成功。

一般情况下，通过使用以下模式的 SQL 语句实现事务：

1. 指示事务的开始。
2. 执行构成事务的 SQL 语句。
3. 如果在步骤 2，回滚事务中的语句之一时出错。
4. 如果没有错误完成所有步骤 2 中的语句，则提交事务。

SQL 语句用于创建、 提交和回滚事务时，可以输入手动编写 SQL 脚本或创建存储过程，或通过以编程方式意味着要使用 ADO.NET 或中的类[ `System.Transactions`命名空间](https://msdn.microsoft.com/library/system.transactions.aspx)。 在本教程中我们将仅检查管理使用 ADO.NET 的事务。 在将来的教程中我们将探讨如何在数据访问层，此时我们将探讨用于创建、 回滚和提交事务的 SQL 语句中使用存储的过程。 在此期间，请查阅[在 SQL Server 存储过程中管理事务](http://www.4guysfromrolla.com/webtech/080305-1.shtml)有关详细信息。

> [!NOTE]
> [ `TransactionScope`类](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx)中`System.Transactions`命名空间使开发人员能够以编程方式将一系列语句包装在事务范围内，并且包括对涉及多个复杂事务的支持两个不同的数据库或甚至不同类型的数据存储，如 Microsoft SQL Server 数据库、 Oracle 数据库和 Web 服务等源。 我已决定而不是在本教程使用 ADO.NET 事务`TransactionScope`类，因为 ADO.NET 是更具体的数据库事务，并在许多情况下，是要少得多占用大量资源。 此外，在某些情况下`TransactionScope`类使用 Microsoft 分布式事务处理协调器 (MSDTC)。 配置、 实现和性能问题周围 MSDTC 使它而不是专用的和高级主题和这些教程的范围之外。


在使用 SqlClient 提供程序在 ADO.NET 中，通过调用启动的事务[`SqlConnection`类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)s [ `BeginTransaction`方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)，它将返回[ `SqlTransaction`对象](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)。 中放入了构成事务的数据修改语句`try...catch`块。 如果在语句中出现错误`try`阻止执行传输到`catch`块，可以回滚事务通过`SqlTransaction`对象 s [ `Rollback`方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)。 如果所有的语句会成功完成，调用`SqlTransaction`对象 s [ `Commit`方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx)末尾`try`块提交事务。 以下代码片段演示此模式。 请参阅[维护与事务的数据库一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)有关 ADO.NET 中使用事务的附加语法和示例。


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample1.vb)]

默认情况下，在类型化数据集中 Tableadapter 不使用事务。 若要为事务提供支持，我们需要增加 TableAdapter 类以包括使用上面的模式来执行一系列的范围内的事务数据修改语句的其他方法。 在步骤 2 中，我们将了解如何使用分部类来添加这些方法。

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>步骤 1： 使用批处理的数据 Web 页创建工作

我们开始探索如何扩展以支持数据库事务的 DAL 之前，让 s 先花点时间来创建我们将在本教程需要 ASP.NET web pages 和遵循的三个。 首先，通过添加一个名为的新文件夹`BatchData`，然后添加以下 ASP.NET 页面中，将使用每个页面相关联`Site.master`母版页。

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`


![将 ASP.NET 页面添加与 SqlDataSource 相关的教程](wrapping-database-modifications-within-a-transaction-vb/_static/image1.gif)

**图 1**： 将 ASP.NET 页面添加与 SqlDataSource 相关的教程


与其他文件夹，一样`Default.aspx`将使用`SectionLevelTutorialListing.ascx`用户控件，若要列出其部分中的教程。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](wrapping-database-modifications-within-a-transaction-vb/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image1.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image2.png))


最后，将这四个页面添加到条目为`Web.sitemap`文件。 具体而言，自定义后添加以下标记站点图`<siteMapNode>`:


[!code-xml[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample2.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧的菜单现在包含批处理的数据教程使用的项。


![站点图现在包括批处理的数据教程使用的条目](wrapping-database-modifications-within-a-transaction-vb/_static/image3.gif)

**图 3**： 站点图现在包括批处理的数据教程使用的条目


## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>步骤 2： 更新数据访问层，以便支持数据库事务

返回在第一个教程中，我们讨论[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)，DAL 中的类型化数据集组成 DataTables 和 Tableadapter。 DataTables 保存数据时，Tableadapter 提供的功能，若要从数据库的数据读入数据表，若要使用到数据表和等所做的更改更新数据库。 前面曾提到，Tableadapter 还提供用于更新数据，我为批量更新和 DB 直接引用了这两种模式。 使用批更新模式时，数据集、 DataTable 或 Datarow 的集合传递 TableAdapter。 此数据枚举和每个插入、 修改或已删除的行， `InsertCommand`， `UpdateCommand`，或`DeleteCommand`执行。 使用 DB 直接模式时，TableAdapter 是改为传递列插入、 更新或删除一条记录所需的值。 DB 直接模式方法然后使用这些传入的值以执行正确`InsertCommand`， `UpdateCommand`，或`DeleteCommand`语句。

无论使用的更新模式，自动生成的 Tableadapter 方法不使用事务。 默认情况下每个 insert、 update 或 delete 执行 TableAdapter 的被视为单个离散操作。 例如，假设由 BLL 中某些代码使用 DB 直接模式是将十个记录插入数据库。 此代码将调用 TableAdapter 的`Insert`方法十倍。 如果前五个插入成功，但第 6 项导致了异常前, 五个插入的记录将保持在数据库中。 同样，如果批更新模式用于执行插入、 更新和删除到插入、 修改和删除数据表中的行，如果第一个的多个修改成功，但更高版本时遇到错误，这些早期的修改，已完成将保留在数据库中。

在某些情况下，我们想要确保在修改的一系列原子性。 若要完成此我们必须通过添加新执行的方法来手动扩展 TableAdapter `InsertCommand`， `UpdateCommand`，和`DeleteCommand`s 之下的事务。 在中[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)我们在使用[分部类](http://en.wikipedia.org/wiki/Partial_type)来扩展类型数据集内 DataTables 的功能。 此方法还可以用于 Tableadapter。

类型化数据集`Northwind.xsd`位于`App_Code`文件夹的`DAL`子文件夹。 创建子文件夹中的`DAL`名为的文件夹`TransactionSupport`并添加名为的新类文件`ProductsTableAdapter.TransactionSupport.vb`（请参阅图 4）。 此文件将保存的部分实现`ProductsTableAdapter`，包括用于执行数据修改使用事务的方法。


![添加一个名为 TransactionSupport 文件夹和名为 ProductsTableAdapter.TransactionSupport.vb 的类文件](wrapping-database-modifications-within-a-transaction-vb/_static/image4.gif)

**图 4**： 添加一个名为文件夹`TransactionSupport`和名为的类文件 `ProductsTableAdapter.TransactionSupport.vb`


输入以下代码到`ProductsTableAdapter.TransactionSupport.vb`文件：


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample3.vb)]

`Partial`关键字在类声明中此处指示中添加的成员为要添加到编译器`ProductsTableAdapter`类中`NorthwindTableAdapters`命名空间。 请注意`Imports System.Data.SqlClient`在文件顶部的语句。 因为 TableAdapter 配置为使用 SqlClient 提供程序，在内部它使用[ `SqlDataAdapter` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx)要向数据库发出其命令对象。 因此，我们需要使用`SqlTransaction`类，以开始事务，然后将其提交或回滚它。 如果使用 Microsoft SQL Server 之外的数据存储，你将需要使用相应的提供程序。

这些方法提供了开始回滚所需的构造块，并提交事务。 它们标记`Public`，使他们能够在使用`ProductsTableAdapter`、 DAL 中的另一个类或从另一个层体系结构，如 BLL。 `BeginTransaction` 此时将打开 TableAdapter s 内部`SqlConnection`（如果需要），开始事务，并将它分配给`Transaction`属性，并将事务附加到内部`SqlDataAdapter`s`SqlCommand`对象。 `CommitTransaction` 并`RollbackTransaction`调用`Transaction`对象 s`Commit`并`Rollback`方法，分别，再关闭内部`Connection`对象。

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>步骤 3： 添加方法以更新和删除数据之下的事务

完成这些方法中，我们重新准备好将方法添加到`ProductsDataTable`或执行一系列命令之下的事务的 BLL。 以下方法使用批更新模式来更新`ProductsDataTable`实例使用的事务。 它通过调用来启动一个事务`BeginTransaction`方法，然后使用`Try...Catch`块以发出数据修改语句。 如果在调用`Adapter`对象 s`Update`方法会引发异常，则执行会传输到`catch`块，将回滚事务并重新引发的异常。 请记住，`Update`方法通过枚举所提供的行来实现批处理更新模式`ProductsDataTable`并执行必要`InsertCommand`， `UpdateCommand`，和`DeleteCommand`s。 如果任何一个的这些命令将导致错误，事务已回滚，撤消上一事务 s 生命周期内进行的修改。 应`Update`语句完成不会出错，整个提交事务。


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample4.vb)]

添加`UpdateWithTransaction`方法`ProductsTableAdapter`类中的分部类通过`ProductsTableAdapter.TransactionSupport.vb`。 或者，此方法无法添加到的业务逻辑层 s`ProductsBLL`类的一些小的语法更改。 也就是说，关键字`Me`中`Me.BeginTransaction()`， `Me.CommitTransaction()`，和`Me.RollbackTransaction()`需要替换`Adapter`(回想一下，`Adapter`中的属性的名称`ProductsBLL`类型的`ProductsTableAdapter`)。

`UpdateWithTransaction`方法使用批更新模式中，但也在事务中，如下所示的方法的范围内使用一系列数据库直接调用。 `DeleteProductsWithTransaction`方法接受作为输入`List(Of T)`类型的`Integer`，这是`ProductID`s 可删除。 方法启动的事务通过调用`BeginTransaction`，然后在`Try`块中，循环访问提供列表调用 DB 直接模式`Delete`方法为每个`ProductID`值。 如果对调用任一`Delete`失败，控制权转至`Catch`块，则回滚事务并重新引发的异常。 如果所有调用`Delete`成功，则将提交事务。 将以下方法添加到`ProductsBLL`类。


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample5.vb)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>应用事务跨多个 Tableadapter

在本教程中检查与事务相关的代码允许使用针对多个语句`ProductsTableAdapter`被视为原子操作。 但是，如果需要以原子方式执行多个不同的数据库表进行修改呢？ 例如，在删除某个类别时，我们可能首先想要重新分配到某些其他类别及其当前产品。 这两个步骤重新分配产品和删除该类别应作为一个原子操作执行。 但`ProductsTableAdapter`包括仅用于修改方法`Products`表和`CategoriesTableAdapter`包括仅用于修改方法`Categories`表。 那么，如何事务可以涵盖这两个 Tableadapter

一种方法是将方法添加到`CategoriesTableAdapter`名为`DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)`然后使该方法调用的存储的过程，同时重新分配产品并删除存储过程中定义的事务范围内的类别。 我们将在以后的教程中介绍了如何开始、 提交、 以及在存储过程中的回滚事务。

另一种方法是在包含 DAL 中创建一个帮助器类`DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)`方法。 此方法将创建的实例`CategoriesTableAdapter`并`ProductsTableAdapter`然后将这些设置两个 Tableadapter`Connection`属性设置为相同`SqlConnection`实例。 在该点的两个 Tableadapter 之一启动通过调用事务`BeginTransaction`。 用于重新分配产品和删除该类别的 Tableadapter 方法会调用在`Try...Catch`事务提交或回滚返回根据需要使用的块。

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>步骤 4： 添加`UpdateWithTransaction`业务逻辑层方法

在步骤 3 中我们添加了`UpdateWithTransaction`方法`ProductsTableAdapter`DAL 中。 我们应将相应的方法添加到 BLL。 表示层可以直接向 DAL 调用下调用时`UpdateWithTransaction`方法，这些教程有努力定义隔离从表示层 DAL 分层式体系结构。 因此，它理应我们继续这种方法。

打开`ProductsBLL`类文件，并添加一个名为`UpdateWithTransaction`到相应的 DAL 方法只需调用。 现在应在两个新方法`ProductsBLL`: `UpdateWithTransaction`，只需添加和`DeleteProductsWithTransaction`，它被添加在步骤 3 中。


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample6.vb)]

> [!NOTE]
> 这些方法不包括`DataObjectMethodAttribute`分配给中的大多数其他方法特性`ProductsBLL`类，因为我们将调用这些方法直接从 ASP.NET 页代码隐藏类。 请记住，`DataObjectMethodAttribute`用于标记哪些方法应出现在 ObjectDataSource 的配置数据源向导和 （选择、 更新、 插入或删除） 哪些选项卡下。 因为 GridView 中没有任何对批处理编辑或删除的内置支持，我们需要以编程方式调用这些方法，而不是使用无代码的声明性方法。


## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>步骤 5： 以原子方式更新数据库数据的表示层

为了说明该事务已更新一批记录时的效果，让 s 创建一个用户界面，列出在 GridView 中的所有产品，并包含一个按钮 Web 控件，单击时，将重新分配产品`CategoryID`值。 具体而言，将进度类别重新分配，以便分配一个有效的第一个的多个产品`CategoryID`分配的值而有些则是有意不存在`CategoryID`值。 如果我们尝试与产品更新数据库，其`CategoryID`不匹配现有类别的`CategoryID`、 外键约束冲突将会发生，将引发异常。 我们将看到在此示例是，当使用事务从外键约束冲突所引发的异常将导致以前有效`CategoryID`要回滚的更改。 当未使用事务，但是，将保持对初始类别进行修改。

首先打开`Transactions.aspx`页中`BatchData`文件夹，然后拖动 GridView 从工具箱拖到设计器。 设置其`ID`到`Products`并从其智能标记，请将其绑定到名为新 ObjectDataSource `ProductsDataSource`。 配置对象数据源以提取其数据从`ProductsBLL`类的`GetProducts`方法。 这将是只读的 GridView，因此设置下拉列表中插入、 更新和删除 （无） 选项卡并单击完成。


[![配置对象数据源使用 ProductsBLL 类的 GetProducts 方法](wrapping-database-modifications-within-a-transaction-vb/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image3.png)

**图 5**： 配置为使用 ObjectDataSource`ProductsBLL`类 s`GetProducts`方法 ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image4.png))


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](wrapping-database-modifications-within-a-transaction-vb/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image5.png)

**图 6**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image6.png))


完成配置数据源向导后，Visual Studio 将创建 BoundFields 和产品数据字段 CheckBoxField。 删除所有这些字段除外`ProductID`， `ProductName`， `CategoryID`，和`CategoryName`并重命名`ProductName`并`CategoryName`BoundFields`HeaderText`为产品和类别中，属性分别。 从智能标记中，选中启用分页选项。 以后进行这些修改，GridView 和 ObjectDataSource s 声明性标记看起来应如下所示：


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample7.aspx)]

接下来，添加 GridView 上面的三个按钮 Web 控件。 设置为刷新网格、 对修改类别 （与事务），第二个 s 和到修改类别 （而无需事务） 的第三个 s s 文本属性的第一个按钮。


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample8.aspx)]

此时 Visual Studio 中的设计视图应类似于屏幕截图中图 7 所示。


[![页包含一个 GridView 和三个按钮 Web 控件](wrapping-database-modifications-within-a-transaction-vb/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image7.png)

**图 7**： 该页包含 GridView 和三个按钮 Web 控件 ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image8.png))


创建事件处理程序为每个三个按钮的`Click`事件并使用以下代码：


[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample9.vb)]

刷新按钮 s`Click`事件处理程序只需重新绑定到 GridView 数据，通过调用`Products`GridView 的`DataBind`方法。

第二个事件处理程序将重新分配产品`CategoryID`s，并使用来自 BLL 来执行数据库的新事务方法更新之下的事务。 请注意，每个产品 s`CategoryID`随意设为相同的值作为其`ProductID`。 这将正常的前几种产品，由于这些产品具有`ProductID`发生这种情况将映射到有效的值`CategoryID`s。 但出现一次`ProductID`s 开始变得过大，这种巧合的重叠`ProductID`s 和`CategoryID`s 不再适用。

第三个`Click`事件处理程序更新产品`CategoryID`中相同的方式，但将更新发送到数据库使用`ProductsTableAdapter`s 默认`Update`方法。 这`Update`方法不会包装在一个事务内的命令系列中，以便在第一个遇到的外键约束冲突错误之前进行这些更改将保持不变。

若要演示此行为，请访问此页上的通过浏览器。 最初应看到数据的第一页，如图 8 中所示。 接下来，单击修改类别 （与事务） 按钮。 这将导致回发并尝试更新的所有产品`CategoryID`值，但会导致违反外键约束 （请参阅图 9）。


[![产品显示在可分页的 GridView](wrapping-database-modifications-within-a-transaction-vb/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image9.png)

**图 8**： 可分页的 GridView 中显示的产品 ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image10.png))


[![重新分配类别导致违反外键约束](wrapping-database-modifications-within-a-transaction-vb/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image11.png)

**图 9**： 重新分配类别导致违反了外键约束 ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image12.png))


现在，单击浏览器 s 后退按钮，然后单击刷新网格按钮。 刷新数据后你应看到完全相同的输出，如图 8 中所示。 也就是说，甚至是虽然某些产品`CategoryID`s 的已更改为合法值和在数据库中更新，它们时回滚发生外键约束冲突。

现在，尝试单击修改类别 （而无需事务） 按钮。 这会导致相同的外键约束冲突错误 （请参阅图 9），这一次的那些产品，但其`CategoryID`值已更改为合法值将不会回滚。 按浏览器 s 后退按钮，然后刷新网格按钮。 如图 10 所示，`CategoryID`的前八个产品已被重新分配。 例如，在图 8 中，更改针对必须`CategoryID`为 1，但在图 10 it s 中被重新分配到 2。


[![某些产品类别 Id 值更新时其他人已不是](wrapping-database-modifications-within-a-transaction-vb/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image13.png)

**图 10**： 某些产品`CategoryID`的值未更新时其他人已 ([单击以查看实际尺寸的图像](wrapping-database-modifications-within-a-transaction-vb/_static/image14.png))


## <a name="summary"></a>总结

默认情况下，TableAdapter 的方法在事务的作用域内不包装执行的数据库语句，但我们可以轻而易举地添加方法将创建、 提交和回滚事务。 在本教程中，我们将创建三个此类方法中的`ProductsTableAdapter`类： `BeginTransaction`， `CommitTransaction`，和`RollbackTransaction`。 我们已了解如何使用这些方法以及`Try...Catch`要进行数据修改语句的一系列原子块。 具体而言，我们创建了`UpdateWithTransaction`中的方法`ProductsTableAdapter`，它使用批更新模式来执行必要的修改的行对所提供的`ProductsDataTable`。 我们还添加了`DeleteProductsWithTransaction`方法`ProductsBLL`类中的 BLL，接受`List`的`ProductID`作为其输入值，并调用 DB 直接模式方法`Delete`为每个`ProductID`。 这两种方法首先创建一个事务，然后执行中的数据修改语句`Try...Catch`块。 如果发生异常，回滚事务，否则它是已提交。

步骤 5 所示事务性批处理更新与忘记了使用事务的批处理更新的效果。 在接下来三个教程中我们将在本教程中的布局的基础之上生成，创建用于执行批量更新、 删除和插入的用户界面。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [维护与事务的数据库一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [管理 SQL Server 中的事务的存储过程](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [事务变得更容易： `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 和 DataAdapters](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [在.NET 中使用 Oracle 数据库事务](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Dave Gardner、 Hilton Giesenow 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](batch-inserting-cs.md)
> [下一页](batch-updating-vb.md)
