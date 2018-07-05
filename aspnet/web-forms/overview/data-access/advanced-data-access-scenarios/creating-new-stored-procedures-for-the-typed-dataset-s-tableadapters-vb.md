---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 创建新存储过程的类型化数据集的 Tableadapter (VB) |Microsoft Docs
author: rick-anderson
description: 在之前的教程中，我们有在我们的代码中创建 SQL 语句，并传递到数据库后，要执行的语句。 另一种方法是使用 s...
ms.author: aspnetcontent
ms.date: 07/18/2007
ms.assetid: a5a4a9ba-d18d-489a-a6b0-a3c26d6b0274
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: 601883ea0e0bbea08e564d77eea5ce7d19956cb7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829608"
---
<a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>创建新存储过程的类型化数据集的 Tableadapter (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_VB.zip)或[下载 PDF](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial67vb1.pdf)

> 在之前的教程中，我们有在我们的代码中创建 SQL 语句，并传递到数据库后，要执行的语句。 另一种方法是使用存储的过程的 SQL 语句都是在数据库中预定义。 在本教程中我们将了解如何使用 TableAdapter 向导为我们生成新的存储的过程。


## <a name="introduction"></a>介绍

这些教程中的数据访问层 (DAL) 使用类型化数据集。 如中所述[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中，类型化数据集包含强类型化 Datatable 和 Tableadapter。 DataTables 时要执行数据访问工作单位的基础数据库的 Tableadapter 接口在系统中表示的逻辑实体。 这包括填充数据表的数据、 执行返回标量数据的查询和插入、 更新和删除数据库中的记录。

Tableadapter 所执行的 SQL 命令可以是任一临时 SQL 语句，如`SELECT columnList FROM TableName`，或存储过程。 我们的体系结构中对 Tableadapter 使用临时 SQL 语句。 许多开发人员和数据库管理员，但是，首选的存储的过程而不是临时 SQL 语句的安全性、 可维护性和可更新性的原因。 有些用户则 ardently 选择其灵活性的临时 SQL 语句。 在我自己的工作中我优先通过临时 SQL 语句的存储的过程，但选择使用临时 SQL 语句来简化之前的教程。

当定义 TableAdapter，或添加新方法，TableAdapter 的向导，可以就像可以轻松地创建新的存储的过程或使用现有存储的过程一样，使用临时 SQL 语句。 在本教程中我们将介绍如何让 TableAdapter 的向导自动生成的存储的过程。 在下一教程中我们将探讨如何配置 TableAdapter 的方法以使用现有的或手动创建的存储的过程。

> [!NOTE]
> 请参阅 Rob Howard 的博客文章[Don t 尚未使用存储过程？](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/)并[Frans Bouma](https://weblogs.asp.net/fbouma/) s 博客文章[存储过程是坏，M Kay？](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx)的优、 缺点的热烈争论存储的过程和即席 SQL。


## <a name="stored-procedure-basics"></a>存储的过程的基础知识

函数是普遍适用于所有的编程语言的构造。 函数是函数调用时执行的语句的集合。 函数可以接受输入的参数，并可能会选择性地返回一个值。 *[存储过程](http://en.wikipedia.org/wiki/Stored_procedure)* 是数据库构造，它们与编程语言中的函数共享许多相似之处。 存储的过程由一组时调用该存储的过程执行的 T-SQL 的语句组成。 存储的过程可以接受零到多个输入参数和可以返回标量值，输出参数，或者是，大多数情况下，结果集从`SELECT`查询。

> [!NOTE]
> 存储的过程通常称为存储过程或 SPs。


使用创建的存储的过程[ `CREATE PROCEDURE` ](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) T-SQL 的语句。 例如，以下 T-SQL 脚本创建一个名为的存储的过程`GetProductsByCategoryID`中名为的单个参数采用`@CategoryID`，并返回`ProductID`， `ProductName`， `UnitPrice`，并`Discontinued`中列的字段`Products`表具有匹配的`CategoryID`值：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

一旦创建此存储的过程后，它可以使用以下语法进行调用：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.sql)]

> [!NOTE]
> 在下一教程中，我们将说明创建存储的过程通过 Visual Studio IDE。 对于本教程中，但是，我们将让 TableAdapter 向导自动为我们生成的存储的过程。


除了简单地返回数据，存储的过程通常用于执行单个事务的作用域内的多个数据库命令。 一个名为的存储的过程`DeleteCategory`，例如，可能需要`@CategoryID`参数，并执行两个`DELETE`语句： 第，一个删除相关的产品和第二个删除指定的类别。 存储过程中的多个语句都*不*自动包装在事务中。 其他的 T-SQL 命令需要发出消息，以确保存储的过程的多个命令将被视为原子操作的 s。 我们将了解如何在后续教程中的事务的作用域内换行的存储的过程的命令。

在体系结构中使用存储的过程，数据访问层的方法将调用特定的存储的过程，而不是发出的临时 SQL 语句。 而不是让它在应用程序 s 体系结构内定义，可集中管理 （数据库） 上执行的 SQL 语句的位置。 此集中管理可以说是可更轻松地查找、 分析和优化查询，并可清楚地了解有关在何处以及如何使用的数据库。

有关存储的过程的基础知识的详细信息，请在本教程末尾查阅更多参考资料部分中的资源。

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>步骤 1： 创建高级的数据访问层方案网页

我们开始讨论创建使用存储的过程的 DAL 之前，让我们来先花点时间在我们的网站项目，我们将需要为它和下一步的多个教程中创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`AdvancedDAL`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`


![添加 ASP.NET 页的高级的数据访问层方案教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**图 1**： 添加 ASP.NET 页的高级的数据访问层方案教程


在其他文件夹中，喜欢`Default.aspx`在`AdvancedDAL`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png))


最后，将这些页面添加到条目为`Web.sitemap`文件。 具体而言，在处理批处理数据后添加以下标记`<siteMapNode>`:


[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在为高级 DAL 方案教程包括的项。


![站点图现在包括项的高级的 DAL 方案教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)

**图 3**： 站点图现在包括项的高级的 DAL 方案教程


## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>步骤 2： 配置 TableAdapter 创建新存储过程

若要演示如何创建数据访问层，而不是临时 SQL 语句中使用存储的过程，让 s 创建新类型中的数据集`~/App_Code/DAL`文件夹名为`NorthwindWithSprocs.xsd`。 由于我们已在前面的教程中逐步完成此过程的详细信息，我们将继续快速完成此处的步骤。 如果你有疑问或需要进一步中创建和配置类型的数据集的分步说明，请返回到[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程。

向项目添加新的数据集，通过右键单击`DAL`文件夹中，选择添加新项，然后选择数据集模板，如图 4 中所示。


[![将新的类型化数据集添加到名为 NorthwindWithSprocs.xsd 的项目](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

**图 4**： 将新的类型化数据集添加到项目名为`NorthwindWithSprocs.xsd`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png))


这会创建新的类型化数据集、 打开其设计器中，创建新的 TableAdapter，并启动 TableAdapter 配置向导。 TableAdapter 配置向导 s 第一步让我们选择要使用的数据库。 Northwind 数据库的连接字符串应在下拉列表中列出。 选择此选项，然后单击下一步。

此下一屏幕中，我们可以选择 TableAdapter 应如何访问数据库。 在前面的教程中，我们选择了第一个选项，使用 SQL 语句。 对于本教程，选择第二个选项、 创建新的存储的过程，并单击下一步。


[![指示 TableAdpater 若要创建新的存储的过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

**图 5**： 指示 TableAdpater 到创建新存储过程 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png))


就像使用临时 SQL 语句，在下一步我们会要求提供`SELECT`TableAdapter s 主查询的语句。 但而不是使用`SELECT`在此处输入直接执行即席查询的语句，TableAdapter 的向导将创建包含此存储的过程`SELECT`查询。

使用以下`SELECT`此 TableAdapter 的查询：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]


[![输入 SELECT 查询](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)

**图 6**： 输入`SELECT`查询 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png))


> [!NOTE]
> 上述查询稍有不同的主查询`ProductsTableAdapter`在`Northwind`类型化数据集。 请记住，`ProductsTableAdapter`在`Northwind`类型化数据集包含两个相关的子查询，以使重新类别名称和每个产品的类别和供应商的公司名称。 在即将推出[使用联接到更新 TableAdapter](updating-the-tableadapter-to-use-joins-vb.md)教程中我们将查看添加到此 TableAdapter 相关数据。


花点时间单击高级选项按钮。 在此处，我们可以指定是否在向导应还生成 insert、 update 和 delete 语句的 TableAdapter，是否使用乐观并发，以及是否应在插入和更新后刷新数据表。 默认情况下检查生成 Insert、 Update 和 Delete 语句选项。 将其选中。 对于本教程，请取消选中使用开放式并发选项。

当遇到 TableAdapter 向导会自动创建的存储的过程，它将显示，刷新数据的表选项将被忽略。 无论是否选中此复选框、 生成 insert 和 update 存储的过程检索只需插入或只是更新的记录，正如我们将在步骤 3 中看到。


![保留选中选项生成 Insert、 Update 和 Delete 语句](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)

**图 7**： 保留选中选项生成 Insert、 Update 和 Delete 语句


> [!NOTE]
> 如果选中使用开放式并发选项，则该向导将添加到其他条件`WHERE`阻止中如果存在其他字段中的更改更新数据的子句。 回头[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程，以使用 TableAdapter s 内置乐观并发控制功能的详细信息。


输入后`SELECT`查询并确认，生成 Insert、 Update 和 Delete 语句选项处于选中状态，单击下一步。 此图 8 所示的下一个屏幕会提示选择、 插入、 更新和删除数据的向导将创建的存储过程的名称。 更改这些存储过程名称传递给`Products_Select`， `Products_Insert`， `Products_Update`，和`Products_Delete`。


[![重命名存储的过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**图 8**： 重命名存储过程 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))


若要查看 T-SQL 使用 TableAdapter 向导将创建四个存储的过程，请单击预览 SQL 脚本按钮。 从预览 SQL 脚本对话框中可能会将脚本保存到文件或将其复制到剪贴板。


![预览用于生成存储的过程的 SQL 脚本](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**图 9**： 预览版使用 SQL 脚本来生成存储的过程


命名存储的过程之后, 单击旁边名为 TableAdapter s 对应的方法。 就像时使用的临时 SQL 语句，我们可以创建填充现有数据表或返回一个新的方法。 我们还可以指定是否 TableAdapter 应包括插入、 更新和删除记录的 DB 直接模式。 保留选中状态，所有三个复选框，但重命名返回的 DataTable 方法`GetProducts`（如图 10 中所示）。


[![命名方法填充和 GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)

**图 10**： 命名方法`Fill`并`GetProducts`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png))


单击下一步以查看向导将执行的步骤的摘要。 单击完成按钮完成该向导。 在向导完成时，您将返回到设计器，现在应包含的数据集 s `ProductsDataTable`。


[![数据集 s 设计器会显示新添加的 ProductsDataTable](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)

**图 11**: s 的数据集设计器显示新添加`ProductsDataTable`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png))


## <a name="step-3-examining-the-newly-created-stored-procedures"></a>第 3 步： 检查新创建的存储的过程

TableAdapter 向导会自动使用在步骤 2 中创建用于选择、 插入、 更新和删除数据的存储的过程。 这些存储的过程可以查看或修改通过 Visual Studio 通过转到服务器资源管理器并向下钻取到数据库 s 存储过程文件夹。 如图 12 所示，Northwind 数据库包含四个新的存储的过程： `Products_Delete`， `Products_Insert`， `Products_Select`，和`Products_Update`。


![在步骤 2 中创建的四个存储的过程可以找到数据库 s 存储的过程文件夹中](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)

**图 12**： 在步骤 2 中创建的四个存储的过程可以找到数据库 s 存储的过程文件夹中


> [!NOTE]
> 如果看不到服务器资源管理器，转到视图菜单并选择服务器资源管理器选项。 如果看不到步骤 2 中添加的与产品相关的存储的过程，请尝试在存储过程文件夹上右键单击并选择刷新。


若要查看或修改存储的过程，请双击其名称在服务器资源管理器或，或者，右键单击存储过程，并选择打开。 图 13 显示了`Products_Delete`打开时的存储过程。


[![可以打开和修改从 Visual Studio 中的存储的过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)

**图 13**： 存储过程可以在打开和修改从在 Visual Studio ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png))


二者的内容`Products_Delete`和`Products_Select`存储的过程都相当直截了当。 `Products_Insert`并`Products_Update`存储的过程，但是，值得仔细观察它们都执行`SELECT`后的语句及其`INSERT`和`UPDATE`语句。 例如，下面的 SQL 构成`Products_Insert`存储过程：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

存储的过程接受作为输入参数`Products`返回的列`SELECT`TableAdapter 的向导和这些值中指定的查询中使用`INSERT`语句。 遵循`INSERT`语句中，`SELECT`查询用于返回`Products`列的值 (包括`ProductID`) 的新添加的记录。 此刷新功能时，可以添加新记录，因为它使用批更新模式自动更新新添加`ProductRow`实例`ProductID`具有分配的数据库的自动递增的值的属性。

下面的代码演示此功能。 它包含`ProductsTableAdapter`并`ProductsDataTable`为创建`NorthwindWithSprocs`类型化数据集。 通过创建一个新的产品添加到数据库`ProductsRow`实例，提供它的值，并调用 TableAdapter s`Update`方法，传入`ProductsDataTable`。 在内部，TableAdapter s`Update`方法枚举`ProductsRow`传入的 DataTable 中的实例 （在此示例中没有只有一个-我们只需添加），并执行相应的插入、 更新或删除命令。 在这种情况下，`Products_Insert`执行存储的过程时，将添加到新的记录`Products`表，并返回新添加的记录的详细信息。 `ProductsRow`实例的`ProductID`然后更新值。 之后`Update`方法后，我们就可以访问的新添加的记录 s`ProductID`值通过`ProductsRow`s`ProductID`属性。


[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.vb)]

`Products_Update`存储的过程同样包括`SELECT`语句后的其`UPDATE`语句。


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample7.sql)]

请注意，此存储过程包含两个输入的参数`ProductID`:`@Original_ProductID`和`@ProductID`。 此功能支持的方案可能已更改的主键。 例如，在员工数据库中，每个员工记录可能会使用员工的社会安全号码作为其主键。 若要更改现有员工的社会安全号码，必须提供新的社会保障号和原始。 有关`Products`无需执行表，此类功能，因为`ProductID`列为`IDENTITY`列，应永远不会更改。 事实上，`UPDATE`中的语句`Products_Update`存储的过程不包括`ProductID`其列列表中的列。 因此，尽管`@Original_ProductID`中使用`UPDATE`语句 s`WHERE`子句，它是多余的`Products`表，并可通过替换`@ProductID`参数。 修改存储的过程的参数时务必使用该存储的过程的 TableAdapter 方法也会更新。

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>步骤 4： 修改存储的过程的参数，并更新 TableAdapter

由于`@Original_ProductID`参数是多余，let s 删除从`Products_Update`完全存储过程。 打开`Products_Update`存储过程，删除`@Original_ProductID`参数，然后在`WHERE`子句`UPDATE`语句中，将更改从使用参数名称`@Original_ProductID`到`@ProductID`。 进行这些更改后，T-SQL 存储过程中应如以下所示：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample8.sql)]

若要将这些更改保存到数据库中，单击工具栏中的保存图标或按 Ctrl + S。 在此情况下，`Products_Update`存储的过程不需要`@Original_ProductID`输入的参数，但 TableAdapter 配置为通过此类参数。 您可以看到 TableAdapter 将发送到的参数`Products_Update`存储过程的 TableAdapter 选择数据集设计器中，转到属性窗口中，并单击中的省略号`UpdateCommand`s`Parameters`集合。 此时将显示图 14 中所示的参数集合编辑器对话框。


![参数集合编辑器列表使用的参数传递给 Products_Update 存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)

**图 14**： 参数集合编辑器列表使用的参数传递给`Products_Update`存储过程


您可以从此处删除此参数，只需选择`@Original_ProductID`成员和单击删除按钮的列表中的参数。

或者，可以刷新设计器中的 TableAdapter 上右键单击并选择配置用于所有方法的参数。 此时会弹出 TableAdapter 配置向导列出存储的过程用于选择、 插入、 更新和删除，以及参数的存储的过程，预计可以收到。 如果在更新下拉列表中单击您所见`Products_Update`存储的过程预期的输入的参数，现在不再包括`@Original_ProductID`（请参阅图 15）。 只需单击完成以自动更新使用 TableAdapter 的参数集合。


[![或者可以使用 TableAdapter 的配置向导以刷新其方法的参数集合](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**图 15**： 也可以选择使用 TableAdapter s 到刷新其方法的参数集合的配置向导 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png))


## <a name="step-5-adding-additional-tableadapter-methods"></a>步骤 5： 添加更多 TableAdapter 方法

步骤 2 中所示，作为创建新的 TableAdapter 时很容易地具有自动生成的相应存储的过程。 这同样适用向 TableAdapter 添加其他方法。 为了说明这一点，让我们来添加`GetProductByProductID(productID)`方法`ProductsTableAdapter`步骤 2 中创建。 此方法将作为输入`ProductID`值并返回有关指定的产品的详细信息。

首先在 TableAdapter 上右键单击并从上下文菜单中选择添加查询。


![向 TableAdapter 添加一个新的查询](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**图 16**： 向 TableAdapter 添加一个新的查询


这将启动 TableAdapter 查询配置向导中，首先会提示输入 TableAdapter 应如何访问数据库。 若要创建的新存储的过程，选择创建新的存储的过程选项，然后单击下一步。


[![选择创建新的存储的过程选项](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)

**图 17**： 选择创建新的存储的过程选项 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png))


下一个屏幕询问我们能够标识执行，它将返回一组行或单个标量值，或执行查询的类型`UPDATE`， `INSERT`，或`DELETE`语句。 由于`GetProductByProductID(productID)`方法将返回一行，将返回行选项选择并按下一步选择。


[![选择它将返回行选项](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)

**图 18**： 选择可返回行选项 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png))


下一屏幕中显示的 TableAdapter s 主查询，其中只列出了存储过程的名称 (`dbo.Products_Select`)。 存储的过程的名称替换为以下`SELECT`语句，返回所有指定的产品的产品字段：


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample9.sql)]


[![存储的过程的名称替换为 SELECT 查询](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)

**图 19**： 替换存储过程名称`SELECT`查询 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png))


后续屏幕要求您将创建的存储的过程的名称。 输入名称`Products_SelectByProductID`单击下一步。


[![命名新的存储的过程 Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**图 20**： 命名新的存储过程`Products_SelectByProductID`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image46.png))


在向导的最后一步，我们可以更改的方法名称生成以及指示是否使用填充 DataTable 模式，则返回的 DataTable 模式，或两者。 此方法中，将保留选中状态，这两个选项，但重命名的方法`FillByProductID`和`GetProductByProductID`。 单击下一步以查看该向导将执行，并单击完成以完成向导步骤的摘要。


[![将 TableAdapter 的方法重命名为 FillByProductID 和 GetProductByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image47.png)

**图 21**： 重命名的 TableAdapter 的方法`FillByProductID`并`GetProductByProductID`([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image49.png))


完成向导后，TableAdapter 具有可用的新方法`GetProductByProductID(productID)`，在调用时，将执行`Products_SelectByProductID`存储刚刚创建的过程。 花点时间查看这个新的存储的过程从服务器资源管理器通过钻取到存储过程文件夹并打开`Products_SelectByProductID`（如果未看到它，在存储过程文件夹上右键单击并选择刷新）。

请注意，`SelectByProductID`存储过程采用`@ProductID`作为输入参数并执行`SELECT`我们在向导中输入的语句。


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>步骤 6： 创建业务逻辑层类

整个系列教程，我们有努力保持表示层进行的所有业务逻辑层 (BLL) 对其调用分层式体系结构。 为了遵循这种设计决策，我们首先需要创建 BLL 类的新类型化数据集，我们可以从表示层访问产品数据之前。

创建名为的新类文件`ProductsBLLWithSprocs.vb`在`~/App_Code/BLL`文件夹并向其添加以下代码：


[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample11.vb)]

此类模仿`ProductsBLL`类从之前的教程，但使用的语义`ProductsTableAdapter`并`ProductsDataTable`对象从`NorthwindWithSprocs`数据集。 例如，而不是让`Imports NorthwindTableAdapters`的类文件作为开头的语句`ProductsBLL`确实`ProductsBLLWithSprocs`类使用`Imports NorthwindWithSprocsTableAdapters`。 同样，`ProductsDataTable`并`ProductsRow`使用此类中的对象都带有前缀`NorthwindWithSprocs`命名空间。 `ProductsBLLWithSprocs`类提供了两个数据访问方法，`GetProducts`和`GetProductByProductID`，和方法来添加、 更新和删除单个产品实例。

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>步骤 7： 使用`NorthwindWithSprocs`从表示层的数据集

此时，我们创建了使用存储的过程来访问和修改基础数据库数据的 DAL。 我们还构建了基本的 BLL 与方法来检索所有产品或添加、 更新的方法以及某一特定产品和删除产品。 表示圆润本教程中，let s 创建 ASP.NET 页使用的 BLL s`ProductsBLLWithSprocs`类用于显示、 更新和删除记录。

打开`NewSprocs.aspx`页中`AdvancedDAL`文件夹，然后从工具箱拖到设计器中，其命名为拖动的 GridView `Products`。 从 GridView s 智能标记选择将其绑定到名为新 ObjectDataSource `ProductsDataSource`。 配置要使用 ObjectDataSource`ProductsBLLWithSprocs`类，如图 22 所示。


[![配置对象数据源以使用 ProductsBLLWithSprocs 类](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image50.png)

**图 22**： 配置为使用 ObjectDataSource`ProductsBLLWithSprocs`类 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image52.png))


下拉列表中选择的选项卡有两个选项，`GetProducts`和`GetProductByProductID`。 由于我们想要在 GridView 中显示所有产品，因此选择`GetProducts`方法。 在更新、 插入和删除选项卡中每个下拉列表中只能有一种方法。 确保每个下拉列表，包含选中其相应方法，然后单击完成。

ObjectDataSource 向导运行完毕后，Visual Studio 将添加 BoundFields 和 CheckBoxField 到 GridView 的产品数据字段上。 通过选中启用编辑和智能标记中存在的启用删除选项启用的 GridView s 内置编辑和删除功能。


[![页包含一个 GridView 的编辑和删除启用支持](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image53.png)

**图 23**： 页面包含一个 GridView 编辑和删除支持已启用 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image55.png))


正如我们已讨论在上一教程中，在向导完成后 ObjectDataSource s，Visual Studio 设置`OldValuesParameterFormatString`属性设置为原始\_{0}。 这需要将还原为其默认值为{0}中的数据修改功能才能正常工作的顺序给出我们 BLL 中的方法所需的参数。 因此，请务必设置`OldValuesParameterFormatString`属性设置为{0}或从声明性语法中完全删除属性。

完成配置数据源向导，开启编辑和删除支持在 GridView 中，并返回 ObjectDataSource s 后`OldValuesParameterFormatString`为其默认值的属性，您的页面 + s 声明性标记应类似于下面：


[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample12.aspx)]

此时我们无法整理 GridView 通过自定义编辑界面以包括验证、 具有`CategoryID`和`SupplierID`列呈现为 Dropdownlist，以此类推。 我们还可以将客户端确认添加到删除按钮，并建议您花时间来实现这些增强功能。 由于已在前面的教程讨论这些主题，但是，我们将不包含它们再次此处。

无论是否增强 GridView 或不，测试在浏览器中的页面 + s 核心功能。 如图 24 所示，页将列出提供每个行编辑和删除功能的 GridView 中的产品。


[![产品可以查看、 编辑和删除从 GridView](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image56.png)

**图 24**: 产品可以查看、 编辑，并从 GridView 的已删除 ([单击以查看实际尺寸的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image58.png))


## <a name="summary"></a>总结

使用临时 SQL 语句从数据库或通过存储过程，Tableadapter 中类型的数据集可以访问数据。 当使用存储过程时，就可以使用任一现有的存储的过程或 TableAdapter 向导可以指导你创建新存储过程根据`SELECT`查询。 在本教程中我们探讨了如何为我们自动创建的存储的过程。

具有自动生成可帮助节省时间的存储的过程，有某些情况下，存储的过程创建的向导不对齐具有什么我们将创建我们自己的位置。 是一个例子`Products_Update`存储过程，应同时`@Original_ProductID`并`@ProductID`即使输入参数`@Original_ProductID`是多余的参数。

在许多情况下，可能已创建的存储的过程，或我们可能想要生成这些手动以便具有更精确地控制存储的过程的 s 命令。 在任一情况下，我们想要指示 TableAdapter 以使用现有的存储的过程的方法。 我们应了解如何完成此操作在下一步的教程。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [创建和维护的存储的过程](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [从存储过程中检索标量数据](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server 存储过程基本知识](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [存储过程： 概述](http://www.sqlteam.com/item.asp?ItemID=563)
- [编写存储的过程](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Hilton Geisenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
> [下一页](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
