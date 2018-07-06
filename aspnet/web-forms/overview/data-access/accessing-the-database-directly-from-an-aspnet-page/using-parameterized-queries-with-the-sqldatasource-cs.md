---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: 通过 SqlDataSource (C#) 使用参数化的查询 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们继续我们看 SqlDataSource 控件，并了解如何定义参数化的查询。 参数可以指定这两个声明...
ms.author: aspnetcontent
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: e4612c48259bfee12a68080ec902c589b2a378b0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819745"
---
<a name="using-parameterized-queries-with-the-sqldatasource-c"></a>通过 SqlDataSource (C#) 使用参数化的查询
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe)或[下载 PDF](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> 在本教程中，我们继续我们看 SqlDataSource 控件，并了解如何定义参数化的查询。 参数声明的方式和以编程方式，可以指定，可以从多个位置，如在查询字符串、 会话状态，其他控件等拉入。


## <a name="introduction"></a>介绍

在上一教程中，我们已了解如何使用 SqlDataSource 控件直接从数据库检索数据。 使用配置数据源向导，我们可以选择数据库，然后将其： 选取要从表或视图; 返回的列输入自定义 SQL 语句;或使用存储的过程。 从表或视图中选择列或输入自定义 SQL 语句，SqlDataSource 控件是否 s`SelectCommand`属性分配生成的临时 SQL`SELECT`语句也是如此这`SELECT`语句时执行SqlDataSource 的`Select()`方法调用 (以编程方式或自动从数据 Web 控件)。

SQL`SELECT`语句中不具备的上一个教程的演示使用`WHERE`子句。 在中`SELECT`语句，`WHERE`子句可用于限制返回的结果。 例如，若要显示的多个 50.00 美元的成本计算的产品的名称，我们可以使用以下查询：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

通常情况下中, 使用的值`WHERE`子句确定由某些外部源，例如查询字符串值、 会话变量中或从 Web 控件的页上的用户输入。 理想情况下，使用指定此类输入*参数*。 使用 Microsoft SQL Server 参数表示使用`@parameterName`，如下所示：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

SqlDataSource 支持参数化的查询，同时`SELECT`语句和`INSERT`， `UPDATE`，和`DELETE`语句。 此外，参数值可以自动提取自很多的源的查询字符串，会话状态的页上，控件和其他操作或可以以编程方式分配。 在本教程中，我们将了解如何定义参数化的查询，也能如何来指定参数值同时以声明方式和以编程方式。

> [!NOTE]
> 上一教程中，比较 ObjectDataSource 我们所选的工具已通过使用 SqlDataSource，注意其概念相似之处是首先 46 的教程。 这些相似之处还扩展到参数。 ObjectDataSource 的参数映射到的输入参数的业务逻辑层中的方法。 使用 SqlDataSource，直接在 SQL 查询中定义参数。 这两个控件具有的参数集合及其`Select()`， `Insert()`， `Update()`，和`Delete()`方法，并且两个可以从预定义源 （查询字符串值、 会话变量等填充这些参数值) 或以编程方式分配。


## <a name="creating-a-parameterized-query"></a>创建参数化查询

SqlDataSource 控件 s 配置数据源向导提供了用于定义要检索数据库记录时所执行的命令的以下三种渠道：

- 通过选择从现有的表或视图中，列
- 通过输入自定义 SQL 语句，或
- 通过选择存储的过程

选取现有表或视图，为参数中的列时`WHERE`子句必须指定通过添加`WHERE`子句对话框。 当创建自定义 SQL 语句时，但是，可以输入的参数直接`WHERE`子句 (使用`@parameterName`来表示每个参数)。 一个[存储过程](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)包含一个或多个 SQL 语句和这些语句可以参数化。 SQL 语句中使用的参数但是，必须是中作为输入参数传递给存储过程。

由于创建参数化的查询取决于如何 SqlDataSource 的`SelectCommand`是指定，可让 s 看在所有这三种方法。 若要开始，打开`ParameterizedQueries.aspx`页中`SqlDataSource`文件夹中，将一个 SqlDataSource 控件从工具箱拖到设计器中，并设置其`ID`到`Products25BucksAndUnderDataSource`。 接下来，单击控件 s 智能标记中的配置数据源链接。 选择要使用的数据库 (`NORTHWINDConnectionString`) 并单击下一步。

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>步骤 1： 添加`WHERE`子句时从表或视图中选择列

选择要从 SqlDataSource 控件与数据库中返回的数据，当配置数据源向导允许我们只需选择要从现有表中返回或查看 （请参阅图 1） 的列。 因此自动执行生成 sql`SELECT`语句，就是发送到数据库时 SqlDataSource 的`Select()`调用方法。 与我们在上一教程中，从下拉列表中选择产品表，并检查`ProductID`， `ProductName`，和`UnitPrice`列。


[![选择要从表或视图中返回的列](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**图 1**： 从表或视图返回结果中选择列 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png))


若要包括`WHERE`中的子句`SELECT`语句中，单击`WHERE`按钮，此时会出现添加`WHERE`子句对话框 （请参见图 2）。 若要添加参数以限制返回的结果`SELECT`查询中，首先选择要筛选的数据的列。 接下来，选择要用于筛选的运算符 (=、 &lt;， &lt;=、 &gt;，依此类推)。 最后，如选择从查询字符串或会话状态参数的值的源。 配置参数后, 单击添加按钮以将其包含在`SELECT`查询。

对于此示例中，let s 只返回这些结果其中`UnitPrice`值是否小于或等于 $25.00。 因此，选取`UnitPrice`从列下拉列表和&lt;= 运算符下拉列表中。 使用硬编码参数值 （如 $25.00) 时或参数值将以编程方式指定，则选择无从源下拉列表。 接下来，25.00 中的值文本框中输入的硬编码参数值，并单击添加按钮完成该过程。


[![限制返回的结果添加 WHERE 子句对话框的](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**图 2**： 限制返回结果中添加`WHERE`子句对话框的 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png))


添加参数后, 单击确定以返回到配置数据源向导。 `SELECT`现在应包含在向导底部语句`WHERE`与名为的参数的子句`@UnitPrice`:


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> 如果指定多个条件中的`WHERE`子句中添加`WHERE`子句对话框的向导将它们联接起来与`AND`运算符。 如果您需要包括`OR`中`WHERE`子句 (如`WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`)，然后您需要生成`SELECT`通过自定义 SQL 语句屏幕的语句。


完成配置的 SqlDataSource （单击下一步，然后完成)，然后检查 SqlDataSource s 声明性标记。 标记现在包括`<SelectParameters>`集合，其中明确指出中参数的源`SelectCommand`。


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

当 SqlDataSource s`Select()`调用方法时，`UnitPrice`参数值 (25.00) 应用于`@UnitPrice`中的参数`SelectCommand`之前发送到数据库。 最终结果是，只有小于或等于 $25.00 返回从这些产品`Products`表。 若要确认此操作，请向页面添加一个 GridView，将其绑定到此数据源，然后查看通过浏览器页面。 您应该只会看到列出的产品小于或等于 $25.00，如图 3 确认。


[![显示只有那些产品小于或等于 $25.00](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**图 3**： 显示仅这些产品小于或等于 $25.00 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png))


## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>步骤 2： 将参数添加到自定义 SQL 语句

添加自定义 SQL 语句时可以输入`WHERE`子句显式或查询生成器的筛选器单元格中指定值。 若要说明这一点，让其价格不超过特定阈值的 GridView 中显示只是这些产品的 s。 首先，通过添加到文本框`ParameterizedQueries.aspx`页后，可以从用户处收集此阈值。 设置文本框 s`ID`属性设置为`MaxPrice`。 添加一个按钮 Web 控件，并设置其`Text`属性设置为显示匹配的产品。

接下来，将 GridView 拖到绘图页上，并从其智能标记选择创建名为新 SqlDataSource `ProductsFilteredByPriceDataSource`。 从配置数据源向导中，转到指定的自定义 SQL 语句或存储的过程屏幕 （请参阅图 4），并输入以下查询：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

输入后查询 （手动或通过查询生成器），单击下一步。


[![只返回那些产品小于或等于参数值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**图 4**： 返回仅这些产品小于或等于参数值 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png))


由于查询包含参数，该向导的下一个屏幕提示我们输入的参数值的源。 从参数源下拉列表中选择控件并`MaxPrice`(TextBox 控件的`ID`值) 从 ControlID 下拉列表。 您还可以输入要在其中用户未输入任何文本的情况下使用的可选的默认值`MaxPrice`文本框中。 目前，不要输入默认值。


[![MaxPrice 文本框的文本属性用作参数源](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**图 5**:`MaxPrice`文本框中 s`Text`属性用作参数源 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png))


通过单击下一步，完成配置数据源向导，然后完成。 对于 GridView、 文本框、 按钮和 SqlDataSource 的声明性标记如下所示：


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

请注意，SqlDataSource s 中的参数`<SelectParameters>`部分`ControlParameter`，其中包括其他属性，如`ControlID`和`PropertyName`。 当 SqlDataSource s`Select()`调用方法时，`ControlParameter`获取从指定的 Web 控件属性的值，并将其分配给中的相应参数`SelectCommand`。 在此示例中， `MaxPrice` s 文本属性用作`@MaxPrice`参数值。

花点时间查看通过浏览器的此页。 当首次访问页面时或者每当`MaxPrice`文本框中缺少任何记录显示 GridView 中的一个值。


[![没有记录将显示当 MaxPrice 文本框为空](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**图 6**： 否记录是否显示时`MaxPrice`文本框中为空 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png))


不显示任何产品的原因是因为，默认情况下，参数值为空字符串转换为数据库`NULL`值。 由于比较`[UnitPrice] <= NULL`计算结果始终为 False，则不返回任何结果。

文本框中输入一个值，如 5.00，然后单击显示匹配的产品按钮。 在回发时，SqlDataSource 通知 GridView 参数源的一个已更改。 因此，GridView 重新绑定到 SqlDataSource，显示这些产品小于或等于到花 5.00 美元。


[![显示产品小于或等于花 5.00 美元](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**图 7**： 显示产品小于或等于花 5.00 美元 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png))


## <a name="initially-displaying-all-products"></a>最初显示所有产品

而不是首次加载页面时显示任何产品，我们可能想要显示*所有*产品。 列出所有产品的一种方法只要`MaxPrice`文本框为空是参数的默认值设置为某个也可能非常高的值设为 1000000，因为它不太可能，Northwind Traders 将不断已列出清单的单位价格 s 超过 1,000,000 美元。 但是，这种方法是狭隘，并且在其他情况下可能无法工作。

在前面的教程-[声明性参数](../basic-reporting/declarative-parameters-cs.md)并[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)我们所面临类似的问题。 有我们的解决方案是将此逻辑放在业务逻辑层。 具体而言，BLL 检查传入的值，如果它是`NULL`或一些保留值，在调用路由到返回所有记录的 DAL 方法。 如果传入的值为正常的筛选值，调用了执行 SQL 语句使用参数化的 DAL 方法进行`WHERE`子句与所提供的值。

遗憾的是，我们跳过该体系结构使用 SqlDataSource 时。 相反，我们需要自定义 SQL 语句以智能方式获取的所有记录，如果`@MaximumPrice`参数是`NULL`或某个保留的值。 对于此练习，let s 使其因此，如果`@MaximumPrice`参数等于`-1.0`，然后*所有*记录的是要返回 (`-1.0`充当保留值，因为没有任何产品可以具有负`UnitPrice`值)。 若要实现此目的，我们可以使用以下 SQL 语句：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

这`WHERE`子句将返回*所有*记录如果`@MaximumPrice`参数等于`-1.0`。 如果参数值不是`-1.0`，这些产品仅其`UnitPrice`小于或等于`@MaximumPrice`返回参数值。 通过设置的默认值`@MaximumPrice`参数`-1.0`，在第一个页面加载 (或每当`MaxPrice`文本框中为空)，`@MaximumPrice`将具有值为`-1.0`和所有产品都将都显示。


[![现在，所有产品都都显示时 MaxPrice 文本框为空](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**图 8**： 现在的所有产品都都显示时`MaxPrice`文本框中为空 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png))


有几点需要注意的这种方法。 首先，请注意，由它推断的参数的数据类型 SQL 查询中的 s 使用情况。 如果您更改`WHERE`从子句`@MaximumPrice = -1.0`到`@MaximumPrice = -1`，运行时将参数视为一个整数。 如果你尝试分配`MaxPrice`的十进制值 （如 5.00) 文本框中，发生错误，会因为它不能将 5.00 转换为整数。 若要解决此问题，请确保你使用`@MaximumPrice = -1.0`中`WHERE`子句或更好，设置`ControlParameter`对象的`Type`属性为十进制数。

其次，通过添加`OR @MaximumPrice = -1.0`到`WHERE`子句，查询引擎不能使用索引，在`UnitPrice`（假设某个存在），从而导致表扫描。 如果有足够大量的中的记录，这可能会影响性能`Products`表。 更好的方法是将该逻辑移到存储过程在其中`IF`语句将执行`SELECT`从查询`Products`表而无需`WHERE`子句时需要返回所有记录或其中一个其`WHERE`子句只包含`UnitPrice`条件，以便可以使用索引。

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>步骤 3： 创建和使用参数化存储的过程

存储的过程可以在存储过程中定义相应的 SQL 语句中包含输入参数，然后，可以使用一的组。 在配置 SqlDataSource 使用接受输入的参数的存储的过程时，则可以指定这些参数值与临时 SQL 语句中使用相同的方法。

为了说明在 SqlDataSource 使用存储的过程，让 s 创建新的存储的过程名为 Northwind 数据库中`GetProductsByCategory`，它接受一个名为参数`@CategoryID`，并返回所有产品的列的`CategoryID`列匹配的`@CategoryID`。 若要创建的存储的过程，请转到服务器资源管理器和向下钻取到`NORTHWND.MDF`数据库。 （如果 don t 查看服务器资源管理器，请将其启动通过转到视图菜单并选择服务器资源管理器选项。）

从`NORTHWND.MDF`数据库、 右键单击存储过程文件夹，选择添加新存储过程，并输入以下语法：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

单击保存图标 （或 Ctrl + S) 保存存储的过程。 可以通过从存储过程文件夹，右键单击该和选择执行测试存储的过程。 这将提示你输入的存储的过程的参数 (`@CategoryID`，在这种情况) 之后该结果将显示在输出窗口中。


[![GetProductsByCategory 存储过程使用执行时@CategoryID为 1](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**图 9**:`GetProductsByCategory`存储过程使用执行时`@CategoryID`为 1 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png))


让我们来使用此存储的过程中的 GridView 中的饮料类别显示所有产品。 向页面添加一个新的 GridView 并将其绑定到名为新 SqlDataSource `BeverageProductsDataSource`。 继续到指定的自定义 SQL 语句或存储的过程的屏幕，选择存储过程单选按钮，并选择`GetProductsByCategory`存储过程从下拉列表。


[![选择 GetProductsByCategory 存储过程从下拉列表](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**图 10**： 选择`GetProductsByCategory`下拉列表中的存储过程 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png))


由于存储的过程接受一个输入的参数 (`@CategoryID`)，单击下一步会提示我们指定此参数的值的源。 饮料`CategoryID`为 1，因此将保留为无参数源下拉列表和默认值文本框中输入 1。


[![使用硬编码值为 1 以返回饮料类别中的产品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**图 11**： 使用 Hard-Coded 值为 1 以返回饮料类别中的产品 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png))


如以下声明性标记所示，当使用存储的过程，SqlDataSource s`SelectCommand`属性设置为存储过程的名称和[`SelectCommandType`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx)设置为`StoredProcedure`，以指示`SelectCommand`是存储的过程而不是临时 SQL 语句的名称。


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

测试浏览器中的页。 尽管显示属于饮料类别的产品*所有*以来的产品显示字段`GetProductsByCategory`存储的过程返回的所有列从`Products`表。 当然，我们可以限制或自定义 GridView 的编辑列对话框中 GridView 中显示的字段。


[![将显示所有饮料](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**图 12**： 将显示所有饮料 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png))


## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>步骤 4： 以编程方式调用 SqlDataSource 的`Select()`语句

示例我们到目前为止看到在上一教程和本教程中已有 SqlDataSource 控件直接绑定到 GridView。 SqlDataSource 控件的数据，但是，可以以编程方式访问和在代码中枚举。 当需要查询的数据对其进行检查，但不要需要显示它，则可能特别有用。 而不是无需编写所有样板 ADO.NET 代码以连接到数据库中，指定命令，并检索结果，您可以让 SqlDataSource 处理此单调的代码。

为了说明使用 SqlDataSource 的数据以编程方式，我们假设您的老板已是您解决与创建显示的随机选择的类别和其关联的产品名称的网页的请求。 即，当用户访问此页时，我们希望随机选择一个类别从`Categories`表、 显示类别名称，并列出属于该类别的产品。

若要实现此目的，我们需要两个 SqlDataSource 控件一个获取从随机类别`Categories`表，另一个用于获取产品的类别。 我们将构建检索随机类别记录在此步骤; SqlDataSource编写检索类别的产品 SqlDataSource 探讨第 5 步。

首先，通过添加到 SqlDataSource`ParameterizedQueries.aspx`并设置其`ID`到`RandomCategoryDataSource`。 因此，它使用以下 SQL 查询来配置它：


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()` 返回按随机顺序进行排序的记录 (请参阅[Using`NEWID()`随机排序记录](http://www.sqlteam.com/item.asp?ItemID=8747))。 `SELECT TOP 1` 从结果集中返回的第一个记录。 总而言之，此查询将返回`CategoryID`和`CategoryName`列从单一的随机选择的类别的值。

若要显示的类别 s`CategoryName`值，向页面添加一个标签 Web 控件，请将其`ID`属性设置为`CategoryNameLabel`，并将清除其`Text`属性。 若要以编程方式从 SqlDataSource 控件检索数据，我们需要调用其`Select()`方法。 [ `Select()`方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx)应类型的单个输入的参数[ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)，它指定应如何在返回前消息数据。 这可以包括排序和筛选数据的说明，由 Web 控件进行排序或分页 SqlDataSource 控件中的数据的数据。 对于我们的示例，不过，我们不 t 需要在返回前要修改的数据，因此将将传递在`DataSourceSelectArguments.Empty`对象。

`Select()`方法返回一个对象，实现`IEnumerable`。 返回的精确的类型取决于 SqlDataSource 控件 s 的值[`DataSourceMode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)。 在上一教程中所述，此属性可以设置为值`DataSet`或`DataReader`。 如果设置为`DataSet`，则`Select()`方法将返回[DataView](https://msdn.microsoft.com/library/01s96x0z.aspx)对象，如果设置为`DataReader`，它返回一个对象，实现[ `IDataReader` ](https://msdn.microsoft.com/library/system.data.idatareader.aspx)。 由于`RandomCategoryDataSource`SqlDataSource 具有其`DataSourceMode`属性设置为`DataSet`（默认值），我们将使用 DataView 对象。

下面的代码演示如何从记录中检索`RandomCategoryDataSource`SqlDataSource 作为数据视图以及如何读取`CategoryName`列从第一个 DataView 行的值：


[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` 返回第一个`DataRowView`数据视图中。 `randomCategoryView[0]["CategoryName"]` 返回的值`CategoryName`此第一行中的列。 请注意，数据视图是松散类型化。 若要引用特定列的值需要传递列的名称作为字符串 （类别名称，在此情况下)。 图 13 显示了中显示的消息`CategoryNameLabel`查看网页时。 当然，显示的实际类别名称随机选择的`RandomCategoryDataSource`SqlDataSource 上每个访问 （包括回发） 此页。


[![S 的显示名称的随机选择的类别](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**图 13**： 显示名称的随机选择的类别 s ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png))


> [!NOTE]
> 如果 SqlDataSource 控制 s`DataSourceMode`属性设置为`DataReader`，从返回的值`Select()`方法将需要强制转换为`IDataReader`。 若要读取`CategoryName`列的值从第一行中，d 我们使用以下代码：


[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

使用 SqlDataSource 随机选择一个类别，我们准备就绪后添加 GridView，其中列出了类别的产品。

> [!NOTE]
> 而不是使用标签 Web 控件以显示类别的名称，我们可能添加 FormView 或 DetailsView 到页上，将其绑定到 SqlDataSource。 使用标签，但是，允许我们，了解如何以编程方式调用 SqlDataSource 的`Select()`语句并使用在代码中其生成的数据。


## <a name="step-5-assigning-parameter-values-programmatically"></a>步骤 5： 以编程方式分配参数值

所有示例中我们已在本教程中到目前为止看到已使用硬编码参数值或从预定义的参数源 （查询字符串值，Web 控件在页上，依次类推） 之一执行。 但是，SqlDataSource 控件的参数还可以设置以编程方式。 若要完成我们当前的示例中，我们需要 SqlDataSource 返回所有属于指定类别的产品。 将具有此 SqlDataSource`CategoryID`参数需要设置其值基于`CategoryID`返回的列的值`RandomCategoryDataSource`SqlDataSource 中的`Page_Load`事件处理程序。

向页添加 GridView 并将其绑定到名为新 SqlDataSource `ProductsByCategoryDataSource`。 像我们在步骤 3 中，以便它将调用配置 SqlDataSource`GetProductsByCategory`存储过程。 将参数源下拉列表设置为 None，但不要输入默认值，因为我们将以编程方式设置此默认值。


[![未指定参数源或默认值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**图 14**： 未指定参数源或默认值 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png))


完成 SqlDataSource 向导后，生成的声明性标记应类似于下面：


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

我们可以将分配`DefaultValue`的`CategoryID`参数中以编程方式`Page_Load`事件处理程序：


[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

添加此元素后，此页包含一个 GridView，显示与随机选择的类别相关联的产品。


[![未指定参数源或默认值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**图 15**： 未指定参数源或默认值 ([单击以查看实际尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png))


## <a name="summary"></a>总结

SqlDataSource 使得页面开发人员可以定义参数化的查询的参数值可以硬编码，从预定义的参数源中提取或以编程方式分配。 在本教程中我们已了解如何创建即席 SQL 查询和存储的过程的配置数据源向导中的参数化的查询。 我们还了解了使用硬编码参数源，为参数源时，Web 控件，并以编程方式指定参数值。

如使用 ObjectDataSource，SqlDataSource 还提供功能来修改其基础数据。 在下一教程中我们将介绍如何定义`INSERT`， `UPDATE`，和`DELETE`使用 SqlDataSource 语句。 添加这些语句后，我们可以利用内置插入、 编辑和删除功能所固有的 GridView、 DetailsView 和 FormView 控件。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Scott Clyde、 Randell Schmidt 和 Ken Pespisa。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](querying-data-with-the-sqldatasource-control-cs.md)
> [下一页](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
