---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 使用现有存储过程的类型化数据集的 Tableadapter (VB) |Microsoft Docs
author: rick-anderson
description: 上一教程中我们介绍了如何使用 TableAdapter 向导来生成新的存储的过程。 在本教程中，我们将了解如何到同一 TableAdapter...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: a478b52387a6bbf726872978a0ad4a83c22c9911
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382891"
---
<a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>使用现有存储过程的类型化数据集的 Tableadapter (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip)或[下载 PDF](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> 上一教程中我们介绍了如何使用 TableAdapter 向导来生成新的存储的过程。 在本教程中我们了解如何同一 TableAdapter 向导才能使用现有的存储过程。 我们还了解如何手动将新的存储的过程添加到我们的数据库。


## <a name="introduction"></a>介绍

在中[前面的教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)我们已了解如何类型化数据集的 Tableadapter 无法配置为使用存储的过程来访问数据而不是临时 SQL 语句。 具体而言，我们介绍了如何使用 TableAdapter 向导自动创建这些存储的过程。 移植到 ASP.NET 2.0 的旧版应用程序时或生成围绕现有的数据模型的 ASP.NET 2.0 网站时，很可能该数据库已包含我们需要的存储的过程。 或者，您可能更愿意手动或通过某些工具以外的存储的过程会自动生成的 TableAdapter 向导创建您的存储的过程。

在本教程中我们将了解如何配置 TableAdapter 以使用现有存储的过程。 因为 Northwind 数据库只有少量的内置存储过程，我们还将在通过 Visual Studio 环境数据库中手动添加新的存储的过程所需的步骤。 让我们来开始 ！

> [!NOTE]
> 在中[包装事务内的数据库修改](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程中我们将方法添加到 TableAdapter 以支持事务 (`BeginTransaction`， `CommitTransaction`，依此类推)。 或者，可以完全在存储过程，它不需要修改数据访问层代码中管理事务。 在本教程中我们将探讨用于执行存储的过程的 s 语句的作用域内的事务的 T-SQL 命令。


## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>步骤 1： 将存储的过程添加到 Northwind 数据库

Visual Studio 便于向数据库添加新的存储的过程。 允许 s 添加到 Northwind 数据库中的所有列返回新的存储的过程`Products`表为具有特定`CategoryID`值。 从服务器资源管理器窗口中，展开 Northwind 数据库，以便显示其文件夹-数据库关系图、 表、 视图和等的。 正如我们看到在前面的教程，存储过程文件夹包含的数据库 s 的现有存储的过程。 若要添加新的存储的过程，只需右键单击存储过程文件夹，然后从上下文菜单中选择添加新存储过程选项。


[![右键单击存储的过程文件夹并添加新的存储的过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**图 1**： 右键单击存储过程文件夹并添加新的存储过程 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png))


如图 1 所示，选择添加新存储过程选项打开一个脚本窗口在 Visual Studio 中创建存储的过程所需的 SQL 脚本的轮廓。 它是我们充实此脚本并执行它的位置的存储的过程将添加到数据库的工作。

输入以下脚本：


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

此脚本中，执行时，将新的存储的过程添加到名为 Northwind 数据库`Products_SelectByCategoryID`。 此存储的过程接受一个输入的参数 (`@CategoryID`，类型的`int`)，则返回的所有字段以匹配的那些产品`CategoryID`值。

若要执行此`CREATE PROCEDURE`脚本和将存储的过程添加到数据库中，单击工具栏中的保存图标或按 Ctrl + S。 执行此操作，存储过程文件夹刷新之后, 显示新创建的存储过程。 此外，窗口中的脚本将更改从一个要点`CREATE PROCEDURE dbo.Products_SelectProductByCategoryID`到`ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`。 `CREATE PROCEDURE` 将新的存储的过程添加到数据库，而`ALTER PROCEDURE`更新现有。 由于该脚本开头已更改为`ALTER PROCEDURE`，更改存储的过程输入参数或 SQL 语句，并单击保存图标将使用这些更改更新存储的过程。

图 2 显示了 Visual Studio 后`Products_SelectByCategoryID`已保存存储的过程。


[![存储的过程 Products_SelectByCategoryID 已添加到数据库](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**图 2**: 存储过程`Products_SelectByCategoryID`已添加到数据库 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png))


## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>步骤 2： 配置 TableAdapter 以使用现有的存储的过程

现在，`Products_SelectByCategoryID`存储的过程已添加到数据库，我们可以配置我们的数据访问层时要使用此存储的过程调用其方法之一。 具体而言，我们将添加`GetProducstByCategoryID(<_i22_>categoryID)<!--_i22_-->`方法`ProductsTableAdapter`中`NorthwindWithSprocs`类型的数据集调用`Products_SelectByCategoryID`我们只需创建存储的过程。

首先打开`NorthwindWithSprocs`数据集。 右键单击`ProductsTableAdapter`和选择要启动 TableAdapter 查询配置向导将添加查询。 在中[前面的教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)我们选择了为我们创建新的存储的过程的 TableAdapter。 对于本教程中，但是，我们想要将新的 TableAdapter 方法连接到现有`Products_SelectByCategoryID`存储过程。 因此，从向导 s 第一步中选择使用现有存储的过程选项，然后单击下一步。


[![选择使用现有存储的过程选项](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**图 3**： 选择使用现有存储过程选项 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png))


下面的屏幕提供了存储的过程使用数据库 s 填充下拉列表。 选择存储的过程列出了其左侧和右侧返回 （如果有） 的数据字段的输入的参数。 选择`Products_SelectByCategoryID`存储从列表中的过程，并单击下一步。


[![选取 Products_SelectByCategoryID 存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**图 4**： 选取`Products_SelectByCategoryID`存储过程 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png))


下一个屏幕询问我们的数据类型返回的存储过程，我们在本文中的答案确定 TableAdapter 的方法返回的类型。 例如，如果我们指示返回表格数据，该方法将返回`ProductsDataTable`使用存储过程返回的记录填充实例。 与此相反，如果我们指示此存储的过程返回单个值将返回 TableAdapter`Object`分配存储过程返回的第一个记录的第一列中的值。

由于`Products_SelectByCategoryID`存储的过程返回的所有产品的特定类别的详细信息，选择第一个答案的表格数据-然后单击下一步。


[![指示存储的过程返回表格格式数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**图 5**： 指示存储过程返回表格格式数据 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png))


剩下的就是以指示要使用的方法模式跟这些方法的名称。 保留这两种填充 DataTable 选项选中状态，但重命名的方法的 DataTable 和返回`FillByCategoryID`和`GetProductsByCategoryID`。 然后单击下一步以查看向导将执行的任务的摘要。 如果一切看上去正确，单击完成。


[![名称方法 FillByCategoryID 和 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**图 6**： 命名方法`FillByCategoryID`并`GetProductsByCategoryID`([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))


> [!NOTE]
> 我们刚刚创建的 TableAdapter 方法`FillByCategoryID`并`GetProductsByCategoryID`，预期类型的输入的参数`Integer`。 此输入的参数值传递到存储过程通过其`@CategoryID`参数。 如果您修改`Products_SelectByCategory`存储过程的参数，将需要更新这些 TableAdapter 方法的参数。 如中所述[前一篇教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)，这可以通过两种方式之一： 通过手动添加或删除参数从参数集合中或通过重新运行 TableAdapter 向导。


## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>步骤 3： 添加`GetProductsByCategoryID(categoryID)`向 BLL 方法

使用`GetProductsByCategoryID`DAL 方法完成下, 一步是提供对业务逻辑层中的此方法的访问。 打开`ProductsBLLWithSprocs`类文件，并添加以下方法：


[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

此 BLL 方法只需返回`ProductsDataTable`从返回`ProductsTableAdapter`s`GetProductsByCategoryID`方法。 `DataObjectMethodAttribute`属性提供了使用 ObjectDataSource s 配置数据源向导的元数据。 具体而言，此方法会在选择的选项卡的下拉列表中。

## <a name="step-4-displaying-products-by-category"></a>步骤 4： 按类别显示产品

若要测试新添加`Products_SelectByCategoryID`存储的过程和相应的 DAL 和 BLL 方法，让我们来创建一个包含 DropDownList 和 GridView 的 ASP.NET 页面。 GridView 将显示属于所选类别的产品时，下拉列表将列出所有数据库中的类别。

> [!NOTE]
> 我们已创建母版/详细信息接口在前面的教程中使用 Dropdownlist。 有关实现此类母版/详细信息报告的更深入信息，请参阅[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)教程。


打开`ExistingSprocs.aspx`页中`AdvancedDAL`文件夹，然后从工具箱拖动到设计器将 DropDownList。 设置 DropDownList s`ID`属性设置为`Categories`并将其`AutoPostBack`属性设置为`True`。 接下来，从其智能标记绑定到名为新 ObjectDataSource DropDownList `CategoriesDataSource`。 配置对象数据源，以便检索其数据从`CategoriesBLL`类的`GetCategories`方法。 设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![从 CategoriesBLL 类的 GetCategories 方法检索数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**图 7**： 从检索数据`CategoriesBLL`类 s`GetCategories`方法 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png))


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**图 8**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png))


完成 ObjectDataSource 向导后，配置要显示 DropDownList`CategoryName`数据字段，并使用`CategoryID`字段作为`Value`为每个`ListItem`。

此时，DropDownList 和 ObjectDataSource s 声明性标记应与以下类似：


[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

接下来，将 GridView 拖到设计器中，将其放在 DropDownList 下面。 设置 GridView s`ID`到`ProductsByCategory`并从其智能标记，请将其绑定到名为新 ObjectDataSource `ProductsByCategoryDataSource`。 配置`ProductsByCategoryDataSource`若要使用的 ObjectDataSource`ProductsBLLWithSprocs`类，再对其检索其数据使用`GetProductsByCategoryID(categoryID)`方法。 由于此 GridView 仅将用于显示数据，设置下拉列表中插入、 更新和删除选项卡添加到 （无），然后单击下一步。


[![配置对象数据源以使用 ProductsBLLWithSprocs 类](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**图 9**： 配置为使用 ObjectDataSource`ProductsBLLWithSprocs`类 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png))


[![从 GetProductsByCategoryID(categoryID) 方法检索数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**图 10**： 从检索数据`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png))


在选择选项卡中选择的方法需要参数，因此该向导的最后一步提示我们输入参数的源。 为控件设置参数源下拉列表，并选择`Categories`ControlID 下拉列表中的控件。 单击完成以完成向导。


[![Categories DropDownList 用作源的 categoryID 参数](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**图 11**： 使用`Categories`作为源的 DropDownList`categoryID`参数 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png))


完成之后 ObjectDataSource 向导，Visual Studio 将为每个产品数据字段添加 BoundFields 和 CheckBoxField。 随时根据需要自定义这些字段。

请访问通过浏览器页面。 当来访的饮料类别选择的页和网格中列出的相应产品。 下拉列表更改为替代的类别，作为图 12 显示了、 导致回发和重新加载新选择的类别的产品的网格。


[![显示在生成类别的产品](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**图 12**： 显示在生成类别的产品 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png))


## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>步骤 5： 包装在事务范围内的存储的过程的语句

在中[包装事务内的数据库修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)我们讨论了用于执行一系列的范围内的数据库修改语句在事务的技术的教程。 回想一下，所有成功要么执行之下的一个事务修改或所有故障，请确保原子性。 使用事务的方法包括：

- 使用中的类`System.Transactions`命名空间，
- 让数据访问层使用 ADO.NET 类，如`SqlTransaction`，和
- 将 T-SQL 事务命令直接在存储过程中添加

*包装事务内的数据库修改*教程中的 DAL 使用 ADO.NET 类。 本教程的其余部分探讨如何管理使用存储过程中的从 T-SQL 命令的事务。

为手动启动、 提交和回滚事务的三个关键 SQL 命令是`BEGIN TRANSACTION`， `COMMIT TRANSACTION`，和`ROLLBACK TRANSACTION`分别。 使用从存储过程，我们需要应用以下模式中的事务时使用 ADO.NET 方法时，如：

1. 指示事务的开始。
2. 执行构成事务的 SQL 语句。
3. 如果从步骤 2 中，回滚事务语句之一中的错误。
4. 如果没有错误完成所有步骤 2 中的语句，则提交事务。

在 T-SQL 的语法中使用以下模板，可以实现此模式：


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

首先定义模板`TRY...CATCH`阻止 SQL Server 2005 到新的构造。 与处理方式一样`Try...Catch`阻止在 Visual Basic 中，SQL`TRY...CATCH`执行中的语句块`TRY`块。 如果任何语句将引发错误，控制立即转移到`CATCH`块。

如果执行 SQL 语句在事务中，该结构没有错误`COMMIT TRANSACTION`语句提交所做的更改并完成该事务。 如果其中一个语句导致错误，但是，`ROLLBACK TRANSACTION`在`CATCH`块将数据库返回到事务开始前的状态。 存储的过程也会引发错误使用[RAISERROR 命令](https://msdn.microsoft.com/library/ms178592.aspx)，这将导致`SqlException`以引发应用程序中。

> [!NOTE]
> 由于`TRY...CATCH`块是新的 SQL Server 2005 中，如果使用较旧版本的 Microsoft SQL Server，则上面的模板将无法工作。 如果不使用 SQL Server 2005，请查阅[在 SQL Server 存储过程中管理事务](http://www.4guysfromrolla.com/webtech/080305-1.shtml)会使用其他版本的 SQL Server 的模板。


让我们来看一个具体示例。 之间存在外键约束`Categories`并`Products`表，这意味着，每个`CategoryID`字段中`Products`表必须映射到`CategoryID`中的值`Categories`表。 任何违反此约束，如尝试删除具有关联的产品类别的操作导致违反外键约束。 若要验证这一点，重新访问二进制数据部分使用中的更新和删除现有的二进制数据示例 (`~/BinaryData/UpdatingAndDeleting.aspx`)。 此页列出每个类别 （请参阅图 13） 的编辑和删除按钮，以及系统中，但如果你尝试删除具有关联的产品-如饮料-类别删除失败由于外键约束冲突 （请参阅图 14）。


[![使用编辑和删除按钮的 GridView 中显示每个类别](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**图 13**： 具有编辑和删除按钮的 GridView 中显示每个类别 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png))


[![无法删除现有产品的类别](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**图 14**： 不能删除现有产品的类别 ([单击以查看实际尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png))


但是，假设我们想要允许删除而不考虑它们是否具有关联的产品的类别。 应删除与产品类别，假设我们想要同时删除其现有的产品 (尽管是另一种方法只需设置其产品`CategoryID`值到`NULL`)。 可以通过外键约束的级联规则实现此功能。 此外，我们可以创建存储的过程接受`@CategoryID`输入的参数并调用时，显式删除所有关联的产品，然后指定的类别。

此类存储过程，我们第一次尝试可能类似以下形式：


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

虽然这肯定将删除关联的产品和类别，它并未这样之下的事务。 想象一下是一些其他外键约束上`Categories`，将禁止删除特定`@CategoryID`值。 问题在于，在这种情况中的所有产品之前，将删除我们尝试删除类别。 最终结果是，对于此类的类别，此存储的过程将删除其所有产品类别依然存在，因为它仍有相关的一些其他表中的记录。

如果存储的过程已换行在事务范围内，但是，到删除`Products`表将在遇到时未能删除上回滚`Categories`。 以下存储的过程脚本使用事务以确保两者之间的原子性`DELETE`语句：


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

请花费片刻时间来添加`Categories_Delete`存储到 Northwind 数据库的过程。 有关将存储的过程添加到数据库的说明为步骤 1 返回引用。

## <a name="step-6-updating-thecategoriestableadapter"></a>步骤 6： 更新`CategoriesTableAdapter`

尽管我们已添加`Categories_Delete`到数据库，DAL 的存储的过程当前配置为使用的临时 SQL 语句来执行删除。 我们需要更新`CategoriesTableAdapter`，并指示它使用`Categories_Delete`改为存储过程。

> [!NOTE]
> 在本教程前面我们已使用`NorthwindWithSprocs`数据集。 但该数据集仅具有单个实体， `ProductsDataTable`，我们需要使用类别。 因此，对于本教程时我讨论的数据访问层 I m 指其余`Northwind`数据集，我们首先在中创建的那个[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程。


打开罗斯文数据集，选择`CategoriesTableAdapter`，并转到属性窗口。 属性窗口中会列出`InsertCommand`， `UpdateCommand`， `DeleteCommand`，和`SelectCommand`使用 TableAdapter，以及其名称和连接信息。 展开`DeleteCommand`属性以查看其详细信息。 如图 15 所示， `DeleteCommand` s`ComamndType`属性设置为文本，指示它发送的文本`CommandText`属性作为即席 SQL 查询。


![若要在属性窗口中查看其属性在设计器中选择 CategoriesTableAdapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**图 15**： 选择`CategoriesTableAdapter`以在属性窗口中查看其属性在设计器中


若要更改这些设置，请在属性窗口中选择 (DeleteCommand) 文本并从下拉列表中选择 （新建）。 这将清除出的设置`CommandText`， `CommandType`，和`Parameters`属性。 接下来，设置`CommandType`属性设置为`StoredProcedure`，然后键入名称的存储过程`CommandText`(`dbo.Categories_Delete`)。 如果你请务必首先按此顺序输入属性`CommandType`，然后`CommandText`-Visual Studio 将自动填充的参数集合。 如果不按此顺序输入这些属性，将需要手动添加到参数集合编辑器中的参数。 在任一情况下，它比较明智的做法单击要打开参数集合编辑器来验证是否正确的参数设置进行了更改 （请参阅图 16） 的参数属性中的椭圆的 s。 如果看不到对话框的中的任何参数，将添加`@CategoryID`参数手动 (不需要添加`@RETURN_VALUE`参数)。


![确保参数设置正确](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**图 16**： 确保在参数设置正确


一旦更新 DAL，如果删除某个类别自动将删除所有相关联的产品和之下的事务执行此操作。 若要验证这一点，返回到更新和删除现有的二进制数据页并单击删除按钮的一个类别。 鼠标的一次单击，将删除该类别及其所有相关联的产品。

> [!NOTE]
> 然后再测试`Categories_Delete`存储的过程，这将删除数以及所选类别的产品，可能会比较明智的做法使您的数据库的备份副本。 如果使用的`NORTHWND.MDF`数据库中`App_Data`，只需关闭 Visual Studio，并复制中的 MDF 和 LDF 文件`App_Data`到其他文件夹。 测试功能之后, 您可以将数据库还原通过关闭 Visual Studio 和替换当前 MDF 和 LDF 文件中`App_Data`与备份副本。


## <a name="summary"></a>总结

TableAdapter 的向导将自动为我们生成的存储的过程，而有些的时候，当我们可能已有创建此类存储的过程或想改为创建这些手动或使用其他工具。 为了适应这种情况下，TableAdapter 还可以将配置为指向现有的存储过程。 在本教程中我们介绍了如何将存储的过程手动添加到通过 Visual Studio 环境数据库以及如何将 TableAdapter 的方法连接到这些存储过程。 我们还探讨了 T-SQL 的命令和用于启动、 提交和回滚从存储过程中的事务脚本模式。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Geisenow、 S ren Jacob Lauritsen 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [下一页](updating-the-tableadapter-to-use-joins-vb.md)
