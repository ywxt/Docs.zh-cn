---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
title: 处理计算列 (C#) |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 创建数据库表时，允许您定义计算的列由表达式计算其值，通常 referen...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 57459065-ed7c-4dfe-ac9c-54c093abc261
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ef548c627cd40159bb3961f479401657a2ac394
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832060"
---
<a name="working-with-computed-columns-c"></a>处理计算列 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_CS.zip)或[下载 PDF](working-with-computed-columns-cs/_static/datatutorial71cs1.pdf)

> 创建数据库表时，Microsoft SQL Server 可以定义计算的列的通常引用同一条数据库记录中的其他值的表达式计算其值。 此类的值为只读数据库，使用 Tableadapter 时需要特别注意的事项。 在本教程中我们将了解如何满足由计算列所带来的挑战。


## <a name="introduction"></a>介绍

Microsoft SQL Server 允许*[计算所得的列](https://msdn.microsoft.com/library/ms191250.aspx)*，从通常引用同一个表中的其他列的值的表达式计算其值的列。 例如，时间跟踪数据模型可能有一个名为的表`ServiceLog`列包括与`ServicePerformed`， `EmployeeID`， `Rate`，和`Duration`，等等。 尽管到期金额每个服务项 （正在持续时间的乘积的速率） 可以计算通过 web 页或其他编程接口，它可能会比较方便包括中的列`ServiceLog`名为表`AmountDue`报告这信息。 此列可以创建为普通的列，但它需要随时更新`Rate`或`Duration`更改列的值。 更好的方法是建立`AmountDue`列使用表达式的计算列`Rate * Duration`。 执行此操作会导致 SQL Server 自动计算`AmountDue`只要它在查询中引用列的值。

由于计算的列的值由一个表达式，此类列是只读的因此不能具有值分配给他们中`INSERT`或`UPDATE`语句。 但是，当计算的列使用的临时 SQL 语句的 TableAdapter 的主查询的一部分时，它们将自动包含在自动生成`INSERT`和`UPDATE`语句。 因此，TableAdapter s`INSERT`并`UPDATE`查询和`InsertCommand`和`UpdateCommand`属性必须更新以删除对任何计算列的引用。

使用的难题之一的计算列使用 TableAdapter 使用的临时 SQL 语句是，TableAdapter s`INSERT`和`UPDATE`查询自动重新生成任何 TableAdapter 配置向导已完成的时间。 因此，计算的列中手动删除从`INSERT`和`UPDATE`重新运行该向导时，查询将重新出现。 尽管使用存储的过程的 Tableadapter 不会受到此受到攻击，它们具有其自己的我们将在步骤 3 中解决的异常。

在本教程中，我们将添加到计算的列`Suppliers`Northwind 数据库中表，然后创建相应的 TableAdapter 以使用此表，其计算所得的列。 我们将使用存储的过程而不是临时 SQL 语句，以便使用 TableAdapter 配置向导时丢失了我们的自定义计划运行 t 我们 TableAdapter。

让我们来开始 ！

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>步骤 1： 添加计算的列到`Suppliers`表

Northwind 数据库不具有任何计算的列，因此我们需要添加一个自己。 对于本教程让我们来添加到计算的列`Suppliers`名为表`FullContactName`采用以下格式返回联系人的名称、 标题和它们工作的公司： `ContactName` (`ContactTitle`， `CompanyName`)。 此计算显示有关供应商的信息时，可能会在报表中使用列。

首先打开`Suppliers`通过右键单击表定义`Suppliers`表在服务器资源管理器中，从上下文菜单中选择打开表定义。 这将显示表及其属性，其数据类型，例如的列是否允许`NULL`s，等等。 若要添加计算的列，请先键入列的名称表定义。 接下来，在列属性窗口中的计算所得的列规范部分下 （公式） 文本框中输入它的表达式 （参见图 1）。 命名计算的列`FullContactName`，并使用以下表达式：


[!code-sql[Main](working-with-computed-columns-cs/samples/sample1.sql)]

请注意，可以在 SQL 连接字符串使用`+`运算符。 `CASE`语句可以用作在传统编程语言中的条件。 在上述表达式中`CASE`语句可以读取为： 如果`ContactTitle`不是`NULL`然后将输出`ContactTitle`串联的用逗号分隔，否则为发出执行任何操作。 有关详细信息的有用性`CASE`语句，请参阅[的 SQL Power`CASE`语句](http://www.4guysfromrolla.com/webtech/102704-1.shtml)。

> [!NOTE]
> 而不是使用`CASE`以下语句中，我们也可以或者使用`ISNULL(ContactTitle, '')`。 [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) 返回*checkExpression*如果，则为非 NULL，否则它将返回*replacementValue*。 尽管可以`ISNULL`或`CASE`将工作在本例中，有更多复杂方案其中的灵活性`CASE`语句不能由匹配`ISNULL`。


添加此计算的列后您的屏幕应如下所示屏幕快照中图 1。


[![添加一个名为 FullContactName 到供应商表的计算的列](working-with-computed-columns-cs/_static/image2.png)](working-with-computed-columns-cs/_static/image1.png)

**图 1**： 添加计算列命名`FullContactName`到`Suppliers`表 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image3.png))


在命名计算的列并输入其表达式之后, 将所做的更改保存到表通过单击工具栏中的保存图标，通过按 Ctrl + S，或通过转到文件菜单并选择保存`Suppliers`。

正在保存表应刷新在服务器资源管理器，其中包括在刚添加的列`Suppliers`表的列列表。 此外，（公式） 文本框中输入的表达式将自动调整为去除不必要的空格，环绕列名称带括号的等效表达式 (`[]`)，并包含括号来更明确显示操作的顺序：


[!code-sql[Main](working-with-computed-columns-cs/samples/sample2.sql)]

有关 Microsoft SQL Server 中的计算列的详细信息，请参阅[技术文档](https://msdn.microsoft.com/library/ms191250.aspx)。 另请参阅[How to: Specify Computed Columns](https://msdn.microsoft.com/library/ms188300.aspx)有关创建计算的列的分步演练。

> [!NOTE]
> 默认情况下，计算的列不以物理方式存储在表中，但会改为重新计算每次在查询中引用它们。 通过选中保留复选框，但是，您可以指示 SQL Server 以物理方式存储在表中的计算的列。 这样做使索引可以提高使用计算的列的值中的查询性能的计算列上创建其`WHERE`子句。 请参阅[对计算列创建索引](https://msdn.microsoft.com/library/ms189292.aspx)有关详细信息。


## <a name="step-2-viewing-the-computed-column-s-values"></a>步骤 2： 查看计算所得的列值 s

数据访问层上开始工作之前，让 s 花点时间查看`FullContactName`值。 从服务器资源管理器，右键单击`Suppliers`表名称，并从上下文菜单中选择新查询。 此时会弹出提示我们选择要在查询中包括的表的查询窗口。 添加`Suppliers`表，然后单击关闭。 接下来，检查`CompanyName`， `ContactName`， `ContactTitle`，和`FullContactName`供应商表中的列。 最后，单击执行查询并查看结果工具栏中的红色感叹号图标。

结果如图 2 所示，包括`FullContactName`，其中列出`CompanyName`， `ContactName`，和`ContactTitle`使用格式指南中; 列`ContactName`(`ContactTitle`, `CompanyName`) .


[![FullContactName 使用格式 ContactName （联系人职务、 公司名称）](working-with-computed-columns-cs/_static/image5.png)](working-with-computed-columns-cs/_static/image4.png)

**图 2**:`FullContactName`使用格式`ContactName`(`ContactTitle`， `CompanyName`) ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image6.png))


## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>步骤 3： 添加`SuppliersTableAdapter`到数据访问层

若要使用我们的应用程序中的供应商信息，我们需要首先在 DAL 中创建的 TableAdapter 和 DataTable。 理想情况下，这将使用完成相同的简单步骤检查在之前的教程。 但是，使用计算列引入了几个值得讨论的褶皱。

如果使用 TableAdapter 使用的临时 SQL 语句，则只需可以 TableAdapter s 通过 TableAdapter 配置向导的主查询中包含计算的列。 此操作，但是，将自动生成`INSERT`和`UPDATE`包含计算的列的语句。 如果您尝试执行这些方法之一`SqlException`消息列*ColumnName*无法修改，因为它是计算的列或者是 UNION 运算符的结果将会引发。 虽然`INSERT`并`UPDATE`语句可以手动将其调整到的 TableAdapter`InsertCommand`和`UpdateCommand`属性，这些自定义项将会丢失，重新运行 TableAdapter 配置向导时。

由于使用的临时 SQL 语句的 Tableadapter 脆弱性，建议我们使用计算列时使用的存储的过程。 如果使用现有的存储的过程，只需配置 TableAdapter 中所述[使用现有存储过程的类型化数据集 s Tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)教程。 但是，如果您有 TableAdapter 向导为你创建的存储的过程，是重要最初忽略主查询中的任何计算的列。 如果主查询中包含计算的列，TableAdapter 配置向导将通知你，完成后，它不能创建相应的存储的过程。 简单地说，我们需要最初配置 TableAdapter 使用计算的列释放主查询，然后手动更新相应的存储的过程和 TableAdapter 的`SelectCommand`包括计算的列。 这种方法是类似于所用[更新 TableAdapter 以使用](updating-the-tableadapter-to-use-joins-cs.md)`JOIN`*s*教程。

对于本教程，让我们来添加新的 TableAdapter，并将其自动为我们创建的存储的过程。 因此，我们将需要最初省略`FullContactName`主查询中的计算的列。

首先打开`NorthwindWithSprocs`中的数据集`~/App_Code/DAL`文件夹。 在设计器中右键单击并从上下文菜单上，选择要添加新的 TableAdapter。 这将启动 TableAdapter 配置向导。 查询数据从指定的数据库 (`NORTHWNDConnectionString`从`Web.config`) 并单击下一步。 由于我们尚未创建任何存储的过程的查询或修改`Suppliers`表中，选择的创建新的存储的过程选项，因此该向导将为我们创建它们，并单击下一步。


[![选择创建新存储的过程选项](working-with-computed-columns-cs/_static/image8.png)](working-with-computed-columns-cs/_static/image7.png)

**图 3**： 选择创建新存储的过程选项 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image9.png))


后续步骤会提示我们主查询。 输入以下查询，返回`SupplierID`， `CompanyName`， `ContactName`，和`ContactTitle`每个供应商的列。 请注意此查询有意省略了计算的列 (`FullContactName`); 我们将更新相应的存储的过程为在步骤 4 中包括此列。


[!code-sql[Main](working-with-computed-columns-cs/samples/sample3.sql)]

输入主查询，并单击下一步之后, 该向导将允许我们命名它将生成的四个存储的过程。 命名这些存储的过程`Suppliers_Select`， `Suppliers_Insert`， `Suppliers_Update`，和`Suppliers_Delete`，如图 4 所示。


[![自定义自动生成的存储过程的名称](working-with-computed-columns-cs/_static/image11.png)](working-with-computed-columns-cs/_static/image10.png)

**图 4**： 自定义 Auto-Generated 存储过程的名称 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image12.png))


下一步的向导步骤可用于名称的 TableAdapter 的方法，并指定用于访问和更新数据的模式。 保留所有三个复选框选中状态，但重命名`GetData`方法`GetSuppliers`。 单击完成以完成向导。


[![将 GetData 方法重命名为 GetSuppliers](working-with-computed-columns-cs/_static/image14.png)](working-with-computed-columns-cs/_static/image13.png)

**图 5**： 重命名`GetData`方法`GetSuppliers`([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image15.png))


单击完成，向导将创建四个存储的过程，并将 TableAdapter 和相应的 DataTable 添加到类型化数据集。

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>步骤 4： 在 TableAdapter s 主查询中包含计算的列

现在，我们需要更新 TableAdapter 和步骤 3 以包括中创建的 DataTable`FullContactName`计算所得的列。 这涉及到两个步骤：

1. 正在更新`Suppliers_Select`存储过程返回`FullContactName`计算的列和
2. 更新以包括相应的 DataTable`FullContactName`列。

首先，导航到服务器资源管理器并向下钻取到存储过程文件夹。 打开`Suppliers_Select`存储过程并更新`SELECT`查询，以便包括`FullContactName`计算所得的列：


[!code-sql[Main](working-with-computed-columns-cs/samples/sample4.sql)]

将所做的更改保存到存储过程，通过单击工具栏中的保存图标，通过按 Ctrl + S，或通过选择保存`Suppliers_Select`从文件菜单选项。

接下来，返回到数据集设计器，右键单击`SuppliersTableAdapter`，然后从上下文菜单中选择配置。 请注意，`Suppliers_Select`列现在包括`FullContactName`其的数据列集合中的列。


[![运行 TableAdapter 的配置向导以更新数据表的列](working-with-computed-columns-cs/_static/image17.png)](working-with-computed-columns-cs/_static/image16.png)

**图 6**： 运行 TableAdapter 的配置向导以更新 DataTable 的列 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image18.png))


单击完成以完成向导。 这将自动添加到相应的列`SuppliersDataTable`。 TableAdapter 向导非常智能，可检测的`FullContactName`列是计算的列，因此它是只读的。 因此，它将设置列 s`ReadOnly`属性设置为`true`。 若要验证这一点，选择从列`SuppliersDataTable`，然后转到属性窗口 （请参阅图 7）。 请注意，`FullContactName`列 s`DataType`和`MaxLength`属性也会相应地设置。


[![FullContactName 列被标记为只读的](working-with-computed-columns-cs/_static/image20.png)](working-with-computed-columns-cs/_static/image19.png)

**图 7**:`FullContactName`列被标记为只读的 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image21.png))


## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>步骤 5： 添加`GetSupplierBySupplierID`到 TableAdapter 方法

对于本教程中，我们将创建可更新网格中显示供应商的 ASP.NET 页。 在过去的教程我们已更新业务逻辑层中的单个记录通过检索特定记录从作为强类型化 DataTable，更新其属性，并将发送更新的 DataTable DAL 回 DAL 将更改传播到在数据库中。 若要完成-检索将 DAL 从更新的记录的此第一步我们需要首先添加`GetSupplierBySupplierID(supplierID)`对 DAL 的方法。

右键单击`SuppliersTableAdapter`数据集设计中，然后从上下文菜单选择添加查询选项。 与我们在步骤 3 中，让向导为我们生成新的存储的过程，通过选择创建新存储的过程选项 （请参阅回图 3 用于此向导步骤的屏幕截图）。 由于此方法将返回具有多个列的记录，则表示我们想要使用 SQL 查询的 select 语句返回的行并单击下一步。


[![选择它返回行选项](working-with-computed-columns-cs/_static/image23.png)](working-with-computed-columns-cs/_static/image22.png)

**图 8**： 选择它返回行选项 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image24.png))


后续步骤会提示我们要使用此方法的查询。 输入以下内容，它将返回相同的数据字段作为主查询，但特定供应商。


[!code-sql[Main](working-with-computed-columns-cs/samples/sample5.sql)]

下一个屏幕询问我们命名将会自动生成的存储的过程。 命名此存储的过程`Suppliers_SelectBySupplierID`单击下一步。


[![命名存储的过程 Suppliers_SelectBySupplierID](working-with-computed-columns-cs/_static/image26.png)](working-with-computed-columns-cs/_static/image25.png)

**图 9**： 命名存储过程`Suppliers_SelectBySupplierID`([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image27.png))


最后，向导提示操作，我们的数据访问模式和方法名称要用于 TableAdapter。 保留选中状态，这两个复选框，但重命名`FillBy`并`GetDataBy`方法添加到`FillBySupplierID`和`GetSupplierBySupplierID`分别。


[![名称 TableAdapter 方法 FillBySupplierID 和 GetSupplierBySupplierID](working-with-computed-columns-cs/_static/image29.png)](working-with-computed-columns-cs/_static/image28.png)

**图 10**： 命名 TableAdapter 方法`FillBySupplierID`并`GetSupplierBySupplierID`([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image30.png))


单击完成以完成向导。

## <a name="step-6-creating-the-business-logic-layer"></a>步骤 6： 创建业务逻辑层

我们创建的 ASP.NET 页的使用步骤 1 中创建计算的列之前，我们首先需要在 BLL 中添加相应的方法。 我们 ASP.NET 页中，我们将创建在步骤 7 中，将允许用户查看和编辑供应商。 因此，我们需要我们 BLL，若要提供，最小值，若要获取的所有供应商和另一个要更新的特定供应商提供的方法。

创建名为的新类文件`SuppliersBLLWithSprocs`在`~/App_Code/BLL`文件夹并添加以下代码：


[!code-csharp[Main](working-with-computed-columns-cs/samples/sample6.cs)]

一样; 与其他 BLL 类`SuppliersBLLWithSprocs`已`protected``Adapter`返回的实例的属性`SuppliersTableAdapter`类，以及两个`public`方法：`GetSuppliers`和`UpdateSupplier`。 `GetSuppliers`方法调用，并返回`SuppliersDataTable`返回的相应`GetSupplier`数据访问层中的方法。 `UpdateSupplier`方法检索有关特定供应商正在通过调用 DAL s 更新的信息`GetSupplierBySupplierID(supplierID)`方法。 然后更新`CategoryName`， `ContactName`，并`ContactTitle`属性并提交到数据库的这些更改，通过调用数据访问层 s`Update`方法，传入已修改`SuppliersRow`对象。

> [!NOTE]
> 除`SupplierID`并`CompanyName`，供应商表中的所有列都允许`NULL`值。 因此，如果传入的`contactName`或`contactTitle`参数是`null`我们需要设置相应`ContactName`并`ContactTitle`属性设置为`NULL`数据库值使用`SetContactNameNull`和`SetContactTitleNull`方法，分别。


## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>步骤 7： 使用从表示层的计算列

使用计算列添加到`Suppliers`表的 DAL 和 BLL 相应地更新，我们已准备好生成适用于 ASP.NET 页`FullContactName`计算所得的列。 首先打开`ComputedColumns.aspx`页中`AdvancedDAL`文件夹，然后拖动 GridView 从工具箱拖到设计器。 设置 GridView s`ID`属性设置为`Suppliers`并从其智能标记，请将其绑定到名为新 ObjectDataSource `SuppliersDataSource`。 配置要使用 ObjectDataSource`SuppliersBLLWithSprocs`类添加了备份在步骤 6 中，并单击下一步。


[![配置对象数据源以使用 SuppliersBLLWithSprocs 类](working-with-computed-columns-cs/_static/image32.png)](working-with-computed-columns-cs/_static/image31.png)

**图 11**： 配置为使用 ObjectDataSource`SuppliersBLLWithSprocs`类 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image33.png))


只有两种方法中定义`SuppliersBLLWithSprocs`类：`GetSuppliers`和`UpdateSupplier`。 请确保这两种方法在 SELECT 中指定和分别更新选项卡，并单击完成以完成 ObjectDataSource 的配置。

在数据源配置向导完成后，Visual Studio 将为每个返回的数据字段添加 BoundField。 删除`SupplierID`BoundField 和更改`HeaderText`的属性`CompanyName`， `ContactName`， `ContactTitle`，并`FullContactName`BoundFields 到公司、 联系人姓名、 标题和完整的联系人名称，分别。 从智能标记中，选中启用编辑复选框可启用 GridView s 内置编辑功能。

除了将 BoundFields 添加到 GridView，完成数据源向导还会导致 Visual Studio 设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为原始\_{0}。 还原此设置改回为其默认值， {0} 。

以后对 GridView 和 ObjectDataSource 中进行这些编辑，其声明性标记看起来应类似于下面：


[!code-aspx[Main](working-with-computed-columns-cs/samples/sample7.aspx)]

接下来，请访问此页上的通过浏览器。 如图 12 所示，在一个网格，其中包括列出每个供应商`FullContactName`列中，其值是只需其他三个列的串联，格式为`ContactName`(`ContactTitle`， `CompanyName`)。


[![在网格中列出每个供应商](working-with-computed-columns-cs/_static/image35.png)](working-with-computed-columns-cs/_static/image34.png)

**图 12**： 在网格中列出每个供应商 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image36.png))


单击编辑按钮，为特定供应商导致回发和中呈现该行其编辑界面 （见图 13）。 在其默认的编辑界面中呈现的前三个列-TextBox 控件`Text`属性设置为数据字段的值。 `FullContactName`列，但是，仍然是以文本形式。 当 BoundFields 已添加到在数据源配置向导，完成 GridView `FullContactName` BoundField s`ReadOnly`属性设置为`true`因为相应`FullContactName`中的列`SuppliersDataTable`具有其`ReadOnly`属性设置为`true`。 步骤 4 中所述`FullContactName`s`ReadOnly`属性设置为`true`因为 TableAdapter 检测到的列是计算所得的列。


[![FullContactName 列是不可编辑](working-with-computed-columns-cs/_static/image38.png)](working-with-computed-columns-cs/_static/image37.png)

**图 13**:`FullContactName`列是不可编辑 ([单击以查看实际尺寸的图像](working-with-computed-columns-cs/_static/image39.png))


继续更新一个或多个可编辑列的值，单击更新。 请注意如何`FullContactName`的值自动更新以反映更改。

> [!NOTE]
> GridView 目前使用 BoundFields 对于可编辑字段，从而导致其默认的编辑界面。 由于`CompanyName`字段是必需的它应转换为 TemplateField 包括一个 RequiredFieldValidator。 我将此作为练习留给感读取器。 请查阅[向编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)教程，了解将 BoundField 转换为 TemplateField 和添加验证控件的分步说明。


## <a name="summary"></a>总结

在定义表的架构时，Microsoft SQL Server 允许包含的计算列。 下面是从通常引用同一条记录中的其他列的值的表达式计算其值的列。 值的计算的列基于表达式，它们是只读的、 之后不能分配中的值`INSERT`或`UPDATE`语句。 将尝试自动生成对应的 TableAdapter 的主查询中使用计算的列时，这会带来的挑战`INSERT`， `UPDATE`，和`DELETE`语句。

在本教程中我们讨论了绕过由计算列所带来的挑战的方法。 具体而言，我们使用存储的过程中我们 TableAdapter 克服中使用的临时 SQL 语句的 Tableadapter 的固有受到攻击。 使用 TableAdapter 向导创建新存储过程时，很重要，我们具有最初省略任何计算的列，因为它们的存在会阻止数据修改存储过程正在生成的主查询。 最初配置 TableAdapter 后，其`SelectCommand`可以进行重组存储的过程，以包含任何计算的列。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Geisenow 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-additional-datatable-columns-cs.md)
> [下一页](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
